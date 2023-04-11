### Redis-04:

- Redis is a service is used to application should be faster in this caching is used.

- Create an ec2 instance for redis .name it as Redis-04.
- Set host name

```bash
set-hostname Redis-04
```

- Redis is used for in-memory data storage(Caching) and allows users to access the data of database over API.
- **Versions of the DB Software you will get context from the developer, Meaning we need to check with developer.**
- Redis offering the repofile as a rpm lets install now

```bash
yum install [https://rpms.remirepo.net/enterprise/remi-release-8.rpm](https://rpms.remirepo.net/enterprise/remi-release-8.rpm) -y
```

- Package is installed or not to check by using the command

```bash
rpm -ql remi-release
```

- its brings the repo files.
- Enable Redis 6.2 from package streams.

```bash
dnf module enable redis:remi-6.2 -y
```

- Now install redis

```bash
yum install redis -y
```

- Usually Redis opens the port only to `localhost(127.0.0.1)`
, meaning this service can be accessed by the application that is hosted on this server only. However, we need to access this service to be accessed by another server, So we need to change the config accordingly.
- open redis configure file and replace 127.0.0.1 to 0.0.0.0

```bash
vim /etc/redis.conf
vim /etc/redis/redis.conf
```

- now start the service

```bash
systemctl enable redis
```

```bash
systemctl start redis
```

### **User-05:**

User is a microservice in roboshop project it is a responsible for user login and registerations in e-commerce in roboshop project.

- Now we need to create an ec2 instance in user . name it as User-05
- Now  set name

```bash
set-hotname User-05
```

- **Developer has chosen NodeJs, Check with developer which version of NodeJS is needed.**
 **Developer has set a context that it can work with NodeJS >18**
- Setup NodeJS repos. Vendor is providing a script to setup the repos.

```bash
curl -sL https://rpm.nodesource.com/setup_lts.x | bash
```

- install nodejs

```bash
yum install nodejs -y
```

- Configure the application.
- our application is developed by the developer of our organisation and it is not having any rpm software just like other softwares. so we need to configure the steps manually.
- Rpm is a bunch of files
- Add the application user

```bash
useradd roboshop
```

- 

- User **roboshop** is a function / daemon user to run the application. Apart from that we dont use this user to login to server.

- Also, username **roboshop** has been picked because it more suits to our project name.

- INFO

- We keep application in one standard location. This is a usual practice that runs in the organization.

- lets set an app directory

```bash
mkdir /app
```

- Download the application code to created app directory.

```bash
curl -L -o /tmp/user.zip [https://roboshop-artifacts.s3.amazonaws.com/user.zip](https://roboshop-artifacts.s3.amazonaws.com/user.zip)
```

```bash
cd /app
```

```bash
unzip /tmp/user.zip
```

- 

- Every application is developed by development team will have some common softwares that they use as libraries. This application also have the same way of defined dependencies in the application configuration.

- Lets download the dependencies.

```bash
npm install
```

- 

- We need to setup a new service in **systemd** so `systemctl` can manage this service

- INFO

- We already discussed in linux basics that advantages of systemctl managing services, Hence we are taking that approach. Which is also a standard way in the OS.

- setup systemd user service

```bash
vim /etc/systemd/system/user.service
```

- configure the file

```bash
[Unit]
Description = User Service
[Service]
User=roboshop
Environment=MONGO=true
Environment=REDIS_HOST=<REDIS-SERVER-IP>
Environment=MONGO_URL="mongodb://<MONGODB-SERVER-IP-ADDRESS>:27017/users"
ExecStart=/bin/node /app/server.js
SyslogIdentifier=user

[Install]
WantedBy=multi-user.target
```

- now above we will put into redis-04 private ip address and also put mongodb-02 private ip address.
- Load the service

```bash
systemctl daemon-reload
```

- Above command is because of we start the new service , we are telling systemd is to reload and it will detach the new service.
- start the service

```bash
systemctl enable user
systemctl start user
```

- now user public ip put into the frontend server to acess it .
- 

- For the application to work fully functional we need to load schema to the Database. Then

### INFO

- Schemas are usually part of application code and developer will provide them as part of development.

- We need to load the schema. To load schema we need to install mongodb client.

- To have it installed we can setup MongoDB repo and install mongodb-client

```bash
vim /etc/yum.repos.d/mongo.repo
```

- configure the file

```bash
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=0
enabled=1
```

```bash
yum install mongodb-org-shell -y
```

- Load schema

```bash
mongo --host MONGODB-SERVER-IPADDRESS </app/schema/user.js
```

## **Cart-06:**

- Cart is also a microservice that is resposbile for add items to cart in roboshop application.
- Developer chooses the nodejs
- Check the developer which version of nodejs is needed.
- Now create Ec2 instance for Cart-06
- Cart is a microservice that is responsible for Cart Service in RobotShop e-commerce portal.
- Setup NodeJS repos. Vendor is providing a script to setup the repos.

```bash
curl -sL [https://rpm.nodesource.com/setup_lts.x](https://rpm.nodesource.com/setup_lts.x) | bash
```

- Install NodeJS

```bash
yum install nodejs -y
```

- 

- Configure the application. Here

- INFO

- Our application developed by the own developer is not having any RPM software just like other softwares. So we need to configure every step manually

### RECAP

- We already discussed in Linux basics section that applications should run as nonroot user.

- Add application User

```bash
useradd roboshop
```

- 

- User **roboshop** is a function / daemon user to run the application. Apart from that we dont use this user to login to server.

- Also, username **roboshop** has been picked because it more suits to our project name.

- INFO

- We keep application in one standard location. This is a usual practice that runs in the organization.

- let setup an app directory

```bash
mkdir /app
```

- Download the application code to created app directory.

```bash
curl -L -o /tmp/cart.zip https://roboshop-artifacts.s3.amazonaws.com/cart.zip
```

```bash
cd /app
```

```bash
unzip /tmp/cart.zip
```

- Every application is developed by development team will have some common softwares that they use as libraries. This application also have the same way of defined dependencies in the application configuration.
- Download the dependencies

```bash
npm install
```

- We need to setup a new service in **systemd**
 so `systemctl`
 can manage this service
- We already discussed in linux basics that advantages of systemctl managing services, Hence we are taking that approach. Which is also a standard way in the OS.
- Setup SystemD Cart Service

```bash
vim /etc/systemd/system/cart.service
```

```bash
[Unit]
Description = Cart Service
[Service]
User=roboshop
Environment=REDIS_HOST=<REDIS-SERVER-IP>
Environment=CATALOGUE_HOST=<CATALOGUE-SERVER-IP>
ExecStart=/bin/node /app/server.js
SyslogIdentifier=cart

[Install]
WantedBy=multi-user.target
```

- in this service file we connect redis and catalougue private ip address for the internall connections.
- Load the service

```bash
systemctl daemon-reload
```

- start the service.

```bash
systemctl enable cart
systemctl start cart
```

- Now cart is ready and connect with the frontend

```bash
vim /etc/nginx/default.d/roboshop.conf
```

## Mysql-07:

- Developer has chosen the database MySQL. Hence, we are trying to install it up and configure it.
- now we need to create an ec2 instance for mysql-07.
- **Versions of the DB Software you will get context from the developer, Meaning we need to check with developer.**
- CentOS-8 Comes with MySQL 8 Version by default, However our application needs MySQL 5.7. So lets disable MySQL 8 version.

```bash
dnf module disable mysql -y
```

- Setup the MySQL5.7 repo file

```bash
vim **/etc/yum.repos.d/mysql.repo**
```

- Configure the file

```bash
[mysql]
name=MySQL 5.7 Community Server
baseurl=http://repo.mysql.com/yum/mysql-5.7-community/el/7/$basearch/
enabled=1
gpgcheck=0
```

- Install MySQL Server

```bash
yum install mysql-community-server -y
```

- Start MySQL Service

```bash
systemctl enable msqld
sytemctl start msqld
```

- Next, We need to change the default root password in order to start using the database service. Use password **`RoboShop@1`**
 or any other as per your choice.

```bash
mysql_secure_installation --set-root-pass RoboShop@1
```

- You can check the new password working or not using the following command in MySQL.

### Shipping-08:

- We need to create an ec2 instance for shipping.

- Shipping service is responsible for finding the distance of the package to be shipped and calculate the price based on that.
- Shipping service is written in Java, Hence we need to install Java.
- Maven is a Java Packaging software, Hence we are going to install **`maven`**
, This indeed takes care of java installation.
- Developer has chosen Maven, Check with developer which version of Maven is needed. Here for our requirement java >= 1.8 & maven >=3.5 should work.

```bash
yum install maven -y
```

- 

- Configure the application.

- INFO

- Our application developed by the developer of our org and it is not having any RPM software just like other softwares. So we need to configure every step manually

### RECAP

- We already discussed in Linux basics section that applications should run as nonroot user.

- Add application User

```bash
useradd roboshop
```

- 

- User **roboshop** is a function / daemon user to run the application. Apart from that we dont use this user to login to server.

- Also, username **roboshop** has been picked because it more suits to our project name.

### INFO

- We keep application in one standard location. This is a usual practice that runs in the organization.

- Lets setup an app directory.

```bash
mkdir /app
```

- Download the application code to created app directory.

```bash
curl -L -o /tmp/shipping.zip https://roboshop-artifacts.s3.amazonaws.com/shipping.zip 
cd /app 
unzip /tmp/shipping.zip
```

- Every application is developed by development team will have some common softwares that they use as libraries. This application also have the same way of defined dependencies in the application configuration.
- Lets download the dependencies & build the application

```bash
cd /app
mvn clean package
mv target/shipping-1.0.jar shipping.jar
```

- We need to setup a new service in **systemd**
 so `systemctl`
 can manage this service
- We already discussed in linux basics that advantages of systemctl managing services, Hence we are taking that approach. Which is also a standard way in the OS.
- Setup SystemD Shipping Service

```bash
vim /etc/systemd/system/shipping.service
```

```bash
[Unit]
Description=Shipping Service

[Service]
User=roboshop
Environment=CART_ENDPOINT=<CART-SERVER-IPADDRESS>:8080
Environment=DB_HOST=<MYSQL-SERVER-IPADDRESS>
ExecStart=/bin/java -jar /app/shipping.jar
SyslogIdentifier=shipping

[Install]
WantedBy=multi-user.target
```

- Load the service

```bash
systemctl daemon-reload
```

- systemctl daemon-reload

```bash
systemctl enable shipping 
systemctl start shipping
```

- 

- For this application to work fully functional we need to load schema to the Database.

### INFO

- Schemas are usually part of application code and developer will provide them as part of development.

- We need to load the schema. To load schema we need to install mysql client.

- To have it installed we can use

```bash
yum install mysql -y
```

- Load Schema

```bash
mysql -h <MYSQL-SERVER-IPADDRESS> -uroot -pRoboShop@1 < /app/schema/shipping.sql
```

- This service needs a restart because it is dependent on schema, After loading schema only it will work as expected, Hence we are restarting this service. This

```bash
systemctl restart shipping
```

- To see the log messges

```bash
tail /var/log/messages
```

- restart and see the log messages at a time by using the command

```bash
systemctl restart shipping ; tail -f /var/log/messages
```

- Now take private ip of shipping and put into the frontend

```bash
vim /etc/nginx/default.d/roboshop.conf
```
