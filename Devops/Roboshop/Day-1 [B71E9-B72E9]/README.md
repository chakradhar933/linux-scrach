**Aws Spot Instances:**

### Generally aws ec2 instances are
- on demand instances
- Reserved instances
- Spot instances (ideal instances)
- To save the cost we will take spot instances.
- Stateless Application:  Statelless applications are does not store the data inside them .
- Stateful Applications : It store the data inside them are called as stateful applications.
- Spot instances are used for Stateless Apps.

### Theoretical Points

- Instances we will take is T3.micro

  - T - Stands for aws instance type

  - 3 - Stands for Hardware refresh number.

- Micro - Instance size.

- SPOT Instance Creating link  : [https://lucky-hide-390.notion.site/How-to-Create-a-SPOT-Instance-fb797bb7d41647c090869bfc2670e49b](https://www.notion.so/How-to-Create-a-SPOT-Instance-fb797bb7d41647c090869bfc2670e49b)

### Practical things the trainer did

- Creating Spot instances
1.     Region : N.virgina
2. Choose launch instances 
3. Name and tag : spot
4. Search in ami search bar  : devops-practice and select centos-8 version
5. Choose instance type : T3.micro
6. Keypair : proceed without keypair
7. Security groups : allow-all
8. Go to Advanced Details

 # click on request Spot instances then click on customise then request type : presitant

# then behaviour : stop then click on launch instance. sucessfully created instance.

- We need to delete the spot instance now goto spot instance and select the instance and then click on actions then click on **cancel request.**
- change the naming conventions.

# Name in Spot Requests: [https://learndevopsonline.github.io/learndevopsonline/build/docs/How-Tos/show-name-tag-in-spot-request](https://learndevopsonline.github.io/learndevopsonline/build/docs/How-Tos/show-name-tag-in-spot-request)

# Request Quota: [https://learndevopsonline.github.io/learndevopsonline/build/docs/How-Tos/increase-spot-quota](https://learndevopsonline.github.io/learndevopsonline/build/docs/How-Tos/increase-spot-quota)

- Ask for 30 count

1. 

### Project is having the following components.

- ![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/roboshop-arch-7608f2225444bab0dca4a241b376f496.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/roboshop-arch-7608f2225444bab0dca4a241b376f496.png)

- The following screenshots help us to understand whether our app is working or not after the setup is done.

1. **When we open roboshop landing page we should see list of categories.**

![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s1-650691c1ea067438e8498052eb328182.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s1-650691c1ea067438e8498052eb328182.png)

1. **I should be able to register and after registration, it should show the registered user information.**

- ![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s2-685ba23403c054b951aed82a4852b679.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s2-685ba23403c054b951aed82a4852b679.png)

1. **Going to categories and any product we should be able to add to cart.**

- ![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s3-35afe6ac11263d85f47318a2ed918363.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s3-35afe6ac11263d85f47318a2ed918363.png)

1. **Post checkout it should show countries.**

- ![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s4-4759c39a3482f2adfd2c061b35323b5f.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s4-4759c39a3482f2adfd2c061b35323b5f.png)

**Post that confirm also should show that final amount**

- ![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s4-1-bff939df2eb8c9161842e46baffaeae2.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s4-1-bff939df2eb8c9161842e46baffaeae2.png)

1. **Pay now should show that payment is done along with order id**

- ![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s5-b83a2fbeded9ba687c7a4e8c81e21c0b.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s5-b83a2fbeded9ba687c7a4e8c81e21c0b.png)

**By clicking on Login back it show the order history.**

- ![https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s5-1-783c94f5912da94511430e697ede5eb3.png](https://learndevopsonline.github.io/learndevopsonline/build/assets/images/s5-1-783c94f5912da94511430e697ede5eb3.png)

- This project is a e-commerce website to sell the robots.

## Frontend-01 :

- Frontend is the service in roboshop to serve the web content over Nginx server.
- This will be the web frame for the web applications.
- Frontend is a static content to serve the static content on web server .
- Developer choose nginx  as a web server.
- switch to noraml user

```bash
sudo su -
```

- Install Nginx

```bash
yum install nginx -y
```

- Start the nginx server

```bash
systemctl enable nginx
systemctl start nginx
```

- Now search in google ip address : 44.192.39.120
- now shown default web page of nginx

 - ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/88f3e69a-9c44-4745-abeb-ccda06a06e72/Untitled.png)

- copy the path in the command line

```bash
/usr/share/nginx/html
```

- To remove the dafult content

```bash
rm -rf /usr/share/nginx/html/*
```

- Download the frontend content

```bash
curl -o /tmp/frontend.zip [https://roboshop-artifacts.s3.amazonaws.com/frontend.zip](https://roboshop-artifacts.s3.amazonaws.com/frontend.zip)
```

- Goto the path where the zip file is available

```bash
cd /usr/share/nginx/html
```

- extract the frontend content

```bash
unzip /tmp/frontend.zip
```

- Now take Public ip and search in google : 44.192.39.120

- ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5346ff7a-ecb5-43d4-8447-471fa40bc47c/Untitled.png)

- Now create nginx reverse proxy configuration.
- now to store the all nginx configuration files at location

```bash
vim /etc/nginx/default.d/roboshop.conf
```

- now insert the config file into roboshop.conf location

```bash
proxy_http_version 1.1;
location /images/ {
  expires 5s;
  root   /usr/share/nginx/html;
  try_files $uri /images/placeholder.jpg;
}
location /api/catalogue/ { proxy_pass http://localhost:8080/; }
location /api/user/ { proxy_pass http://localhost:8080/; }
location /api/cart/ { proxy_pass http://localhost:8080/; }
location /api/shipping/ { proxy_pass http://localhost:8080/; }
location /api/payment/ { proxy_pass http://localhost:8080/; }

location /health {
  stub_status on;
  access_log off;
}
```

- :wq save and quit
- now see the file

```bash
cat /etc/nginx/default.d/roboshop.conf
```

- Now restart the nginx
- Whole eco-system is

- install softwares .

- customize configuration .

- Apply and restart .