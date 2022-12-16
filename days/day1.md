# My bugbounty journal day: 1 - nothing ever goes as planned and that is a good thing
- [My bugbounty journal day: 1 - nothing ever goes as planned and that is a good thing](#my-bugbounty-journal-day-1---nothing-ever-goes-as-planned-and-that-is-a-good-thing)
  - [Preparation - this is a joke](#preparation---this-is-a-joke)
  - [Picking targets - this is another joke](#picking-targets---this-is-another-joke)
  - [Organizing our work](#organizing-our-work)
  - [DevMode - Getting our hands dirty](#devmode---getting-our-hands-dirty)
  - [AdminMode - Lets see this thing](#adminmode---lets-see-this-thing)
  - [Tools of the day](#tools-of-the-day)
  - [Observations of the day](#observations-of-the-day)
  - [Conclusions of the day](#conclusions-of-the-day)

First day was consisting of mostly figuring staff out. how the intigriti ui works, how to pick a program to work on and similar tasks.

I would be lying if i said i made significant progress with any target but it was a fun night nonetheless.

Hours on it: ~1am - 6am

## Preparation - this is a joke
I started with 0 preparation almost. My preparation for the day, other than speaking with friends and asking for advice was:

1. a fresh install of kali on virtualbox, booted first time on the time i set to start (midnight of 25/11/2022). This installation will help with tools that require some sort of UI, as well as providing a ready configured set of browsers to do my work. But i hate working on UI as i feel i am too slow with the mouse.
2. a Docker kali image with the kali `metapackage` installed. This image is more closer to my liking and if configured properly can provide an almost transparent way that i can use the kali tools from my main workstation without having to keep the container image up all the time.

## Picking targets - this is another joke
I didnt wanna waste time so I jumped right into the intigriti website to look for a way to find good programs. I know, from the many friends on twitter, that duplicates are a killjoy so my way to avoid this was to pick a program that has a long history and hasnt had an update for a long time.

I thought that a company like intigriti would have an API for its hackers to do all those nice queries, but apparently they dont!!!
_Well, technically they have if you go do hacky scripts, using the bearer token from the web app into a cli tool, but i dont like that and since this could be seen as violating their ToS i chose not to use it._

My query for programs was formed as follows:
* Filters
    - Confidentiality: public
    - Status: Open
    - Reward methods: bounty
* Sort by: Latest submission last

I picked 3 programs that seemed to have good responsiveness and a nice spread of payouts with as few "competitors" as possible.
* One of the program was based on a software which part of the scope was detecting misconfigurations. They allowed you to run the software through docker on your local system. This means that i can play with it while waiting for any tools to finish. At least that was my idea, as it turned out i forgot i even had it running until the next day...
* The second program had a narrow scope. An API here, a website there and nothing much else. It also required to set some ridiculous rate limits (something like 1 request per year), which made this testable only manually. Which is something that i love doing, so i figured i'll be able to jump here when I'm stuck with the other two...
* The third program was HUGE, close to 300 unique hostnames, not counting that every path was a different application (/app1, /app2 etc). This, I figured it will have to be dealt with mostly by automation, so i will have to get familiar with all those tools the "cool kids" use. Little did i know that some of the tools were so counter intuitive, i ended up using the normal tools i would use as admin.

## Organizing our work
For each program, i created a private gitlab repository using the program name as repo name. There i will dump documents, files and logs as well as track assets and todo as issues.

Nothing went as planned... but it was to be expected. Out of all i ended up spending most of my time on the last one, while trying to work out if the processes we used in the past could still be applied.

Since i didnt search for tools before hand, i had to figure out how to do things on the spot and by doing so, identify problems or specific needs in my process.

## DevMode - Getting our hands dirty
So the developer in me jumped into one of the API's with a web browser, dev tools and `copy to curl`.

Immediately i realized that it would have been handy to be able to extract these requests all in one go so that i can study them with my favorite editors.

There is no option "show me requests only for this domain" that i could find. Luckily the number of requests i needed to extract where not that many... but that was a single page load, i recon if i crawled the website this number of requests would have been in the thousands. This is one of the things i knew Burp and Zap (among a plethora of other tools) could have done easily.

Created a document to keep track of these needs for later since i didnt wanna stop in the middle of the engagement to start googling.

I wanted to find out as much as i could for my targets.

## AdminMode - Lets see this thing
So then the admin in me took over and I started looking for telltale signs in headers and sources so as to understand what kind of software they use.
* Are there any headers, cookies that may trigger the use of a specific component? (ie `apollograph-web-client: blah v1.0`)
* Are there any specific images, favicons, strange url names, robots etc that can provide us with frameworks and what not?
This stage was mostly dumping headers and googling/githubing.

Based on what i found from the following steps, i jumped into github and tried to find the repositories for these applications. What i was looking for here was:
* What is the application for/What does it do?
* What programming language does it use?
* What are some of the dependencies of the application?
* What are some of the latest reported issues that my look as promising "bugs"?
* What are some (if any) of the latest vulnerabilities about?
* Are there administrators/users/getting started manuals for it?
* Does any of the application dependencies have a vulnerability?
* Does any of the application dependencies seem custom made for this particular project?

Using these i was able to find some endpoints that would otherwise be kind of difficult to find without launching excesive number of scanners.

## Tools of the day
* `host`: For DNS lookups on targets A LOT
* `curl`: almost all requests where performed by `curl` one way or another
* `sort`, `grep`, `awk`, `tr` for output manipulation and filtering
* `assetfinder`: :heart: this tool :heart:, when i went into its github pages i saw 4 years old and was like "dang it". Worth every second using it.
* `git`: Lots of git to update the repos with latest findings
* `jq`: for parsing and querying so many json files
* `docker` for running the kali image
* `VirtualBox` with fresh Kali installed (_that died when it tried to exist the screensaver so there was very little use of it_)
* `chrome` and `firefox` dev console
* A LOT of bash scripting (one liner loops where all over my bash history)

The tools that were the unexpected heroes of the day where **`host`** and **`assetfinder`**

## Observations of the day
My first day experience was a mix bag of feelings... Looking at the programs and remembering tweets i've seen over the past months i made some observations...

* I think that nobody (hackers) really cares about the program warnings (eg **`3 requests/sec`**). Everyone i saw was using scanners that i failed to find how to "ratelimit" properly.
* Many programs have such a low number of requests that only can be scaned by hand manualy
* Many programs have shady rules which quite frankly give them the power to eliminate any report. Notices like the following are a red flag to me
  __In case that a reported vulnerability was already known to the company from their own tests, it will be flagged as a duplicate.__
  and quite frankly make me wonder If you found the vulnerability already then why havent you fixed it or updated the out-of-scope so that people dont waste their time?
* During the engagements i couldnt stop but feeling as if i was being watched and judged, an anxciety like "oh man i am such a noob i bet others would have found something by now". Thankfully i was able to detect it early on and slap my self really hard to get it out of my head. I reminded my self why i do this and ignore the voices in my head...
* Dear Intigriti, for the love of god can you add a download as Markdown, json, txt, csv SOMETHING?  This would have made working on a program so much easier
* funny as it may sound, you have to copy paste each target in scope, each of which can include `*` domains, and exclude the out-of-scope by hand... 100s of hackers are doing the same steps in each engagement (copy, mass scan, grep -v). How about providing the engagement details so that it is guaranteed people are scanning IN SCOPE items only?
* It is obvious to me that the majority of hacking tools are authored by people who didnt have experience or understanding of the unix philosophies (but we still love you :heart: ), even though these tools are primarily for linux :penguin:
* There are **A LOT OF GRAPHQL** endpoints out there...

## Conclusions of the day
Well my first day conclusions is that maybe i should have done a bit more preparation. But even like that i am quite happy with my progress.

1. Document everything: Documenting and figuring out a proper structure to hold your engagement data is much more important than the actual scan. Its easy to miss critical information when you dump logs all over the place.
2. Some "oldschool" ways, miraculously enough, are much more useful during the early stages of the engagements. They provide accurate and to the point results which give you a good idea on how to later proceed using the big guns
3. As hackers we like to point the finger at the developers often, but A LOT of hacking tools are so badly written that i dont thing we deserve to point fingers. We need to lead by example.
5. None of the programs that i picked "clicked" with me, i was able to find things here and there but it felt like a chore. But i dont mind, i know from my experience in developing targets that the  all you have to do is be persistent. Leave the target or program who currently doesnt make sense and jump into the next. Eventually it will come to you.
6. I need to organize my work better, at the end of the day the place was filled with log files.
7. I need to think about the information that i keep and how i keep it so that it is easier to digest and use.
8. Some tooling is required
9. I need to study graphql more


Need to investigate more, but by now its 6am and my brain is ready to explode. So i'll stop here and cleanup after.
_PS: Some notes were kept as i was working so i dont forget what was going on through my mind, but some corrections took place after i woke up :rofl:_

- [day 2 - this new plan will work for sure](day2.md)
- [Go back HOME](../)