# Docker Installation on Ubuntu (Step-by-Step Guide)

---

## Prerequisites

- Ubuntu 20.04 / 22.04 / 24.04
- A user with `sudo` privileges
- Active internet connection

---

## Step 1: Update the Package Index

```bash
sudo apt-get update
```

**Explanation:**
This updates the local package index so your system knows about the latest available packages.

---

## Step 2: Install Required Dependencies

```bash
sudo apt-get install ca-certificates curl -y
```

**Explanation:**

- `ca-certificates`: Allows secure HTTPS connections
- `curl`: Used to download Docker’s GPG key

---

## Step 3: Create Directory for APT Keyrings

```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

**Explanation:**
Creates a secure directory to store trusted GPG keys for external repositories.

---

## Step 4: Add Docker’s Official GPG Key

```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

**Explanation:**

- Downloads Docker’s official signing key
- Sets read permissions so APT can verify Docker packages

---

## Step 5: Add Docker Repository to APT Sources

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo \"${UBUNTU_CODENAME:-$VERSION_CODENAME}\") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

**Explanation:**
Adds the official Docker repository so Docker packages can be installed and updated via APT.

---

## Step 6: Update Package Index Again

```bash
sudo apt-get update
```

**Explanation:**
Reloads the package list including the newly added Docker repository.

---

## Step 7: Install Docker Engine and Components

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

**Explanation:**

- `docker-ce`: Docker Engine
- `docker-ce-cli`: Docker command-line tool
- `containerd.io`: Container runtime
- `docker-buildx-plugin`: Advanced build features
- `docker-compose-plugin`: Docker Compose v2

---

## Step 8: Start Docker Service

```bash
sudo systemctl start docker
```

**Explanation:**
Starts the Docker daemon so containers can run.

---

## Step 9: Enable Docker at System Boot

```bash
sudo systemctl enable docker
```

**Explanation:**
Ensures Docker automatically starts after a system reboot.

---

## Step 10: Run Docker Without sudo (Recommended)

```bash
sudo usermod -aG docker $USER
newgrp docker
```

**Explanation:**
Adds your user to the Docker group, allowing Docker commands without `sudo`.

> Note: If `newgrp` doesn’t work, log out and log back in.

---

## Step 11: Verify Docker Installation

```bash
docker --version
docker compose version
docker run hello-world
```

**Explanation:**

- Confirms Docker is installed
- Confirms Docker Compose v2 is installed
- Runs a test container to verify everything works

---

## 🎉 Installation Complete

Docker is now successfully installed and ready to use on your Ubuntu system.

---