- Qs : We have database at the ending and app only going to here and get into the data but why can’t frontend can go and fetch the data?

- Ans: Frontend is not designed such a way becuase of frontend which is a html content . The html content is not went for that and that’s why it cannot do that. You require some other programming launguage to deal with the data base.

### Theoretical Points

**MongoDB:**

- Developer choose the database as MongoDB . Hence , we are trying to install it and configure it.
- Versions of the Database software you will get from the developer, we need to check with the developer.
- **Developer has shared the version information as MongoDB-4.x**
- Create Ec2 instance for MongoDB server . Name = MongoDB-02
- To many servers will be their and then some confusions will be happen now to overcome the problems  to set each server having give specific name by using command

```bash
set-hostname frontend
set-hostname MongoDB
```

- Setup monogoDB repo file

```bash
vim /etc/yum.repos.d/mongo.repo
```

- repo file is created then configure the data

```bash
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=0
enabled=1
```

- Now install mongodb

```bash
yum install mongodb-org -y
```

- enable and start mongodb

```bash
systemctl enable mongod
systemctl start mongod
```

- check the port of mongod by using command

```bash
netstat -lntp
```

- ip address of the mongodb check by using the command

```bash
ip a
```

- Usually MongoDB opens the port only to `localhost(127.0.0.1)`
, meaning this service can be accessed by the application that is hosted on this server only. However, we need to access this service to be accessed by another server, So we need to change the config accordingly.
- Update listen address from 127.0.0.1 to 0.0.0.0 now open

```bash
vim /etc/mongod.conf
```

- now this is setup of the mongodb . Now application gohead and talk to the database server.

## **Catalogue-03:**

- Catalogue is a microservice that is responsible for serving the list of items that display in roboshop application.
- Developer chooses the NodeJs .check with developer which version of NodeJs is needed.
- Now create Ec2 instance for catalogue.
- Now rename it as a

```bash
set-hostname catalouge
```

- now check

```bash
cd /etc/yum.repos.d
```

- Setup NodeJS repos. Vendor is providing a script to setup the repos.

```bash
curl -sL [https://rpm.nodesource.com/setup_lts.x](https://rpm.nodesource.com/setup_lts.x) | bash
```

- now install nodejs

```bash
yum install nodejs -y
```

- Configure the application.
- Our application developed by the developer of our org and it is not having any RPM software just like other softwares. So we need to configure every step manually.
- RPM is a bunch of files that packed as a one file.
- Now check what are the files installed

```bash
rpm -ql nodejs
```

- Add the application user

```bash
useradd roboshop
```

- User **roboshop**
 is a function / daemon user to run the application. Apart from that we dont use this user to login to server.
- Also, username **roboshop**
 has been picked because it more suits to our project name.
- We keep application in one standard location. This is a usual practice that runs in the organization.
- Lets create an app directory

```bash
mkdir /app
```

- Download the application code to create an app directory.

```bash
curl -L -o /tmp/catalogue.zip [https://roboshop-artifacts.s3.amazonaws.com/catalogue.zip](https://roboshop-artifacts.s3.amazonaws.com/catalogue.zip)
```

```bash
unzip /tmp/catalogue.zip
```

```bash
cd /app
```

- 

- Every application is developed by development team will have some common softwares that they use as libraries. This application also have the same way of defined dependencies in the application configuration.

- Lets download the dependencies.

```bash
cd /app
```

```bash
npm install
```

- We need to setup a new service in **systemd** so `systemctl` can manage this service

* INFO

- We already discussed in linux basics that advantages of systemctl managing services, Hence we are taking that approach. Which is also a standard way in the OS.

```bash
vim /etc/systemd/system/catalougue.service
```

- Setup SystemD Catalogue Service
- then configure the file

```bash
[Unit]
Description = Catalogue Service

[Service]
User=roboshop
Environment=MONGO=true
Environment=MONGO_URL="mongodb://<MONGODB-SERVER-IPADDRESS>:27017/catalogue"
ExecStart=/bin/node /app/server.js
SyslogIdentifier=catalogue

[Install]
WantedBy=multi-user.target
```

- in configuration file we need to update the mongoDB private ip address becuase of the internal communications.
- Load the service

```bash
systemctl daemon-reload
```

- Above command is because of we start the new service,we are telling systemd is to reload and it will detech the new service.
- Start the service

```bash
systemctl enable catalougue
```

```bash
systemctl start catalougue
```

- Now we need to connect the catalougue to frontend now  open frontend then open configuration file

```bash
 vim /etc/nginx/default.d/roboshop.conf
```

- now take public ip of catalougue then put into the configuration file .
- now restart the nginx server

```bash
systemctl restart nginx
```

- For the application to work fully functional we need to load the schema to the databas.
- Schema is generally devloped by the developer only.
- We need to load the schema manually. load the schema we need to install the mongodb client.
- To have it installed we can setup MongoDB repo and install mongodb-client.

```bash
vim /etc/yum.repos.d/mongo.d
```

- now configure the file.

```bash
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=0
enabled=1
```

- Load schema

```bash
mongo --host MONGODB-SERVER-IPADDRESS </app/schema/catalogue.js
```

- now update the mongodb private ip address.
- Now catagories are going to display at the frontend server.
- Catalougue is completed.