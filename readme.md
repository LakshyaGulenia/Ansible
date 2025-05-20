# 🛠️ Ansible Overview & Setup Guide

## 📌 What is Ansible?

Ansible is an **automation platform** used for:

- 🔧 Configuration Management  
- 🚀 Application Deployment & CI/CD  
- ☁️ Provisioning Management  
- 🌐 Network Automation  

Ansible works by taking **YAML playbooks** and converting them into Python code that is executed on the **managed nodes**.

> ✅ **Note:** The only prerequisite on managed nodes is **Python** (usually pre-installed on most systems).

---

## 🔁 Terraform vs Ansible

| Feature             | Terraform                           | Ansible                                  |
|---------------------|-------------------------------------|-------------------------------------------|
| Primary Focus       | Infrastructure as Code (IaC)        | Configuration + Provisioning + CI/CD + More |
| Language            | HCL (HashiCorp Configuration Language) | YAML (converted to Python)               |
| Speed of Updates    | Faster, as it's focused on IaC      | Slower in provisioning-related features   |
| Use Case            | Best for Provisioning/IaC           | Good for multi-purpose automation         |

> ✅ **Recommendation:**  
> For pure provisioning/IaC, **Terraform** is preferred due to its focus and faster updates.  
> For broader automation needs (including config & deploy), **Ansible** is more versatile.

---

## 🧪 Ansible Installation on Ubuntu

### 🧱 Install using `apt` (recommended for simplicity):

```bash
sudo apt update
sudo apt install python3-pip
sudo apt install ansible

### 🧱 copy pem key to remote from local
scp -i ansible-key.pem ansible-key.pem ubuntu@13.126.156.228:/home/ubuntu/

# SSH Access Setup for EC2 and Azure VMs

This guide explains how to configure SSH access to EC2 instances (AWS) and Azure VMs, focusing on enabling key-based login for EC2 and password login for Azure VMs.

---

## EC2 Instances (AWS)

### Goal:
- Disable password login
- Enable SSH key-based authentication only

### Steps:

1. **Copy SSH Key to EC2 Instance**

```bash
ssh-copy-id -f "-o IdentityFile <PATH_TO_PEM_FILE>" ubuntu@<INSTANCE_PUBLIC_IP>

If you get errors while copying the key, try:
eval "$(ssh-agent -s)"
chmod 400 ~/my-work.pem
ssh-add ~/my-work.pem
ssh-copy-id -f "-o IdentityFile <PATH_TO_PEM_FILE>" ubuntu@<INSTANCE_PUBLIC_IP>
Connect directly without PEM file
ssh ubuntu@<INSTANCE_PUBLIC_IP>

Azure VMs
Goal:
Allow password authentication

Enable SSH key login optionally

Steps:
Edit SSH configuration on the worker node
If using AWS EC2, config file is:
vim /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
If not using EC2 (e.g., Azure VM), edit:
vim /etc/ssh/sshd_config
Update SSH configuration

Find the line:PasswordAuthentication no
and change it to:PasswordAuthentication yes
Restart SSH service
sudo systemctl restart ssh

Set a new password for the user on the worker node
sudo passwd ubuntu
From the master node, copy your SSH public key to the worker node
ssh-copy-id ubuntu@<IP_ADDRESS>
Connect to the worker node
ssh ubuntu@<IP_ADDRESS>

Notes
For EC2, PEM file is required initially to authenticate.

For Azure VMs, password authentication must be enabled explicitly.

Always secure your private keys and limit password login when possible.



Ad Hoc Commands-
used to create empty file--
ansible all -i inventory.ini -m file -a "dest=/home/ubuntu/adhoc.txt mode=0644 owner=ubuntu group=ubuntu state=touch"
used to create directory
ansible all -i inventory.ini -m file -a"dest=/home/ubuntu/new mode=755 owner=ubuntu group=ubuntu state=directory"
used to del directory
ansible all -i inventory.ini -m file -a"dest=/home/ubuntu/new state=absent"
used to copy file from master to slave
ansible all -i inventory.ini -m copy -a "src=/home/ubuntu/file.txt dest=/home/ubuntu/file.txt mode=0644 owner=ubuntu group=ubuntu"
used to update linux
ansible all -i inventory.ini -m apt -a "update_cache=yes" --become --- used become to get root priv
