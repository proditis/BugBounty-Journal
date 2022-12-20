# My bugbounty journal
![image](assets/bluffty_dub.png)
- [My bugbounty journal](#my-bugbounty-journal)
  - [Daily Log](#daily-log)
  - [Notes](#notes)
  - [Automation](#automation)

This is my attempt to keep a journal of my experience with bug bounty. I want to approach this entire experience coming from a sysadmin and developer background with a lot of vulnerability research on the sides.

I am going to attempt to document my experience, thoughts before and after in the hopes that this may help others.

The reasons I am doing this are:
* Get a better understanding of the bugbounty process and get first hand experience with it
* Get better ideas for making targets for our echoCTF platform
* Learn a few of the tools i never wanted to learn, on the go and on the need, ie force my self to understand what gap each of the tool is trying to fill
* Create a Gitlab and Github pipeline that would allow bugbounty hunters and pen-testers to automate some tasks
* (maybe) Get lucky and score a payout in the process 😊

My trip to the bugbounty world starts at midnight of 25/11/2022. Unfortunately i cannot work on it during the day, so my attempts will have to be more directed and with purpose if i plan on doing anything significant.

**WARNING:**

1. I have absolutely no idea what i am doing.
2. I am making fun of my self a lot
3. I dont know what i am doing (did i say that already?)
4. I am trying to figure this up as i go...

_I may occasionally update a previous days entry to include new details. This will mostly include spell checking and inclusion of details that i believe will be useful but didnt have the foresight to include them in the first place._

## Daily Log
* [day 1 - nothing ever goes as planned and that is a good thing](days/day1.md)
* [day 2 - this new plan will work for sure](days/day2.md)
* [day 3 - lets use some tooling](days/day3.md)
* [day 4 - lets use some more tooling](days/day4.md)
* [day 5 - the best laid plans often go... to waste](days/day5.md)
* [day 6 - GOTO DAY 5](days/day6.md)

## Notes
Here i will keep my notes about specific tools that i use on my daily attempts. I am trying to document **ONLY** what i use and not create an encyclopedia.

* [CDN specifics](notes/cdn.md)
* [Useful DNS Commands](notes/dns.md)
* [Gitlab specifics](notes/gitlab.md)
* [HubSpot notes](notes/hubspot.md)
* [GraphQL notes](notes/graphql.md)
* [PHP notes](notes/php.md)
* [Useful `/.well-known/` locations](notes/well-known.md)
* [WSDL APIs](notes/wsdl.md)


## Automation
The gitlab pipelines collection has started getting bigger and bigger and it makes no sense to keep them here. A new project repo has been created to hold the gitlab pipelines (and future Github actions).

[https://github.com/proditis/bugbounty-cicd](https://github.com/proditis/bugbounty-cicd)