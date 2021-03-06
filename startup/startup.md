# Startup Room


## Enumeration

#### nmap Scan

The command I used!

```java
nmap -sV -sC -vv -T4 -oA result 10.10.60.47
```

![****](/startup/Screenshots/nmap.PNG)


```java
PORT      STATE    SERVICE REASON      VERSION
21/tcp    open     ftp     syn-ack     vsftpd 3.0.3
22/tcp    open     ssh     syn-ack     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
```


#### Content Discovery!

The command used!

```java
gobuster dir -u 10.10.60.47 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -o dirbuster--result.txt
```

The results!

```
/files                (Status: 301) [Size: 310] [--> http://10.10.60.47/files/]
```

![****](/startup/Screenshots/web.PNG)

After checking the website! I instantely released that this web server has a relationship with the FTP! means, let try to upload something in the ftp and see if we got the results in our folder!

### FTP

Tried to login to the FTP server as Anonymous!

![****](/startup/Screenshots/ftp.PNG)

It worked! Now let try to upload a shell if we can!

![****](/startup/Screenshots/put.PNG)

It worked! Now let check the website!!

![****](/startup/Screenshots/shell.PNG)

Let see if we get a connection back to our Netcat listenner!

![****](/startup/Screenshots/netcat.PNG)

## Task 1

![****](/startup/Screenshots/task1.PNG)

## Task 2

That ```incidents``` folder is weird! right? Let check it out!

![****](/startup/Screenshots/download.PNG)

Let Download the file, open it and try to analyse it!

![****](/startup/Screenshots/pw.PNG)

After analysing, we got a password! Maybe it's ```lennie```'s' password?

![****](/startup/Screenshots/lennie.PNG)

We did it boiis!!

## Task 3

Now, lets check inside lennie's home directory! right? we see a folder wth root privlges! Let see what is inside! 

![****](/startup/Screenshots/ls.PNG)

We see that ```startup_list.txt``` file is modified recently! Mean there's a kind of automation!! Now let check ```planner.sh```

![****](/startup/Screenshots/planner.PNG)

hmmm! ```/etc/print.sh``` looks interesting!

After listing the file and it's info! we notice that this file is created by our user lennie! means we can edit it!
Let try to make a reverse shell and see if we can get root access!

![****](/startup/Screenshots/root.PNG)

We added our malicious code to the file! after a minute! the file is executed by the root! and we got our shell as root user!

Well done!

