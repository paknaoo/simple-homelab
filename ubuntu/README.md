## Ubuntu Servers in the Lab

The Ubuntu machines in this lab are used to simulate different roles commonly found in real-world environments.

Three Ubuntu systems are used in this homelab.

| Server         | IP Address    | Role                                  |
| -------------- | ------------- | ------------------------------------- |
| Ubuntu Desktop | 192.168.50.10 | Web, database and file server         |
| Ubuntu Server  | 192.168.50.30 | Docker host and container environment |
| Ubuntu Server  | 192.168.50.40 | Wazuh SIEM server                     |

### Roles Overview

* **Ubuntu Desktop (192.168.50.10)**
  Used for traditional services such as:

  * Nginx (web server)
  * MySQL (database)
  * Samba (file sharing)

* **Ubuntu Server – Docker Host (192.168.50.30)**
  Used for containerization and DevOps-related tasks:

  * Docker Engine
  * Portainer (container management)
  * vulnerable applications (DVWA, WebGoat, bWAPP)
  * Wazuh agent (host + container monitoring)

* **Ubuntu Server – Wazuh (192.168.50.40)**
  Acts as a centralized security platform:

  * Wazuh Manager
  * Wazuh Indexer
  * Wazuh Dashboard (web UI)
  * log collection and threat detection

This separation reflects a more realistic architecture with **services, containers, and security monitoring isolated across different systems**.

---

## Network Configuration

During setup, a network connectivity issue was encountered and resolved by editing the Netplan configuration file:

```bash
/etc/netplan/01-netcfg.yaml
```

This provided practical experience with:

* Netplan configuration
* YAML syntax and indentation

---

## Lessons Learned

During the setup and testing of the lab, the following practical skills were developed:

### Linux & Networking

* Understanding how **Netplan** manages network configuration
* Importance of correct **YAML indentation**
* Managing services with **systemctl**
* Testing connectivity between systems

### System Administration

* Installing and configuring:

  * Nginx (web server)
  * MySQL (database server)
  * Samba (file sharing)
* Accessing SMB shares using **smbclient**

### DevOps & Containers

* Installing and configuring **Docker Engine**
* Managing repositories and **GPG keys**
* Running and testing containers
* Using **Portainer** for container management
* Creating Docker volumes and networks

### Security & Monitoring

* Network discovery using **nmap**
* Deploying vulnerable applications for testing
* Installing and configuring **Wazuh agent**
* Monitoring host and container activity
* Centralized logging and alerting with **Wazuh SIEM**

---

## Summary

This lab evolved from a simple Linux environment into a **multi-role infrastructure** that includes:

* traditional services (Ubuntu Desktop)
* containerized workloads (Docker host)
* centralized security monitoring (Wazuh)
