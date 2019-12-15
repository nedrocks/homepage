+++
title = "Early Agile OR How to stop worrying and love self management"
date = 2019-12-07T20:41:27-08:00
description = "How the evolution of agile organically trumps imposed top-down agile-ity"
categories = ["management"]
tags = ["software", "management"]
draft = false
+++

While researching the history of the standup meeting, I came across Jim Coplien's 1994 retrospective on development 
of [Borland Quattro Pro for Windows](https://sites.google.com/a/gertrudandcope.com/info/Publications/Patterns/Process/QPW). 
In it, Jim analyzes a herculean effort where a team of eight developers wrote over 1 million lines of code over a 31 month period,
or approximately 1,000 lines of code per week per developer[^bignote]. 

During development the team stumbled across early core agile principles almost a decade before the [Agile Manifesto](https://agilemanifesto.org/) would be 
published. This study led to some of the early publications of XP and Daily Scrum a few years later which would evolve 
into modern day agile in 2001.

Agile effectively defines a pattern for a team to self-direct[^1]. In this case the team described had a small two-pizza team with extremely well known and defined roles

> When I asked what their development roles were (with a short definition of what I meant by role) the answers were immediate, intuitive, and reflected a single model 
of the organization shared by its members.

I doubt these roles originated with a central project management chain saying "Alice you work on implementing an observable pattern across all layers of the application." 

Let's imagine how this took shape. In one of the daily multi-hour architecture meetings, Alice brought up a frustration with the inefficiency of propagating changes 
throughout the system and proposed using the observer pattern consistently throughout the application. Her colleagues agreed and so she became the de facto 
observable person on the team. No project manager bestowed this title on her, but if anyone asked her what her role was, that likely came near the top of the list. 
She likely spent big chunks of the project ensuring the observable pattern was followed consistently.

This simple example embodies three out of the four points in the Agile Manifesto. Alice becoming the observable goto person embodies the first Agile point: 
"Individuals and interactions over processes and tools". Her push to build software in a workable way during frequent architecture meetings embodied the 
second point: "Working software over comprehensive documentation". Due to there being eight Alices on this team (maybe some were Bobs) the daily architecture
meetings likely resulted in changes and moving pieces which the team actively leaned into, emobodying the fourth point: "Responding to change over following a plan."

The only point from the manifesto the team does not fully address is "Customer collaboration over contract negotiation". The retrospective specifically calls out 
"QPW wasn't working to a customer requirements document. They simply knew what needed to be done", or put another way they treated themselves as the customer and 
did not feel the need to interact with their customer. Jeff Bezos would tear them in half. 

Leaving customer obsession aside, this team self-evolved into largely what would become modern-day agile methodologies. And if you're a in the tech world who has 
seen imposed Agile structure work less-efficiently in practice than on paper (spoiler: you have,) you're wondering what was so different.

The agile that doesn't work for your team is the same agile that doesn't work for others. Plain and simple agile works because it's the outcome of a self-management 
system built by smart, likely introverted, and geeky builders. The outcome looks easy to reproduce - in fact the agile manifesto looks remarkably similar to the 
self-management that evolved within QPW - but cargo culting almost never works. For instance, the QPW team had daily multiple-hour-long architecture meetings. 
Imagine trying to time-box their daily touchpoint standups to 15 minutes because the Agile certification said so.

The agile system that worked for this team is the same agile system that works for others. Their agile system built on the foundation of three necessities for your dev team:

* Trust[^1] - Without trusting your developers, they will not self manage and Agile becomes an excellent petri dish of micromanagement.
* A culture of respect, identity, and ownership - Frequently as a manager one can fall into the trap of short-tenure and replaceable talent, but having strong respect 
for team member's abilities and specialties will drive self-management because it brings respect, identity, and ownership.
* Time to provide inflection points - Knowledge work is not something trackable in hours. We tend to equate complexity with story points and other crude mechanisms, 
but leaps for individuals and teams happen at inflection points. An eight hour day might have 45 minutes of actual progress, but that 45 minutes produced eight hours 
of work. The other 7.25 hours were allowing the dev to hit the required inflection point.

The second point is interesting when looked through the lens of intra-development team, especially with short tenures and strict trivia and competitive hiring practices. 
The legibility of each dev's status[^1] in the team pushes them to try to constantly improve their standing (hence the instability of most dev teams and thus short tenures.) 
That's a subject for another post though.

So does Agile work? Yes, and it requires trust, culture, and time.

[^bignote]: While I don't believe in LoC as an accurate velocity measure because it rarely equates to true velocity. For instance the following two python snippets do the same thing (one significantly less efficiently.) The first is two lines of code and the second is nine. However, that said 1,000 lines of code per week for 31 months presents a truly epic accomplishment.

        input = [str(i) for i in range(100)]
        print(','.join(input))
 
        input2 = []
        for i in range (100):
            input2.append(str(i))
        strOutput = ''
        for i, elem in enumerate(input2):
            strOutput += elem
            if i != len(input2) - 1:
                strOutput += ','
        print(strOutput)
[^1]: Probably self-selection bias: well-published teams with strong self-direction have had major influence on the agile pattern.
[^1]: "Trust your devs" taken directly from Erik Dietrich's excellent overview of the [perils of certification for Agile](https://daedtech.com/in-devs-we-trust/)
[^1]: Status illegibility is described in [part IV](https://www.ribbonfarm.com/2010/10/14/the-gervais-principle-iv-wonderful-human-beings/) of Venkatesh Rao's essay series The Gervais Principle.