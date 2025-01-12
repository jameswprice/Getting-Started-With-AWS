
# Navigating Site
[aws search](https://github.com/user-attachments/assets/c0a90c43-dc4a-4be5-8292-77377e17122e)

[aws search expanded](https://github.com/user-attachments/assets/08ef5f57-017d-4a0d-93a6-64c9d136dd51)

# Billing & Cost Management - Create Budget from Template

[URL](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html)

1. Sign in to the AWS Management Console and open the AWS Cost Management console at ![](https://console.aws.amazon.com/cost-management/home)
2. In the navigation pane, choose Budgets.
3. At the top of the page, choose Create budget.
4. Under Budget setup, choose Use a template (simplified).
5. Under Templates, choose a template that best matches your use case:
    Zero spend budget: A budget that notifies you after your spending exceeds AWS Free Tier limits.
    Monthly cost budget: A monthly budget that notifies you if you exceed, or are forecasted to exceed, the budget amount.


## IAM - Non-Root, Admin User

## OPTIONAL Route 53 (Custom Domain)

## OPTIONAL Certificate Manager  (SSL/TLS certificate)

## S3 - Host Static HTTP Website Hosted on S3
Source: [Setting permissions for website access](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html)

### Create Bucket & Upload Files 
[Create S3 Bucket] (https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html)

Download & Unzip folder, Resume-HTML


###

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

Copy the following bucket policy, and paste it in the Bucket policy editor, NOTE Under Resource section, update bucket name.

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Replace-Bucket-Name/*"
            ]
        }
    ]
}

Click Save changes

### Choose Properties

    Under Static website hosting, choose Edit.

    Choose Use this bucket to host a website.

    Under Static website hosting, choose Enable.

    In Index document, enter index.html.

## CloudFront - Secure (HTTPS) Static S3 Website

## Amplify - Host Secure S3 Website & APP (Vitae)

## Elastic Beanstalk - Host APP

## EC2 & Elastic Load Balancer - Host site on Apache Server

Sources: [Linux 2023] (https://docs.aws.amazon.com/linux/al2023/ug/ec2-lamp-amazon-linux-2023.html

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

    --logout & login to pickup permissions

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

    AWS CLI
    aws s3 sync s://bucket-name /var/www/html/
    rm -rf /var/www/html
    ls

    Down free site from [Free CSS} (https://www.free-css.com/free-css-templates/page296/inance)

    cd /var/www/html
    
    Down free site from [Free CSS} (https://www.free-css.com/free-css-templates/page296/inance)
    
    wget https://www.free-css.com/assets/files/free-css-templates/download/page296/inance.zip

    unzip
    inance-html
    sudo mv /home/ec2-user/inance-html/* /var/www/html/

## Windows 11 (SSH) & WINSCP 

