---
layout: post
date: 2023-01-19 12:00
title: Weird Node Networking
permalink: /weird-node-networking/
---

[This change](https://github.com/nodejs/node/commit/1b2749ecbe) has ruined my life the last few days. I've been trying to figure out why I was suddenly getting eConReset errors working on an internal application. Apparently in Node17, it was decided to change the default dns result order from always being ipv4 to following the host machines preferences, which is ipv6 on most machines.

You can undo this by setting a flag `--dns-result-order ipv4first`
