# AWS CLI Installation on Ubuntu (Step-by-Step Guide)

This document explains how to **download, install, and configure AWS CLI v2 on an Ubuntu system**. AWS CLI is required to manage AWS services from the command line and is widely used in DevOps and cloud projects.

---

## Prerequisites

- Ubuntu 20.04 / 22.04 / 24.04
- User with `sudo` privileges
- Active internet connection

---

## Step 1: Update the System Packages

```bash
sudo apt update
```

**Explanation:**
Updates the local package index so the system is aware of the latest available packages.

---

## Step 2: Install Required Dependencies

```bash
sudo apt install curl unzip -y
```

**Explanation:**

- `curl` is used to download files from the internet
- `unzip` is required to extract the AWS CLI installer

---

## Step 3: Download AWS CLI v2 Installer

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

**Explanation:**
Downloads the official AWS CLI v2 installer package for 64-bit Linux systems.

---

## Step 4: Extract the Installer

```bash
unzip awscliv2.zip
```

**Explanation:**
Extracts the AWS CLI installation files into a directory named `aws`.

---

## Step 5: Install AWS CLI v2

```bash
sudo ./aws/install
```

**Explanation:**
Installs AWS CLI v2 on the system. The `aws` command will be available globally.

---

## Step 6: Verify AWS CLI Installation

```bash
aws --version
```

**Explanation:**
Confirms that AWS CLI is installed successfully. Expected output includes:

```
aws-cli/2.x.x Python/3.x Linux/...
```

---

## Step 7: Configure AWS CLI

```bash
aws configure
```

**Explanation:**
You will be prompted to enter:

- AWS Access Key ID
- AWS Secret Access Key
- Default region (example: `us-east-1`)
- Default output format (`json` recommended)

This step allows AWS CLI to authenticate and interact with your AWS account.

---

## Step 8: Verify AWS Configuration

```bash
aws sts get-caller-identity
```

**Explanation:**
Validates that AWS CLI is properly configured and can access your AWS account.

---

## Step 9: Clean Up Installer Files (Optional)

```bash
rm -rf aws awscliv2.zip
```

**Explanation:**
Removes temporary installation files to keep the system clean.

---

## 🎉 Installation Complete

AWS CLI v2 is now successfully installed and configured on your Ubuntu system.

---