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

---
---

## Observations:

1. Hard coded values: Remember our best practice hint from the beginning? Both the availability_zone and cidr_block arguments are hard coded. 
We should always endeavour to make our work dynamic.

2. Multiple Resource Blocks: Notice that we have declared multiple resource blocks for each subnet in the code. This is bad coding practice. We need to create a single resource block that can dynamically create resources without specifying multiple blocks. 
Imagine if we wanted to create 10 subnets, our code would look very clumsy. 

So, we need to optimize this by introducing a count argument.

## Now let us improve our code by refactoring it.

*First, destroy the current infrastructure. 
Since we are still in development, this is totally fine. Otherwise, DO NOT DESTROY an infrastructure that has been deployed to production.*

To destroy whatever has been created run 
```
terraform destroy 
```
command, and type yes after evaluating the plan.

![terraform destroy](images/destroy.jpg)

![destroy approved](images/destroyed.jpg)

![subnet after destroy](<images/subnet after destroy.jpg>)

![vpc after destroy](<images/vpc after destroy.jpg>)

---
---
# Fixing The Problems By Code Refactoring

## Fixing Hard Coded Values: We will introduce variables, and remove hard coding.

Starting with the provider block, declare a variable named **region**, give it a default value, 
and update the provider section by referring to the declared variable.

```
    variable "region" {
        default = "us-east-1"
    }

    variable "vpc_cidr" {
        default = "172.16.0.0/16"
    }

    variable "enable_dns_support" {
        default = "true"
    }

    variable "enable_dns_hostnames" {
        default ="true" 
    }

    variable "enable_classiclink" {
        default = "false"
    }

    variable "enable_classiclink_dns_support" {
        default = "false"
    }

    provider "aws" {
    region = var.region
    }

    # Create VPC
    resource "aws_vpc" "main" {
    cidr_block                     = var.vpc_cidr
    enable_dns_support             = var.enable_dns_support 
    enable_dns_hostnames           = var.enable_dns_support
    enable_classiclink             = var.enable_classiclink
    enable_classiclink_dns_support = var.enable_classiclink

    }

```
## Fixing multiple resource blocks: 

This is where things become a little tricky. 
It's not complex, we are just going to introduce some interesting concepts. 
*Loops & Data sources*

Terraform has a functionality that allows us to pull data which exposes information to us. 
For example, every region has Availability Zones (AZ). 
Different regions have from 2 to 4 Availability Zones. 
With over 20 geographic regions and over 70 AZs served by AWS, 
it is impossible to keep up with the latest information by hard coding the names of AZs. 
Hence, we will explore the use of Terraform's Data Sources to fetch information outside of Terraform. 
In this case, from AWS.

we will fetch Availability zones from AWS, and replace the hard coded value in the subnet's availability_zone section.

```
        # Get list of availability zones
        data "aws_availability_zones" "available" {
        state = "available"
        }
```
We will need to introduce a count argument in the subnet block to make use of this new data resource, : Something like this.

```
    # Create public subnet1
    resource "aws_subnet" "public" { 
        count                   = 2
        vpc_id                  = aws_vpc.main.id
        cidr_block              = "172.16.1.0/24"
        map_public_ip_on_launch = true
        availability_zone       = data.aws_availability_zones.available.names[count.index]

    }

```

```
    # Create public subnet1
    resource "aws_subnet" "public" { 
        count                   = 2
        vpc_id                  = aws_vpc.main.id
        cidr_block              = cidrsubnet(var.vpc_cidr, 4 , count.index)
        map_public_ip_on_launch = true
        availability_zone       = data.aws_availability_zones.available.names[count.index]

    }

```
## Let us quickly understand what is going on here.

The count tells us that we need 2 subnets. 
Therefore, Terraform will invoke a loop to create 2 subnets.
The data resource will return a list object that contains a list of AZs. 
Internally, Terraform will receive the data like this

  ```["us-east-1a", "us-east-1b"]```

Each of them is an index, the first one is index 0, while the other is index 1. 
If the data returned had more than 2 records, then the index numbers would continue to increment.

Therefore, each time Terraform goes into a loop to create a subnet, it must be created in the retrieved AZ from the list. 
Each loop will need the index number to determine what AZ the subnet will be created. 
That is why we have data.aws_availability_zones.available.names[count.index] as the value for availability_zone. 
When the first loop runs, the first index will be 0, therefore the AZ will be *us-east-1a*. 
The pattern will repeat for the second loop.

But we still have a problem. 
If we run Terraform with this configuration, 
it may succeed for the first time, 
but by the time it goes into the second loop, 
it will fail because we still have cidr_block hard coded. 
The same cidr_block cannot be created twice within the same VPC. 
So, we have a little more work to do.

## Let's make cidr_block dynamic.

We will introduce a function cidrsubnet() to make this happen. 
It accepts 3 parameters. Let us use it first by updating the configuration, 
then we will explore its internals.

```
    # Create public subnet1
    resource "aws_subnet" "public" { 
        count                   = 2
        vpc_id                  = aws_vpc.main.id
        cidr_block              = cidrsubnet(var.vpc_cidr, 4 , count.index)
        map_public_ip_on_launch = true
        availability_zone       = data.aws_availability_zones.available.names[count.index]

    }
```
---

A closer look at *cidrsubnet* - this function works like an algorithm to dynamically create a subnet CIDR per AZ. 

Regardless of the number of subnets created, it takes care of the cidr value per subnet.

Its parameters are cidrsubnet
(prefix, newbits, netnum)

The prefix parameter must be given in CIDR notation, same as for VPC.

The newbits parameter is the number of additional bits with which to extend the prefix. 

For example, if given a prefix ending with /16 and a newbits value of 4, the resulting subnet address will have length /20

The *netnum* parameter is a whole number that can be represented as a binary integer with no more than newbits binary digits, which will be used to populate the additional bits added to the prefix.

You can experiment how this works by entering the 
```
terraform console
```
and keep changing the figures to see the output.

On the terminal, run terraform console
type 

```
cidrsubnet("172.16.0.0/16", 4, 0)
```
Hit 

```
enter
```

See the output

Keep change the numbers and see what happens.
To get out of the console, type 

```
exit
```

---

## The final problem to solve is removing hard coded count value.

If we cannot hard code a value we want, then we will need a way to dynamically provide the value based on some input. 

Since the data resource returns all the AZs within a region, it makes sense to count the number of AZs returned and pass that number to the count argument.

To do this, we can introuduce length() function, which basically determines the length of a given list, map, or string.

Since 

```
data.aws_availability_zones.available.names
``` 

returns a list like 

```
["us-east-1a", "us-east-1b", "us-east-1c"]
```

 we can pass it into a lenght function and get number of the AZs.

```
length(["us-east-1a", "us-east-1b", "us-east-1c"])
```

Open up terraform console and try it


---
can simply update the public subnet block like this
```
# Create public subnet1
    resource "aws_subnet" "public" { 
        count                   = length(data.aws_availability_zones.available.names)
        vpc_id                  = aws_vpc.main.id
        cidr_block              = cidrsubnet(var.vpc_cidr, 4 , count.index)
        map_public_ip_on_launch = true
        availability_zone       = data.aws_availability_zones.available.names[count.index]

    }
```


```
# Get list of availability zones
data "aws_availability_zones" "available" {
state = "available"
}

variable "region" {
      default = "us-east-1"
}

variable "vpc_cidr" {
    default = "172.16.0.0/16"
}

variable "enable_dns_support" {
    default = "true"
}

variable "enable_dns_hostnames" {
    default ="true" 
}

variable "enable_classiclink" {
    default = "false"
}

variable "enable_classiclink_dns_support" {
    default = "false"
}

  variable "preferred_number_of_public_subnets" {
      default = 2
}

provider "aws" {
  region = var.region
}

# Create VPC
resource "aws_vpc" "main" {
  cidr_block                     = var.vpc_cidr
  enable_dns_support             = var.enable_dns_support 
  enable_dns_hostnames           = var.enable_dns_support
  enable_classiclink             = var.enable_classiclink
  enable_classiclink_dns_support = var.enable_classiclink

}


# Create public subnets
resource "aws_subnet" "public" {
  count  = var.preferred_number_of_public_subnets == null ? length(data.aws_availability_zones.available.names) : var.preferred_number_of_public_subnets   
  vpc_id = aws_vpc.main.id
  cidr_block              = cidrsubnet(var.vpc_cidr, 4 , count.index)
  map_public_ip_on_launch = true
  availability_zone       = data.aws_availability_zones.available.names[count.index]

}

```
---
---
# Variables and tvars

## Introducing variables.tf & terraform.tfvars

Instead of havng a long lisf of variables in main.tf file, we can actually make our code a lot more readable and better structured by moving out some parts of the configuration content to other files.

* We will put all variable declarations in a separate file.

* And provide non default values to each of them

1. Create a new file and name it variables.tf

1. Copy all the variable declarations into the new file.

1. Create another file, name it terraform.tfvars
Set values for each of the variables.

## main.tf
```
# Get list of availability zones
data "aws_availability_zones" "available" {
state = "available"
}

provider "aws" {
  region = var.region
}

# Create VPC
resource "aws_vpc" "main" {
  cidr_block                     = var.vpc_cidr
  enable_dns_support             = var.enable_dns_support 
  enable_dns_hostnames           = var.enable_dns_support

}

# Create public subnets
resource "aws_subnet" "public" {
  count  = var.preferred_number_of_public_subnets == null ? length(data.aws_availability_zones.available.names) : var.preferred_number_of_public_subnets   
  vpc_id = aws_vpc.main.id
  cidr_block              = cidrsubnet(var.vpc_cidr, 4 , count.index)
  map_public_ip_on_launch = true
  availability_zone       = data.aws_availability_zones.available.names[count.index]
}

```

# variables.tf
```
variable "region" {
      default = "us-east-1"
}

variable "vpc_cidr" {
    default = "172.16.0.0/16"
}

variable "enable_dns_support" {
    default = "true"
}

variable "enable_dns_hostnames" {
    default ="true" 
}

variable "enable_classiclink" {
    default = "false"
}

variable "enable_classiclink_dns_support" {
    default = "false"
}

  variable "preferred_number_of_public_subnets" {
      default = null
}

```
# terraform.tfvars
```
region = "us-east-1"

vpc_cidr = "172.16.0.0/16" 

enable_dns_support = "true" 

enable_dns_hostnames = "true"  

enable_classiclink = "false" 

enable_classiclink_dns_support = "false" 

preferred_number_of_public_subnets = 2

```

![error](images/error.jpg)

![validate](images/validate.jpg)

![plan](images/plan.jpg)

# everything went fine...

















