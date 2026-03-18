# Network Diagram and IP Plan

## Overview

This document describes the network layout and IP addressing used in the **simple-homelab** environment.

The lab network is intentionally simple but now includes multiple systems with different roles:

* firewall (pfSense)
* attacker machine (Kali Linux)
* service host (Ubuntu Desktop)
* container host (Docker)
* security monitoring system (Wazuh)

All virtual machines are connected to a single LAN network behind a pfSense firewall.

---

## Network Diagram

```
                +-------------------+
                |     Internet      |
                +---------+---------+
                          |
                          | WAN (DHCP)
                    +-----+-----+
                    |  pfSense  |
                    | Firewall  |
                    +-----+-----+
                          |
                   LAN 192.168.50.0/24
                          |
      +--------+----------+-----------+-----------+
      |        |          |           |           |
+-----+-----+  |   +------+-----+ +---+------+ +--+-------+
| Kali Linux |  |   | Ubuntu     | | Ubuntu   | | Ubuntu   |
| Attacker   |  |   | Desktop    | | Server   | | Server   |
| .20        |  |   | Services   | | Docker   | | Wazuh    |
+------------+  |   | .10        | | .30      | | .40      |
                |   +------------+ +----------+ +----------+
```

---

## Network Configuration

| Component      | Interface              | IP Address    | Role                        |
| -------------- | ---------------------- | ------------- | --------------------------- |
| pfSense        | WAN (VMnet8/NAT)       | DHCP          | Internet access             |
| pfSense        | LAN (VMnet3/Host-only) | 192.168.50.1  | Default gateway             |
| Kali Linux     | LAN                    | 192.168.50.20 | Security testing / attacker |
| Ubuntu Desktop | LAN                    | 192.168.50.10 | Web, DB, file services      |
| Ubuntu Server  | LAN                    | 192.168.50.30 | Docker host                 |
| Ubuntu Server  | LAN                    | 192.168.50.40 | Wazuh SIEM server           |

---

## LAN Network

* **Network:** 192.168.50.0/24
* **Gateway:** 192.168.50.1
* **DNS:** 192.168.50.1

All machines use **static IP addressing**.

---

## Traffic Flow (Concept)

* Kali Linux → scans and attacks targets
* Ubuntu (.10 / .30) → act as targets (services & containers)
* Wazuh (.40) → collects and analyzes logs
* pfSense → controls and routes traffic

---

## Notes

* All virtual machines are connected to the same virtual LAN in VMware Workstation
* pfSense acts as the **default gateway and firewall**
* The network is flat (no VLANs yet), which simplifies initial setup
* Static IP addressing improves consistency and troubleshooting
* This design allows:

  * attack simulation (Kali)
  * service hosting (Ubuntu Desktop)
  * containerization (Docker host)
  * centralized monitoring (Wazuh)

---

## Future Improvements

* introduce **network segmentation (VLANs)**
* isolate attacker machine from internal services
* add a **reverse proxy / load balancer**
* implement stricter firewall rules in pfSense

---

## Summary

The network evolved from a simple two-host setup into a **multi-role lab environment**.

It now supports:

* networking practice (pfSense)
* system administration (Ubuntu)
* containerization (Docker)
* security testing (Kali Linux)
* security monitoring (Wazuh)
