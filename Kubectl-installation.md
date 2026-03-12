# Install and Configure kubectl and AWS CLI (Step-by-Step Guide)

This guide explains how to install **kubectl** (Kubernetes command-line tool) and **AWS CLI v2** on a Linux (Ubuntu) system, with clear explanations for each step. This setup is commonly used for managing Kubernetes clusters, especially Amazon EKS.

---

## Prerequisites

- Ubuntu 20.04 / 22.04 / 24.04
- User with `sudo` privileges
- Active internet connection

---

## Step 1: Download kubectl Binary

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

**Explanation:**

- Downloads the latest stable version of `kubectl`
- `stable.txt` ensures you always get the most recent supported release

---

## Step 2: Install kubectl Binary

```bash
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

**Explanation:**

- Installs `kubectl` system-wide
- Sets correct ownership and permissions
- Makes the command available for all users

---

## Step 3: Verify kubectl Installation

```bash
kubectl version --client
```

**Explanation:**

- Confirms that kubectl is installed correctly
- Displays the client version only (no cluster connection required)

---

## Step 4: Download AWS CLI v2 Installer

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

**Explanation:**

- Downloads the official AWS CLI v2 installer package

---

## Step 5: Install unzip Utility

```bash
sudo apt install unzip -y
```

**Explanation:**

- `unzip` is required to extract the AWS CLI installer files

---

## Step 6: Extract AWS CLI Installer

```bash
unzip awscliv2.zip
```

**Explanation:**

- Extracts the AWS CLI installation directory

---

## Step 7: Install AWS CLI v2

```bash
sudo ./aws/install
```

**Explanation:**

- Installs AWS CLI v2 on the system
- AWS CLI will be available at `/usr/local/bin/aws`

---

## Step 8: Verify AWS CLI Installation

```bash
aws --version
```

**Explanation:**

- Confirms AWS CLI v2 installation
- Expected output includes `aws-cli/2.x.x`

---

## Step 9: Configure AWS CLI

```bash
aws configure
```

**Explanation:**
You will be prompted to enter:

- AWS Access Key ID
- AWS Secret Access Key
- Default region (example: `us-east-1`)
- Output format (json is recommended)

This step allows your system to authenticate with AWS services.

---

## Step 10: (Optional but Recommended) Configure kubectl for EKS

If you are using Amazon EKS, update your kubeconfig:

```bash
aws eks update-kubeconfig --region <region-name> --name <cluster-name>
```

**Explanation:**

- Links kubectl with your EKS cluster
- Downloads cluster credentials into kubeconfig

---

## Step 11: Verify Cluster Access

```bash
kubectl get nodes
```

**Explanation:**

- Confirms kubectl can communicate with the Kubernetes cluster
- Displays worker nodes if access is successful

---

## Step 12: Cleanup Installation Files (Optional)

```bash
rm -rf aws awscliv2.zip kubectl
```

**Explanation:**

- Removes temporary installation files
- Keeps the system clean

---

## 🎉 Installation Complete

You have successfully installed and configured:

- kubectl (Kubernetes CLI)
- AWS CLI v2

Your system is now ready to manage Kubernetes clusters and AWS services.

---