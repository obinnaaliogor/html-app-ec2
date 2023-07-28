Title: Host an HTML website on a single EC2 instance in the default VPC
Instructions:
Task 1:
1. Download the web file from the following 
link: https://drive.google.com/file/d/15ql0ixVoZ0nILDAXYrodPpTKiHZRpK7U/
view?usp=sharing
2. Upload the web files to an S3 bucket.
3. Create a script that downloads the web files from the S3 bucket and hosts the
HTML website on an EC2 instance. Refer to the sample script provided in the 
image below.
4. Add the script to the EC2 user data at launch to host the HTML website.
Task 2:
1. Download the web file from the following 
link: https://drive.google.com/file/d/15ql0ixVoZ0nILDAXYrodPpTKiHZRpK7U/
view?usp=sharing
2. Upload the web files to a public GitHub repository.
3. Create a script that downloads the web files from the GitHub repository and 
hosts the HTML website on an EC2 instance. Refer to the sample script 
provided in the image below.
4. Add the script to the EC2 user data at launch to host the HTML website.
Acceptance Criteria:
1. You need to create two separate scripts that can be added to the EC2 user 
data at launch to host the HTML website using the provided web file.

-----------------

## SOLUTION ##

**Title:** Host an HTML website on a single EC2 instance in the default VPC

**Description:**
This Jira issue is to create two separate scripts for hosting an HTML website on a single EC2 instance in the default VPC. The website files will be provided through web links and need to be uploaded either to an S3 bucket or a public GitHub repository, depending on the chosen task. The EC2 user data will be used to run the scripts automatically when launching the EC2 instance.

**Instructions:**

**Task 1: Hosting HTML website using S3 bucket**

1. Download the web files from the provided link: [Web Files S3 Link](https://drive.google.com/file/d/15ql0ixVoZ0nILDAXYrodPpTKiHZRpK7U/view?usp=sharing)
2. Upload the web files to an S3 bucket.
3. Create a script that downloads the web files from the S3 bucket and hosts the HTML website on an EC2 instance.

**Task 2: Hosting HTML website using a public GitHub repository**

1. Download the web files from the provided link: [Web Files GitHub Link](https://drive.google.com/file/d/15ql0ixVoZ0nILDAXYrodPpTKiHZRpK7U/view?usp=sharing)
2. Upload the web files to a public GitHub repository.
3. Create a script that downloads the web files from the GitHub repository and hosts the HTML website on an EC2 instance.

**Acceptance Criteria:**

1. Two separate scripts are created, one for each task, that can be added to the EC2 user data at launch to host the HTML website using the provided web files.

**Sample Script for Task 1:**

```bash
#!/bin/bash

# Install required packages (if needed)
sudo yum update -y
sudo yum install -y httpd

# Configure AWS CLI (if not already configured)
# Follow the prompts to enter your AWS Access Key ID, Secret Access Key, and default region
# aws configure

# Set variables
S3_BUCKET_NAME="your-s3-bucket-name"
INDEX_FILE_NAME="index.html"

# Download web files from S3 bucket
aws s3 cp s3://${S3_BUCKET_NAME}/${INDEX_FILE_NAME} /var/www/html/${INDEX_FILE_NAME}

# Start Apache HTTP server
sudo service httpd start
sudo chkconfig httpd on
```

**Sample Script for Task 2:**

```bash
#!/bin/bash

# Install required packages (if needed)
sudo yum update -y
sudo yum install -y httpd git

# Set variables
GITHUB_REPO_URL="https://github.com/yourusername/your-repo.git"
INDEX_FILE_NAME="index.html"

# Clone the GitHub repository
git clone ${GITHUB_REPO_URL} /var/www/html

# Start Apache HTTP server
sudo service httpd start
sudo chkconfig httpd on
```

**Note:** Please replace "your-s3-bucket-name" and "yourusername/your-repo" with your actual S3 bucket name and GitHub repository URL, respectively, in the sample scripts.
