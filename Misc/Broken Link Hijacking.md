# Broken Link Hijacking
## **Introduction**
Broken Link Hijacking (BLH) exists whenever a target links to an expired domain or page

## **How to Find**
1. Manually find external links on the target site (For example, check some links to social media accounts)
2. Try [broken-link-checker](https://github.com/stevenvachon/broken-link-checker) tools to find broken link, this is the command

```
blc -rof --filter-level 3 https://vuln.com/
```

References:
- [Broken Link Hijacking - How expired links can be exploited.](https://edoverflow.com/2017/broken-link-hijacking/)

- [How I was able to takeover the company’s LinkedIn Page](https://medium.com/@bathinivijaysimhareddy/how-i-takeover-the-companys-linkedin-page-790c9ed2b04d)