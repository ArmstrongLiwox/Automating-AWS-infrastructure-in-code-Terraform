![header](<images/New Project.png>)

#### Automating AWS infrastructure in code using Terraform - Armstrong

We will Automate AWS infrastructure provisioning and management using Terraform in this project, enabling efficient and scalable deployment of resources with code.

# Automate Infrastructure With laC using Terraform Part 1

![structure](images/structure.jpg)

# Preliminary Steps

• Create an IAM (Identity and Access Management) )ser, name it terraform (ensure that the user has only programatic access to your AWS account) and grant this user AdministratorAccess permissions. 

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
# what is an SDK
> SDK stands for Software Development Kit. It contains a set of preconfigured tools and libraries. The AWS SDK for Python (Boto3) provides a Python API for AWS infrastructure services. Using the SDK for Python, you can build applications on top of Amazon S3, Amazon EC2, Amazon DynamoDB, and more.

# what is Boto3

> Boto3 allows us to write Python code that interacts with AWS services. It acts like an intermidiary between us and the service we want to manage. It contains easy-to-use APIs to many AWS services.


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

![change passwords](<images/change password.jpg>)

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


# Installing AWS CLI

![Alt text](<images/cli get started.jpg>)
---
![Alt text](<images/cli install.jpg>)
---
![Alt text](<images/run cli.jpg>)
---

---
https://awscli.amazonaws.com/AWSCLIV2.msi

```
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```
```
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi /qn
```
```
aws --version
```
![install aws cli](<images/install cli.jpg>)
---
![accessed aws cli](images/accessed.jpg)

![aws configure](<images/aws configure.jpg>)


# Install Terraform

![download terraform](<images/downloadl terraform.jpg>)

![move file](<images/move to program files.jpg>)

![copy path](<images/copy path.jpg>)

![system variables](<images/path system variables.jpg>)

![new path](images/path.jpg)

![terraform -version](<images/terraform version.jpg>)

## Terraform has been set up successfully



# Create S3 bucket

Create an S3 bucket to store Terraform state file.

```terr-cli-practice```

S3 bucket names must be unique unique within a region partition.
 
you can read about S3 bucken naming in this article - 
https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html


## General purpose buckets naming rules
The following naming rules apply for general purpose buckets.
```
Bucket names must be between 3 (min) and 63 (max) characters long.

Bucket names can consist only of lowercase letters, numbers, dots (.), and hyphens (-).

Bucket names must begin and end with a letter or number.

Bucket names must not contain two adjacent periods.

Bucket names must not be formatted as an IP address (for example, 192.168.5.4).

Bucket names must not start with the prefix xn--.

Bucket names must not start with the prefix sthree- and the prefix sthree-configurator.

Bucket names must not end with the suffix -s3alias. This suffix is reserved for access point alias names
```
## Directory bucket naming rules
Directory bucket names must:
```
Be unique within the chosen AWS Region and Availability Zone.

Be no more than 3–63 characters long, including the suffix.

Consists only of lowercase letters, numbers and hyphens (-).

Begin and end with a letter or number.

Must include the following suffix: --azid--x-s3.

A suffix is automatically added to the base name that you provide. This suffix includes the Availability Zone ID of the Availability Zone that you chose.
```
---


We will use this bucket from Project-17 onwards.

![s3](images/s3.jpg)

![s3 name](<images/s3 namee.jpg>)

![s3 create](<images/create s3.jpg>)

![s3 created](<images/bucket createdd.jpg>)

![s3 confirmed](<images/s3 confirmed.jpg>)
---

## Make sure you can programmatically access your AWS account 

by running following commands in >python:

```
s3 = boto3.resource('s3')
for bucket in s3.buckets.all():
    print(bucket.name)
```
![python](images/python.jpg)

```
pip install boto3
```
```
 python.exe -m pip install --upgrade pip
```

![install boto3](<images/pip install boto3.jpg>)
---
```
python.exe -m pip install --upgrade pip
```
![update boto 3](<images/update boto 3.jpg>)

![upgrade pip](<images/upgrade pip.jpg>)
---

```
import boto3
```
```
import json
```
---
![import boto3](<images/import boto3.jpg>)


import boto3
s3 = boto3.resource('s3')

```
aws configure
```

```
cat ~/.aws/credentials
```

print(bucket.name)

The terraform glossary shows brief definitions of some of the technical terms used in the documentation for Terraform, as well as some terms that come up frequently in conversations throughout the Terraform community.

## Terraform specific terminology
> These are Terraform-specific terminology, such as:

[Attribute,
Resource,
Interpolations,
Argument,
Providers,
Provisioners,
Input Variables,
Output Variables,
Module,
Data Source,
Local Values,
Backend.](https://developer.hashicorp.com/terraform/docs/glossary)


## Configuration Syntax

The syntax of Terraform configurations is called HashiCorp Configuration Language (HCL). 
It is meant to strike a balance between human readable and editable as well as being machine-friendly. 
For machine-friendliness, Terraform can also read JSON configurations. 
For general Terraform configurations, however, we recommend using the HCL Terraform syntax.

> The Terraform language syntax is built around two key syntax constructs: *arguments and blocks.*

- Arguments

An argument assigns a value to a particular name:
```image_id = "abc123"```

The identifier before the equals sign is the argument name, and the expression after the equals sign is the argument's value

- Blocks
A block is a container for other content:
```resource "aws_instance" "example" {
  ami = "abc123"

  network_interface {
    # ...
  }
}
```
$$
A block has a type (resource in this example). Each block type defines how many labels must follow the type keyword. The resource block type expects two labels, which are aws_instance and example in the example above. A particular block type may have any number of required labels, or it may require none as with the nested network_interface block type.

After the block type keyword and any labels, the block body is delimited by the { and } characters. Within the block body, further arguments and blocks may be nested, creating a hierarchy of blocks and their associated arguments.

The Terraform language uses a limited number of top-level block types, which are blocks that can appear outside of any other block in a configuration file. Most of Terraform's features (including resources, input variables, output values, data sources, etc.) are implemented as top-level blocks.
$$




## Local values

A local value assigns a name to an expression, so you can use it multiple times within a module without repeating it.

If you're familiar with traditional programming languages, it can be useful to compare Terraform modules to function definitions:

*Input variables* are like function arguments.
*Output values* are like function return values.
*Local values* are like a function's temporary local variables.

*Note:* For brevity, local values are often referred to as just "locals" when the meaning is clear from context.

## Backend
The part of Terraform's core that determines how Terraform stores state and performs operations (like plan, apply, import, etc.).

## Data Type

Data type is a general programing concept, it refers to how data represented in a programming language and defines how a compiler or interpreter can use the data. Common data types are:

$$
Integer,
Float,
String,
Boolean, etc.
$$

## Best practices
1. Ensure that every resource is tagged using multiple key-value pairs. You will see this in action as we go along.

2. Try to write reusable code, avoid hard coding values wherever possible. (For learning purpose, we will start by hard coding, but gradually refactor our work to follow best practices).

# Base Infrastructure Automation (VPC | Subnets | Security Groups)

We will create a directory structure via Visual Studio Code:

1. Create a folder called PBL

2. Create a file in the folder, name it main.tf
---
![main.tf file](images/main.tf.jpg)
---
### Provider and VPC resource section

> Set up Terraform CLI as per this instruction.

1. Add AWS as a provider, and a resource to create a VPC in the main.tf file.

2. Provider block informs Terraform that we intend to build infrastructure within AWS.

3. Resource block will create a VPC.

```
provider "aws" {
  region = "us-east-1"
}

# Create VPC
resource "aws_vpc" "main" {
  cidr_block                     = "172.16.0.0/16"
  enable_dns_support             = "true"
  enable_dns_hostnames           = "true"
  enable_classiclink             = "false"
  enable_classiclink_dns_support = "false"

}
```

---
![main.tf content](<images/main.tf 2.jpg>)
---

```
terraform init
```
![terraform error](<images/terraform error.jpg>)

![terraform provider](<images/terraform providers.jpg>)

![terraform vpc](<images/terraform vpc.jpg>)

```
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.5.2"
}


# Create VPC
resource "aws_vpc" "main" {
  cidr_block                     = "172.16.0.0/16"
  enable_dns_support             = "true"
  enable_dns_hostnames           = "true"
  enable_classiclink             = "false"
  enable_classiclink_dns_support = "false"
}

```
---
![terraform initialized](<images/terraform initialized.jpg>)
---
```
terraform plan
```
terraform shows error

![plan error](<images/plan error.jpg>)


# Terraform commands

The available commands for execution are listed below.
The primary workflow commands are given first, followed by
less common or more advanced commands.
Usage: terraform [global options] <subcommand> [args]


## Main commands:

1. terraform init:          Prepare your working directory for other commands

 1. terraform validate:      Check whether the configuration is valid

 1. terraform plan:          Show changes required by the current configuration

 1. terraform apply:         Create or update infrastructure

 1. terraform destroy:       Destroy previously-created infrastructure

## All other commands:

 1. terraform console:       Try Terraform expressions at an interactive command prompt

 1. terraform fmt:          Reformat your configuration in the standard style

 1. terraform force-unlock:  Release a stuck lock on the current workspace

 1. terraform get:           Install or upgrade remote Terraform modules

 1. terraform graph:         Generate a Graphviz graph of the steps in an operation

 1. terraform import:        Associate existing infrastructure with a Terraform resource

 1. terraform login:         Obtain and save credentials for a remote host

 1. terraform logout:        Remove locally-stored credentials for a remote host

 1. terraform metadata:      Metadata related commands

 1. terraform output:        Show output values from your root module

 1. terraform providers:     Show the providers required for this configuration

 1. terraform refresh:       Update the state to match remote systems

 1. terraform show:          Show the current state or a saved plan

 1. terraform state:         Advanced state management

 1. terraform taint:         Mark a resource instance as not fully functional

 1. terraform test:          Execute integration tests for Terraform modules

 1. terraform untaint:       Remove the 'tainted' state from a resource instance

 1. terraform version:       Show the current Terraform version

 1. terraform workspace:     Workspace management

## Global options (use these before the subcommand, if any):

 1. terraform -chdir=DIR:    Switch to a different working directory before executing the given subcommand.

 1. terraform -help:         Show this help output, or the help for a specified subcommand.

 1. terraform -version:      An alias for the "version" subcommand.
---

---

terraform validate shows errors

![validate error](<images/validate error.jpg>)

let's impliment the recommended change

terraform validate shows success

![validate success](<images/validate success.jpg>)

```
terraform plan
```
![terraform plan](<images/terraform plan.jpg>)
```
terraform apply
```
VPC before terraform apply

![vpc before apply](<images/vpc before.jpg>)

![approve apply](<images/approve apply.jpg>)

![apply success](<images/apply suuccess.jpg>)

VPC after terraform apply

![vpc after apply](<images/vpc after apply.jpg>)

### Observations:

1. A new file is created terraform.tfstate This is how Terraform keeps itself up to date with the exact state of the infrastructure. 
It reads this file to know what already exists, what should be added, or destroyed based on the entire terraform code that is being developed.
2. If you also observed closely, you would realise that another file gets created during planning and apply. 
But this file gets deleted immediately. 
terraform.tfstate.lock.info  is what Terraform uses to track, who is running its code against the infrastructure at any point in time. 
This is very important for teams working on the same Terraform repository at the same time. 
The lock prevents a user from executing Terraform configuration against the same infrastructure when another user is doing the same - it allows to avoid duplicates and conflicts.
---
---

# Refactoring bad practice

## Subnets resource section

According to our architectural design, we require 6 subnets:

* 2 public
* 2 private for webservers
* 2 private for data layer

Let us create the first 2 public subnets.

We are creating 2 subnets, therefore declaring 2 resource blocks - one for each of the subnets.

We are using the vpc_id argument to interpolate the value of the VPC id by setting it to aws_vpc.main.id. This way, Terraform knows inside which VPC to create the subnet.

Add below configuration to the main.tf file:

```
# Create public subnets1
    resource "aws_subnet" "public1" {
    vpc_id                     = aws_vpc.main.id
    cidr_block                 = "172.16.0.0/24"
    map_public_ip_on_launch    = true
    availability_zone          = "eu-central-1a"

}

# Create public subnet2
    resource "aws_subnet" "public2" {
    vpc_id                     = aws_vpc.main.id
    cidr_block                 = "172.16.1.0/24"
    map_public_ip_on_launch    = true
    availability_zone          = "eu-central-1b"
}

```

*Run terraform validate, terraform plan and terraform apply*

![validate subnets](<images/validate subnets.jpg>)

![subnet plan](<images/subnet plan.jpg>)

![subnets before](<images/subnet before.jpg>)

![subnets apply error](<images/subnet apply error.jpg>)

subnets created successfully

![subnets succes](<images/subnets success.jpg>)

![subnets after apply](<images/subnets after apply.jpg>)

