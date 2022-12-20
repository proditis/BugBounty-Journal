# My bugbounty journal day: 8 - insert meaningful title here
- [My bugbounty journal day: 8 - insert meaningful title here](#my-bugbounty-journal-day-8---insert-meaningful-title-here)
  - [Plan for the day](#plan-for-the-day)
  - [Targets of the day](#targets-of-the-day)
  - [Tools of the day](#tools-of-the-day)
  - [Observations of the day](#observations-of-the-day)
  - [Conclusions of the day](#conclusions-of-the-day)
  - [Final words](#final-words)

Another day... having another go at it. I am really pumped for the day as i plan to try out some new tools that i found.

Unfortunately as you can tell from just the 3 hours that i invested, something went wrong and i had to stop, pack my things and go get some sleep.

Work hours: 00:00 - 03:00 am

## Plan for the day
The plan for the day is to continue on with the program i had most familiarity by now and see if any of the new tools that i found will make it easier for me to find something out.

Last time i was struggling with HTTP requests so, during the day i practiced some new tools to not waste time during my engagements.

## Targets of the day
Again no new targets were added to the list (although i came to regret it later on).

I chose to focus on the program that i had the most familiarity with by now. So after a quick review of my data i jumped into `http-prompt` and started messing with some interesting endpoints that i had discovered.

My main focus was to try and discover some more implementation specific details, such as application and library names, versions, operating systems etc. With this information i can then check to see if there are any "new" vulnerabilities discovered that the program owners might have missed.

This went quite well and i was able to figure out application and library names and versions, as well as identify certain vulnerable components that i could attack. I got really really excited with this and i could almost taste victory.

> Excitement is good to keep you going (even if no results come out of it).

However, my excitement was short lived, as it turned out the program that i picked to work on for the day got... **_Suspended_**

That hit harder than i expected... It killed my desire and my interest for the rest of the day and gave up shortly after, spending instead my time in pondering at all those "could have been submissions"... :sob:

## Tools of the day
* `httpie`: for quick and easy cli http requests
* `unfurl`: :exploding_head: awesome tool for quickly manipulating urls
* `concurl`: :exploding_head: this was used on manual tests but its amazing for doing exactly what i want, run curl concurrently capturing the output including headers and command line (i had a for loop for that without the parallelism)
* `meg`: for combining paths with hosts (alleluia)
* `http-prompt`: for interacting with http endpoints through a _shell_ :heart:
* `spfparse`: a small tool i hacked together to probe a domain DNS for interesting details (the name will probly change in the future)

## Observations of the day

It could have been nice to have to know the end life of each program before hand. If i knew that the program was to be suspended so soon, i would have picked a different strategy for approaching it.

Although it was disappointing, I didnt consider my time on the program wasted for **two** main reasons:
* There is a good chance for the program to come back. Large programs need their BugBounty presence for marketing purposes :rofl:
* I was able to refine my methodology, to where it is now, by having to mess with a program like the one i picked. So even though there were no submissions as a result, i was still somewhat satisfied by where i'm currently at
* I love simplicity and some tools out there are so simple that makes integrating them into the pipelines a breeze. @tomnomnom's tools are a testament to that
* I would still like to have a few more automated stages for later steps, as i feel that i'm doing some reparative manual hands that could have been automated.
* I am starting to think that on these platforms it may **not worth** investing so much time on a single target? Rather than that, take a more "brute force" approach of _scan everything from every program_ and only focus on results that seem promising

## Conclusions of the day

* Always check the status of the program you are about to work on BEFORE you start... (future me please dont forget this)

## Final words
I had the opportunity to test some really awesome tools this day. I dont think its by accident that most of them were from @tomnomnom :smiley:

- [NEXT DAY](day+1.md)
- [Go back HOME](../)
- [PREV DAY](day-1.md)