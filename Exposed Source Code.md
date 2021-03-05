# Exposed Source Code

## **Introduction**
Source code intended to be kept server-side can sometimes end up being disclosed to users. Such code may contain sensitive information such as database passwords and secret keys, which may help malicious users formulate attacks against the application.

## **How to Find**
1. Exposed Git folder
```
https://site.com/.git
```
![GIT folder](https://1.bp.blogspot.com/-wTZOuULaqNw/XliI9jS0w3I/AAAAAAAAATA/VZxs7VL5PCY8FdnoKaEjS6AWpcjoJz4MgCLcBGAsYHQ/s1600/1.png)

2. Exposed Subversion folder
```
https://site.com/.svn
```
![SVN folder](https://1.bp.blogspot.com/-5bC_EhFShgk/XliJqiw8pJI/AAAAAAAAATI/2HhrX0Ea3MwQ60Ax2tzNprNvulggPrZAACLcBGAsYHQ/s1600/1.png)

3. Exposed Mercurial folder
```
https://site.com/.hg
```
![HG folder](https://1.bp.blogspot.com/-4FaqUeTlv4k/XliKHBOpgmI/AAAAAAAAATQ/sLdwhvSF-Jgn0WF5P-PouLp6uTeHUAOWACLcBGAsYHQ/s1600/1.png)

4. Exposed Bazaar folder
```
http://target.com/.bzr
```
![BZR folder](https://1.bp.blogspot.com/-67WO_kL_iB8/XliKl1jggAI/AAAAAAAAATc/mWBw7igq05EdKR3JZmbXYN4LqjpBOrESgCLcBGAsYHQ/s1600/1.png)

5. Exposed Darcs folder
```
http://target.com/_darcs
```

6. Exposed Bitkeeper folder
```
http://target.com/Bitkeeper
```

Reference:
- [NakanoSec (my own post)](https://www.nakanosec.com/2020/02/exposed-source-code-pada-website.html)
