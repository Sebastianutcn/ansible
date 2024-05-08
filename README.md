# Terraform provisioning and Ansible configuration
- Provisioned an AWS infrastructure using Terraform with VPCs and 3 EC2 instances. 
- Install and start nginx server on each EC2 instance and allowing access to TCP port 80. 


## **Terraform files:**
1. [`main.tf`](https://github.com/Sebastianutcn/ansible-terraform/blob/main/main.tf) is used to create the EC2 instance and the VPC with: subnets, internet gateway, route table and security groups 
2. [`output.tf`](https://github.com/Sebastianutcn/ansible-terraform/blob/main/output.tf) is used to show the public IP of the instances.
3. [`variables.tf`](https://github.com/Sebastianutcn/ansible-terraform/blob/main/variables.tf) is used to define some variables used in `main.tf`.
4. [`inventory.tf`](https://github.com/Sebastianutcn/ansible-terraform/blob/main/inventory.tf) is used to provision a sensitive local file with a private key and generates an Ansible inventory file, utilizing AWS instance public IP addresses and a specified file path for SSH authentication.

## Installation
- Terraform command to initialize the project
```
terraform init
```
* Terraform command to plan the changes and to check again the resources that were added, changed or deleted
```
terraform plan -out plan.out
```
- Terraform command to apply the changes
```
terraform apply plan.out --auto-approve
```

## **Ansible files:**
1. `playbook.yml` has a play for a host group named [aws_ec2], where are tasks defined to install Nginx, allow access on port 80 and start the Nginx server.
2. `inventory.ini` is used to store hosts.
3. `ansible.cfg` is used as a configuration file for ansible, the inventory file is defined and host_key_checking is set to 'false'.

## Execute tasks
- Ansible command to execute the defined tasks on the specified hosts
```
ansible-playbook playbook.yml
```
