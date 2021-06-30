---
title: A Story of When Tech Debt Is Okay
layout: post
date: 2019-10-22
---

As a newly minted software engineer, one of the first things you encounter is likely to be the concept of Tech Debt. It can take many forms: an non-optimized algorithm, an unhandled edge case, or a value that's hard coded instead of being configurable. Whatever it happens to be, it drives you insane. You sit there thinking, "How on earth could someone have let that slip during development?". Something you'll have to come to grips with during your career though is that sometimes tech debt is okay, or even a conscious choice.

---

Let's start with a story. I just finished a couple month long project that was the first of its kind at work whose main goal was to increase our familiarity in the product type as well as meet a customer commitment for when it would be live in production. Without going into too much detail, the task was to build an API behind OAuth with an overall response time of less than a second. Doesn't sound too bad, right?

It wouldn't have been if any of us had been familiar with building such a thing, but of course it was a first for the entire team. That meant that we had to build the core functionality of the API, the authentication, stand up the infrastructure to support it, oh and learn what that even meant all within those couple months. During the course of the project, we had many opportunities where decisions had to be made in order to stay within the timeline.

First we tackled building out the actual core logic of the API as this was the part that we, a team of backend engineers, were most familiar with. To the backend engineers out there, the trade offs are pretty easy to guess. In the first pass of functionality we stored lookup values in local files instead of a database, hard coded certain values, and didn't perform validation or proper error handling of input values instead choosing to just throw generic errors. These are all things that can be fixed in future iterations of the code.

Then the team moved on to the authentication securing the API. We hadn't worked with OAuth before, so before starting to build we researched exactly how OAuth worked. When we had a firm grasp of what was needed, we were able to start work. Decisions were made to support only the bare minimum of the endpoints and functionality that were needed, which let us get to work without having to do further research. We knew we were only creating a limited subset of the OAuth spec, but for the time being with only one customer that was fine.

Finally, we moved on to setting up the infrastructure within AWS to support this. Knowing that the infrastructure of a project is hard to change after it's been built, and that this was the part that the customer would actually interact with we made sure that the design was rock solid before we started building. This meant using multiple AWS regions, Route 53, Certificate Manager, API Gateway, and Lambda. While it was a pain to setup, and there were things that we could have left to later, the whole team felt better knowing that the underlying core of the API was going to be the best that it could be.

In the above example, it's pretty easy to see what the tech debt is, namely:

1. Local files instead of a database
2. Hard coded values
3. Vague error handling
4. Minimal subset of OAuth implemented

What may not be as clear though is why those things were allowed to be within the first pass of the finished project. All of the above, and most trade offs made in general, can be explained through one thing: Consequence.

What is the consequence of having values stored in a local file when compared to a database? Well, it may be easier in the language to read from a local file and you don't have to worry about network issues when connecting to the database, but it will also be harder to update those values without changing the code. In this case, the savings of having the developers be more productive is well worth the consequences. This also leads to one of the beautiful parts of working with software, namely that things can more or less easily be changed after the fact through an update.

The consequences of the other trade offs are roughly the same, and boil down to "Let's do the slightly worse thing now to save developer time" which is normally the most expensive part of any software project. At my company, and I'm sure many others, management is trained to treat every engineering hour as being worth $50. When including salary, benefits, and unproductive time that seems to work out, so you want to make sure that you're spending the money in the right place.

This becomes even more important when dealing with a project that hasn't been proven yet, and is ultimately the origin of the MVP (Minimal Viable Product). If you don't know that a project is going to earn any money at all, it becomes even more important to ensure that money is being spent in the best way possible.

These things are never black and white though. If management had decided that we were going to take these shortcuts instead of letting the engineers decide for themselves, I may have been the angry engineer dealing with the tech debt instead of creating it.

---

Overall, I hope that any junior engineers can come to understand that sometimes tech debt has its merits, and to not be too mad at those that create it because it will almost certainly be you one day.
