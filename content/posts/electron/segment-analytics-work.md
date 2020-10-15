---
title: "Making Analytics Work with Segment"
date: 2020-10-08T09:53:41-07:00
tags: [engineering, electron]
draft: false
---

As part of work on my new company, [Debrief](https://www.getdebrief.com), I've gone through a self-taught Electron crash course. I have found it maddening to find good Electron resources. As such, I am committed to publishing my learnings, including code snippets, to this blog. Knowing me, I'll forget at some point to keep things updated, so if you read this and want more, please email me (ned @ this domain) and give me a kick in the butt.

# Electron Analytics with Segment.com
I struggled mightily with this problem. All in I probably spent 15 hours getting this solution correct. Hopefully this helps you spend less time than I did.

Segment maintains a bunch of great libraries to send events seamlessly to their service. The two I'm focused on here are [browser Analytics.js](https://segment.com/docs/connections/sources/catalog/libraries/website/javascript/supported-browsers/) and [analytics-node](https://segment.com/docs/connections/sources/catalog/libraries/server/node/).

The libraries I ended up trying but had nightmarish, hair pulling problems with are listed in a footnote[^1] so when skimming you don't accidentally think I'm recommending them.

Segment documentation around Electron support partially recommends a pattern of using these two. Beyond that they don't clearly recommend a path forward (at least that I could find, and I searched.)

Anyway, here is what worked, then I'll talk about what didn't.

## Use analytics.js in your renderer
**This is the working solution.**

This solution is great because it pulls updated integration settings from segment on load. It also tracks paths reasonably well. The two files you need to update are your `app.html` (or whatever html file you load in your renderer) and some analytics module (in my case `renderer/analytics.ts`).

### app.html (or whatever HTML file your renderer loads)
I'm going to assume your main renderer uses app.html for brevity. Install the script tag from Segment in the head section:

```
<script>
  !(function () {
    var analytics = (window.analytics = window.analytics || []);
    <!-- SNIP -->
    analytics.load(
      new URLSearchParams(window.location.search).get('segment_key')
    );
  })();
```

The last part where we load analytics with a parameter from the query is important when running in sanboxed mode (which [you should be doing](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox.md)). Access to `process.env` is not available in sandbox mode. Don't let a dev server let you think otherwise because you'll get upset when you package and release your app.

When you load the renderer BrowserWindow remember to pass the query parameter (note that since this is called from the main process, we have access to `process.env`):
```
mainWindow.loadURL(
  `file://${app.getAppPath()}/app.html?segment_key=${process.env.SEGMENT_KEY}`
);
```

### analytics.ts
You'll likely want a renderer module to encapsulate your analytics. I personally like to have all of my analytics events wrapped in a function call so we can have typescript guarantee the types are passed properly. Note that because Electron has both renderer process(es) and a main process, you should keep files that cannot be shared in explicit directories. We have a `renderer` folder and a `main` folder to help me with this. For this module, store it in `renderer/analytics.ts`.

Inside this module create an initialize function. (As a side note if you plan to initialize other analytics-esque packages this can serve for that purpose. We intiailize Sentry in this function.) In this, setup the middleware in `window.analytics`. Due to Electron requiring a hash router or in memory router, segment will not know the path or page currently active when sending an event. Because we use a hash router, the path and URL sent without middleware becomes `/` all the time. Tracking funnels and flows would prove quite difficult without it.

We set things up as follows:

```
export const initialize = () => {
  // SNIP...

  // eslint-disable-next-line @typescript-eslint/ban-ts-comment
  // @ts-ignore
  window.analytics?.addSourceMiddleware(({ payload, next }) => {
    let path = history.location.pathname;
    if (!path || path.length === 0) {
      path = '/';
    }
    if (payload && payload.obj) {
      if (payload.obj.context && payload.obj.context.page) {
        payload.obj.context.page.url = path;
        payload.obj.context.page.path = path;
      }
      if (payload.obj.properties) {
        if (payload.obj.properties.path) {
          payload.obj.properties.path = path;
        }
        if (payload.obj.properties.url) {
          payload.obj.properties.url = path;
        }
      }
    }
    next(payload);
  });
};
```

# Example Event
From here setup events how you want. Here's my `gqlLatency` event as an example:

```
enum EventType {
  GQL_LATENCY = 'GqlLatency',
}

class DebriefAnalytics {
  static gqlLatency(operationName: string, latencyMS: number) {
    window.analytics?.track(EventType.GQL_LATENCY, {
      operationName,
      latencyMS,
    });
  }
}
```

# Conclusion
Hopefully this helped you save some time, or at least helped you not get incredibly frustrated! For other electron tips, check out the electron section [here](/tags/electron/). If you want to talk more about eletcron, reach out to me or leave a comment. I'd love to hear from you.

[^1]: Other libraries I tried working with: [analytics.js-integrations](https://github.com/segmentio/analytics.js-integrations), [analytics.js-core](https://github.com/segmentio/analytics.js-core).