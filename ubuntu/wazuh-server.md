# Wazuh Server (Ubuntu Server)

## Overview

This Ubuntu Server (**192.168.50.40**) is used as the **Wazuh SIEM server** in the homelab.

It is responsible for:

* collecting security events from agents
* analyzing logs and detecting threats
* providing a centralized security monitoring platform

---

## Ubuntu Installation

Ubuntu Server was installed as a virtual machine in VMware Workstation.

The following steps were completed:

* Ubuntu Server installation
* Static IP configuration (**192.168.50.40**)
* SSH installation and configuration

---

## Remote Administration

The server can be accessed remotely via SSH:

```bash
ssh adam@192.168.50.40
```

All installation steps were performed remotely.

---

## Wazuh Server Installation

Wazuh was installed using the **official quickstart installation script**.

Official documentation:
https://documentation.wazuh.com/current/quickstart.html

### Download Installation Script

```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
```

### Run Installation

```bash
sudo bash ./wazuh-install.sh -a
```

The `-a` (all-in-one) option installs:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard

---

## Accessing Wazuh Dashboard

After installation, the Wazuh web interface is available at:

```
https://192.168.50.40
```

Login credentials are displayed at the end of the installation process.

---

## Agent Integration

The Wazuh server is configured to receive data from agents installed on:

* Docker host (**192.168.50.30**)
* Kali Linux (**192.168.50.20**)

Agents send:

* system logs
* security events
* Docker activity (via Docker listener)

---

## Purpose

The Wazuh server enables:

* centralized log collection
* threat detection and alerting
* monitoring of Docker containers and host systems
* visibility into lab security events

This system acts as a **basic SIEM platform** within the homelab.

---

## Notes

* The installation script deploys all components automatically
* Default ports must be reachable within the lab network
* Access should be restricted via firewall rules (pfSense)

---

## Future Improvements

* create custom detection rules
* integrate with vulnerability scanning tools
* simulate attacks and analyze alerts

---

## Summary

This server transforms the lab into a **security monitoring environment**, allowing:

* attack simulation (Kali Linux)
* vulnerable services (Docker host)
* detection and logging (Wazuh)

This creates a complete **attack → detection → analysis workflow**.
