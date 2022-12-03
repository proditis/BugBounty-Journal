# day 3 - lets use some tooling
- [day 3 - lets use some tooling](#day-3---lets-use-some-tooling)
  - [Plan for the day](#plan-for-the-day)
  - [Add some more targets](#add-some-more-targets)
  - [Tools of the day](#tools-of-the-day)
  - [Observations of the day](#observations-of-the-day)
  - [Conclusions of the day](#conclusions-of-the-day)

Its Friday again, (02/12/2022) and i'm preparing my plan for the day. I have spend parts of the week in studying a bit of GraphQL and deciding on some tooling that i will use.

I am a bit feverish today (flu probly), so this will be fun :D

Hours on it: ~1am -

## Plan for the day
I have prepared some pipelines that i want to test tonight and see if i can get better results and how this will work out.

The thing that worries me is that an almost weeklong break might be too much, as it will have a lot of catching up to do. I will cleanup my work from the previous days a bit before i start and see if this helps to refresh my memory.

My fear came kinda true, due to the fact that i had cleaned up already the repositories for the programs so there was nothing to do to _refresh my memory_. The good part is that this exposed another limitation in the way that i was keeping documentation and notes about the programs. So i'll try to address this today.

## Add some more targets
My plan was not to look into any other programs and instead refine my methodology with the programs i've already played a bit. But i saw a couple really interesting ones which involve non web technologies and this is right up into my alley. So as you have guessed i added a few more programs into the repositories.

<sarcasm>so i start my copy paste like a good hunter...</sarcasm>

I think that i found a program that has clicked with me. Has technologies that were not web based and just by looking at the first subdomain enumerations it was pure gold.

I had the change to test and finalize some of my pipelines with some more tooling. I think that have improved my methodology which included a staged iteration of
10. add desired Gitlab pipeline jobs from the collection
20. download artifacts from succesfull jobs
30. remove succesfull jobs from the pipeline
40. correct failed jobs
50. `GOTO 10`


## Tools of the day
I had the chance to look at some more tools this time which helped me at certain stages of the process.
The days picks included:
- `certgrabber` For grabbing server certificates (https://github.com/stavinski/certgrabber)
- `gau` for grabbing urls
- `wget` for mirroring purposes
- `nmap` for some basic scans that produced xml output
- `xsltproc` for converting the xml reports into html


I cant stop but thinking that i have forgot to log some of the tools that i used for the day, but you'll have to excuse me for that as i was trying to keep this log at the same time as working on 3 other different repositories, under "in-flu-ense" (not what you think). I mean flu, i think i got the flu :D

## Observations of the day
* I need to automated the gitlab repository creation somehow. Maybe with a browser extension/bookmarklet? Seems to be the easier option atm.
* I need to work on a unified pipeline which will allow for all the jobs to be present at the same time, including potential "custom" commands


## Conclusions of the day
The day went really really well. I found lots of juicy targets which where using the kind of obscure services i have configured in the past as CTF targets, so i felt really confident. However, it seems that the fever had its toll in my ability to pay attention to **BIG** details (you'll see).

* I should pay CLOSER ATTENTION at the inscope with bounty items. As it turns out i spent more than half my day looking at non bounty items :facepalm:
* I can see significant improvement at the way it went this time, very few issues, my folder is cleaned
* I should inspect more carefully a private program before i join. I dont know if there is a way to "leave" a program yet. Need to check at the intigriti UI
* I produce better results when i focus on a single program, as long as the program clicks with me...
* I think its time to give burp or zap a better look, i definitely need some tooling for the visually elaborate web applications

Its 4:10AM at the moment and i dont think i can keep working. Finding out that i spend all my time on non bounty items killed my motive, in part because it felt like i . I will attempt to cleanup and push my changes and go to sleep.

- [day 4](day4.md)
- [Go back HOME](../)
- [day 2](day2.md)