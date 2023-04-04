### Theoretical Points
- Find command is used to search the files by using naming convention.
- Syntax : find <which-location-find> <search-critria>

```bash
find / -name f1
find / -name "*f1*"
```
- command line browser curl is used.
- Most of the time we need to browse urls to find that content from the command line CURL is used.
- curl command is used to download the files from the browser.
- Syntex : curl <url>
```bash
curl google.com
```

```bash
curl -O https://archive.apache.org/dist/tomcat/tomcat-8/v8.0.0-RC1/bin/apache-tomcat-8.0.0-RC1-deployer.tar.gz
```
- Extract the files from the **tar or zip .**
- Many times in the linux world allthe softwares are packaged either in .zip or .tar.g
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

### Pipes
- Pipes are used to send the output of one command to another command without storing the content anyware physically on disk.
- syntax : com1 | com2
- fil1 | file 2

```bash
cat /etc/passwd | grep root
```
- **Note**
: All the commands will not accept inputs over pipes. In case if we need to take the input then we take the help of `xargs`
 command.
- touch sam.txt

```bash
echo sam.txt | rm -f
```

```bash
echo sam.txt | xargs rm -f
```

- Linux basics is completed
- In this killercoda limitations are done .
### Linux Adminstration:
- In this adminstration topics we are used for AWS cloud to create a virtual Machines.
- Signin with AWS account and create an ec2 instances and connect with your local machine like putty or mobaXterm etc..,
- In this Linux Admin part we are going covered adminstrative commands.
1. Process Management
2. User Management
3. Package management
4. Service management
5. Permission management
6. network management.