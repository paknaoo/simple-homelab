## Ubuntu Servers in the Lab

The Ubuntu machine acts as a simple server used to practice installing and configuring common Linux services.

Two Ubuntu servers are used in this homelab.

| Server          | IP Address    | Role                                  |
| --------------- | ------------- | ------------------------------------- |
| Ubuntu Server 1 | 192.168.50.10 | Web, database and file server         |
| Ubuntu Server 2 | 192.168.50.30 | Docker host and container environment |

The first server is used to practice traditional Linux services, while the second server is used for container-based workloads with Docker and Portainer.


## Network Configuration

After installation there was an issue with network connectivity.
The problem was resolved by editing the Netplan configuration file:

```bash
/etc/netplan/01-netcfg.yaml
```

This also provided practice with **YAML indentation**, which is required for correct Netplan configuration.







