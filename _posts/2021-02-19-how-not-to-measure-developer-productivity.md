---
title: How Not To Measure Developer Productivity
layout: post
date: 2021-02-19
---

Everyone knows that trying to manage engineers is as hard as herding cats. It’s even harder to try to track how productive your cats (software engineers) are. I’m sure this is a problem that everyone reading this has faced.

> If you can’t measure it, you can’t improve it.
> — Peter Drucker

Finding metrics that allow one to track this is... hard. As software engineers or their managers, we want to have data on everything. It turns out, through the magic of all the various software that we use day-to-day, we can measure a lot. But the real question isn’t what should we track, but why are we?

> Not everything that can be counted... counts
> - Albert Einstein

The problem stems from how hard it is to measure a developer’s output. It’s easy to try tracking output using any of the common bad metrics. With these being the number of commits, the number of lines of code, pull request count, among others. These are not only tracking the wrong thing, they actually encourage anti-patterns. Who wants to write more code than they have?

Metrics such as the above, that count the quality of output are hard to escape. When leaders have no metrics they feel as if they are flying blind. There is a solution, though. Instead of trying to measure output, we should measure the process. First, create a well-defined process. Then start measuring how your developers stack up against expectations.

As well, rather than measuring averages, you should measure against defined benchmarks. An example would be the percent of peer reviews that took longer than 24 hours. This is a more useful metric than measuring the average number of hours a peer review took. For starters, it’s not weighted by outliers. Next, you don’t care if the metric is green. Finally, it tells you right away when things are taking too long.

When doing this, it’s not so much the exact metric that matters. Just choose a metric, use it as your canary in the coal mine, which will let you know when danger is ahead.

Finally, one last tip: avoid individual metrics. If a dev doesn’t feel blame, then they have no reason to try and game the metric.

