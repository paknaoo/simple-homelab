# Docker Host (Ubuntu Server)

## Overview

This Ubuntu Server (**192.168.50.30**) is used as a **Docker host** in the homelab.

It is dedicated to containerized workloads, container management, and basic security monitoring using Wazuh.

---

## Ubuntu Installation

Ubuntu Server was installed as a virtual machine in VMware Workstation.

The following steps were completed:

* Ubuntu Server installation
* Static IP configuration
* SSH installation and configuration

---

## Remote Administration

The server is managed remotely from the Kali Linux machine using SSH:

```bash
ssh adam@192.168.50.30
```

All configuration steps were performed remotely through the SSH session.

---

## Docker Installation

Docker Engine was installed using the official Docker documentation:

https://docs.docker.com/engine/install/ubuntu/

### Add Docker Repository

```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

```bash
sudo apt update
```

### Install Docker

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Verify Installation

```bash
sudo docker run hello-world
```

---

## Portainer Installation

Portainer was deployed to provide a web-based interface for Docker management.

### Create Volume

```bash
sudo docker volume create portainer_data
```

### Run Container

```bash
docker run -d \
-p 8000:8000 \
-p 9443:9443 \
--name portainer \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data \
portainer/portainer-ce:sts
```

### Verify

```bash
docker ps
```

---

## Accessing Portainer

```
https://192.168.50.30:9443
```

---

## Container Deployment

Containers were deployed using Portainer and pulled from **Docker Hub**.

### Test Containers

* Nginx container
* Custom Docker networks

---

## Vulnerable Applications

The following intentionally vulnerable applications were deployed:

* **bWAPP**
* **DVWA (vulnerables/web-dvwa)**
* **WebGoat**

### Purpose

These applications are used to:

* practice vulnerability scanning using **Nmap**
* test web application security
* simulate real-world vulnerable environments
* perform testing from the Kali Linux machine

---

## Wazuh Agent Installation

The Wazuh agent was installed to monitor the Docker host and container activity.

### Add Repository

```bash
sudo apt-get install gnupg apt-transport-https

curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | \
gpg --no-default-keyring \
--keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import

sudo chmod 644 /usr/share/keyrings/wazuh.gpg

echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | \
sudo tee -a /etc/apt/sources.list.d/wazuh.list

sudo apt-get update
```

### Install Agent

```bash
WAZUH_MANAGER="<MANAGER_IP>" sudo apt-get install wazuh-agent
```

---

## Docker Monitoring with Wazuh

### Step 1 – Python Environment

```bash
python3 -m venv /var/ossec/venv
source /var/ossec/venv/bin/activate
pip install --upgrade pip
```

Edit listener script:

```bash
sudo nano /var/ossec/wodles/docker/DockerListener
```

Change shebang:

```bash
#!/var/ossec/venv/bin/python3
```

Install dependencies:

```bash
pip3 install docker==7.1.0 urllib3==1.26.20 requests==2.32.2 --break-system-packages
```

---

### Step 2 – Enable Docker Listener

Edit config:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Add:

```xml
<wodle name="docker-listener">
  <disabled>no</disabled>
</wodle>
```

Restart agent:

```bash
sudo systemctl restart wazuh-agent
```

---

## Purpose

This Docker host is used to:

* run containerized applications
* manage containers using Portainer
* simulate vulnerable environments
* perform security testing from Kali Linux
* monitor system and container activity using Wazuh

This setup combines **containerization and security monitoring** in a single lab environment.
