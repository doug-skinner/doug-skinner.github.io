---
layout: page
title: Weblog
permalink: /weblog/
---

## Aug 8, 2023, 8:56 AM

Just migrated the website from a standard blogging format to a single page weblog format. Hopefully this will make it easier to maintain and update. I've also added a few new pages, including a [reading list](/hobbies/reading/) and a [list of my other hobbies](/hobbies/). As always, this site is a work in progress so not all content is complete.

## Jan 19, 2023, 12:00 PM

[This change](https://github.com/nodejs/node/commit/1b2749ecbe) has ruined my life the last few days. I've been trying to figure out why I was suddenly getting eConReset errors working on an internal application. Apparently in Node17, it was decided to change the default dns result order from always being ipv4 to following the host machines preferences, which is ipv6 on most machines.

You can undo this by setting a flag `--dns-result-order ipv4first`

## Jan 1, 2023, 11:01 AM

After work required MFA to keep using our Github accounts, I found a cool blog post about using [your MacBook's Touch ID as a Security Key for Github](https://www.stevemar.net/touch-id-as-a-security-key/). Posting for future reference.
