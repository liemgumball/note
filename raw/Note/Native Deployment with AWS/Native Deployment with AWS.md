---
Created by: liemgumball
Created time: 2024-07-18T14:35
tags:
  - Guides
---
## Setup

- Create your EC2 instance: [https://docs.aws.amazon.com/efs/latest/ug/gs-step-one-create-ec2-resources.html](https://docs.aws.amazon.com/efs/latest/ug/gs-step-one-create-ec2-resources.html)
- Setup your own ssh and connect to your server
- Install git on ubuntu: [https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-20-04)
- Clone your source code: `git clone ...`
- Setup your [[NodeJS|Nodejs]] on ubuntu:
    - [https://nodejs.org/en/download/package-manager](https://nodejs.org/en/download/package-manager)
    - [https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04)
- Setup your mysql:
    
    - [https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)
    
    ```Bash
    sudo apt install mysql-server
    sudo systemctl start mysql.service
    
    # Access to mysql
    sudo mysql
    # Modiy root user password
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    
    # Create your database
    CREATE DATABASE sgroup
    # Exit mysql
    exit
    
    # Test mysql status
    systemctl status mysql.service
    ```
    
    - Now you have mysql setup with user `root` and password `password` with port 3306 and database `sgroup`

## Try to run your app

- Create your `.env` file and setup your environment
- Try to run your app with setup mysql by: `npm run start`
- Verify that your app connected to your database successfully

  

## Publish your app to external

- Setup your nginx: [https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04)
    
    ```Bash
    sudo apt update
    sudo apt install nginx
    sudo ufw app list
    sudo ufw allow 'Nginx HTTP'
    sudo ufw status
    # If ufw is disable, please enable it
    sudo ufw enable
    systemctl status nginx
    ```
    
    - Now your nginx is ready on port 80.
- Setup Inbound:
    - Add rule HTTP 80 firewall to Inbound Groups: [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/working-with-security-groups.html)
    - This would help you access port 80 from external resource
- Try to access our aws instance via public IP, now you should see nginx default page:
    
    ![[raw/Note/Native Deployment with AWS/attachments/Untitled.png|Untitled.png]]
    
- Proxy pass nginx to your app port, there are some cases to do this, I will demo 1 of the way to do that:
    - Create your nginx config file

```Bash
cd /etc/nginx/sites-available
vi sgroup.conf
```

- Setup your reverse proxy for example:

```Bash
server {  
              listen 80;
              server_name SUBDOMAIN.DOMAIN.TLD;
              location / {  
                           proxy_pass https://PRIVATE_IP:3000;  
                           proxy_http_version 1.1;  
                           proxy_set_header Upgrade $http_upgrade;  
                           proxy_set_header Connection 'upgrade';  
                           proxy_set_header Host $host;  
                           proxy_cache_bypass $http_upgrade;  
               }  
}
```

  

```Bash
server {  
              listen 80;
              server_name _;
              location / {  
                           proxy_pass https://0.0.0.0:3000;  
                           proxy_http_version 1.1;  
                           proxy_set_header Upgrade $http_upgrade;  
                           proxy_set_header Connection 'upgrade';  
                           proxy_set_header Host $host;  
                           proxy_cache_bypass $http_upgrade;  
               }  
}
```

  

## Let’s finish running our app

Let’s try run our app on the server, now you should access your app via public IP, but there is one final concern: **we have to keep our app alive**

Let’s use [https://pm2.keymetrics.io/](https://pm2.keymetrics.io/)

```Bash
npm install pm2@latest -g
pm2 start app.js
```

And now your app is alive in the detach mode

## Related

- [[NodeJS]]
- [[Docker]]