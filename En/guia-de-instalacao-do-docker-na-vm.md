# 🐳 Docker Installation Guide for Ubuntu

This guide provides an automated script to install **Docker Engine** on **Ubuntu Linux** systems. The script handles dependency installation, configuration of Docker's official repository, and adding the user to the `docker` group.

---

## 📄 Prerequisites

* **Ubuntu 20.04+** operating system
* **Superuser (sudo)** access
* Internet connection

---

## 📥 Step-by-Step Instructions

### 1. Download the script

Create a file called `install-docker.sh`:

```bash
nano install-docker.sh
```

Paste the following content into the file:

```bash
#!/bin/bash

set -e

echo "🔄 Updating system packages..."
sudo apt update && sudo apt upgrade -y

echo "🐳 Installing Docker dependencies..."
sudo apt install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

echo "🔐 Adding Docker's official GPG key..."
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo "📦 Adding Docker repository..."
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

echo "🔄 Updating packages again to include Docker repository..."
sudo apt update

echo "📥 Installing Docker Engine..."
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

echo "✅ Enabling and starting Docker service..."
sudo systemctl enable docker
sudo systemctl start docker

echo "👤 Adding your user to the docker group..."
sudo usermod -aG docker $USER

echo "🚀 Docker successfully installed! Log out and log back in or restart your session to use Docker without sudo."
```

### 2. Grant execution permission

```bash
chmod +x install-docker.sh
```

### 3. Run the script

```bash
./install-docker.sh
```

---

## ✅ Verifying the Installation

After restarting your session (log out/log in):

```bash
docker --version
```

You should see output similar to:

```
Docker version 24.0.x, build xxxxx
```

---

## 🛠️ Possible Adjustments

If you don't want to restart your session, run:

```bash
newgrp docker
```

This will immediately apply the `docker` group to your current terminal session.

---

## 📚 References

* [Official Docker Documentation](https://docs.docker.com/engine/install/ubuntu/)