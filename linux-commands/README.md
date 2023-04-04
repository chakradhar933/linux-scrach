### important commands
- uname : This command is used to display the which operating system you are using
```bash
uname
```
- uname -a , uname -all : To display the complete output.
```bash
uname -a
uname -all
```
- cat /etc/*release : To check  the operating system details.
```bash
cat /etc/*release
```
- cat /proc/cpuinfo : To check the cpu information. 
```bash
cat /proc/cpuinfo
```
- cat /proc/meminfo : To check the memory information.
```bash
cat /proc/cpuinfo
```
- lsblk : To check the disk information.
```bash
lsblk
```
- uname -i : To check the archictecture whether it is 64bit or 32bit.
```bash
uname -i
```
- ls : To shown the list of all files and directories.
```bash
ls 
```
- ls -A : To list list of all hidden files.
```bash
ls -A
```
- ls -l : long list of all files and directories.
```bash
ls -l
```
- cat > "file name" : To create a file and add the content . 
# ctr+d to come out from the file
```bash
cat > f1
```
- touch <f1> <f2> : To create empty files.
```bash
touch f1 f1
```
- cp <source file> <destination> : To copy the file one file to another file.
```bash
cp f2 f1
```
- mv <source file> <destination file> : To move the file one file to another file . (overwrited)
```bash
mv f1 f2
```
- pwd : We want to know about which place or location we are present in .
```bash
pwd
```

- cd : To navigate one location to another location. 
```bash
cd
```
- cd .. :To go back to the one location.
```bash
cd ..
```
- cd ../.. : To go back mulitiple locations
```bash
cd ../..
```
- mkdir <name>: To create a diretory or folder.
```bash
mkdir <linux>
```
- cp -r <soucrce dir name> <destination dir name> : To copy the one directory to another directory .
```bash
cp -r l1 l2
```

- mv <source file name> < destination directory name> : To move the file to the directory.
```bash
mv f1 l1
```

- To move the one directory to another directory

```bash
mv f2 f1
```
- rm -r : To remove the directory.
```bash
rm -r f1 f2
```
- rm -rf  : To remove the directory forcefully
```bash
rm -rf <dir name>
```
- head : In a file having more numbers of lines to shown only 1st 5 lines
```bash
head -n 5 <filename>
```
- tail :If you want to have only last 5 lines.
```bash
tail -n 5 <filename>
```
-grep : The grep filter searches a file for a particular pattern of charcters, and display all lines that contain that platform
```bash
grep <word> <file name>
grep root /etc/passwd
```

-awk : In such cases the content needs to be filtered based on the columns in that awk command is used.
```bash
awk -F : '{print $column-number}' <file name>
awk -F : '{print $1 $2}' /etc/passwd
```
- and also cama seperated files
```bash
awk -F , '{print $cama-number}' <file name>
awk -F , '{print $1}' /etc/passwd
```
- vim  : editer is used to create a file and modify the files.
`vim file` -> Press `Insert` or `i` -> Make Changes -> Press `ESC` -> Press Colon `:` -> Press `wq` -> Done
```bash
vim <file name>
```
- Find : Find command is used to search the files by using naming convention.
- Syntax : find <which-location-find> <search-critria>
```bash
find / -name f1
```
- curl : command line browser curl is used.
- Most of the time we need to browse urls to find that content from the command line CURL is used.
- curl command is used to download the files from the browser.
```bash
curl google.com
```
```bash
curl -O https://archive.apache.org/dist/tomcat/tomcat-8/v8.0.0-RC1/bin/apache-tomcat-8.0.0-RC1-deployer.tar.gz
```
- unzip , tar :Extract the files from the **tar or zip .**
- Many times in the linux world all the softwares are packaged either in .zip or .tar.g
tar -xf tar -xf apache-tomcat-8.0.0-RC1-deployer.tar.gz
unzip <filename>.zip
- Syntax :tar -xf <filename>.tar.gz
```bash
tar -xf tar -xf apache-tomcat-8.0.0-RC1-deployer.tar.gz
```
- Syntax : unzip <file name>.zip
```bash
unzip curl -L -o shipping.zip https://github.com/roboshop-devops-project/shipping/archive/refs/heads/main.zip
unzip shipping.zip
```
- Pipes : Pipes are used to send the output of one command to another command without storing the content anyware physically on disk.
- syntax : com1 | com2
- fil1 | file 2
```bash
cat /etc/passwd | grep root
```
### Linux adminstration topics
# Process management
- ps : list of process which are running on the system .
```bash
ps
```
- ps -u :If you want to see the all the process by using command.
```bash
ps -u
```
- ps -e :If i don't want all the process which are running  i want only related to my user and my session i want whole process which are running in my system .
```bash
ps -e
```
- “e” stand for all
- ps -ef : To shown the information with length.
```bash
ps -ef
```
- sleep :  stop means we can resume back after completed the time.
```bash
sleep <timer>
sleep 5
```
- sleep 100 : To give the fast output by using the command.
```bash
sleep 100 &
```
- ps -ef : To backround check the process.
```bash
ps -ef | grep sleep
```
- kill : To end the task in linux completly by using the command **kill.**
- Syntax kill <pid>
```bash
kill <process id>
kill 920
```
```bash
kill -9 <pid>
kill -9 1542
```
## **User Management:**
- useradd : To create the user .
```bash
useradd <name>
useradd john
```
- id  : To check the user is created or not .
```bash
id <username>
id john
```
- Every user can be associate with a numbers.
- passwd : To create the password to the user.
```bash
passwd <username>
passwd john
``` 
- The following command will run some services inside the system and you can check those process are ran by a certain user but not by a root user.
```bash
curl -s https://raw.githubusercontent.com/devopstrainings/linux-basics-katakoda/master/linux-adminstration/files/daemon-services.sh | bash
```
- You can check the process of some system services runs as a normal user but not as a root user.
```bash
ps -ef | grep httpd
```
```bash
ps -ef | grep tomcat
```
```bash
ps -ef | grep mysql
```
- su : To switch the one user to another user .
```bash
su - <username>
su - john
```

- userdel : To delete the user by using 
```bash
userdel <user name>
userdel john
```
- groupadd : we can also add group first and then add the user as well.
```
groupadd admins
useradd -g admins steve
id steve
```
## **Package Management:**
- yum list : If you want to list out the packages which are installed in the system.
```bash
sudo yum list installed
```
- If you want to know packages are available to installed by using the command.
```bash
sudo yum list available 
```
- yum list all : If you know the both installed and available packages.
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
- Other way to check the packages are installed by using.
```bash
sudo yum list installed | grep vim
```
- yum install : Install the new packages by using
```bash
sudo yum installed <package name> 
sudo yum install nginx -y
```
- yum update : To update the package .
```bash
sudo yum update <package name> -y
sudo yum update nginx -y
```
- To update the complete system

```bash
sudo yum update -y
```
- yum remove : To remove the package.
```bash
sudo yum remove nginx -y
```
- rpm -ql : Asking for installed locations for nginx.
```bash
rpm -ql ngnix
```
### System Management:
- To list of all services which are running on the os by using the command
```bash
sudo systemctl list-units -t service
```
- press q come out from the list
- systemctl status : To check the status of the nginx single service.
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

## permission Management:

In the echo system of Linux OS, Files properties management are categorized in two.

1. File Ownerships
2. File Permissions

When a file created inside a system, that file has to be associated to a `user` which is **Owner** and also a `group` which is **Group Owner**.

When we create a file the ownerships to that file is getting the information from the user whom created that file.

You can check the ownerships of a file using `ls -l` command.

`touch sample.txt | ls -l sample.txt`

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


```bash
sudo chmod ugo-rwx sample.txt
```

```bash
sudo chmod u+r sample.txt
```






