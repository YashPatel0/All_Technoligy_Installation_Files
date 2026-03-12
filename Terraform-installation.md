# Install Terraform on Ubuntu (AWS EC2)

This guide explains how to install **Terraform** on a Linux-based **Ubuntu system**, such as an AWS EC2 instance.

---

## Prerequisites

- AWS EC2 instance with **Ubuntu 20.04 / 22.04**
- SSH access to the instance
- Internet access (outbound HTTPS – port 443)

---

## Installation Steps

### Step 1: Create an EC2 Instance

- Launch an Ubuntu-based EC2 instance from AWS Console
- Attach IAM polict to EC2 instance (AdministratorAccess)
- Configure key pair and security group (allow SSH – port 22)

---

### Step 2: SSH into the Instance

```bash
ssh ubuntu@<EC2_PUBLIC_IP>
```

### Step 3 Update the System

```bash
Update the System
```

### Step 4 Install Terraform

- Run the following commands inside the instance:

```bash
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform -y

```

### Step 5: Verify Installation

```bash
terraform version
```