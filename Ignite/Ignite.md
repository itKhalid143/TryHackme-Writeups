# The CodeIgniter framework

## Enumeration

### nmap scan!

![****](/Ignite/Screenshots/nmap.PNG)

```java
PORT   STATE SERVICE REASON  VERSION
80/tcp open  http    syn-ack Apache httpd 2.4.18 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 1 disallowed entry 
|_/fuel/
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Welcome to FUEL CMS
```

Checking the website!

![****](/Ignite/Screenshots/fuel.PNG)

Now let check for any common exploit of this version of CMS!

![****](/Ignite/Screenshots/exploitdb.PNG)

We've found something!!
Let try to use it! and get our reverse shell!

![****](/Ignite/Screenshots/python.PNG)

Our Netcat Listenner!

![****](/Ignite/Screenshots/listenner.PNG)

# user.txt

Let see what's inside the home directory!

![****](/Ignite/Screenshots/flag.PNG)

We've got it! that wasn't hard!

# root.txt

- Trying some known privesc methods! but don't really have the password for the user! so instead I was looking in the files for database config files and found it in! ```/var/www/html/fuel/application/config/database.php```

- After getting the password! just tried the ```su root```, didn't have hopes that it will work! surprisingly it did! 

![****](/Ignite/Screenshots/root.PNG)

![****](/Ignite/Screenshots/root2.PNG)

Thanks!