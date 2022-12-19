# SOAP and WSDL
- [SOAP and WSDL](#soap-and-wsdl)
  - [Resources](#resources)
  - [Tools](#tools)
  - [Tips and Tricks](#tips-and-tricks)
    - [Commonly used headers (for curl)](#commonly-used-headers-for-curl)
    - [Examples](#examples)

## Resources
* https://www.w3schools.com/xml/xml_wsdl.asp
* https://www.tutorialworks.com/wsdl/

## Tools
* Useful tools SoapUI

## Tips and Tricks
* On servers running Windows Communication Foundation (WCF) services, which is also SOAP based, you see a message like this:
  ```
    <p class="heading1">Service</p>
    <p>Endpoint not found.</p>
  ```


### Commonly used headers (for curl)
* `-H "Content-Type: application/soap+xml"`
* `-H 'Content-Type: text/xml'`
* `-H 'SOAPAction: service:getSomething'`

### Examples
* Download WSDL spec
```sh
curl -o service.wsdl https://site/dir/service?wsdl
```

* Grep `schemaLocation` to get the XSD file locations to check if they are present
```sh
$ grep schemaLocation service.wsdl
<xsd:import namespace="https://site/dir" schemaLocation="service?xsd=service.xsd"/>
```

* download the XSD-Files:
```
curl -o service.xsd https://site/dir/service?xsd=service.xsd
```

* cURL SOAP request
```
curl -X POST http://site/dir/service \
  -H 'Content-Type: text/xml' \
  -H 'SOAPAction: service:getSomething' \
  -d '
  <soapenv:Envelope
    xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
    xmlns:blz="http://site/dir/service">
    <soapenv:Header/>
    <soapenv:Body>
      <blz:geSomething>
        <blz:blz>10020200</blz:blz>
      </blz:getSomething>
    </soapenv:Body>
  </soapenv:Envelope>'
```

* Authentication example
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:axis="http://axis2wstest">
  <soapenv:Header>
    <wsse:Security xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" soapenv:mustUnderstand="1">
      <wsse:UsernameToken xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd" wsu:Id="123">
        <wsse:Username>test</wsse:Username>
        <wsse:Password Type="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0#PasswordText">pass</wsse:Password>
      </wsse:UsernameToken>
    </wsse:Security>
  </soapenv:Header>
  <soapenv:Body>
    <axis:testws>
      <!--Optional:-->
      <axis:x>5</axis:x>
    </axis:testws>
  </soapenv:Body>
</soapenv:Envelope>
```
