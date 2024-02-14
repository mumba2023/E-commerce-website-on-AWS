Dynamic E-Commerce Web App Deployment on AWS
This repository contains scripts and diagrams for deploying a dynamic E-Commerce web application on AWS. The project utilizes various AWS services and configurations to ensure high availability, fault tolerance, and scalability of the application.

Architecture Overview
The architecture of the deployed solution includes the following components:

Virtual Private Cloud (VPC) with public and private subnets across two availability zones.
Internet Gateway for communication between instances in the VPC and the internet.
Network Address Translation (NAT) Gateway for instances in private subnets to access the internet.
Bastion Host for secure SSH access to instances in private subnets.
Elastic File System (EFS) for sharing files across availability zones.
MySQL RDS database for data storage.
Application Load Balancer (ALB) to distribute web traffic across multiple EC2 instances.
Auto Scaling Group to dynamically create and manage EC2 instances based on traffic demand.
Route 53 for domain registration and DNS routing.
AWS S3 to store web files.
IAM Role for EC2 instances to access files stored in S3.


Deployment Scripts.

Startup Server Deployment Script

The following script is used to launch the startup server:

bash

# Update packages and create html directory
sudo su
yum update -y
mkdir -p /var/www/html
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-03c9b3354880b36a6.efs.us-east-1.amazonaws.com:/ /var/www/html

# Install Apache
sudo yum install -y httpd httpd-tools mod_ssl
sudo systemctl enable httpd 
sudo systemctl start httpd

# Install PHP 7.4
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y

# Install MySQL 5.7
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld

# Set permissions
sudo usermod -a -G apache ec2-user
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
sudo find /var/www -type f -exec sudo chmod 0664 {} \;
chown apache:apache -R /var/www/html 

# Download WordPress files
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
cp -r wordpress/* /var/www/html/

# Create wp-config.php file
cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php

# Edit wp-config.php file (Update Database details)

# Restart the webserver
service httpd restart
Application Server Installation Script
The following script installs WordPress on the application server:

bash
Copy code
#!/bin/bash
yum update -y
sudo yum install -y httpd httpd-tools mod_ssl
sudo systemctl enable httpd 
sudo systemctl start httpd
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld
echo "fs-03c9b3354880b36a6.efs.us-east-1.amazonaws.com:/ /var/www/html nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 0 0" >> /etc/fstab
mount -a
chown apache:apache -R /var/www/html
sudo service httpd restart
Diagram
The reference diagram for the project is available in the repository.

For any questions or issues, please contact [maintainer's email/contact].

Feel free to enhance the README with more details on configuration, dependencies, and troubleshooting steps. Adjust the template according to your specific project needs.






