## Docker Environment

A second Ubuntu Server was installed in the lab to practice **containerization with Docker** and basic container management.

### Ubuntu Installation

Ubuntu Server was downloaded and installed as a virtual machine.

The following steps were completed successfully:

* Ubuntu Server installation
* Static IP configuration
* SSH installation and configuration

### Remote Administration

The server was accessed remotely from the Kali Linux machine using SSH:

```bash
ssh adam@192.168.50.20
```

All Docker installation steps were performed remotely through the SSH session.

---

## Docker Installation

Docker Engine was installed following the official Docker documentation:

https://docs.docker.com/engine/install/ubuntu/

### Add Docker Repository

Add Docker's official GPG key:

```bash
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Add the Docker repository to APT sources:

```bash
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

Update package list:

```bash
sudo apt update
```

### Install Docker Packages

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Verify Docker Installation

Docker installation was verified by running the test container:

```bash
sudo docker run hello-world
```

The container executed successfully, confirming that Docker was installed correctly.

---

## Portainer Installation

Portainer was installed to provide a **web-based management interface for Docker containers**.

### Create Portainer Data Volume

```bash
sudo docker volume create portainer_data
```

### Run the Portainer Container

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

### Verify Container Status

```bash
docker ps
```

---

## Accessing Portainer

The Portainer web interface can be accessed from a web browser:

```
https://192.168.50.20:9443
```

(Replace the IP address with the address of the server running Portainer.)

---

## Container Testing

Portainer was used to perform basic container management tasks:

* creating a new **Docker container**
* deploying an **Nginx container**
* creating a **new Docker network**
* managing containers through the **Portainer GUI**

These tests confirmed that the Docker environment is functioning correctly inside the lab.

