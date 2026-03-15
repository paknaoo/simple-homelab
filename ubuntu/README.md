## Ubuntu Servers in the Lab

The Ubuntu machine acts as a simple server used to practice installing and configuring common Linux services.

Two Ubuntu servers are used in this homelab.

| Server          | IP Address    | Role                                  |
| --------------- | ------------- | ------------------------------------- |
| Ubuntu Desktop  | 192.168.50.10 | Web, database and file server         |
| Ubuntu Server   | 192.168.50.30 | Docker host and container environment |

The first server is used to practice traditional Linux services, while the second server is used for container-based workloads with Docker and Portainer.


## Network Configuration

After installation there was an issue with network connectivity.
The problem was resolved by editing the Netplan configuration file:

```bash
/etc/netplan/01-netcfg.yaml
```

This also provided practice with **YAML indentation**, which is required for correct Netplan configuration.

## Lessons Learned

During the setup and testing of the Ubuntu servers in this lab several practical skills were learned:

* Understanding how **Netplan** manages network configuration in Ubuntu.
* Importance of correct **YAML indentation** when editing configuration files.
* Managing Linux services using **systemctl** (start, enable, status).
* Installing and configuring common Linux server services.
* Basic configuration of a **web server (Nginx)**.
* Installing and accessing a **MySQL database server**.
* Setting up a **Samba file share** for local network access.
* Testing connectivity between machines in a small lab network.
* Using **nmap** for basic network discovery and host identification.
* Accessing and testing SMB shares using **smbclient**.
* Installing and configuring **Docker Engine** on Ubuntu.
* Adding external repositories and **GPG keys** for secure package installation.
* Running and testing Docker containers.
* Deploying and managing containers using **Portainer**.
* Creating Docker volumes and networks for containerized services.







