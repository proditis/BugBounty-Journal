# CDN
* Use the `register`, `forgot password` and similar operations to grab the IP of the server protected behind a CDN

## Cloudflare
### Only cloudflare IP's allowed?
Use the cloudflare workers to perform requests on given hosts and thus appearing as if the source IP was from cloudflare. (confirmed)

### Use cloudflare workers to perform unfiltered url scans?
Using the workers API one could create a specific worker that will perform massive scans on hosts protected by cloudflare? This is just an idea at this point.


### Breaking DNS for sites not hosted on cloudflare for cloudflare clients
Cloudflare allows you to add any domain but in theory, it wont answer for it until you verify the ownership.

However, this does not hold true, in practice cloudflare creates an empty zone, that is happy to answer queries for until you verify the ownership. The resolution will not work (ie you cant have hosts in this DNS zone), but cloudflare will be happy to answer for it, effectively braking resolution for the given domain for clients that use the cloudflare resolvers. Not sure how this could be used but there you have it.