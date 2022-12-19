# DNS Information Gathering
- [DNS Information Gathering](#dns-information-gathering)
  - [`host` command](#host-command)

## `host` command
* DKIM
  ```shell
  # Office365
  host -t txt selector1._domainkey.$DOMAIN
  host -t txt selector2._domainkey.$DOMAIN
  ```
* Look for TXT records and in particular SPF since they often list mail server ips, particularly useful if the site is behind a CDN, it may leak IPs
  ```
  host -t txt $DOMAIN
  ```
* Look for authoritative DNS (easy check for servers behind cdn)
  ```
  host -t ns $DOMAIN
  ```

* Look for MX records on each domain (mx server usually give their IP)
  ```
  host -t mx $DOMAIN
  ```

* Get any available records from DNS regarding the domain
  ```
  host -t any $DOMAIN
  ```
