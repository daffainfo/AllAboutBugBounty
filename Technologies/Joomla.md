# Grafana

## Introduction
What would you do if you came across a website that uses Joomla ?

## How to Detect
Try to HTTP request to `https://example.com/` and if you see the source code, you will see something like this `<meta name="generator" content="Joomla! - Open Source Content Management" />`

1. Find the related CVE by checking the core, plugins, and theme version
* How to find the joomla version
```
https://target.com/administrator/manifests/files/joomla.xml
```

* How to find the joomla plugin version
```
https://target.com/administrator/components/com_NAMEPLUGIN/NAMEPLUGIN.xml

for example

https://target.com/administrator/components/com_contact/contact.xml
```

> or change NAMEPLUGIN.xml to `changelog.txt` or `readme.md` or `readme.txt`

* How to find the theme version
```
https://target.com/wp-content/themes/THEMENAME/style.css
https://target.com/wp-content/themes/THEMENAME/readme.txt (If they have readme file)
```
If you found outdated core / plugins, find the exploit at https://exploit-db.com

2. Joomla! Config Dist File
```
https://example.com/configuration.php-dist
```
3. Database File List
```
https://example.com/libraries/joomla/database/
```

## References
- [Exploit-db #6377](https://www.exploit-db.com/ghdb/6377)