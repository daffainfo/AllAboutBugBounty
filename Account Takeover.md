## Account Takeover

1. Using OAuth Misconfiguration
   - Victim has a account in evil.com
   - Attacker creates an account on evil.com using OAuth. For example the attacker have a facebook with a registered victim email
   - Attacker changed his/her email to victim email.
   - When the victim try to create an account on evil.com, it says the email already exists.

2. Try re-sign up using same email
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