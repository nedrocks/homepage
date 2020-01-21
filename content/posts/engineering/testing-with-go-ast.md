---
title: "Testing consts and switch statements with go/ast"
description: "A working (albeit hacky) solution to ensure your switch statement includes all consts within a file."
date: 2020-01-19T20:01:00-08:00
categories: ["engineering"]
tags: ["engineering", "golang"]
images: ["/img/Go_gopher_app_engine_color.jpg"]
draft: false
---

(If you just want to look at the code, check it out on [my github](https://github.com/nedrocks/switch-const-test/blob/master/errs/error_test.go). Leave a comment if you want to chat about it!)

I believe that services in golang should abstract `error`s between their `internal` package and their `api` package. I find this makes managing errors and logic flows much more manageable, with one exception. There needs to exist a layer to convert an internal error into its API representation.

That conversion step isn't too hard, just build an `errs` package or something similar. So long as we call the function when returning to the api layer, we will convert the error accurately, and all is well.

Golang can get a bit annoying because the way consts are defined we cannot ensure at compile time that all are handled. In an object-oriented language with inheritance such as Java, we would handle this by pushing the logic to the object.

```
abstract class InternalError {
    abstract ExternalError convertToExternal();
}

class NotFoundInternalError extends InternalError {
    ...
}
```

In golang enforcing this becomes more difficult because idiomatic golang pushes us to such verbose boilerplate. Instead, we construct an interface for an internal error and a function to convert internal errors to external errors based on an ErrorCode or something similar.

```
type ExternalError interface {
    error
    Code() InternalErrorCode
}

func ConvertToExternalError(e InternalError) error {
    ...
    switch e.Code() {
        ...
    }
    ...
}
```

The problem with this model is when we add a new InternalErrorCode definition, we do not verify at compile time that the switch statement needs a new branch. To my knowledge, there is not a simple way to do this without adding significant boilerplate.

Creating a new struct for each error type could work. This requires and defining the interface for each struct, similar to the earlier Java implementation. However, nothing stops an engineer from **not** doing that because the concept of `abstract` doesn't exist in golang.

#### Enter go/ast
Before diving into the AST, let's quickly look at [the code](https://github.com/nedrocks/switch-const-test/tree/master/errs). First, we define a set of `const` error codes in a file by itself:

```
type InternalErrorCode string

const (
    IncorrectInformation = InternalErrorCode("incorrect_information")

    IncorrectLoginProfile = InternalErrorCode("incorrect_login_profile")

    Forbidden = InternalErrorCode("Forbidden")

    AccessTokenRevoked = InternalErrorCode("access_token_revoked")

    NotFound = InternalErrorCode("not_found")

    Unknown = InternalErrorCode("unknown")

    DownstreamError = InternalErrorCode("downstream_error")

)
```

Then in another file in the same package we define our `InternalError` type as well as a function to convert it to an external error:

```
// InternalError describes an error interface to use internally for the service.
type InternalError interface {
    error

    Code() InternalErrorCode

    WrappedError() error
}

// ConvertToExternalError Will attempt to convert to an external Twirp error.
func ConvertToExternalError(e InternalError) error {
    if e == nil {
        return nil
    }

    if err, ok := e.(twirp.Error); ok {
        return err
    }

    switch e.Code() {
    case IncorrectInformation:
        fallthrough
    case IncorrectLoginProfile:
        return twirp.NewError(twirp.InvalidArgument, "incorrect information")
    case Forbidden:
        fallthrough
    case AccessTokenRevoked:
        return twirp.NewError(twirp.Unauthenticated, "forbidden")
    case NotFound:
        return twirp.NewError(twirp.NotFound, "not found")
    case Unknown:
        fallthrough
    case DownstreamError:
        return twirp.NewError(twirp.Unknown, "unknown error")
    }

    return twirp.InternalErrorWith(e)
}
```

There isn't a clean way to unit test that we handle every const defined in error_codes.go. Unless that is, we use go/ast. This package (and related packages) allow us to parse the code and walk the abstract syntax tree. Using this technique, we can find every defined const in a file as well as every branch in a switch statement:

```
func Test_ConvertChecksAllConstsInSwitch(t *testing.T) {
    declaredNames := []string{}
    switchCaseNames := []string{}

    // First find all of the names of declared variables in error_codes.go.
    // This will obviously not work if we instantiate varibles of type
    // InternalErrorCode elsewhere. However, if we keep all of these variables
    // to that file (and no other variables) then this list will be comprehensive.
    fset := token.NewFileSet() // positions are relative to the file set.
    f, err := parser.ParseFile(fset, "error_codes.go", nil, 0)
    if err != nil {
        t.Fatal(err)
    }

    ast.Inspect(f, func(n ast.Node) bool {
        switch x := n.(type) {
        case *ast.Ident:
            if x.Obj != nil && x.Obj.Kind == ast.Con {
                obj := x.Obj
                d := obj.Decl
                if declAsValue, ok := d.(*ast.ValueSpec); ok {
                    if len(declAsValue.Names) > 0 {
                        declaredNames = append(declaredNames, declAsValue.Names[0].Name)
                        return true
                    }
                }
            }
        }
        return true
    })

    // Now find all of the case checks in the switch statement in `error.go`.
    // Keep in mind this will break if there is more than one switch statement
    // in that file. This is pretty hacky :-).
    fset = token.NewFileSet() 
    f, err = parser.ParseFile(fset, "error.go", nil, 0)
    if err != nil {
        t.Fatal(err)
    }
    ast.Inspect(f, func(n ast.Node) bool {
        switch x := n.(type) {
        case *ast.CaseClause:
            if len(x.List) > 0 {
                if listElemAsIdent, ok := x.List[0].(*ast.Ident); ok {
                    switchCaseNames = append(switchCaseNames, listElemAsIdent.Name)
                }
            }
        }
        return true
    })

    Convey("Switch statement cases should be the same as declared names", t, func() {
        sort.Strings(declaredNames)
        sort.Strings(switchCaseNames)

        So(declaredNames, ShouldResemble, switchCaseNames)
    })
}
```

The code here is very hacky and relies on specific implementation details. With more in-depth analysis, we can build a more robust version, but this works in a pinch.

Have any feedback or a better way to do this? I'd love to hear from you. Shoot me an email at [ned@nedrockson.com](mailto:ned@nedrockson.com) or drop a comment below.