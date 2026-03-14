# Ubuntu Server

This directory documents the installation and configuration of the **Ubuntu Server** virtual machine used in the homelab.

The Ubuntu machine acts as a simple server used to practice installing and configuring common Linux services.

## System Information

| Parameter  | Value                         |
| ---------- | ----------------------------- |
| OS         | Ubuntu Server                 |
| Role       | Web, Database and File Server |
| IP Address | 192.168.50.10                 |
| Network    | EasyLab (192.168.50.0/24)     |

## Network Configuration

After installation there was an issue with network connectivity.
The problem was resolved by editing the Netplan configuration file:

```bash
/etc/netplan/01-netcfg.yaml
```

This also provided practice with **YAML indentation**, which is required for correct Netplan configuration.

## SSH Server

SSH was installed to allow remote access to the server.

Check SSH status:

```bash
systemctl status ssh
```

Enable SSH at system startup:

```bash
sudo systemctl enable ssh
```

Start SSH service:

```bash
sudo systemctl start ssh
```

Connection test from the Kali Linux machine:

```bash
ssh adam@192.168.50.10
```

The connection was successfully established.

## Web Server

A web server was installed using **Nginx**.

Installation:

```bash
sudo apt install nginx
```

Test:

```
http://192.168.50.10
```

The default Nginx page loaded successfully.

Web root directory:

```bash
/var/www/html
```

## Database Server

MySQL database server was installed.

Installation:

```bash
sudo apt install mysql-server
```

Access to MySQL:

```bash
sudo mysql
```

Optional security hardening (not performed in this lab):

```bash
sudo mysql_secure_installation
```

## File Server (Samba)

Samba was installed to provide a simple file share inside the lab network.

Installation:

```bash
sudo apt install samba
```

Shared directory:

```bash
/srv/share
```

Samba configuration file:

```bash
/etc/samba/smb.conf
```

Network interface configuration:

```bash
interfaces = 127.0.0.1 192.168.50.0/24
```

Share configuration:

```bash
[share]
path = /srv/share
browsable = yes
read only = no
guest ok = yes
```

This allows machines in the lab network to access the shared folder.

## Services Running on This Server

The following services are running on this Ubuntu machine:

| Service | Purpose                     |
| ------- | --------------------------- |
| SSH     | Remote administration       |
| Nginx   | Web server                  |
| MySQL   | Database server             |
| Samba   | File sharing inside the lab |


## Connectivity Tests

Basic connectivity between the router (pfSense), Kali Linux and Ubuntu Server was successfully tested.

### Network Discovery

The network was scanned from the Kali Linux machine using **nmap**.

```bash
nmap 192.168.50.0/24
```

Scan results showed three active hosts:

```
192.168.50.1  - pfSense (gateway)
192.168.50.10 - Ubuntu Server
192.168.50.20 - Kali Linux
```

### Samba Share Test

The Samba server running on Ubuntu was tested from the Kali machine.

List available shares:

```bash
smbclient -L //192.168.50.10
```

Connect to the shared folder:

```bash
smbclient //192.168.50.10/share
```

### File Operations

After connecting to the share, basic file operations were tested:

* creating files
* creating directories
* verifying access permissions

These tests confirmed that the Samba share is accessible from other machines in the lab network.

