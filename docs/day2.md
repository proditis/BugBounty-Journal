# day 2 - this new plan will work for sure

- [day 2 - this new plan will work for sure](#day-2---this-new-plan-will-work-for-sure)
	- [Plan for the day](#plan-for-the-day)
	- [Picking extra targets](#picking-extra-targets)
	- [Organizing my work](#organizing-my-work)
	- [Tools of the day](#tools-of-the-day)
	- [Observations of the day](#observations-of-the-day)
	- [Conclusions of the day](#conclusions-of-the-day)


Alright, after a devastating first day lets see what this day will bring. I am a bit sore from staying up all night and messing up my sleep cycle but its fine. Although I am not sure what i will be able to do today.

Hours on it: 2am - 5am

## Plan for the day
My plan for the day was to focus on organizing my work a little better in general so that i have less cleanups to do the next day.

1. Find some more programs to scan (this will further help me to improve my project structure and how i keep my data)
2. Automate the boring staff which are non "rate-limited" (such as dns probes and other passive scans). I am going to utilize my pipeline experience with gitlab to make this step automatically execute when i create the repo :fingers_crossed:
3. Start cleaning up some data from day 1 and see if we missed anything
4. Maybe work today with the local application

## Picking extra targets
I picked two more large programs which also required a lot of manual scanning (see how carefuly i avoid using those more complicated tools??).

Just like the previous day i created a repo for each new program, this time things went a bit smoother/faster. The difference for the day was the use of gitlab to perform the initial scans.


![Information Gathering Stage](https://cdn.discordapp.com/attachments/1012759357982773268/1046057852684488814/image.png)

My plan for the pipelines was as to create a pipeline that utilizes a docker image with the tools so that the scans that i need for each program take place exactly when i push the repo. For each scan i produce a log of the data i need to keep and i use the gitlab artifacts capability to have the scan results ready for download.

![Artifacts download](https://cdn.discordapp.com/attachments/1012759357982773268/1046058644845895710/SPOILER_image.png)

Here is an example of a small pipeline job (that i didnt use yet)
```yml
stages:
  - information_gathering
  - scanning

variables:
  DEBIAN_FRONTEND: noninteractive
  DOMAIN: example.com
	API_BASE: "v2/gql"
	API_TYPE: "graphql"

zap_api_scan: # Name of the job
	stage: information_gathering # Stage of the engagement
	image: owasp/zap2docker-weekly # Docker image to use
	before_script:
	- mkdir -p /zap/wrk
	script:
	- zap-api-scan.py -t https://${DOMAIN}/${API_BASE} -f ${API_TYPE} -w "${DOMAIN}-report.md" -x "${DOMAIN}-report.xml" -r "${DOMAIN}-report.html" -d
	artifacts:
		name: "$DOMAIN:$CI_JOB_NAME:zap_api_scan"
		paths:
		- wrk/${DOMAIN}-report.*
	rules:
	- if: $CI_PIPELINE_SOURCE == "web" && $API_BASE != "" && $API_TYPE != ""
	  when: manual
```

## Organizing my work
I tried a different approach this time, dumping similar dumps under their own folders in raw format and then studying them to extract information into a single large document. While doing this i open issues for specific things that i wanna try and comment on my success, failure.

Improved my devtools usage a bit, now i preserve all the requests i perform and i export all requests in a single HAR (HTTP Archive) file. Using a few `python` scripts and a bit of `jq` helped a lot. This time i used a lot more "mainstream" tooling, although i was not satisfied by it (maybe i use it the wrong way, will check when i have the time).

I also ended working through a combination of vscode and terminals with kali.

## Tools of the day
* `curl`
* `subfinder`
* `python`
* `zap-api-scan.py` (unsuccessfully)
* `amass`
* `assetfinder`
* `ffuf`
* HAR parser https://gist.github.com/craSH/892479/21d5c3222739743cad6e6e5c5f1597daecbe560e
* Gitlab a lot of editing of the pipeline until it was ready to be used

## Observations of the day
I was expecting for the worse, but instead everything worked so fast that it exposed an issue that was also visible the day before. The pipelines i created worked so good that i had the results ready almost instantly.

Some of the observations for the day:
* `amass` is extremely good at finding data for a target. However, it seemed to me its way too good to be of any real use for me at the moment. I used it mostly as a quick overview of what has ever existed for a given target.
* `zap-api-scan` seems extremely powerful but it seems (???) to take too much time for my liking.
* `ffuf` loved its simplicity, fairly to the point tool, but it needs wordlists. The problem with the available wordlists for me is that they seem to be trying to include every url that ever appeared on a single list, making it fairly painful for hackers and servers alike.
* Most of the servers i encountered seem to be behind some sort of CDN (cloudflare, akamai etc)
* `HEAD` (part of the lwp-request tools) came handy and made me check with both follow and non follow redirects (which i almost always forget to try with `curl`)

## Conclusions of the day

1. I need to work on finding some carefully crafted lists for various purposes so that i can use them with `ffuf`
2. Automation is good and great and all, but I need to improve my workings now
3. Understanding your tooling is important if you dont want to waste time and loose some juicy targets
4. Sometimes is good to follow redirects, my goto tool for such requests is usually something like `curl -I ${TARGET}` (notice the lack of `-L`).
5. I need to find some tricks for hosts behind CDN's even if they are minor
6. It may be a good idea to create a few targets for echoCTF that will be used by new users to actually familiarize with the tools and see them in action under more carefully crafted scenarios. This will also help me to do the same :smiley:

By now i am exhausted compared to the previous day, my mind doesnt seem to work properly and everything i try to do is taking way too long. I call it a day and going to get some sleep so that i can cleanup when i wake up, and update this journal entry.

Unfortunately my next attempts will be again this next Friday (01/12/2022), so i will take the time in between to cleanup and practice with a few more tools.


- [day 3 - lets use some tooling](day3.md)
- [Go back HOME](../)
- [day 1 - nothing ever goes as planned and that is a good thing](day1.md)