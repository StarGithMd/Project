
#########################################################################################################################
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ GUVI Assignment 17 Task -1 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#########################################################################################################################

### Terraform_Task -1
https://docs.google.com/document/d/1rNQWkSvWAdo5TKPvqjZUT__qidven4yjQzX4QKwMX6s/edit?usp=sharing

#### Techstacks needs to be used : 
   - AWS EBS
   - AWS EC2

#### How do I submit my work?
   - Push all your work files to GitHub (O/P screenshot images must).
   - Submit your URLs in the portal.

#### Terms and Conditions?
   - You agree to not share this confidential document with anyone. 
   - You agree to open-source your code (it may even look good on your profile!). Do not mention our company’s name anywhere in the code.
   - We will never use your source code under any circumstances for any commercial purposes; this is just a basic assessment task. 

   - NOTE: Any violation of Terms and conditions is strictly prohibited. You are bound to adhere to it.

#### Task Description:
- 01_Q. Launch Linux EC2 instances in two regions using a single Terraform file.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Activity GUVI Assignment 17 Task -1  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To setting it up Terraform on ubuntu, create projects and manage users is a core skill for DevOps. Let’s walk through the essentials step by step. Afterward, push the project files to a GitHub repository.

1.	Update System Packages:
sudo apt update && sudo apt upgrade -y

2.	Install Prerequisites:
sudo apt install -y gnupg software-properties-common curl

3.	Add HashiCorp's GPG key and repository:
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg]
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \ sudo tee
/etc/apt/sources.list.d/hashicorp.list

4.	Install Terraform:
sudo apt update
sudo apt install terraform
5. Verify the installation:
terraform -version

6.	Set up a working directory and write config:
mkdir ~/terraform-project && cd ~/terraform-project
nano main.tf
Add your provider and resource blocks (example for AWS):
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0abcdef1234567890"
  instance_type = "t2.micro"
}
7.	Initialize, plan, and apply:
terraform init      # downloads providers/modules
terraform validate  # checks syntax
terraform plan       # shows what will be created/changed
terraform apply       # applies the changes (type "yes" to confirm)

8.	Single Terraform configuration that launches Linux EC2 instances in two AWS regions using provider aliases.
Vi main.tf
terraform {
  required_version = ">= 1.5.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

# ---------------------------
# Providers for two regions
# ---------------------------
provider "aws" {
  alias  = "region1"
  region = "us-east-1"
}

provider "aws" {
  alias  = "region2"
  region = "eu-west-1"
}

# ---------------------------
# Latest Amazon Linux 2023 AMI - Region 1
# ---------------------------
data "aws_ami" "al2023_region1" {
  provider    = aws.region1
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["al2023-ami-*-x86_64"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }
}

# ---------------------------
# Latest Amazon Linux 2023 AMI - Region 2
# ---------------------------
data "aws_ami" "al2023_region2" {
  provider    = aws.region2
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["al2023-ami-*-x86_64"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }
}

# ---------------------------
# EC2 Instance - Region 1 (us-east-1)
# ---------------------------
resource "aws_instance" "instance_region1" {
  provider      = aws.region1
  ami           = data.aws_ami.al2023_region1.id
  instance_type = var.instance_type

  tags = {
    Name = "instance-us-east-1"
  }
}

# ---------------------------
# EC2 Instance - Region 2 (eu-west-1)
# ---------------------------
resource "aws_instance" "instance_region2" {
  provider      = aws.region2
  ami           = data.aws_ami.al2023_region2.id
  instance_type = var.instance_type

  tags = {
    Name = "instance-eu-west-1"
  }
}

# ---------------------------
# Variables
# ---------------------------
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

# ---------------------------
# Outputs
# ---------------------------
output "region1_instance_id" {
  value = aws_instance.instance_region1.id
}

output "region1_public_ip" {
  value = aws_instance.instance_region1.public_ip
}

output "region2_instance_id" {
  value = aws_instance.instance_region2.id
}

output "region2_public_ip" {
  value = aws_instance.instance_region2.public_ip
}

9.	Deployment steps:
# 1. Set up AWS credentials (if not already configured)
aws configure

# 2. Initialize Terraform (downloads AWS provider)
terraform init

# 3. Validate syntax
terraform validate

# 4. Preview the changes
terraform plan

# 5. Apply — creates instances in both regions
terraform apply

md_rustam@DESKTOP-CPK0PUB:~/Project$ git add .; git commit -m "17_Terraform_Task_1"; git push
[main af9ba5e] 17_Terraform_Task_1
 2 files changed, 222 insertions(+)
 create mode 100644 17_Terraform_Task_1/Terraform_Task_1.md
 create mode 100644 17_Terraform_Task_1/terraform_Task1.jpg
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 1.51 MiB | 1.82 MiB/s, done.
Total 5 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/StarGithMd/Project.git
   1bf6676..af9ba5e  main -> main










