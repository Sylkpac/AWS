# Table of Content:

1.  [Configuring AWS CLI for Secure Cloud Operations](#Configuring-AWS-CLI)
2.  

------------------------------------------------------

# Configuring AWS CLI for Secure Cloud Operations<a name="Configuring-AWS-CLI"></a>  

## Objective
Learn how to install and configure the AWS Command Line Interface (CLI) for secure access to AWS resources and manage IAM users. This lab will guide you through the process of setting up AWS credentials, configuring AWS CLI, and running a simple command to verify access. These steps are foundational for interacting with AWS services, especially S3 buckets, in a secure and efficient manner.

## Prerequisites

* AWS account (non-root user recommended).
* IAM user with necessary permissions to interact with AWS services.
* AWS CLI installed on a Linux machine.

## Tools Required
* AWS Console access (for creating IAM users and access keys).
* Linux machine with AWS CLI installed. I'm using WSL on Windows. 

## Step-by-Step Procedure

### 1. Install AWS CLI on Linux (if not installed)

`sudo apt install awscli`

Check to see if it was installed

`aws --version`

### 2. Log in to AWS Console
Open the AWS Console and DO NOT use your root account. Always operate as an IAM user for better security practices.

### 3. Navigate to IAM (Identity and Access Management)
In the AWS Console, go to All Services > 'IAM' under the Security, Identity, & Compliance section.

Select 'Users' on the left-hand pane under the 'Access management' drop down

### 4. Create IAM Access Keys
Choose the specific IAM user name you want to generate credentials for.

Click the Security credentials tab, then under Access Keys, select Create access key.

*Important: The access key and secret access key generated here are sensitive information—treat them like passwords and never share them publicly.

### 5. Configure AWS CLI
In your Linux terminal, type the following command to configure the AWS CLI:

`aws configure`

You will be prompted to enter the following information:

**AWS Access Key ID:** Paste the access key from the IAM user.

**AWS Secret Access Key:** Paste the secret key from the IAM user.

**Default region name:** Enter the region you'd like to work in (e.g., us-east-1). This can be changed later.

**Default output format:** Choose your preferred format for output (e.g., json, text, or table). Press Enter if you want to skip.

### 6. Verify AWS CLI Configuration
Run a command to verify that AWS CLI is working:

`aws iam list-users`

This command lists all the IAM users in your AWS account along with details... 

_‘User name’ is an IAM user in your AWS account._

_The 'UserId' and 'Arn' are AWS’s way of uniquely identifying the user within your account._ 

_The user was created on [Date], and last logged in to AWS using their password on [Date]_

Confirm that your configuration is correct by reviewing the output. If the list of users is displayed, your setup is successful.

## Why Should a Cloud Security Engineer Know This?

Understanding how to securely configure AWS CLI is crucial for a cloud security engineer. The CLI enables you to interact with AWS services programmatically, which can be more efficient than using the AWS Management Console, especially for automation tasks. By using IAM roles and access keys, you minimize the security risks associated with root accounts. Furthermore, managing access to AWS services securely is foundational to cloud security, as misconfigurations or exposed credentials can lead to vulnerabilities and breaches. Ensuring that your environment is set up securely allows you to maintain proper access control and audit user activity efficiently.



## Why Should a Cloud Security Engineer Know This?

Understanding how to securely configure AWS CLI is crucial for a cloud security engineer. The CLI enables you to interact with AWS services programmatically, which can be more efficient than using the AWS Management Console, especially for automation tasks. By using IAM roles and access keys, you minimize the security risks associated with root accounts. Furthermore, managing access to AWS services securely is foundational to cloud security, as misconfigurations or exposed credentials can lead to vulnerabilities and breaches. Ensuring that your environment is set up securely allows you to maintain proper access control and audit user activity efficiently.

------------------------------------------------------

