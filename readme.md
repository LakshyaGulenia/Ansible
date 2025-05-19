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
