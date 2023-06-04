# Launch an EC2 Instance using Terraform
 creating ec2_instance 

# Files
  We'll use the following terraform files:
- main.tf
- output.tf
- provider.tf
- terraform.tfvars
- varaibles.tf
- versions.tf
- .gitignore
  
 # main.tf
 - nresource "aws_instance" "demo_ec2" {
 - ami                    = var.ami_id
 - instance_type          = var.inst_type
 - key_name               = var.key_name
 - vpc_security_group_ids = var.sg_ids
 - subnet_id              = var.subnet_id
 - region                 = var.region
  
  - tags = {
  - Name = "terrform-demo-ec2"
  - Environment = "training"
   - }
  - }

#  output.tf
  - output "demo_ec2_id" {
  - description = "Print the ID of EC2 Instance"
  - value       = aws_instance.demo_ec2.id
- }

  - output "demo_ec2_private_ip" {
  - description = "Print the Private IP of EC2 Instance"
  - value       = aws_instance.demo_ec2.private_ip
 -}

  - output "demo_ec2_public_ip" {
  - description = "Print the Public IP of EC2 Instance"
  - value       = aws_instance.demo_ec2.public_ip
  -}

# provider.tf
  - provider "aws" {
  - region = var.region
- }

- terraform {
 - backend "s3" {       
    - key            = "terraform.tfstate"
    - region         = "us-east-1"
    - bucket         = "snr-us-east-1-tfstates"    (create bucket before pasting the bucket name)
  
  -}
 -}

# terraform.tfvars
  - ami_id = "ami-0557a15b87f6559cf"
  - inst_type = "t2.micro"
  - key_name = "demokey"
  - sg_ids  = ["sg-02bf6af1a3264efb4"]
  - subnet_id = "subnet-032fb21e1ee472561"
  - region = "us-east-1"

# varaibles.tf
 - variable "ami_id" {}

 - variable "inst_type" {}

 - variable "key_name" {}

 - variable "sg_ids" {}

 - variable "subnet_id" {}

  - variable region {}

# .gitignore.

   - *.terraform*
   - *.tfstate*
   - *.terraform.lock*

# commands used
 - 1. terraform init
      Initializing the backend...
      Initializing provider plugins...    
 - 2. terraform apply
 - 3. terraform destroy
 - 4. terraform init -migrate-state
 - 5. terraform init -reconfigure



