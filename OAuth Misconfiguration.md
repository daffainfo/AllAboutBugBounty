# OAuth Misconfiguration
1. OAuth token stealing: Changing redirect_uri to attacker(.)com(Use IDN Homograph or common bypasses).
2. Change Referral header to attacker(.)com while requesting OAuth.
3. Create an account with victim@gmail(.)com with normal functionality. Create account with victim@gmail(.)com using OAuth functionality. Now try to login using previous credentials.
4. OAuth Token Re-use.
5. Missing or broken state parameter.
6. Lack of origin check.
7. Open Redirection on another endpoint > Use it in redirect_uri
8. If there is an email parameter after signin then try to change the email parameter to victim's one.
9. Try to remove email from the scope and add victim's email manually.
10. Only company's email is allowed? > Try to replace hd=company(.)com to hd=gmail(.)com
11.  Check if its leaking client_secret parameter.
12.  Go to the browser history and check if the token is there.

Reference:
- https://twitter.com/tuhin1729_/status/1417843523177484292
