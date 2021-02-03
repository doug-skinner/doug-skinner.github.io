---
title: A Pattern For Using AWS AppConfig
layout: post
date: 2021-02-02
permalink: /appconfig-usage-pattern/
---

Recently at my job [@CommerceHub](https://www.commercehub.com/), the team had a use case for needing to dynamically update configuration data about the environment that an application lives in. An example would be having the application reach out to instance A of an external application instead of instance B based on certain criteria.

## The Problem

For the sake of walking through this thought exercise without being too generic, let's say that we have a [Next.js](https://nextjs.org/) application that stores a users favorite animals at the zoo, called _Zoo Keeper_. Let's also assume that I was pretty succesful in selling _Zoo Keeper_ to all of the zoos in the surrounding couple of cities, such that I have three zoos connected to the application. Finally, let's assume that I have made it so a user of _Zoo Keeper_ only needs one account to be able to keep track of their favorite zoo animals across all of the zoos that I connect with, but the application only handles one connection at a time and we'll keep track of this by setting a value called `zoo-partition`.

Each zoo that the application connects too may allow access to their data in a different way. Some of them may expose APIs, some may allow direct acces into a database, etc. To the code living within __Zoo Keeper_, this shouldn't matter too much. As such, we're just going to store this data in a configuration file, where we will store a mapping of `zoo-partition -> data-access-address`. 

This situation gives us the following (very rough) architecture diagram:

<div class="mermaid">
flowchart LR;
  A(User);
  B(State Zoo Database);
  C(City Zoo Database);
  D(Other City Zoo Database);
  
  subgraph Zoo Keeper;
    A;
  end;
  
  subgraph State Zoo;
    B;
  end;
  
  subgraph City Zoos;
    C;
    D;
  end;
  
  A-->|if zoo-partition == 1|B;
  A-->|if zoo-partition == 2|C;
  A-->|if zoo-partition == 3|D;
</div>

This is all flows along pretty smoothly, as there are a bunch of different ways of dealing with this configuration data. Let's say it's a few years down the road now, and _Zoo Keeper_'s sales team is killing it, allowing us to be connected to hundreds of zoos across the country, each of which has their own way of storing their animal data. There's also the problem of having to suspend various connections for various billing reasons, so we need to introduce configuration that can be handled without doing a full deployment for each addition or subtraction of a connection.

To sum up, we have a need to consume environmental configuration that may change at any time, as well as needing to standup infrastructure that will allow the data to change.

## The Solution

To save the day, we have [AWS AppConfig](https://docs.aws.amazon.com/appconfig/latest/userguide/what-is-appconfig.html). AppConfig was made to create, manage, and quickly deploy application configurations, which is almost entirely what we need here.

⚠️This may not be the **best** way to use AppConfig, but it is certainly **a** way to use AppConfig ⚠️

### Solution Overview

At a high level, AWS AppConfig pretty much solves our problem for us. AppConfig allows a developer to create a configuration that can be updated dynamicallyand deployed with ease, with a few caveats. There are two hard parts about working with AppConfig. The first is getting your configuration data into AppConfig, without someone having to manually enter a piece of data. The second is being able to dynamically use that data.

To solve the first part, we're going to build an event-based pipeline that will take in changes to configuration, in our case adding and removing zoos, that will then update the stored configuration within AppConfig and trigger a new deployment. To solve the second, we will construct a "cron" process within our Next.js application that will periodically fetch the configuration and provide it to the rest of the application.

### Solution In Detail


