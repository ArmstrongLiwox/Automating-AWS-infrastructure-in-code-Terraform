# Automating-AWS-infrastructure-in-code-Terraform-
![header](<images/New Project.png>)

Automate your AWS infrastructure provisioning and management using Terraform in this project, enabling efficient and scalable deployment of resources with code
Getting started with best practices
Automate Infrastructure With laC using Terraform Part 1
After you have built AWS infrastructure for 2 websites manually, it is time to automate the process using Terraform.
Let us start building the same set up with the power of Infrastructure as Code (laC)


Prerequisites before writing Terraform code

• You must have completed Terraform course from the Learning dashboard

• Create an IAM user, name it terraform (ensure that the user has only programatic access to your AWS account) and grant this user AdministratorAccess permissions. • Copy the secret access key and access key ID. Save them in a notepad temporarily.

• Configure programmatic access from your workstation to connect to AWS using the access keys copied above and a Python SDK (boto3). 

https://www.python.org/downloads/
https://boto3.amazonaws.com/v1/documentation/api/latest/index.html
https://docs.python.org/3.12/tutorial/index.html
https://docs.python.org/3.12/index.html
https://docs.python.org/3.12/using/windows.html
https://docs.python.org/3.12/whatsnew/3.12.html

You must have Python 3.6 or higher on your workstation.

If you are on Windows, use gitbash, if you are on a Mac, you can simply open a terminal . Read here to configure the Python SDK properly.
For easier authentication configuration - use AWS CLI with aws configure command.
• Create an S3 bucket to store Terraform state file. You can name it something like <yourname>-dev-terraform-bucket (Note: S3 bucket names must be unique unique within a region partition, you can read about $3 bucken naming in this article). We will use this bucket from Project-17 onwards.
When you have configured authentication and installed boto3, make sure you can programmatically access your AWS account by running following commands in