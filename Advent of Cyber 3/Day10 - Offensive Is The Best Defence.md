# Networking! 

## Task 1 & 2 & 3
 
```java
nmap -sT 10.10.138.50
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task10/q1.PNG)

```java
22/tcp open  ssh
80/tcp open  http
```

## Task 4

```
nmap -sS 10.10.138.50
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task10/q4.PNG)

```java
 open  ssh
80/tcp open  http
```

- We got the same result as the first scan!

## Task 5

```java
nmap -sV 10.10.138.50
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task10/q5.PNG)

```java
80/tcp   open     http            Apache httpd 2.4.49
```

## Task 6

- A quick search on Google, it turned out that this version of apache is vulnerable to ***Path Traversal & Remote Code Execution***.

![****](/Advent%20of%20Cyber%203/Screenshots/Task10/q6.PNG)

## Task 7

Scanning all ports! 

```java
nmap -p1-65535 -T5 10.10.138.50
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task10/q7.PNG)


```java
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
20212/tcp open  unknown
```

## Task 8

![****](/Advent%20of%20Cyber%203/Screenshots/Task10/q8.PNG)

```java
PORT      STATE SERVICE VERSION
20212/tcp open  telnet  Linux telnetd
```

It turned out this is a telnet service!