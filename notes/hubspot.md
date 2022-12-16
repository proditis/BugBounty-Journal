# HubSpot CMS

## Endpoints
```
/_hcms/perf
/_hcms/search
/_hcms/postlisting
/_hcms/api
/_hcms/api/authenticate
/_hcms/api/submit
/_hcms/api/register
/_hcms/oembed?url=/&autoplay=0
/_hcms/mem/login?redirect_url
/_hcms/mem/register
/_hcms/mem/reset/request
/_hcms/mem/reset
```

## Headers
* Headers that can be used to trigger different responses
* `-H 'Accept: application/json'`
* `-H 'X-HubSpot-Trace: db5e4d104197e0f846705bba21687822'`
* `-H 'X-HubSpot-Correlation-Id: 330238d5-55ad-4f15-8192-8bb6ad03c51d'`
* `-H 'X-HS-Internal-Request: 1'`
* `-H 'X-HS-User-Request: 0'`
* `-H 'X-HS-Internal-User-Request: 0'`
* `-H 'X-Forwarded-For: 127.0.0.1'`

## Commonly used keys to look for
* `HUBSPOT_PORTAL_ID`
* `HUBSPOT_API_KEY`