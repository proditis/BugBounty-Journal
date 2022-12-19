# CDN
- [CDN](#cdn)
  - [Cloudflare](#cloudflare)
    - [Status Codes](#status-codes)
    - [Workers](#workers)
    - [`wrangler dev`](#wrangler-dev)
      - [Only cloudflare IP's allowed?](#only-cloudflare-ips-allowed)
      - [Use cloudflare workers to perform unfiltered(!?) scans?](#use-cloudflare-workers-to-perform-unfiltered-scans)
    - [Breaking DNS for sites not hosted on cloudflare for cloudflare clients](#breaking-dns-for-sites-not-hosted-on-cloudflare-for-cloudflare-clients)

* Use the `register`, `forgot password` and similar operations to grab the IP of the server protected behind a CDN

## Cloudflare

### Status Codes
* `530`: Error 530 indicates Cloudflare is unable to send requests to your server because its origin IP cannot resolve the A or CNAME DNS record requested


### Workers

### `wrangler dev`
The best way to work with workers is to register with a throw away account and then use wrangler to test and upload your code.

The `wrangler dev` command has less restrictions while offering the same benefits for our purposes (ie it still masks our IP's and other identifying details). Furthermore, it allows certain blocked requests to pass, so definitely prefer work on dev than on live, but this depends!!!

#### Only cloudflare IP's allowed?
Use the cloudflare workers to perform requests on given hosts and thus appearing as if the source IP was from cloudflare. The Cloudflare workers documentation is excellent and includes lots of examples on the subject.

* **NOTE 1**: When using workers to perform requests the URL is being filtered, certain keywords will make it fail (ie `/etc/passwd` ). However, other parts of the request seem to go unfiltered (such as json `POST` data).

* **NOTE 2**: There is filtering performed on the uploading of your code into cloudflare. For example a source file with any mention of `/etc/passwd` other than comments causes the service to fail to upload!!! Keep this in mind as it may require some minor obfuscation from your part in order to bypass this (ie rot13 the payload :D)

#### Use cloudflare workers to perform unfiltered(!?) scans?
Using the workers API one could create a specific worker that will
perform ~massive~ simple scans on hosts protected by cloudflare.

After testing this through, it seems to be feasible to some extend.
You can perform all sorts of web requests to the target system and
there will be no identification other than your worker environment
name which is included into the request headers, performed by the
workers (`cf-worker: name.workers.dev`).

The following is a list of headers that are being send
```c
host:	www.cylog.org
connection:	Keep-Alive
Accept-Encoding:	gzip
X-Forwarded-For:	2a06:98c0:3600::103
CF-RAY:	blablah-FRA
content-length:	64
X-Forwarded-Proto:	https
CF-Visitor:	{"scheme":"https"}
content-type:	application/json;charset=UTF-8
CF-EW-Via:	15
CDN-Loop:	cloudflare; loops=1; subreqs=1
cf-worker:	myworkersname.workers.dev
CF-Connecting-IP	2a06:98c0:3600::103
```

### Breaking DNS for sites not hosted on cloudflare for cloudflare clients
Cloudflare allows you to add any domain but in theory, it wont answer for it until you verify the ownership.

However, this does not hold true, in practice cloudflare creates an empty zone, that is happy to answer queries for until you verify the ownership. The resolution will not work (ie you cant have hosts in this DNS zone), but cloudflare will be happy to answer for it, effectively braking resolution for the given domain for clients that use the cloudflare resolvers. Not sure how this could be used but there you have it.