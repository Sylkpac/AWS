# Table of Content:

1.  [Securing AWS Accounts and Setting Up Billing Budgets for Cloud Operations](#securing_aws_accounts)
2.  [Configuring AWS CLI for Secure Cloud Operations](#configuring-aws-cli)

------------------------------------------------------

# Securing AWS Accounts and Setting Up Billing Budgets for Cloud Operations<a name="securing_aws_accounts"></a> 

## Objective
This lab will guide you through securing an AWS root account with Multi-Factor Authentication (MFA), creating a dedicated admin user for day-to-day tasks, and setting up a billing budget to monitor cloud expenses. These steps ensure the secure management of AWS environments and help control costs.

## Prerequisites
* AWS root account credentials.
* Authenticator app (e.g., Duo, Authy, Google Authenticator).
* Basic familiarity with the AWS Management Console.

## Tools Required
* AWS Management Console access.
* Authenticator app for MFA setup.

## Step-by-Step Procedure

### 1. Log in to AWS Root Account
Log in to the AWS Management Console using the root account credentials.

### 2. Set Up MFA for the Root User
In the AWS search bar, type IAM and select the IAM service.
On the IAM dashboard, select Security Recommendations and click Add MFA.
Give your device a recognizable name (e.g., "My Phone").
Select Authenticator App and follow the instructions to link it with your MFA app (e.g., Duo Mobile, Authy, Google Authenticator).
Tip: Use the root account only for limited actions like creating users or handling billing. Avoid using it for infrastructure management.

### 3. Create an Admin User
In the IAM dashboard, under Access Management, select Users and click Create user.
Provide a username (e.g., admin_user).
Tick the following options:  

_Provide user access to the AWS Management Console_         
_I want to create an IAM user_  
_Autogenerated password_    

Click Next to proceed to permissions.

### 4. Assign Permissions to the Admin User
Under Attach policies directly, search for and select the following policies:

_AdministratorAccess_   
_AWSBillingConductorFullAccess_  
_Billing_    
_IAMUserChangePassword_ 

Click Create user.

### 5. Enable Billing Access for IAM Users
Still logged in with the root user, click your username at the top right and select Account.
Scroll to IAM user and role access to billing information, click Edit, tick Activate IAM Access, and click Update.

### 6. Log Out of the Root Account
Save your root account credentials securely (e.g., in a password manager).
Log out from the root account.

### 7. Log in Using the Admin User
Log in to the AWS Management Console with the admin user you just created.
Navigate to IAM, and follow the same steps as earlier to add MFA to the admin user.

### 8. Set Up an AWS Budget
In the AWS Console, search for Billing and Cost Management and open the dashboard.
Under Budget status, click Setup Required.
In the Templates - New section, select Monthly Cost Budget.
Set a budget amount that aligns with your needs and enter your email address(es) to receive alerts.
Click Create Budget.

## Why Should a Cloud Security Engineer Know This?
Properly securing AWS accounts and setting up cost management are foundational skills for cloud security engineers.
MFA ensures the root and admin accounts are protected from unauthorized access. This reduces the risk of account compromise.
Admin users allow for secure operations without exposing the root account, following the principle of least privilege.
Billing budgets help track cloud costs, preventing unexpected expenses—critical for both security and financial governance.
By following these best practices, cloud security engineers ensure a secure and cost-efficient cloud environment.

------------------------------------------------------

# Configuring AWS CLI for Secure Cloud Operations<a name="configuring-aws-cli"></a>  

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

