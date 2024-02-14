
### Dynamic E-Commerce Web App Deployment on AWS

This repository contains scripts and a reference diagram for deploying a dynamic E-Commerce web application on Amazon Web Services (AWS). The project utilizes various AWS services and follows best practices for security, scalability, and fault tolerance.

### Architecture Overview
The deployment architecture includes the following components:
#### VPC Configuration: 
Configured with public and private subnets across two availability zones for high availability and fault tolerance.
#### Internet Gateway: 
Allows communication between instances in the VPC and the internet.
#### Security Groups: 
Utilized for firewall configurations for EC2 instances to control inbound and outbound traffic.
#### NAT Gateway: 
Enables instances in private subnets to access the internet while remaining protected.
#### Bastion Host: 
Provides secure SSH access to instances in private subnets.
#### Load Balancer: 
Distributes web traffic across multiple EC2 instances in different availability zones.
#### Elastic File System (EFS): 
Facilitates file sharing across availability zones for EC2 instances.
#### MySQL RDS Database: 
Managed relational database service for storing application data.
#### Flyway: 
Used for database migration.
#### Autoscaling Group: 
Dynamically creates EC2 instances to ensure high availability, scalability, fault tolerance, and elasticity of the web application.
#### Route 53: 
Manages domain registration and DNS routing.
#### AWS S3: 
Stores web files for the application.
#### IAM Role: 
Grants EC2 instances permission to download web files from S3.
#### Deployment Steps
Clone the Repository: Clone this repository to your local machine to access deployment scripts and reference diagrams.
### Set Up AWS Environment:
Create a VPC with public and private subnets across multiple availability zones.
######  Configure internet gateway  NAT gateway, and security groups for EC2 instances.
###### Set up a Bastion Host for secure access to instances in private subnets.
###### Configure Elastic File System (EFS) for file sharing.
###### Create an RDS instance for the MySQL database.
##### Deploy EC2 Instances:
##### Launch EC2 instances in private subnets for web servers.
###### Configure IAM role to grant EC2 instances access to S3.
#### Database Setup:
##### Set up MySQL database using RDS.
###### Use Flyway for database migration.
###### Configure Load Balancer:
#### Set up Application Load Balancer to distribute web traffic.
###### Configure Autoscaling Group for EC2 instances to ensure scalability and fault tolerance.
###### Domain Registration and DNS Routing:
##### Register domain name using Route 53.
Create appropriate record sets for routing traffic to the Load Balancer.
##### Store Web Files in S3:
##### Upload web files to AWS S3 bucket for storage.
#### Final Steps:
##### Initiate the website on EC2 instances.
###### Create an AMI once the website is initialized for future deployments.
#### For detailed deployment steps and scripts, please refer to the repository files.

#### Reference Architecture
<img src="4.WordPress_SG (1).jpg">

###### Contributors

#### Charles Sangi/Devops Team
