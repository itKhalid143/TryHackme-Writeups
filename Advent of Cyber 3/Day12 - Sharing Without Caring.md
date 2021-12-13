
# Task 1

Let try to scan the host with ```-Pn``` flag!

```
nmap -Pn 10.10.91.15
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task12/q1.PNG)

``` java
PORT     STATE SERVICE
22/tcp   open  ssh
111/tcp  open  rpcbind
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
2049/tcp open  nfs
3389/tcp open  ms-wbt-server
```

# Task 2
From the previous scan we can see that NFS runs on port 2049, here's another scan for more detailed results!

![****](/Advent%20of%20Cyber%203/Screenshots/Task12/q2.PNG)

```java
PORT     STATE SERVICE VERSION
2049/tcp open  mountd  1-3 (RPC #100005)
```

# Task 3 & 4

- Network File System (NFS) is a protocol that allows the ability to transfer files between different computers and is available on many systems.

![****](/Advent%20of%20Cyber%203/Screenshots/Task12/q3.PNG)

# Task 5

- Let try to mount ```/share``` folder! and see what's inside it! as we have permission! the folder can be seen by everyone! 

![****](/Advent%20of%20Cyber%203/Screenshots/Task12/q5.PNG)

![****](/Advent%20of%20Cyber%203/Screenshots/Task12/q5-1.PNG)

# Task 6 & 7

From the shares! we can see an interesting share! which is ```confidential```
- Let now mount ```/confidential``` folder and see what's inside!

![****](/Advent%20of%20Cyber%203/Screenshots/Task12/q6.PNG)

```
id_rsa  id_rsa.pub
```

Let get the ```md5sum``` of ```id_rsa``` per the question!

![****](/Advent%20of%20Cyber%203/Screenshots/Task12/q7.PNG)

Thank you!
