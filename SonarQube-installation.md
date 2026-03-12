Here is a **clean and professional README.md** for installing **SonarQube** on Linux using **PostgreSQL** and **OpenJDK**.

---

# SonarQube Installation Guide

This guide explains how to install and configure **SonarQube** on a Linux server using **PostgreSQL** as the database.

---

# Prerequisites

Before installing SonarQube, make sure the following packages are installed:

* Java 17 (OpenJDK)
* PostgreSQL
* unzip
* wget

---

# 1. Install Java and PostgreSQL

```bash
apt update -y
apt install openjdk-17-jdk -y
apt install postgresql -y
```

Start PostgreSQL service:

```bash
systemctl start postgresql
systemctl enable postgresql
```

---

# 2. Configure PostgreSQL Database

Switch to PostgreSQL user and open the database shell:

```bash
sudo -u postgres psql
```

Create database and user for SonarQube:

```sql
CREATE USER linux PASSWORD 'redhat';
CREATE DATABASE sonarqube;
GRANT ALL PRIVILEGES ON DATABASE sonarqube TO linux;
\c sonarqube;
GRANT ALL PRIVILEGES ON SCHEMA public TO linux;
\q
```

---

# 3. Configure Linux System Limits

SonarQube requires higher system limits.

Run the following commands:

```bash
sysctl -w vm.max_map_count=524288
sysctl -w fs.file-max=131072
ulimit -n 131072
ulimit -u 8192
```

---

# 4. Download and Install SonarQube

Download SonarQube:

```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-25.5.0.107428.zip
```

Install unzip and extract:

```bash
apt install unzip -y
unzip sonarqube-25.5.0.107428.zip
```

Move the extracted folder to `/opt`:

```bash
mv sonarqube-25.5.0.107428 /opt/sonar
cd /opt/sonar
```

---

# 5. Configure SonarQube Database Connection

Edit the configuration file:

```bash
vim conf/sonar.properties
```

Add or modify the following properties:

```
sonar.jdbc.username=linux
sonar.jdbc.password=redhat
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
```

Save and exit the file.

---

# 6. Create SonarQube User

For security reasons, SonarQube should not run as root.

Create a dedicated user:

```bash
useradd sonar -m
chown sonar:sonar -R /opt/sonar
```

Switch to the sonar user:

```bash
su sonar
```

---

# 7. Start SonarQube Server

Navigate to the SonarQube binary directory:

```bash
cd /opt/sonar/bin/linux-x86-64
```

Start SonarQube:

```bash
./sonar.sh start
```

Check the status:

```bash
./sonar.sh status
```

---

# 8. Access SonarQube Dashboard

Open your browser and access:

```
http://<SERVER-IP>:9000
```

Default login credentials:

```
Username: admin
Password: admin
```

You will be prompted to change the password after the first login.

---

# 9. Generate SonarQube Token

Example token:

```
sqp_3ea721be647ce5845122fff97dcd288bccdbf856
```

This token can be used for CI/CD integrations such as Jenkins or GitHub Actions.

---

# Architecture Overview

```
Developer Code
       │
       ▼
   Sonar Scanner
       │
       ▼
   SonarQube Server
       │
       ▼
   PostgreSQL Database
```
---
