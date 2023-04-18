## Shipping-08:
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

Configure the application.

INFO

Our application developed by the developer of our org and it is not having any RPM software just like other softwares. So we need to configure every step manually

RECAP

We already discussed in Linux basics section that applications should run as nonroot user.

- Add application User

```bash
useradd roboshop
```

- 

User **roboshop** is a function / daemon user to run the application. Apart from that we dont use this user to login to server.

Also, username **roboshop** has been picked because it more suits to our project name.

INFO

We keep application in one standard location. This is a usual practice that runs in the organization.

Lets setup an app directory.

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

For this application to work fully functional we need to load schema to the Database.

INFO

Schemas are usually part of application code and developer will provide them as part of development.

We need to load the schema. To load schema we need to install mysql client.

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

#### RabbitMQ-09:

- RabbitMQ is a messaging Queue which is used by some components of the applications.
- Now create one ec2 instance for rabbitMQ and connect with the server.
- Configure YUM Repos from the script provided by vendor.

```bash
curl -s https://packagecloud.io/install/repositories/rabbitmq/erlang/script.rpm.sh | sudo bash
```

- Install ErLang

```bash
yum install erlang -y
```

- Configure YUM Repos for RabbitMQ.

```bash
curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | sudo bash
```
- Install RabbitMQ
```bash
yum install rabbitmq-server -y
```
- Start RabbitMQ Service
```bash
systemctl enable rabbitmq-server 
systemctl start rabbitmq-server
```
- RabbitMQ comes with a default username / password as `guest/guest`
. But this user cannot be used to connect. Hence, we need to create one user for the application.

```bash
rabbitmqctl add_user roboshop roboshop123
rabbitmqctl set_user_tags roboshop administrator
rabbitmqctl set_permissions -p / roboshop ".*" ".*" ".*"
```
## Payment-10 :

- We need to create one ec2 instance for the payment service.
- This service is responsible for payments in RoboShop e-commerce app. This service is written on `Python 3`
, So need it to run this app.
- Developer has chosen Python, Check with developer which version of Python is
- needed.Install Python 3.6

```bash
yum install python36 gcc python3-devel -y
```

- Configure the application.

- Our application developed by the developer of our org and it is not having any RPM software just like other softwares. So we need to configure every step manually

* RECAP

- We already discussed in Linux basics section that applications should run as nonroot user.

- Add application User 

- User **roboshop** is a function / daemon user to run the application. Apart from that we dont use this user to login to server.

- Also, username **roboshop** has been picked because it more suits to our project name.

- INFO
We keep application in one standard location. This is a usual practice that runs in the organization.
- Lets setup an app directory.
```bash
mkdir /app
```
- Download the application code to created app directory.

```bash
curl -L -o /tmp/payment.zip https://roboshop-artifacts.s3.amazonaws.com/payment.zip 
cd /app 
unzip /tmp/payment.zip
```
- Every application is developed by development team will have some common softwares that they use as libraries. This application also have the same way of defined dependencies in the application configuration.

- Lets download the dependencies.

```bash
cd /app 
pip3.6 install -r requirements.txt
```

- 

- We need to setup a new service in **systemd** so `systemctl` can manage this service

* INFO

- We already discussed in linux basics that advantages of systemctl managing services, Hence we are taking that approach. Which is also a standard way in the OS.

```bash
vim /etc/systemd/system/payment.service
```

```bash
[Unit]
Description=Payment Service

[Service]
User=root
WorkingDirectory=/app
Environment=CART_HOST=<CART-SERVER-IPADDRESS>
Environment=CART_PORT=8080
Environment=USER_HOST=<USER-SERVER-IPADDRESS>
Environment=USER_PORT=8080
Environment=AMQP_HOST=<RABBITMQ-SERVER-IPADDRESS>
Environment=AMQP_USER=roboshop
Environment=AMQP_PASS=roboshop123

ExecStart=/usr/local/bin/uwsgi --ini payment.ini
ExecStop=/bin/kill -9 $MAINPID
SyslogIdentifier=payment

[Install]
WantedBy=multi-user.target
```
- Load the service.
```bash
systemctl daemon-reload
```
- This above command is because we added a new service, We are telling systemd to reload so it will detect new service.
- Start the service.
```bash
systemctl enable payment
systemctl start payment
```
## Dispatch-11 :
- Now we nned to create an one ec2 instance for dispatch

- Dispatch is the service which dispatches the product after purchase. It is written in GoLang, So wanted to install GoLang.

- Developer has chosen GoLang, Check with developer which version of GoLang is needed.
- Install GoLang
```bash
yum install golang -y
```
### Configure the application.

* INFO
- Our application developed by the developer of our org and it is not having any RPM software just like other softwares. So we need to configure every step manually

- RECAP

- We already discussed in Linux basics section that applications should run as nonroot user.

- add the application user

```bash
useradd roboshop
```
- User **roboshop** is a function / daemon user to run the application. Apart from that we dont use this user to login to server.

- Also, username **roboshop** has been picked because it more suits to our project name.

- INFO

- We keep application in one standard location. This is a usual practice that runs in the organization.
- Lets setup an app directory.
```bash
mkdir /app
```
- Download the application code to created app directory.
```bash
curl -L -o /tmp/dispatch.zip https://roboshop-artifacts.s3.amazonaws.com/dispatch.zip 
cd /app 
unzip /tmp/dispatch.zip
```
- Every application is developed by development team will have some common softwares that they use as libraries. This application also have the same way of defined dependencies in the application configuration.
- Lets download the dependencies & build the software.

```bash
cd /app 
go mod init dispatch
go get 
go build
```
- We need to setup a new service in **systemd** so `systemctl` can manage this service

- INFO

- We already discussed in linux basics that advantages of systemctl managing services, Hence we are taking that approach. Which is also a standard way in the OS.

- Setup SystemD Payment service.

```bash
vim /etc/systemd/system/dispatch.service
```

```bash
[Unit]
Description = Dispatch Service
[Service]
User=roboshop
Environment=AMQP_HOST=RABBITMQ-IP
Environment=AMQP_USER=roboshop
Environment=AMQP_PASS=roboshop123
ExecStart=/app/dispatch
SyslogIdentifier=dispatch
[Install]
WantedBy=multi-user.target
```
- load the service
```bash
systemctl daemon-reload
```
- start the service
```bash
systemctl enable dispatch 
systemctl start dispatch
```
### Practical things the trainer did

- Roboshop project manual setup is sucessfully completed.