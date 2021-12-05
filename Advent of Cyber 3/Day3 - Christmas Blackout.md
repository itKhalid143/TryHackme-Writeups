# Content Discovery

## We're bruteforcing contents using gobuster (Most powerful tool out there!)

```gobuster dir -u 10.10.240.102 -w wordlist.txt   
```

## The result like this!
![****](/Advent%20of%20Cyber%203/Screenshots/Task3/gobuster.PNG)
```
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.240.102
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                wordlist.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/12/05 02:09:45 Starting gobuster in directory enumeration mode
===============================================================
```
```js
/admin/               (Status: 200) [Size: 2251]
```
```                                                
===============================================================
2021/12/05 02:09:45 Finished
===============================================================
```

## Now let's try to check the hidden directory that we've found!


![****](/Advent%20of%20Cyber%203/Screenshots/Task3/login.PNG)

## Aw! as penetration testers! our first move is Guessing the credentials! from the default!

![****](/Advent%20of%20Cyber%203/Screenshots/Task3/default.PNG)


![****](/Advent%20of%20Cyber%203/Screenshots/Task3/in.PNG)

## We're in!