---
title: Estimating Time
layout: post
date: 2018-11-11
---
I've had many jobs, titles, and teams in the last few years. I've often had the task of estimating how long a task will take. I've almost always been wrong.

Why is that? Well, you don't know what you don't know. Especially when it's the first time that you are estimating a task of a specific nature. You'll likely only have a vague idea of what accomplishing said task is going to consist of. Without knowing that you're almost doomed to fail.

To take an example from my current job as a software developer, it's easy to under-estimate how long a task will take. We frequently get blind-sided by only focusing on the coding time.

For this example that we're going to walk through, the company estimates things in "Developer Days". A Developer Day for our purposes is roughly five hours. This is the story of how one little bug can ruin a developer's week, and throw all project estimation out the window.

Say a Customer Service Representative reported a bug. The normal way that this goes down is the CS rep will open a bug report. On the team, an engineer will pick it up and say something like "This looks like an easy fix. An hour or two at most." So the ticket get's recorded as half a Developer Day. Then the secondary developer, the one actually doing the work, picks up what they think is an easy ticket. In the future, they'll be blindsided by the fact that this easy fix winds up not being ready for release for three days. Where did this extra time go?

For starters the description in the ticket was vague.

> "Customer X not seeing required field within the search box".

Which, while not clear might get the job done if the person reporting the issue is the same one that fixes it. That's not the case here. Now the developer has to reach out to customer service to find out what field is missing in which search box.

After reaching out, the CS rep scheduled a meeting so that they can show the developer an example. With this meeting done, the developer returns to their desk with a screenshot in tow.

The developer finally knows what the problem is. They can start digging in to find out why the problem is happening. After looking at the codebase, confusion ensues. Everything should be working fine and are now stumped about the cause of the issue. So now the quest is on to look at all the tickets that released recently. Once done digging through the releases for the last week, two tickets stand out.

A meeting is set up with each of the original developers to find out why the changes may have caused the bug. There's a debate about how the two respective tickets shouldn't have broken anything. As all tests had passed for the two tickets, it's obvious there is a gap in the test coverage of the application. Being the good test-driven developer that they are they created a test that failed the build. Having accomplished no visible progress, the dev went home for the day.

Armed with a failing test, the developer can now look through all the previous releases again. Once they found the culprit, it was time to write the fix. It wound up being a three-line fix, as the previous dev had passed the wrong variable name into a specific method. Mad at themselves for not catching this issue sooner, the developer went on a tear. The developer set out to make the variable names clearer. This also included changing other variable names in the file to be more specific.

With this new code in hand, the developer put the code up for review by a teammate and thought the ticket done. Things never being this simple, the renaming of a dozen variables stuck out to the reviewer. The reviewer scheduled a meeting to go over the reasoning behind the refactor.

The developer explained their case, and the reviewer agreed with the reasoning. The code was finally pushed forward for testing. A QA engineer picked up the code for testing. It passed all basic test cases on the first try and was set up for overnight automated testing. Once the QA came in on the third day and saw that the full test suite has passed they marked it ready for release.

Something identified as being a "two-hour" task had taken the better part of three days. This is roughly thirteen hours.

Now it would be easy to blame the extra time on the lack of knowledge by the dev. Or the excessive meetings. Or the extra time the QA process took. The reality though, is that all that time should be taken into account at the start.

The original engineer should have seen that the ticket description was vague. And should have added time to find out a better description. Or take it upon themselves to reach out to CS before handing the ticket off. The estimate should have taken into account the known QA time. Every single ticket has to go through that same process. Finally, the original estimate was optimistic, to begin with. The work of looking into the problem, adding a test case, and manual testing is never happening in a two-hour time window. The engineer should have known that.

If the estimating engineer, didn't take that all into account something must be off, but what? Well, for starters humans tend to be terrible at estimating time in general. Try it yourself. Look at a clock until it starts the next minute, and then look away for sixty seconds. See? If we can't even estimate how long a minute feels how are we supposed to estimate tasks that can take hours or days?

Humans tend to focus on optimistic times. We estimate how long something will take based on the fastest time that it has ever happened in. For an example of this, think of your commute to work. Say according to the GPS it's a twenty-minute drive. You know that if you hit every light you actually arrive at the office in fifteen minutes. The human brain will then adjust the expected time to be fifteen minutes.

Don't believe me? Try this: go up to some co-workers and ask them how long it takes them on average to commute to the office. Then have them check it with a GPS app. Their responses will almost always be quicker than the GPS estimation.

The same thing happens with code. The estimating engineer may have had a similar bug come in with a different part of the website. They identified resolved the issue within thirty minutes. Had a five-minute code review, and a pass of only the "light" test cases then the ticket took them an hour, two at most. So when they are tasked with estimating the task, an hour or two has become the default case when in reality it is exceptional.

For the sake of your coworkers and yourself, I challenge you to try to be better. Estimate each ticket by looking at all the possible things that can go into the ticket. You will annoy the project manager when this first happens. But, when they realize that they now have much more accurate accounting they will thank you. And with the few tickets that do take twenty percent of the estimate, well that helps them look better on the bottom line.
