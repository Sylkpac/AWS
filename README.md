# Table of Content:

1.  [Securing AWS Accounts and Setting Up Billing Budgets for Cloud Operations](#securing_aws_accounts)
2.  [Configuring AWS CLI for Secure Cloud Operations](#configuring-aws-cli)
3.  [Creating and Managing S3 Buckets Using AWS CLI for Secure Cloud Storage](#creating_s3)
4.  [Creating IAM Users and Assigning Read-Only Access to S3 via AWS CLI](#creating_iam)
5.  [Web Application Architecture on AWS With Summary and Flow](#webapp_arch)
6.   

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

------------------------------------------------------

# Creating and Managing S3 Buckets Using AWS CLI for Secure Cloud Storage<a name="creating_s3"></a> 

## Objective
This lab guides you through creating an Amazon S3 bucket using AWS CLI, uploading files to it, and verifying the contents. This hands-on activity helps you understand how to manage S3 buckets programmatically, an essential skill for cloud security engineers who need to monitor, audit, and automate storage operations.

## Prerequisites
* AWS CLI installed and configured on your system.
* IAM user with permissions to create S3 buckets and upload files (e.g., `AmazonS3FullAccess` policy).
* Basic knowledge of the command line interface (CLI).

## Tools Required
* AWS Management Console (optional, for cross-checking).
* Terminal with AWS CLI installed.

## Step-by-Step Procedure
### 1. Create an S3 Bucket
Run the following command, replacing <your-bucket-name> with a unique name:

`aws s3 mb s3://<your-bucket-name>`

### Example:

`aws s3 mb s3://bucketoctober`

### Explanation:
* `aws s3`: Tells the CLI to interact with S3.
* `mb`: Stands for "make bucket."
* `s3://bucketoctober`: The name of the bucket you’re creating.

### 2. OR Create an S3 Bucket in a Specific Region
You can specify a region with the `--region` flag:

`aws s3 mb s3://bucketoctober --region <region-name>`
### Example:

`aws s3 mb s3://bucketoctober --region us-east-1`

### 3. Verify the Bucket Creation
Check if the bucket was successfully created by listing all buckets:

`aws s3 ls`

If the bucket appears in the list, it means the creation was successful.
### 4. Create a Test File
In your terminal, create a simple text file to upload to the S3 bucket:

`echo "hello world" > test.txt`

### 5. Upload the File to the S3 Bucket
Use the `aws s3 cp` command to copy the file to your S3 bucket:

`aws s3 cp test.txt s3://<your-bucket-name>/`
### Example:

`aws s3 cp test.txt s3://bucketoctober/`
### Explanation:
`cp`: Stands for "copy," used to transfer files between your machine and the S3 bucket.

`s3://bucketoctober/`: The bucket name with a `/` at the end means the file will be uploaded to the root directory of the bucket.
### 6. Verify the File Upload
List the contents of your bucket to confirm the file is there:

`aws s3 ls s3://bucketoctober/`

You should see `test.txt` isted in the output.

## Why Should a Cloud Security Engineer Know This?
Understanding how to create and manage S3 buckets using AWS CLI is essential for cloud security engineers. Automating tasks like creating buckets and uploading files helps enforce security best practices, such as:
* **Auditing and monitoring**: CLI access allows programmatic checks on bucket configurations and contents.
* **Automated backups and storage**: Securely upload logs, configurations, or backups to S3.
* **Controlled access**: Using IAM policies ensures the right people or services access your data.
* **Incident response**: Engineers can quickly upload or retrieve forensic evidence from S3 buckets.

Mastering these skills enables cloud security engineers to efficiently manage cloud resources while maintaining security and compliance.

------------------------------------------------------

# Creating IAM Users and Assigning Read-Only Access to S3 via AWS CLI<a name="creating_iam"></a>

## Objective
This lab demonstrates how to create an IAM user and assign a managed policy using AWS CLI. Assigning specific permissions ensures the principle of least privilege, where users get only the access they need, enhancing cloud security.

## Prerequisites
* AWS CLI installed and configured with appropriate IAM permissions.
* IAM role or user with permissions to manage IAM users and policies (e.g., IAMFullAccess).

## Tools Required:
* AWS Management Console (optional for validation).   
* Terminal with AWS CLI installed and configured.

## Step-by-Step Procedure

### Part 1: Create a New IAM User
**Run the following command to create a new IAM user:**

`aws iam create-user --user-name <UserName>`

Replace <UserName> with the desired username. 

Example:

`aws iam create-user --user-name Sarah`

**Verify User Creation:**
List all IAM users to confirm that your new user has been created:

`aws iam list-users`    
If the new user appears in the output, the creation was successful.

### Part 2: Attach a Policy to the New User
**Attach the AmazonS3ReadOnlyAccess Policy:**   
Grant the user read-only access to S3 buckets by attaching the AmazonS3ReadOnlyAccess policy:

`aws iam attach-user-policy --user-name <UserName> --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess`

Example:

`aws iam attach-user-policy --user-name Sarah --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess`

Explanation:

`aws iam`: Specifies that the command interacts with the IAM service.  
`create-user`: Subcommand to create a new IAM user.   
`attach-user-policy`: Subcommand to attach a policy to the specified user.    
`--user-name <UserName>`: Option to specify the IAM user (e.g., Sarah).  
`--policy-arn`: Provides the Amazon Resource Name (ARN) of the policy being attached.   
Example ARN: `arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess` grants the user read-only access to S3.

**Verify the Policy Attachment:**   
Run the following command to list the attached policies for the user and confirm the policy is in place:

`aws iam list-attached-user-policies --user-name <UserName>`

Example:

`aws iam list-attached-user-policies --user-name Sarah`

## Why Should a Cloud Security Engineer Know This?
IAM user management is essential for secure cloud operations. A cloud security engineer needs to:

* Implement the principle of least privilege by assigning users only the permissions necessary to perform their tasks.
* Manage access control to ensure compliance with security policies and regulations.
* Enhance accountability by creating separate IAM users for specific tasks, enabling detailed tracking and auditing.
* Use managed policies effectively to streamline permission management and reduce the chance of misconfiguration.

Mastering IAM and policies ensures cloud environments remain secure and resilient, with minimal risk of unauthorized access.

------------------------------------------------------

# Web Application Architecture on AWS With Summary and Flow<a name="webapp_arch"></a> 

## Reference & Helpful Resources

* [AWS Architecture Example Diagrams](https://aws.amazon.com/architecture/reference-architecture-diagrams/?achp_navlib4&solutions-all.sort-by=item.additionalFields.sortDate&solutions-all.sort-order=desc&whitepapers-main.sort-by=item.additionalFields.sortDate&whitepapers-main.sort-order=desc&awsf.whitepapers-tech-category=*all&awsf.whitepapers-industries=*all&whitepapers-main.q=web&whitepapers-main.q_operator=AND&awsm.page-whitepapers-main=3)   
*Find all the AWS provided example architectures here

* Videos I used to learn how to draw Cloud Architecture Diagrams
  
  - [Primer](https://www.youtube.com/watch?v=zK8DUZM18UA)
  - [AWS services explained](https://youtu.be/FDEpdNdFglI?si=3U3g-jCOcf0_YGSX)
  - [How to copy diagrams from AWS](https://www.youtube.com/watch?v=5oonyR-CyME)
  - [How to animate diagrams](https://www.youtube.com/watch?v=UibU8g503G0)

* [The practice architecture I choose to copy](https://d1.awsstatic.com/architecture-diagrams/ArchitectureDiagrams/web-application-architecture-on-aws-ra.pdf?did=wp_card&trk=wp_card)
* Design app I used [Canva](https://www.canva.com/);along with downloadng all the [AWS icons](https://aws.amazon.com/architecture/icons/) to then upload the ones I needed to Canva

![My Web App Example Diagram](https://github.com/Sylkpac/Files-/blob/main/Web%20App%20Gif.gif)

## Architecture Components Overview

### [1] Amazon Route 53 (DNS Service)

**Purpose:** Maps domain names to IP addresses and routes traffic based on policies (e.g., latency or geolocation).       

**Why:** Improves availability and latency by routing users to healthy and nearest endpoints.       

**Flow:** 
- A web client makes a request (e.g., by entering a website URL).
- Route 53 resolves the domain to a CloudFront endpoint and directs traffic.

### [2] AWS WAF (Web Application Firewall)

**Purpose:** Protects the web application by filtering traffic to block attacks (e.g., SQL injections, DDoS).

**Why:** Ensures that only legitimate traffic reaches your app, preventing malicious requests.

**Flow:** WAF inspects requests before they reach CloudFront, blocking harmful traffic early.

### [3] Amazon CloudFront (Content Delivery Network)
**Purpose:** Delivers static content (e.g., images, CSS) through a global network of edge locations to reduce latency.

**Why:** Speeds up content delivery by caching assets closer to users.

**Key Detail:** 
- *Edge Locations:* These are data centers around the globe used by CDNs like CloudFront to store cached content.
- *TLS/SSL Certificates:* CloudFront secures connections using certificates from AWS Certificate Manager (ACM).

**Flow:** 
1. CloudFront checks its edge location cache for the requested content.

2. If cached, it serves the content to the client directly.
3. If not, CloudFront fetches content from the origin (e.g., S3 or a backend server).

### [4] Amazon S3 (Storage Service)

**Purpose:** Stores static assets (e.g., images, CSS files) and backups.

**Why:** Reduces the need to store static content on EC2 instances, improving cost efficiency.

**Analogy:** Think of CloudFront as RAM (fast access), while S3 is like disk storage (slower but larger).

### [5] AWS Certificate Manager (ACM)

**Purpose:** Manages SSL/TLS certificates for encrypted communication.

**Why:** Ensures secure connections between users and services without manual certificate renewals.

**Flow:** 
- ACM-provided certificates are used by CloudFront and the Application Load Balancer (ALB) to encrypt traffic.
- Certificates are provisioned once and attached to resources, not generated per connection.

### [6] Application Load Balancer (ALB)

**Purpose:** Distributes traffic evenly across multiple backend EC2 instances (which will act as a backend server).

**Why:** Increases fault tolerance by rerouting traffic if an instance becomes unhealthy.

**Flow:**

1. ALB forwards requests from CloudFront to backend EC2 instances.
2. It ensures that the load is balanced across multiple instances.


### [7] NAT Gateway

**Purpose:** Allows EC2 instances in private subnets to access the internet (e.g., for updates) without exposing them to incoming traffic.

**Why:** Adds a layer of security by keeping private instances shielded from the public internet.

### [8] Auto Scaling Group

**Purpose:** Dynamically adds or removes EC2 instances based on traffic.

**Why:** Helps maintain performance during demand spikes and saves costs during idle periods.

**Flow:** If traffic increases, new instances launch automatically. If traffic drops, instances are terminated.

### [9] Amazon RDS (Relational Database Service)

**Purpose:** Provides a managed relational database for application data.

**why:** Automates backups and scaling, reducing administrative overhead.

**Flow:**
- Backend app servers interact with the primary RDS instance for database operations.
- If the primary database fails, the standby instance takes over to ensure availability.

### [10] Amazon ElastiCache (Caching Service)

**Purpose:** Caches frequently accessed data to reduce database load.

**Why:** Improves response times by avoiding repeated queries to the database.

### [11] Amazon EFS (Elastic File System)

**Purpose:** Provides shared storage accessible by multiple EC2 instances.

**Why:** Useful for sharing files (e.g., logs) between servers.

## VPC (Virtual Private Cloud) vs. AWS Cloud

**AWS Cloud:** Refers to the broader AWS infrastructure where global services like Route 53 and CloudFront operate. These services must remain public-facing to handle internet traffic.

**VPC:**  A private, isolated network inside the AWS Cloud, hosting resources like EC2 instances, RDS, and NAT gateways with controlled access.

## Subnet Roles

**Public Subnet (Web Layer):** Hosts public-facing resources like web servers and NAT gateways.

**Application Subnet (App Layer):** Runs backend logic and application servers privately.

**Database Subnet:** Stores sensitive data securely without internet exposure.

**Public NAT Gateway Subnet:** Allows private instances to make outbound internet requests.

## Client Request Flow – End-to-End Journey

### 1. Route 53 (DNS Resolution)

- Client sends a request to access the website.
- Route 53 resolves the domain to the nearest CloudFront endpoint.

### 2. AWS WAF (Security Inspection)

- WAF inspects the request for malicious content (like SQL injections).
- If safe, the request moves to CloudFront.

### 3. CloudFront (Content Delivery)

- CloudFront serves cached content from its nearest edge location if available.
- If not, it forwards the request to the backend servers through the ALB.

### 4. Amazon S3 (Static Content Retrieval)

- If the requested content is static (like images), CloudFront pulls it from S3 and caches it.

### 5. ACM (Secure Communication)

- CloudFront or ALB uses ACM certificates to establish a secure HTTPS connection with the client.

### 6. Application Load Balancer (Traffic Distribution)

- For dynamic content, ALB routes requests to the appropriate backend EC2 instances.

### 7. NAT Gateway (Private Internet Access)

- If backend servers need internet access (e.g., for patches), they use the NAT gateway.

### 8. Auto Scaling Group (Scaling Resources)

- Auto Scaling adjusts the number of instances based on demand.

### 9. RDS (Database Operations)

- Backend servers interact with RDS to retrieve or store data.

### 10. ElastiCache (Faster Data Retrieval)

- Frequently accessed data is cached in ElastiCache for faster response times.

### 11. EFS (Shared Storage)

- If servers need access to shared files, they use EFS.
