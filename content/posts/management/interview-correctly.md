---
title: "Interview Correctly: Are You Selecting for the Right Things?"
date: 2020-01-12T21:24:00-08:00
categories: ["management", "interviewing"]
tags: ["interviewing", "engineering"]
images: ["/img/interview-whiteboard.png"]
draft: false
---

I have been lucky to have interview training from small companies, large companies, and external consultants. I've practiced my skills while conducting at least 750 interviews over my career. I'd go so far as to call myself a well-trained interviewer.

In case you've never been part of a technical interview, I'll give you a quick rundown. The candidate's interview usually lasts between three to eight hours, with each interview taking between 30 minutes and one hour. They often start with introductions and a quick 5-15 minute question about a problem the candidate solved in the past. Something like, "Ah, I see you have worked in React. Tell me about the problem you solved with the bloo blah blee."[^1]

![](/img/interview-whiteboard.png)

The majority of the remaining time involves one or more technical questions. Sometimes the candidate knows how many to expect and what would a good, great, or excellent performance looks like, although this is pretty rare. The questions are mostly one of the following types.

1. Brainteaser - A logic puzzle that tries to test for creativity and flexibility of the candidate's mind. For example, "If I shrank you to the size of a nickel and put you in a blender, how would you escape?"[^2]
1. Fermi question - An estimation problem where the candidate sets up the constraints and attempts to arrive at an answer. The answer doesn't matter, just how the candidate thinks through the problem. For example, "How many golf balls would fit inside a 747?"
1. Algorithm/Data structure question - A question the candidate must think of an algorithm or data structure to solve the posed question and then write it in code on a whiteboard or in a code editor. [Leetcode](https://leetcode.com/)'s focus is mostly algorithm and data structure question training.
1. System Design / Architecture - A question where the candidate designs a much larger system than can be built in an hour and usually draws boxes and lines on a whiteboard. Generally, this tests bigger problem solving and communication skills. For example, "design Twitter" is a widespread system design question.
1. "Real-World" problems - The candidate solves a "real-world" (generally fabricated) bug or feature similar to what they would work on if hired. For instance, I've had people redesign a homepage using live APIs.

After somewhere between three to eight of these interviews, you're done. Easy right?

#### The Secretly Terrible Engineer
The **vast** majority of interviews try to ensure the candidate is not a [Secretly Terrible Engineer (STE)](https://techcrunch.com/2015/03/08/on-secretly-terrible-engineers/). "Résumé be damned," the interviewer thinks, "in this 1-hour block of time, I can sniff out the imposter." The interviewers set up a mental obstacle course that the candidate must do well (although not *too* well[^3]) running through. They must also keep the correct interpersonal attitude: talkative, friendly, and professional. 

This entire framework of sniffing out the STE propagated into nearly every interview process, partially because the interviewers want to ensure they don't hire the dreaded STE. It's also partially to indicate to candidates their potential coworkers could never be STEs. Even worse, it is expected by both interviewer and candidate that interview questions have tricks designed to trip up the candidate. The candidate should handle these tricks to show their mental agility.

I believe there are no (or at least incredibly few) STEs (or Secretly Terrible insert-
profession-here's) in the world. However, tech seems to be the only place we force candidates to prove they can accomplish obscure tasks, live. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/3nGQLQF1b6I" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

This hyperbolic level of scrutiny the interview process requires reminds me of a scene from 1991's "My Cousin Vinny." Marisa Tomei plays the titular character's (played by Joe Pesci) fiance and automobile expert. She grew up and spent her entire life with cars and knows them exceptionally well.

Pesci calls Tomei as an expert automobile witness. The (almost-entirely male) cast exhibit blatant sexism when they cannot believe she has automobile expertise. To admit her testimony, the DA poses her a hyper-specific question about a 30-year-old car. The DA acquiesces because she gets the trick and can explain the minutiae.

> The reality is, few professions seem so openly hostile to their current members as software engineering.

This scene is so reminiscent of technical interview techniques it's comical. Sexism aside (a severe problem in tech,) a candidate's background of working years (or decades) in a specialty is thrown to the side unless he or she can answer an incredibly specific question
designed to trip him or her up.

#### Something Is Wrong Here
As an industry, we focus on hiring exceptional talent. Most companies brag about how they hire the best. I've said this and truly meant it.

However, we hire people based mainly on their ability to jump through hoops. Experts[^4] have shown these hoops have a weak correlation with success on the job (maximum R<sup>2</sup> of 0.26.)

So if statistics prove the process does not filter for the best, shouldn't it have evolved through natural selection? I argue no because it selects for rule followers.

#### Selecting for Rule Followers
To my knowledge, no one enjoys interviewing as a candidate. As a candidate, one necessarily takes a position of less power than the interviewer. The interviewer must prove themselves by answering Sophomore-year-in-college algorithm questions or imagine how to escape from a blender as an ant.

But those candidates who bite the bullet and put up with the pomp and circumstance enough to receive an offer have shown that they can follow the rules and accomplish tasks. From a management perspective, this may rival or even eclipse hiring an exceptional technical mind. If a technical hire has basic knowledge and can follow the rules and deliver on a deadline, they rival the greats (or even the best if you're into that whole supremacy type of thing.)[^5]

I talked to a Product Manager from a top tech company last weekend and shared some of these thoughts. When I mentioned that the existing interview process tends to select rule-followers above all else, he was elated. Engineers who follow his direction to the letter are the best, in his mind.

#### Hiring The Best
If you've gotten this far, you're probably hoping I have a magic bullet for you, and I do (kind of)! There is no "The Best." Instead, there exists the person who can do well at the job you have right now. So to find what you call "The Best" is to figure out what the job you need doing is and find someone who will do well at it.

You can only accomplish this if you work backward from your problem. Working backward is one of the core principles I learned at Amazon, and it's insanely powerful.

> I will invoke a learning from Amazon here: Work backward from your problem.

Getting at the core of **why** you want to hire an engineer is difficult. Do you need someone to redesign the architecture for your fleet of microservices? Do you need someone who can be trusted to operate independently and train other engineers? Do you need someone to close tickets efficiently and consistently?

If you can diagnose the job you need doing right now, you can focus on hiring the right person for that job. Someone who develops microservice architecture may not fit the mold of a generalist engineer. They might tell you to shove it when asked to implement a red-black tree on the whiteboard. However, that's not the job that needs doing.

Once you have defined the problem and the criteria for the interview, follow Ben Horowitz's advice and look for reasons to hire the candidate. When interview panels search for weaknesses or disqualifications, they often hire a safe candidate with no perceivable flaws. However, this candidate is likely bland and may not stand out anywhere in positive ways, either. Instead of finding disqualifications, find qualifying reasons to hire a candidate. There will never be a perfect candidate.

#### So, What?
So maybe the interview process is a thinly veiled way to find rule-following professionals. So many people are shifting their careers toward tech. Merely finding a professional person with the necessary skills is sufficient for many roles.

I think we can do better. I also think there are bright spots. In researching this post, I talked with several engineering leaders at startups. I want to call out two companies doing somethings incredibly right.

[Mixmax](https://mixmax.com/careers/) has an entire section of their interview process devoted to real-life Mixmax problems. The candidate is asked to review a pull request, not for a production machine but written by an engineer on their team, and give a full code review. The interviewer gets to see what the candidate does when critiquing and analyzing a potential peer's code.

[Alphaflow](https://www.alphaflow.com/careers/) moves fast, and the process assesses the candidate's ability to work outside of their comfort zone. The interviewer presents them with an existing open-source codebase outside of the candidate's comfort zone. The candidate needs to build a new method and write it into the codebase. The candidate's solution and thought processes show their ability to work with an existing codebase in a real-world use case.

#### What have I missed?
So many companies have unique interviewing styles. Do you have one that you want to talk about? I'm always interested in learning about successful interview styles. Reach out to me at ned@nedrockson.com if you want to chat!

[^1]: Actually, at Amazon, we also ask questions about (Leadership Principles)[https://www.amazon.jobs/en/principles] in this block, which tend to be far more abstract, but still sound like similarly-phrased open-ended questions.
[^2]: These questions are very seldom asked anymore but were extremely common in the aughts.
[^3]: I've seen more than one candidate rejected because they did too well. Their excellent performance led to the interviewers believing the candidate somehow cheated and thus rejected.
[^4]: Google's former Head of People, Laszlo Bock, breaks down the effectiveness of different types of interview questions in [Work Rules](https://www.amazon.com/dp/B00MEMMVB8). The most effective style of questions has an R<sup>2</sup> of 0.26.
[^5]: To be clear, I have worked with fantastic engineers who went through this process, so clearly great engineers make it through this process as well. Even non-rule-followers like me make it through.