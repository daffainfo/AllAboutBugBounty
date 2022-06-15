# Exposed API Keys / Token OAuth

## Introduction
Sometimes in a web application, an attacker can find some exposed API keys / token which can lead to financial loss to a company.

## How to find
1. Find API keys / token by looking at the JavaScript code on the website
2. Find API keys / token by checking the request / response header

## Tools
* [Key-Checker](https://github.com/daffainfo/Key-Checker)

# References
* [keyhacks](https://github.com/streaak/keyhacks) is a repository which shows quick ways in which API keys leaked by a bug bounty program can be checked to see if they're valid. There is 79 list of how to check the validity of the API keys
* [all-about-apikey](https://github.com/daffainfo/all-about-apikey) is a repository of detailed information about API Key / Oauth tokens. The repository contain description API key, HTTP request, the response if the API key is valid / no, regex, and the example