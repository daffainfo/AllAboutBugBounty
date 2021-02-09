# JWT Vulnerabilities
## Introduction
JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

## How to Exploit
1. Modify the algorithm to "none" algorithm
```
{
  "alg": "none",
  "typ": "JWT"
}
```
2. Modify the algorithm RS256 to HS256

If you change the algorithm from RS256 to HS256, the backend code uses the public key as the secret key and then uses the HS256 algorithm to verify the signature.

3. Bruteforce HS256
   
the HS256 key strength is weak, it can be directly brute-forced, such as using the secret string as a key in the PyJWT library sample code.

Reference:
- [Hacking JSON Web Token (JWT)](https://medium.com/101-writeups/hacking-json-web-token-jwt-233fe6c862e6)