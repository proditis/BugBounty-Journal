# My bugbounty journal days: 7 - lets focus some more on DNS
- [My bugbounty journal days: 7 - lets focus some more on DNS](#my-bugbounty-journal-days-7---lets-focus-some-more-on-dns)
  - [Plan for the day](#plan-for-the-day)
  - [Targets of the day](#targets-of-the-day)
  - [Tools of the day](#tools-of-the-day)
  - [Observations of the day](#observations-of-the-day)
  - [Conclusions of the day](#conclusions-of-the-day)
  - [Final words](#final-words)

Well we're back for another session, last time i left things neat and tidy so there was not much cleaning up to do (other than this journal :smiley:).

I started up the day a bit earlier than usual but i also stopped a bit earlier than usual so there is that :man_shrugging:

Work hours: 11:00pm - 03:00 am

## Plan for the day
The plan for the day was to continue with the programs from last week and see if i can get into some juicer results, but for some reason i got lost into a DNS quest. Keep on reading and you'll find out.

## Targets of the day
I started looking at tools for DNS enumeration, but i couldnt find any that would do the sort of info gathering that i wanted so... (dont laugh) i hacked together a couple of snippets and a small dns prober was born.


## Tools of the day
* `dig`: for different types of lookups
* `checksoa`: [modified check-soa.go](https://github.com/darkoperator/golang-dns/blob/master/contrib/check-soa/check-soa.go) for fetching SOA records from authoritative DNS servers of a given domain name


## Observations of the day
Due to the fact that i was wasting my time playing with go and DNS i didnt really achieve anything significant as far as hunting goes, but i got a few good ideas about some tools i would like to make.
* There is a lot of `dig`/`host`/`grep`/`awk` involved when enumerating DNS, i need to take a look at tools that will ease in this regard
*

## Conclusions of the day
I came to the realization that my gluttony to include more and more tools into the pipeline has made me stray away from the main course... which is to devise a methodology that works better, faster and produces the results that i need 1st and foremost.

For this reason i decided to release the pipelines as a separate project. People can contribute their improvements or additional pipelines there and i can focus on devising my own methodology, which can later be added there as a pipeline _profile_ :smiley:

## Final words
Yet again i didnt do all i set out to do on this day, but i consider it progress. Unfortunately i didnt learn anything noteworthy to include into my notes this time.

- [day 8 - insert meaningful title here](day8.md)
- [Go back HOME](../)
- [day 6 - GOTO DAY 5](day6.md)