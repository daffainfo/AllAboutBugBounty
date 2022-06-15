# Email Spoofing

## Introduction
Email spoofing is a technique used in spam and phishing attacks to trick users into thinking a message came from a person or entity they either know or can trust. In spoofing attacks, the sender forges email headers so that client software displays the fraudulent sender address, which most users take at face value.

## How to detect
1. Check the SPF records, if the website don't have a SPF record, the website must be vulnerable to email spoofing
```
v=spf1 include:_spf.google.com ~all
```
2. Check the DMARC records, if the website don't have a DMARC record or the value of tag policy is `none`, the website must be vulnerable to email spoofing
```
v=DMARC1; p=none; rua=mailto:dmarc@yourdomain.com
```

Reference:
- [Hackerone #1071521](https://hackerone.com/reports/1071521)