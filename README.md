# Step 1: Set Up AWS EC2 Instance

Create an AWS Account: If you don’t already have an AWS account, create one. 
Launch an EC2 Instance: Go to the AWS Management Console. 
Navigate to EC2 Dashboard and click on Launch Instance. Choose an Amazon Machine Image (AMI). 
Select Amazon Linux 2 AMI. 
Choose an instance type. For simplicity, select t2.micro (free tier eligible). 
Configure instance details. 
Keep default settings. Add storage. Keep the default settings. 
Add tags. Optionally, add tags to identify your instance. 
Configure security group: Create a new security group. 
Add a rule to allow HTTP traffic on port 80 from anywhere (0.0.0.0/0). 
Add a rule to allow SSH traffic on port 22 from your IP address. 
Review and launch the instance.
Create a new key pair or use an existing one. Download the key pair and save it securely.

# Add this script to your user data file before launching your instance.

#!/bin/bash sudo yum update -y sudo amazon-linux-extras install nginx1 -y sudo systemctl start nginx sudo systemctl enable nginx

# Launch the instance.

# Create a repository and save your HTML, CSS and JavaScript files in it.

Eg: mkdir website_files, cd into website_file and vi into index.html, styles.css and scripts.js

# Move the website_files directory to the NGINX Document Root:

sudo mv /home/ec2-user/website_files/* /usr/share/nginx/html/

# Set Permissions:

sudo chmod -R 755 /usr/share/nginx/html 
sudo chown -R nginx:nginx /usr/share/nginx/html

# Edit the NGINX Configuration File to add your public IP address:

sudo vi /etc/nginx/nginx.conf

server { listen 80; server_name your-ec2-public-ip;

location / { root /usr/share/nginx/html; index index.html index.htm; }

error_page 404 /404.html; location = /404.html { internal; }

error_page 500 502 503 504 /50x.html; location = /50x.html { internal; } }

# Restart NGINX to Apply the Changes:

sudo systemctl restart nginx

Open your browser with your public IP address and add the port number (80).
