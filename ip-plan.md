# Network Diagram and IP Plan

## Overview

This document describes the network layout and IP addressing used in the **simple-homelab** environment.

The lab network is intentionally minimal. All virtual machines are connected to a single LAN network behind a pfSense firewall.

The firewall separates the internal lab network from the external network (WAN).

## Network Diagram

                +-------------------+
                |      Internet     |
                +---------+---------+
                          |
                          | WAN (DHCP)
                    +-----+-----+
                    |  pfSense  |
                    | Firewall  |
                    +-----+-----+
                          |
                     LAN 192.168.10.0/24
                          |
          +---------------+---------------+
          |                               |
    +-----+-----+                   +-----+------+
    | Kali Linux |                   | Ubuntu     |
    |  Scanner   |                   |  Server    |
    |192.168.10.10|                 |192.168.10.20|
    +-------------+                 +-------------+

## Network Configuration

| Component     | Interface | IP Address    | Notes                         |
| ------------- | --------- | ------------- | ----------------------------- |
| pfSense       | WAN       | DHCP          | Receives IP from host network |
| pfSense       | LAN       | 192.168.10.1  | Default gateway               |
| Kali Linux    | LAN       | 192.168.10.10 | Security testing machine      |
| Ubuntu Server | LAN       | 192.168.10.20 | Linux server                  |

## LAN Network

Network: 192.168.10.0/24
Gateway: 192.168.10.1
DNS: 192.168.10.1

All machines in the LAN use static IP addressing.

## Notes

* All virtual machines are connected to the same virtual LAN in VMware Workstation.
* pfSense acts as the **default gateway** for the internal network.
* Kali Linux is used for network scanning and analysis.
* Ubuntu Server is used to host and test different services.
* Static IP addressing simplifies lab configuration and documentation.
