![header](<images/New Project.png>)

#### Automating AWS infrastructure in code using Terraform - Armstrong

We will Automate AWS infrastructure provisioning and management using Terraform in this project, enabling efficient and scalable deployment of resources with code.

# Automate Infrastructure With laC using Terraform Part 1

![structure](images/structure.jpg)

# Preliminary Steps

• Create an IAM user, name it terraform (ensure that the user has only programatic access to your AWS account) and grant this user AdministratorAccess permissions. 

• Copy the secret access key and access key ID. Save them in a notepad temporarily.

• Configure programmatic access from your workstation to connect to AWS using the access keys copied above and a Python SDK (boto3). 

• You must have Python 3.6 or higher on your workstation.

• For Windows OS, use gitbash, if you are on a Mac, you can simply open a terminal . 

• Read here (https://boto3.amazonaws.com/v1/documentation/api/latest/guide/quickstart.html) to configure the Python SDK properly.

> Documentation and developers tend to refer to the AWS SDK for Python as “Boto3,” and this documentation often does so as well.

For easier authentication configuration - use 
 ```AWS CLI``` with aws configure command.

• Create an S3 bucket to store Terraform state file. You can name it something like <yourname>-dev-terraform-bucket (Note: S3 bucket names must be unique unique within a region partition, you can read about $3 bucken naming in this article). We will use this bucket from Project-17 onwards.
When you have configured authentication and installed boto3, make sure you can programmatically access your AWS account by running following commands in

>Useful websites
```
https://www.python.org/downloads/
https://boto3.amazonaws.com/v1/documentation/api/latest/index.html
https://docs.python.org/3.12/tutorial/index.html
https://docs.python.org/3.12/index.html
https://docs.python.org/3.12/using/windows.html
https://docs.python.org/3.12/whatsnew/3.12.html
https://github.com/boto/boto3
```

# Creating an IAM user

![iam](<images/iam - Copy.jpg>)
---
![user](<images/user - Copy.jpg>)
---
![terraform user](<images/user terraform - Copy.jpg>)
---
![admin access](<images/admin access.jpg>)
---
![iam user](<images/iam user.jpg>)
---

https://004134777362.signin.aws.amazon.com/console

TERRAFORM_user

password : ..........

[login details](<images/iam credentials.txt>)
---
![created user](<images/user created.jpg>)
---
![new user](<images/new user.jpg>)
---
---

![access key](<images/create access key.jpg>)
---
![cli key](<images/cli access key.jpg>)
---
![create key](<images/create key.jpg>)
---
![id and password](images/id.jpg)
---


