# Lian_Yu Room
- This ain't an easy room as stated! I needed a lot of searches!

## Enumeration
### Nmap Scan
- The scan command I used!

```java
nmap -sV -sC -vv -T5 -oA result 10.10.166.125
```

- The results!

```java
PORT     STATE    SERVICE     REASON      VERSION
21/tcp   open     ftp         syn-ack     vsftpd 3.0.2
22/tcp   open     ssh         syn-ack     OpenSSH 6.7p1 Debian 5+deb8u8 (protocol 2.0)
| ssh-hostkey: 
|   1024 56:50:bd:11:ef:d4:ac:56:32:c3:ee:73:3e:de:87:f4 (DSA)
| ssh-dss AAAAB3NzaC1kc3MAAACBAOZ67Cx0AtDwHfVa7iZw6O6htGa3GHwfRFSIUYW64PLpGRAdQ734COrod9T+pyjAdKscqLbUAM7xhSFpHFFGM7NuOwV+d35X8CTUM882eJX+t3vhEg9d7ckCzNuPnQSpeUpLuistGpaP0HqWTYjEncvDC0XMYByf7gbqWWU2pe9HAAAAFQDWZIJ944u1Lf3PqYCVsW48Gm9qCQAAAIBfWJeKF4FWRqZzPzquCMl6Zs/y8od6NhVfJyWfi8APYVzR0FR05YCdS2OY4C54/tI5s6i4Tfpah2k+fnkLzX74fONcAEqseZDOffn5bxS+nJtCWpahpMdkDzz692P6ffDjlSDLNAPn0mrJuUxBFw52Rv+hNBPR7SKclKOiZ86HnQAAAIAfWtiPHue0Q0J7pZbLeO8wZ9XNoxgSEPSNeTNixRorlfZBdclDDJcNfYkLXyvQEKq08S1rZ6eTqeWOD4zGLq9i1A+HxIfuxwoYp0zPodj3Hz0WwsIB2UzpyO4O0HiU6rvQbWnKmUaH2HbGtqJhYuPr76XxZtwK4qAeFKwyo87kzg==
|   2048 39:6f:3a:9c:b6:2d:ad:0c:d8:6d:be:77:13:07:25:d6 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDRbgwcqyXJ24ulmT32kAKmPww+oXR6ZxoLeKrtdmyoRfhPTpCXdocoj0SqjsETI8H0pR0OVDQDMP6lnrL8zj2u1yFdp5/bDtgOnzfd+70Rul+G7Ch0uzextmZh7756/VrqKn+rdEVWTqqRkoUmI0T4eWxrOdN2vzERcvobqKP7BDUm/YiietIEK4VmRM84k9ebCyP67d7PSRCGVHS218Z56Z+EfuCAfvMe0hxtrbHlb+VYr1ACjUmGIPHyNeDf2430rgu5KdoeVrykrbn8J64c5wRZST7IHWoygv5j9ini+VzDhXal1H7l/HkQJKw9NSUJXOtLjWKlU4l+/xEkXPxZ
|   256 a6:69:96:d7:6d:61:27:96:7e:bb:9f:83:60:1b:52:12 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBPfrP3xY5XGfIk2+e/xpHMTfLRyEjlDPMbA5FLuasDzVbI91sFHWxwY6fRD53n1eRITPYS1J6cBf+QRtxvjnqRg=
|   256 3f:43:76:75:a8:5a:a6:cd:33:b0:66:42:04:91:fe:a0 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDexCVa97Otgeg9fCD4RSvrNyB8JhRKfzBrzUMe3E/Fn
80/tcp   open     http        syn-ack     Apache httpd
| http-methods: 
|_  Supported Methods: OPTIONS GET HEAD POST
|_http-server-header: Apache
|_http-title: Purgatory
111/tcp  open     rpcbind     syn-ack     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          39086/udp6  status
|   100024  1          45512/tcp6  status
|   100024  1          52090/udp   status
|_  100024  1          56941/tcp   status
1272/tcp filtered cspmlockmgr no-response
1600/tcp filtered issd        no-response
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

## Content Discovery!

- The scan command I used!

```java
gobuster dir -u 10.10.166.125 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -o dirbuster-first.txt -q -t 30
```
- The results!

```java
/island               (Status: 301) [Size: 236] [--> http://10.10.166.125/island/]
```

![****](/Lian_Yu/Screenshots/island.PNG)

![****](/Lian_Yu/Screenshots/page1.PNG)

- They told us, we need to look for a directory, that has numbers! it's 4 digits numbers! so I did this!

```java
gobuster dir -u 10.10.166.125/island -w /usr/share/seclists/Fuzzing/4-digits-0000-9999.txt -o dirbuster-second.txt -q -t 30
```
- The result!

```java
/2100                 (Status: 301) [Size: 241] [--> http://10.10.166.125/island/2100/]
```

![****](/Lian_Yu/Screenshots/2100.PNG)

![****](/Lian_Yu/Screenshots/page2.PNG)


```java
gobuster dir -u 10.10.204.227/island/2100 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -o dirbuster-thinrd.txt -x .ticket -q -t 30

```

```java
/green_arrow.ticket   (Status: 200) [Size: 71]
```

![****](/Lian_Yu/Screenshots/ticket.PNG)

![****](/Lian_Yu/Screenshots/page3.PNG)

## It seems we got some Credentials here! Let try to open that FTP!

- First I've tried to use the current Password! it didn't work! so I needed to check that hit! and Boom! it's ```Base58``` decoded.

```java
vigilante:!#th*****
```

### FTP 

![****](/Lian_Yu/Screenshots/ftp.PNG)

```java
ftp> ls -la 
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 1001     1001         4096 May 05  2020 .
drwxr-xr-x    4 0        0            4096 May 01  2020 ..
-rw-------    1 1001     1001           44 May 01  2020 .bash_history
-rw-r--r--    1 1001     1001          220 May 01  2020 .bash_logout
-rw-r--r--    1 1001     1001         3515 May 01  2020 .bashrc
-rw-r--r--    1 0        0            2483 May 01  2020 .other_user
-rw-r--r--    1 1001     1001          675 May 01  2020 .profile
-rw-r--r--    1 0        0          511720 May 01  2020 Leave_me_alone.png
-rw-r--r--    1 0        0          549924 May 05  2020 Queen's_Gambit.png
-rw-r--r--    1 0        0          191026 May 01  2020 aa.jpg
226 Directory send OK.
```

- Everything I do after opening an FTP is! ```Downloading everything!```, Everything is valuable!


![****](/Lian_Yu/Screenshots/ftpls.PNG)

Let try to run ```file``` command on our new discovered files!

![****](/Lian_Yu/Screenshots/file.PNG)

- We noticed that ```aa.jpg``` is hiding something under it!! it's time for some Steganography!

```java
steghide extract -sf ./aa.jpg
```

![****](/Lian_Yu/Screenshots/steg.PNG)

- We need a password to open it! Let check that ```Leave_me_alone.png``` file!


![****](/Lian_Yu/Screenshots/leaveme.PNG)
![****](/Lian_Yu/Screenshots/leaveme2.PNG)

- This is Intereting! Let dig more!

```java
xxd Leave_me_alone.png
```

```java
0007ce80: 169f 63ba 5687 a49c ec2b 199c 78fb f3e7  ..c.V....+..x...
0007ce90: bf0f d9ff 90f5 af19 593a b956 e02a fe3d  ........Y:.V.*.=
0007cea0: 3a4d 1e40 c10f 357f 0e95 4032 c8b9 3ed3  :M.@..5...@2..>.
0007ceb0: 0a02 d267 6864 448d 7c2e 1cdb 6991 c0fd  ...ghdD.|...i...
0007cec0: b07e f85d 339d 3a3e ab74 e704 d0fe 687d  .~.]3.:>.t....h}
0007ced0: be75 fd0f a885 37b2 807d 465d 0000 0000  .u....7..}F]....
0007cee0: 4945 4e44 ae42 6082                      IEND.B`.
```

- Hmmm! a quick search on google ```IEND file format``` the last chunk show us this is a png file. Let try to see the header! 

![****](/Lian_Yu/Screenshots/cunk.PNG)

```java
00000000: 5845 6fae 0a0d 1a0a 0000 000d 4948 4452  XEo.........IHDR
00000010: 0000 034d 0000 01db 0806 0000 0017 a371  ...M...........q
00000020: 5b00 0020 0049 4441 5478 9cac bde9 7a24  [.. .IDATx....z$
```

- This is weird!


- We know PNG file signature starts with ```89 50 4E 47 0D 0A 1A 0A``` thanks to filesignatures.net, now let edit!

![****](/Lian_Yu/Screenshots/hexeditor.PNG)

- This is better!

![****](/Lian_Yu/Screenshots/password.PNG)

- We did it boys!

now let try to ```steghide``` with password is ```password```
```java
steghide extract -sf ./aa.jpg
Enter passphrase: 
wrote extracted data to "ss.zip".
```

![****](/Lian_Yu/Screenshots/ss.PNG)

# It's time for some SSH!

- I've tried with Oliver and vigilente Username! None worked! Then I remembered we downloaded a file from the FTP with the name ```.other_user```.

![****](/Lian_Yu/Screenshots/names.PNG)

- There's a lot of names to try! let see with Slade!

![****](/Lian_Yu/Screenshots/ssh.PNG)

- We did it!

![****](/Lian_Yu/Screenshots/user.png)

## Time for some privesc!

- as always! I am ```sudo -l``` fan! with some help of GTFOBins.

![****](/Lian_Yu/Screenshots/root.png)

# We did it Amazing Hackers!

