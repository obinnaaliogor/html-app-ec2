This Jira issue is to create two separate scripts for hosting an HTML website on a single EC2 instance in the default VPC. The website files will be provided through web links and need to be uploaded either to an S3 bucket or a public GitHub repository, depending on the chosen task. The EC2 user data will be used to run the scripts automatically when launching the EC2 instance.

TASK 1 USING S3 BUCKET FOR THE STORAGE OF THE WEBFILES

#!/bin/bash

# Install required packages (if needed)

sudo yum update -y

sudo yum install -y httpd

# Create an AMI role that will enable ec2 instance to pull the webfiles from the s3 bucket

# The IAM permission (s3 full access) should be attached to the ec2 instance

# Set variables

S3_BUCKET_NAME="myhtml-bucket"

INDEX_FILE_NAME="mole-main.zip"

APP_CODE_UNZIP="mole-main"



# Download web files from S3 bucket

sudo aws s3 cp s3://${S3_BUCKET_NAME}/${INDEX_FILE_NAME} /var/www/html/${INDEX_FILE_NAME}

cd /var/www/html

sudo unzip ${INDEX_FILE_NAME}

sudo mv ${APP_CODE_UNZIP}/* .

sudo mv ${APP_CODE_UNZIP}/.* .

#Delete the uzipped and zip files

sudo rm -rf ${INDEX_FILE_NAME}  ${APP_CODE_UNZIP}

# Start Apache HTTP server

sudo service httpd enable

sudo service httpd start

sudo chkconfig httpd on



 TASK 2 USING GITHUB  FOR THE STORAGE OF THE WEBFILES

#!/bin/bash

Install required packages (if needed)

sudo yum update -y
sudo yum install -y httpd git

Set variables

GITHUB_REPO_URL="https://github.com/obinnaaliogor/html-app-ec2/archive/refs/heads/main.zip"
INDEX_FILE_NAME="main.zip"
UNZIPPED_FILES="html-app-ec2-main"

Clone the GitHub repository

cd /var/www/html
sudo wget ${GITHUB_REPO_URL} /var/www/html
sudo unzip ${INDEX_FILE_NAME}
sudo mv ${UNZIPPED_FILES}/* . ${UNZIPPED_FILES}/.* .
sudo rm -rf ${INDEX_FILE_NAME} ${UNZIPPED_FILES}

Start Apache HTTP server

sudo service httpd enable
sudo service httpd start
sudo chkconfig httpd on
