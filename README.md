# AWS Instance Terraform Module 

A Terraform module which allows creation and management of AWS EC2 instances.

This type of resource is supported :
- [EC2- aws_instance](https://www.terraform.io/docs/providers/aws/r/instance.html)

# Features

The goal of this module is to give a standard way of generating and managing certificates issued by Amazon.
The module supports :

- Domain Name
- Subject Alternatives Names
- Validation Method
- Tags

## Terraform versions

Support of Terraform 0.12 is not yet implemented. (WIP)

If you are using Terraform 0.11 you can use versions `v1.*`.

## Usage

Simple EC2 Instance creation example: 

```hcl
data "aws_ami" "ami" {
  most_recent = true

  filter {
    name   = "name"
    values = ["RHEL-7.4_HVM_GA-20170808-x86_64-2-Hourly2-GP2"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  owners = ["309956199498"] # Red Hat
}

module "aws_instance" {
  source = "app.terraform.io/<ORG_NAME>/instance/aws"
  ami    = "${data.aws_ami.ami.id}"

  instance_tags = {
    "Name" = "whatever"
  }

  vm_count               = "1"
  vpc_security_group_ids = ["123456789"]
  subnet_id              = "subnet-ahhbbg12"
  key_name               = "mykey"
}
```

## Authors

* **Nicolas Ehrman** - *Initial work* - [Hashicorp](https://www.hashicorp.com)



