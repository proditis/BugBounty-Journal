# My bugbounty journal day: 5 - the best laid plans often go... to waste
- [My bugbounty journal day: 5 - the best laid plans often go... to waste](#my-bugbounty-journal-day-5---the-best-laid-plans-often-go-to-waste)
  - [Plan for the day](#plan-for-the-day)
  - [Targets of the day](#targets-of-the-day)
  - [Tools of the day](#tools-of-the-day)
  - [Observations of the day](#observations-of-the-day)
  - [Conclusions of the day](#conclusions-of-the-day)
  - [Final words](#final-words)

Well i'm back again (after a horrendous week of full-blown sickness), not fully recovered but i wanted to try and keep up my schedule even if i dont get anything worthwhile out of it.


Hours on it: ~2am - ~8am

## Plan for the day
So i'm starting the day with the plan to continue one of the programs from last time. I found some SOAP endpoints and during the week i was researching their specifications in order to have something to try this time around.

In the week in between i had a chance to refresh my memory of SOAP based API's and a bit of studying of some more tools which i'd like to integrate into my methodology.

Also, in the week tha passed, a friend and i had the chance to move forward with the idea about the database wordlist thingy which gave birth to [Orunmila](https://github.com/proditis/orunmila). I want to integrate this also into my process for asset and program details handling. Hopefully this will improve my asset gathering and find some good feature ideas while testing it.


## Targets of the day
This time no new targets where added. Instead I tried to clean up my data from last time and see if i was missing any details, while i tried to catch up to where i left off exactly. 

So i started with importing existing details which i would later use for my scans into an `orunmila.db`, this included a lot of different types of lists such as subdomains, interesting urls, endpoints, api's, keys and ids and much more.
```sh
orunmila i -tags inscope,domain inscope-domains.list
orunmila i -tags inscope,url inscope-urls.list
orunmila i -tags gau,url gau-results.log
orunmila i -tags assetfinder,domain assetfinder.log
orunmila i -tags subfinder,domain subfinder.log
```

Through my tests i would occasionally run `orunmila s -tags api,domain` to get a list of API subdomains or run `orunmila s -tags api,url` and get a list of API url endpoints. During my testing any new information i found that i need to keep i was adding it into the db with and continued on with my testing without loosing my thought process.
```sh
orunmila a -tags api,urls https://new.url/blah/blah
```

Another thing that i realized is that in some of the programs that i had picked on my previous days, I didnt have the same _quality_, _types_ or _volume_ of results as some of my my latests scans had. 

This is mostly because i was still figuring out my methodology back then, but now its much more streamlined and I am mostly let the pipelines do the job.

So i merged some of the new tools and methods that i picked along and i fired up a pipeline to deal with it. By now the pipeline is several steps, 10 and counting, with dependencies between jobs, and transfers of artifacts all over.

I was able to refine my method a bit more and also managed to use some other sources for finding information about a program such as mobile applications.

When a program has available Android applications, even if you dont audit the app, its always good to download the APK as it may have interesting urls and other details that are not available on the usual places. I was able to find endpoints, names, emails and other such information from downloading an APK.

> I prefer passive methods a lot more (for obvious reasons), than going full on guns blazing and causing all sorts of alarms going off from early stages.

Another thing that i noticed is that SNI enabled hosts need special care when working with them (duh!). A lot of times its not enough to change the `HOST:` header since the SNI negotiation has already took place and as such you wont be able to reach the proper host. So something like the following is not enough.
```sh
curl -H "Host: example.com" https://another-example.com
```

Instead we need something like the `--resolve` option for curl
```sh
curl --resolve example.com:443:1.2.3.4:443 https://example.com
```

In some cases you get an entire different set of results depending on how you approach the TLS enabled hosts. 

Right about here, this is the moment that I had an idea to start a couple another tools 😭... Now i dont only have to create them but i also have to include them into the pipelines 2*😭...

## Tools of the day
* `https://apps.evozi.com/apk-downloader/?id=<APP_ID>` for downloading APK's from google play
* `https://ibotpeaches.github.io/Apktool/` to extract APK's with decoded XML's and other details
* `grep -Ero "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"` to grab emails from files

## Observations of the day
Things went a lot smoother this time, but i found my self doing certain things on the spot which became tiresome after a while. I am able to produce a large number of mostly accurate information with the pipelines, but its still not where i want it to be. 

The main toolset and methodology works waaaayyy too good right now. To the point that i now i have less than 30% of free runners time available on gitlab. 

In the future it may word having separate gitlab group per program altogher, in order to take advantage of more free times. Once you're done with a project you dont need to keep it around any more, you archive it, download and remove it from gitlab.

I needed 3 things today which i didnt have
* a tool to parse cert files and display their alternate subject names (openssl and shell scripting did the job buuuuuut)
* a tool that will connect on an ssl host, grab the alternate subject names and try to connect to the same ip but with new hostname while respecting SNI
* a tool that will connect on a host, grab the Content Security Policy header and extract IPs and Hostnames

Some general observations about the progress of my day:
* I was able to produce a lot more in less time, than in all the other times, but still the methodology felt somewhat uncomfortable to me
* Performing and manipulating HTTP requests in an efficient way is still a huge issue for me but none of the available tools seems to fit my way of working, i still dont know what to do about that :-/

## Conclusions of the day
Overall the day went well and i was able to hone in my initial stages of information gathering about my target(s).

* KISS: There is no need to include EVERY scanner available into my methodology
* Some tools may be "best" but come with penalties
* The best of the side-effects of doing bug bounty is that it _kinda_ forces me to follow up on my ideas about tools and scripts, and i'm loving it :heart: (last time i made a tool that was for _hacking_ exclusively was 2002 so dont laugh :rofl: )
* It is way faster to hack together Golang snippets that perform simple tasks than i was expecting
* If something works dont touch it
* Dont hack while under influence of medication for headache and fever!!!


## Final words
Unfortunately i was not 100% yet so after the first hour or so i forgot to keep updating my notes for this journal and since it was around 8am in the morning i had to pass out. Then, when i woke up, i had forgotten all about what went on during the night so this is it :smiley: 

My plan for the day went unexpectedly well and even though my methodology still takes some ironing out, i think that i'll stick to it.

- [day 6 - GOTO DAY 5](day6.md)
- [Go back HOME](../)
- [day 4 - lets use some more tooling](day4.md)
