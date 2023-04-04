Linux adminstration topic continution of previous video

- **Process Management:**
- For example lets take chrome is not working properly then open windows task manager to shown the process which are running on the windows. Same way that linux also process which are running inside the linux same process management can be used.
- In redhat family OS, every command you excute is going to create a process in the system. Also that process is going to get one unique number allocated to it which is called as “PID”(processid)
- Those process can be fetched by using the command **ps**
- list of process which are running on the system by using command

```bash
ps
```

- If you want to see the all the process by using command

```bash
ps -u
```

- If i dont want all the process which are running  i want only related to my user and my session i want whole process which are running in my system by using the command

```bash
ps -e
```

- “e” stand for all
- To shown the information with length

```bash
ps -ef
```

- How do you stop the process in linux by using **sleep** command in this command we will give the number of sec of the command line process will stop until the timer is completed.
- stop means we can resume back after completed the time.

```bash
sleep <timer>
sleep 5
```

- To give the fast output by using the command

```bash
sleep 100 &
```

- To backround check the process

```bash
ps -ef | grep sleep
```

- To end the task in linux completly by using the command **kill.**
- Syntax kill <pid>

```bash
kill <process id>
kill 920
```

- Sometimes kill will be their we need to kill the process forcefully by using command.
- Process management is used to process the applications which are running inside the OS.
- Process Management is used to identify the my application is running or not.

```bash
kill -9 <pid>
kill -9 1542
```

## **User Management:**

- We use our servers to run the web applications these applications are process inside the system . The process is used to run the normal user rather than root user.
- For security purposes user mangement can used.
- To create the user by using command

```bash
useradd <name>
useradd john
```

- To check the user is created or not by using command

```bash
id <username>
id john
```

- Every user can be associate with a numbers.
- To create the password to the user by using command

```bash
passwd <username>
passwd john
```

- 

```bash
The following command will run some services inside the system and you can check those process are ran by a certain user but not by a root user.
```

```bash
curl -s https://raw.githubusercontent.com/devopstrainings/linux-basics-katakoda/master/linux-adminstration/files/daemon-services.sh | bash
```

```bash
You can check the process of some system services runs as a normal user but not as a root user.
```

```bash
ps -ef | grep httpd
```

```bash
ps -ef | grep tomcat
```

```bash
ps -ef | grep mysql
```

- To switch the one user to another using by using command **su**

```bash
su - <username>
su - john
```

- How to delete the user by using **userdel** command

```bash
userdel <user name>
userdel john
```

- 

Optionally we can also add group first and then add the user as well.

```
groupadd admins
useradd -g admins steve
id steve
```

- Sudors later we will see.
- 

## **SUDOERS**

In companies even though we know the ROOT user password, We might not login directly with ROOT user. Usually that root user login is used only during the maintenances of the system or in some extreme cases.

So we usually create users in the system and those users login to the system to perform or do some work like installing application or running application. But a normal user cannot do the admin activities and also as a standard practice we cannot login with root user. Hence we need an alternate option to login as a normal user but perform the work as root user.

To gain the above scenario we need to use some Privilege Escalation tools and few of them are

1. SUDO
2. PowerBroker
3. Centrify... etc

You can refer this link. [https://www.sudo.ws/other.html](https://www.sudo.ws/other.html)

Out of lot many tools **SUDO** is one of the default and widely used tool. Hence we are discussing SUDO further now..

You can add some files under `/etc/sudoers.d` and sudo program will load them.

Sudoers configuration syntax looks like below:

`user-name MACHINE=COMMANDS`

`ALL` is a default keyword which is available in sudoers to add all the commands access to all the machines.

`sample-user ALL=ALL`

In case I have three machines `SERVER1,SERVER2,SERVER3` and I need to allow a user to run `useradd` command only on `SERVER2 & SERVER3` then

```
Host_Alias APP_SERVERS = SERVER2, SERVER3
Cmnd_Alias MANAGE_USER = /sbin/useradd

sample-user APP_SERVERS = MANAGE_USER

```

Now the user can execute the commands as normal user by using sudo privilege and those commands will be executed as root user in the background.

First switch to normal user.

`su - john`

Then

`sudo useradd appuser1`

- How do you logins into your machines?
- I was login with username and password we have the sso(signle sign on) account.
- i have an my sso account i simply login with my account.

## **Package Management:**

- Package management is the key admin activity that most of the times as a devops guy we deal with install and update the packages all the time.
- If you want to list out the packages which are installed in the system by using the command

```bash
sudo yum list installed
```

- If you want to know packages are available to installed by using the command

```bash
sudo yum list available 
```

- If you know the both installed and available packages by using the command

```bash
sudo yum list all
```

- To list of all the packages by using number word count is going to be used.

```bash
sudo yum list | wc -l
```

- installed packages are donated as **@ sysmbol**
- To the find the packages with name whether it is installed or not

```bash
sudo yum list | grep nginx
sudo yum list | grep unzip
sudo yum list | grep vim
```

- Other way to check the packages are installed by using

```bash
sudo yum list installed | grep vim
```

- Install the new packages by using

```bash
sudo yum installed <package name> 
sudo yum install nginx -y
```

- To update the package by using the command

```bash
sudo yum update <package name> -y
sudo yum update nginx -y
```

- To update the complete system

```bash
sudo yum update -y
```

- To remove the package by using the command

```bash
sudo yum remove nginx -y
```

- 
- However, if you wondered that how `yum` in managing the installation, You will see that it is downloading the package and installing it. But from where it is downloading?
- Command `yum` will refer the repos available under `/etc/yum.repos.d/*.repo` files and reach out to only those destinations to download the files.
- Asking for installed locations for nginx by using command

```bash
rpm -ql ngnix
```

## System Management:

- A server is used to serve a service which runs all the time in the background. Unlike the commands which we ran sofar are foreground commands which will get terminated when we disconnect the session. So just to run the process in the background and as well as managing it in a better way we have some utilities that comes under service management.
- To list of all services which are running on the os by using the command

```bash
sudo systemctl list-units -t service

```

- press q come out from the list
- To check the status of the nginx single service

```bash
sudo systemctl status nginx
```

- To start the service

```bash
sudo systemctl start nginx
```

- To stop the service

```bash
sudo systemctl stop nginx
```

- To enable the service

```bash
sudo systemctl enable ngnix
```

- To disable the service

```bash
sudo systemctl disable nginx
```

## System Management:

- 

In the echo system of Linux OS, Files properties management are categorized in two.

1. File Ownerships
2. File Permissions

When a file created inside a system, that file has to be associated to a `user` which is **Owner** and also a `group` which is **Group Owner**.

When we create a file the ownerships to that file is getting the information from the user whom created that file.

You can check the ownerships of a file using `ls -l` command.

`touch sample.txt ls -l sample.txt`

When we want to change the ownership we use `chown` command. When we want to change the group ownership then we use `chgrp` command. To change ownership:

`chown centos sample.txt ls -l sample.txt`

To change group ownership:

`groupadd devops chgrp devops sample.txt ls -l sample.txt`

In above situation you are dealing with a file, If that is a directory then use `-R` option along with both the commands.

One more thing from the above situation is we are using two commands to change the owner and group, Where as we can do that with one single command.

`chown centos:devops sample.txt ls -l sample.txt chown root:root sample.txt ls -l sample.txt`

Permissions of a file telling that which owner can do what.

The operations performed on the file are

1. read (`r` )
2. write (`w` )
3. execute (`x` )

Owners of a file are three

1. File Owner (`u` )
2. Group Owner (`g` )
3. Others as Owners. (`o` )

Following diagram illustrates the output of `ls -l` command showing the permissions.

![https://github.com/devopstrainings/linux-basics-katakoda/raw/master/linux-adminstration/images/permissions.jpeg](https://github.com/devopstrainings/linux-basics-katakoda/raw/master/linux-adminstration/images/permissions.jpeg)

Now we can change those permissions using `chmod` command.

`touch sample.txt ls -l sample.txt chmod ugo+rwx sample.txt ls -l sample.txt`

Those options can be used in the way shown in the following diagram.

![https://github.com/devopstrainings/linux-basics-katakoda/raw/master/linux-adminstration/images/permissions.jpeg](https://github.com/devopstrainings/linux-basics-katakoda/raw/master/linux-adminstration/images/permissions.jpeg)

```bash
sudo chmod ugo-rwx sample.txt
```

```bash
sudo chmod u+r sample.txt
```

### Theoretical Points