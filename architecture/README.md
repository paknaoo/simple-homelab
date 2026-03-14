# Architecture

This directory contains documentation describing the design and structure of the **simple-homelab** environment.

The goal of this folder is to document how the lab network is organized and how the virtual machines communicate with each other.

## Contents

* **ip-plan.md**
  Describes the IP addressing scheme used in the lab environment.

* **network-diagram.md**
  Contains a visual diagram of the lab network topology.

## Lab Design

The lab architecture is intentionally simple and designed for learning purposes.

The environment consists of three virtual machines:

* **pfSense** – firewall and network gateway
* **Ubuntu Server** – Linux server used for testing services
* **Kali Linux** – machine used for network scanning and security testing

All machines are connected to a single LAN network behind the pfSense firewall.

## Purpose

The architecture documentation helps to:

* understand the network topology
* keep track of IP addresses and services
* document the lab configuration
* make the project easier to understand for others
