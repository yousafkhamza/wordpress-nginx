# WordPress Provision through Ansible Playbook.
[![Builds](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)
## Description:
A simple wordpress site provision through ansible-playbook. Furthermore, the ansible playbook is installed in complete packages like the lamp. Also, you can create multiple WordPress sites with appending your decision. In addition, the playbook is basically designed for ubuntu 20.04, and it's using Nginx. 

It's just a try for application provision through ansible. Maybe it has bugs with other Debian distributer. So please let me know if you have to face any issues while using this then I will help you to figure out and correct the issue. So, please ping me via linked that would be more helpful to correct if any bugs you got.

## Features:
- Easy to create wordpress sites on ubuntu (with the help of nginx)
- Domain name, wordpress databases, password is appending your descision. you don't needs to edit in core files who used this.
- All the components are installed through the playbook like (Nginx, MySQL, PHP, Wordpress)

## Components and Resources:
- Ubuntu 20.04 (Ansible-Client)
- Nginx (Used webserver)
- PHP and dependencies
- MySQL
- WordPress 5.7 
- Ansible2 (Ansible-Master. Please note that I have used master server is RedHat Distributer "amazon-linux") 

## Pre Requisites:
- In this scenario we have used Master server as Amazon Linux 2 and Client  server as Ubuntu 18.04 LTS with desired ports 22, 80 opened. 
- Master server installed with [Ansible2](https://docs.ansible.com/ansible/2.3/index.html) (For your reference visit [How to install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html))
##### Ansible Modules used:
- [Inventory](https://docs.ansible.com/ansible/2.3/intro_inventory.html) 
- [File](https://docs.ansible.com/ansible/2.3/list_of_files_modules.html)
- [Database](https://docs.ansible.com/ansible/2.3/list_of_database_modules.html)
- [Shell](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/shell_module.html)

## How to Use:
### Method 1
```sh
yum install git -y
amazon-linux-extras ansible2 -y
```
> Please create your client key.pem file and hosts (Inventory) file manually and please copy the same to the working directory which you used. 
```sh
git clone https://github.com/yousafkhamza/wordpress-nginx.git
cd wordpress-nginx
ansible -i hosts all -m ping <========== its just check your master and client connection with your inventory file which you copied or create manually.
ansible-playbook -i hosts main.yml
```

### Method 2
- > Created one Master and Two clients through terraform IaC. Please choose debian distributer when you choose this otherwise it doesn't work 
- > Please note that Remove one client manually if you don't need or please remove one hosts (inventory) entry on hosts file because otherwise the same site will be installed on two client servers. Please see the below link for further details: https://github.com/yousafkhamza/ansible_infra_making_terraform
```sh
 git clone https://github.com/yousafkhamza/ansible_infra_making_terraform.git
 cd ansible_infra_making_terraform/
 chmod +x setup.sh
 sh setup.sh
```
> Please login your ansible master manually with the output public IP which you get.
```sh
ssh -i key.pem ec2-user@public_ip    <============== public IP will be printed after create the script
```
> After login Ansible Master:
```sh
yum install git -y
git clone https://github.com/yousafkhamza/wordpress-nginx.git
cd wordpress-nginx
cp ../key.pem ./
cp ../hosts ./
ansible -i hosts all -f 1 -m ping
ansible-playbook -i hosts main.yml
```

## Sample Screenshot: 
![alt text](https://i.ibb.co/LvZC0nB/sample.png)

### Optional Security Feature:

Here we have used the "variables.vars" file to pass the variables as a plain text, to overcome this we can encrypt the files with a password. [Ansible_vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html) encrypts variables and files so you can protect sensitive content such as passwords or keys rather than leaving it visible as plaintext in playbooks or roles.

To encrypt a file, use the ansible-vault encrypt command.
```sh
ansible-vault encrypt main.yml hosts key.pem
```
To prompt for the password:
```sh
ansible-playbook -i hosts --ask-vault-pass main.yml
```

## If you have using a demo website Please use the site for create localhost loading.
https://hosts.cx/

## Conclusion: 
It's just a try for application provision through ansible. Maybe it has bugs with other Debian distributer. So please let me know if you have to face any issues while using this then I will help you to figure out and correct the issue. So, please ping me via linked that would be more helpful to correct if any bugs you got.

### ⚙️ Connect with Me

<p align="center">
<a href="mailto:yousaf.k.hamza@gmail.com"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/yousafkhamza"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a> 
<a href="https://www.instagram.com/yousafkhamza"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a>
<a href="https://wa.me/%2B917736720639?text=This%20message%20from%20GitHub."><img src="https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white"/></a>
