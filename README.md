
# Getting Started With AWS

AWS Service - Task:

Billing & Cost Management - Create Budget 

Identity Access Management (IAM) - Create Non-Root, Admin User & EC2 Service Role

OPTINAL Route 53 & Certificate Manager

S3 & CloudFront - Secure Static Web Site w/ custom Domain

Amplify - Secure Static S3 Website w/ custom Domain & Vite app (GitHub)

Elastic Beanstalk - Host Python App with Secure Custom Domain

EC2 & Application Load Balancer - Apache web server w/ secure Custom Domain

Windows 11 - Configure SSH, AWS CLI & WINSCP




## Billing & Cost Management - Create Budget from Template

[Budgets](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html)

Sign in to the AWS Management Console

Search for Billing and Cost Management 

On left, choose Budgets

At the top of the page, choose Create budget

Under Budget setup, choose Use a template (simplified)

Under Templates, choose a template that best matches your use case:

Select Zero spend budget: A budget that notifies you after your spending exceeds AWS Free Tier limits.

Enter Email Receiptents

Create Budget

## IAM - Non-Root, Admin User


## OPTIONAL Route 53 (Custom Domain)


## OPTIONAL Certificate Manager  (SSL/TLS certificate)


## S3 - Host Static HTTP Website Hosted on S3
Source: [Setting permissions for website access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html)


### Create Bucket & Upload Files 
[Create S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html))

**** Download & Unzip folder, Resume-HTML

Left navigation pane, choose Buckets.
Choose Create bucket.
Create bucket page opens.
Under General configuration, verify AWS Region
Under Bucket type, choose General purpose.
For Bucket name, enter globhally unique name
Uncheck Block Public Access settings for this bucket
Check box to acknpwledge unblocking public access
Maintain remaining default selections
Click icon, Create bucket

### Choose Permissions.

Under Bucket Policy, choose Edit.

https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html

### Choose Properties

Under Static website hosting, choose Edit.

Choose Use this bucket to host a website.

Under Static website hosting, choose Enable.

In Index document, enter index.html.

## CloudFront - Secure (HTTPS) Static S3 Website


## Amplify - Host Secure S3 Website & APP (Vitae)


## Elastic Beanstalk - Host APP


## EC2 & Elastic Load Balancer - Host site on Apache Server

Sources: [Linux 2023] (https://docs.aws.amazon.com/linux/al2023/ug/ec2-lamp-amazon-linux-2023.html)

[AWS Docker] (https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html)

### User Data - Demo how userdata scripts can be used at startup, scripts are executed as root

#!/bin/bash
#install httpd docker git 
yum update -y
yum install -y httpd docker
service docker start
systemctl start httpd
systemctl enable httpd
echo "<h1>AWS Demo from $(hostname -f)</h1>" > /var/www/html/index.html

### Post ec2 launch - Add ec2-user to docker & apache groups
sudo usermod -a -G docker ec2-user
sudo usermod -a -G apache ec2-user
if needed, logout & login to pickup permissions
groups
docker info

### Change the group ownership of /var/www and its contents to the apache group

sudo chown -R ec2-user:apache /var/www

### Add group write permissions, set group ID, & change the directory permissions of /var/www and subdirectories

sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;

### Add group write permissions, recursively change the file permissions of /var/www and its subdirectories

find /var/www -type f -exec sudo chmod 0664 {} \;

### Test Server
EC2 Console
Locate EC2's public dns adddress
Click link to launch brower
Allow request to timeout or error out
Copy url address
Open a seperate broswer tab
Paste url address but remove 's' from https

### Static Web Site - S3 & WGET SITE

aws s3 sync s://bucket-name /var/www/html/

rm headshot.jpg index.html styles.css scripts.js

### Download free site from [Free CSS] (https://www.free-css.com/free-css-templates/page296/inance)

cd /var/www/html

ls
 
wget https://www.free-css.com/assets/files/free-css-templates/download/page296/inance.zip

unzip
 
cd inance-html
    
sudo mv /home/ec2-user/inance-html/* /var/www/html/

Test Server

### Configure Application Load Balancer, Target Group, Custom Domain


## Windows 11 (SSH) & WINSCP 

