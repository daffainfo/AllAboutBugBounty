# Shodan Dorks
## Basic
### City:
Find devices in a particular city.
```
city:"Bangalore"
```

### Country:
Find devices in a particular country.
```
country:"IN"
```

### Geo:
Find devices by giving geographical coordinates.
```
geo:"56.913055,118.250862"
```

### Location
```
country:us
country:ru
city:chicago
country:ru country:de city:chicago
```

### Hostname:
Find devices matching the hostname.
```
server: "gws" hostname:"google"
hostname:example.com
hostname:example.com,example.org
```

### Net:
Find devices based on an IP address or /x CIDR.
```
net:210.214.0.0/16
```

### Organization
```
org:microsoft
org:"United States Department"
```

### Autonomous System Number (ASN)
```
asn:ASxxxx
```

### OS:
Find devices based on operating system.
```
os:"windows 7"
```

### Port:
Find devices based on open ports.
```
proftpd port:21
```

### Before/after:
Find devices before or after between a given time.
```
apache after:22/02/2009 before:14/3/2010
```

### SSL/TLS Certificates
- Self signed certificates
```
ssl.cert.issuer.cn:example.com ssl.cert.subject.cn:example.com
```
- Expired certificates
```
ssl.cert.expired:true
ssl.cert.subject.cn:example.com
```

### Device Type
```
device:firewall
device:router
device:wap
device:webcam
device:media
device:"broadband router"
device:pbx
device:printer
device:switch
device:storage
device:specialized
device:phone
device:"voip phone"
device:"voip adaptor"
device:"load balancer"
device:"print server"
device:terminal
device:remote
device:telecom
device:power
device:proxy
device:pda
device:bridge
```

### Operating System
```
os:"windows 7"
os:"windows server 2012"
os:"linux 3.x"
```

### Product
```
product:apache
product:nginx
product:android
product:chromecast
```

### Customer Premises Equipment (CPE)
```
cpe:apple
cpe:microsoft
cpe:nginx
cpe:cisco
```

### Server
```
server: nginx
server: apache
server: microsoft
server: cisco-ios
```

### ssh fingerprints
```
dc:14:de:8e:d7:c1:15:43:23:82:25:81:d2:59:e8:c0
```

## Web

### Pulse Secure
```
http.html:/dana-na
```

### PEM Certificates
```
http.title:"Index of /" http.html:".pem"
```

## Databases
### MySQL 
```
"product:MySQL"
```

### MongoDB 
```
"product:MongoDB"
```

### elastic 
```
port:9200 json
```

### Memcached 
```
"product:Memcached"
```

### CouchDB 
```
"product:CouchDB"
```

### PostgreSQL 
```
"port:5432 PostgreSQL"
```

### Riak 
```
"port:8087 Riak"
```

### Redis 
```
"product:Redis"
```

### Cassandra 
```
"product:Cassandra"
```

## Industrial Control Systems
### Samsung Electronic Billboards
```
"Server: Prismview Player"
```

### Gas Station Pump Controllers
```
"in-tank inventory" port:10001
```

### Fuel Pumps connected to internet:
No auth required to access CLI terminal.
```
"privileged command" GET
```

### Automatic License Plate Readers
```
P372 "ANPR enabled"
```

### Traffic Light Controllers / Red Light Cameras
```
mikrotik streetlight
```

### Voting Machines in the United States
```
"voter system serial" country:US
```

### Open ATM:
```
May allow for ATM Access availability
NCR Port:"161"
```

### Telcos Running Cisco Lawful Intercept Wiretaps
```
"Cisco IOS" "ADVIPSERVICESK9_LI-M"
```

### Prison Pay Phones
```
"[2J[H Encartele Confidential"
```

### Tesla PowerPack Charging Status
```
http.title:"Tesla PowerPack System" http.component:"d3" -ga3ca4f2
```

### Electric Vehicle Chargers
```
"Server: gSOAP/2.8" "Content-Length: 583"
```

### Maritime Satellites
Shodan made a pretty sweet Ship Tracker that maps ship locations in real time, too!
```
"Cobham SATCOM" OR ("Sailor" "VSAT")
```

### Submarine Mission Control Dashboards
```
title:"Slocum Fleet Mission Control"
```

### CAREL PlantVisor Refrigeration Units
```
"Server: CarelDataServer" "200 Document follows"
```

### Nordex Wind Turbine Farms
```
http.title:"Nordex Control" "Windows 2000 5.0 x86" "Jetty/3.1 (JSP 1.1; Servlet 2.2; java 1.6.0_14)"
```

### C4 Max Commercial Vehicle GPS Trackers
```
"[1m[35mWelcome on console"
```

### DICOM Medical X-Ray Machines
Secured by default, thankfully, but these 1,700+ machines still have no business being on the internet.
```
"DICOM Server Response" port:104
```

### GaugeTech Electricity Meters
```
"Server: EIG Embedded Web Server" "200 Document follows"
```

### Siemens Industrial Automation
```
"Siemens, SIMATIC" port:161
```

### Siemens HVAC Controllers
```
"Server: Microsoft-WinCE" "Content-Length: 12581"
```

### Door / Lock Access Controllers
```
"HID VertX" port:4070
```

### Railroad Management
```
"log off" "select the appropriate"
```

### Tesla Powerpack charging Status:
Helps to find the charging status of tesla powerpack.
```
http.title:"Tesla PowerPack System" http.component:"d3" -ga3ca4f2
```

### XZERES Wind Turbine
``` 
title:"xzeres wind"
```

### PIPS Automated License Plate Reader 
```
"html:"PIPS Technology ALPR Processors""
```

### Modbus
``` 
"port:502"
```

### Niagara Fox 
```
"port:1911,4911 product:Niagara"
```

### GE-SRTP 
```
"port:18245,18246 product:"general electric""
```

### MELSEC-Q 
```
"port:5006,5007 product:mitsubishi"
```

### CODESYS 
```
"port:2455 operating system"
```

### S7 
```
"port:102"
```

### BACnet 
```
"port:47808"
```

### HART-IP 
```
"port:5094 hart-ip"
```

### Omron FINS 
```
"port:9600 response code"
```

### IEC 60870-5-104 
```
"port:2404 asdu address"
```

### DNP3 
```
"port:20000 source address"
```

### EtherNet/IP 
```
"port:44818"
```

### PCWorx 
```
"port:1962 PLC"
```

### Crimson v3.0 
```
"port:789 product:"Red Lion Controls"
```

### ProConOS 
```
"port:20547 PLC"
```

## Remote Desktop
### Unprotected VNC
```
"authentication disabled" port:5900,5901
"authentication disabled" "RFB 003.008"
```

### Windows RDP
99.99% are secured by a secondary Windows login screen.

```
"\x03\x00\x00\x0b\x06\xd0\x00\x00\x124\x00"
```
## Network Infrastructure
### Hacked routers:
Routers which got compromised
```
hacked-router-help-sos
```

### Redis open instances
```
product:"Redis key-value store"
```

### Citrix:
Find Citrix Gateway.
```
title:"citrix gateway"
```

### Weave Scope Dashboards
Command-line access inside Kubernetes pods and Docker containers, and real-time visualization/monitoring of the entire infrastructure.
```
title:"Weave Scope" http.favicon.hash:567176827
```

### MongoDB
Older versions were insecure by default. Very scary.
```
"MongoDB Server Information" port:27017 -authentication
```

### Mongo Express Web GUI
Like the infamous phpMyAdmin but for MongoDB.
```
"Set-Cookie: mongo-express=" "200 OK"
```

### Jenkins CI
```
"X-Jenkins" "Set-Cookie: JSESSIONID" http.title:"Dashboard"
```

### Jenkins:
Jenkins Unrestricted Dashboard
```
x-jenkins 200
```

### Docker APIs
```
"Docker Containers:" port:2375
```

### Docker Private Registries
```
"Docker-Distribution-Api-Version: registry" "200 OK" -gitlab
```

### Pi-hole Open DNS Servers
```
"dnsmasq-pi-hole" "Recursion: enabled"
```

### Already Logged-In as root via Telnet
```
"root@" port:23 -login -password -name -Session
```

### Telnet Access:
NO password required for telnet access.
```
port:23 console gateway
```

### Polycom video-conference system no-auth shell
```
"polycom command shell"
```

### NPort serial-to-eth / MoCA devices without password
```
nport -keyin port:23
```

### Android Root Bridges
A tangential result of Google's sloppy fractured update approach.
```
"Android Debug Bridge" "Device" port:5555
```

### Lantronix Serial-to-Ethernet Adapter Leaking Telnet Passwords
```
Lantronix password port:30718 -secured
```

### Citrix Virtual Apps
```
"Citrix Applications:" port:1604
```

### Cisco Smart Install
Vulnerable (kind of "by design," but especially when exposed).
```
"smart install client active"
```

### PBX IP Phone Gateways
```
PBX "gateway console" -password port:23
```

### Polycom Video Conferencing
```
http.title:"- Polycom" "Server: lighttpd"
"Polycom Command Shell" -failed port:23
```

### Telnet Configuration:
```
"Polycom Command Shell" -failed port:23
```

### Bomgar Help Desk Portal
```
"Server: Bomgar" "200 OK"
```

### Intel Active Management CVE-2017-5689
```
"Intel(R) Active Management Technology" port:623,664,16992,16993,16994,16995
”Active Management Technology”
```

### HP iLO 4 CVE-2017-12542
```
HP-ILO-4 !"HP-ILO-4/2.53" !"HP-ILO-4/2.54" !"HP-ILO-4/2.55" !"HP-ILO-4/2.60" !"HP-ILO-4/2.61" !"HP-ILO-4/2.62" !"HP-iLO-4/2.70" port:1900
```

### Lantronix ethernet adapter’s admin interface without password
```
"Press Enter for Setup Mode port:9999"
```

### Wifi Passwords:
Helps to find the cleartext wifi passwords in Shodan.
```
html:"def_wirelesspassword"
```

### Misconfigured Wordpress Sites:
The wp-config.php if accessed can give out the database credentials.
```
http.html:"* The wp-config.php creation script uses this file"
```

## Outlook Web Access:
### Exchange 2007
```
"x-owa-version" "IE=EmulateIE7" "Server: Microsoft-IIS/7.0"
```

### Exchange 2010
```
"x-owa-version" "IE=EmulateIE7" http.favicon.hash:442749392
```

### Exchange 2013 / 2016
```
"X-AspNet-Version" http.title:"Outlook" -"x-owa-version"
```

### Lync / Skype for Business
```
"X-MS-Server-Fqdn"
```

## Network Attached Storage (NAS)
### SMB (Samba) File Shares
Produces ~500,000 results...narrow down by adding "Documents" or "Videos", etc.
```
"Authentication: disabled" port:445
```

### Specifically domain controllers:
```
"Authentication: disabled" NETLOGON SYSVOL -unix port:445
```

### Concerning default network shares of QuickBooks files:
```
"Authentication: disabled" "Shared this folder to access QuickBooks files OverNetwork" -unix port:445
```

### FTP Servers with Anonymous Login
```
"220" "230 Login successful." port:21
```

### Iomega / LenovoEMC NAS Drives
```
"Set-Cookie: iomega=" -"manage/login.html" -http.title:"Log In"
```

### Buffalo TeraStation NAS Drives
```
Redirecting sencha port:9000
```

### Logitech Media Servers
```
"Server: Logitech Media Server" "200 OK"
```
### Plex Media Servers
```
"X-Plex-Protocol" "200 OK" port:32400
```

### Tautulli / PlexPy Dashboards
```
"CherryPy/5.1.0" "/home"
```

### Home router attached USB
```
"IPC$ all storage devices"
```

## Webcams
### D-Link webcams
```
"d-Link Internet Camera, 200 OK"
```

### Hipcam
```
"Hipcam RealServer/V1.0"
```

### Yawcams
```
"Server: yawcam" "Mime-Type: text/html"
```

### webcamXP/webcam7
```
("webcam 7" OR "webcamXP") http.component:"mootools" -401
```

### Android IP Webcam Server
```
"Server: IP Webcam Server" "200 OK"
```

### Security DVRs
```
html:"DVR_H264 ActiveX"
```

### Surveillance Cams:
With username:admin and password: :P
```
NETSurveillance uc-httpd
Server: uc-httpd 1.0.0
```

## Printers & Copiers:
### HP Printers
```
"Serial Number:" "Built:" "Server: HP HTTP"
```

### Xerox Copiers/Printers
```
ssl:"Xerox Generic Root"
```

### Epson Printers
```
"SERVER: EPSON_Linux UPnP" "200 OK"
"Server: EPSON-HTTP" "200 OK"
```

### Canon Printers
```
"Server: KS_HTTP" "200 OK"
"Server: CANON HTTP Server"
```

## Home Devices
### Yamaha Stereos
```
"Server: AV_Receiver" "HTTP/1.1 406"
```

### Apple AirPlay Receivers
Apple TVs, HomePods, etc.
```
"\x08_airplay" port:5353
```

### Chromecasts / Smart TVs
```
"Chromecast:" port:8008
```

### Crestron Smart Home Controllers
```
"Model: PYNG-HUB"
```

## Random Stuff
### OctoPrint 3D Printer Controllers
```
title:"OctoPrint" -title:"Login" http.favicon.hash:1307375944
```

### Etherium Miners
```
"ETH - Total speed"
```

### Apache Directory Listings
Substitute .pem with any extension or a filename like phpinfo.php.
```
http.title:"Index of /" http.html:".pem"
```

### Misconfigured WordPress
Exposed wp-config.php files containing database credentials.
```
http.html:"* The wp-config.php creation script uses this file"
```

### Too Many Minecraft Servers
```
"Minecraft Server" "protocol 340" port:25565
```

### Literally Everything in North Korea
```
net:175.45.176.0/22,210.52.109.0/24,77.94.35.0/24
```