# Linux Server Hardening & Infrastructure Automation Lab

## Overview
## Network Topology

The following diagram illustrates the network architecture
of this homelab project.

![Network Topology](documentation/topoloy.png)

A personal homelab project designed to simulate a small enterprise network infrastructure using Debian 13 virtual machines.

This project focuses on Linux server administration, network segmentation, firewall configuration, DNS management, SSH hardening, and infrastructure automation using Ansible.

## Network Architecture

The infrastructure consists of three virtual machines:

| Server | Role | IP Address |
|---|---|---|
| Router Server | Routing, NAT, Firewall | Multiple Interfaces |
| INT Server | BIND9 DNS, Ansible Controller | 10.0.1.11 |
| DMZ Server | Nginx Web Server | 10.0.2.11 |

## Technologies

- Debian 13
- VMware Workstation
- nftables
- BIND9
- OpenSSH
- Ansible
- Nginx

## Implemented Features

- Network segmentation using INT and DMZ networks.
- IPv4 forwarding and NAT configuration.
- Firewall configuration using nftables.
- Internal DNS management using BIND9.
- SSH key-based authentication.
- SSH security hardening.
- Automated Nginx installation using Ansible.
- Automated website deployment using Ansible.

## Testing & Validation

- Network connectivity between virtual machines.
- DNS resolution for `web.nusantara.id`.
- SSH key-based authentication.
- Ansible connectivity testing.
- Automated Nginx deployment.
- Website accessibility through an internal DNS hostname.

## Project Status

Core infrastructure, DNS integration, SSH hardening, and Ansible-based web deployment have been implemented and tested.

Future improvements:
- Server monitoring.
- Security testing.
- Backup and recovery.
- Infrastructure documentation.

## Author

Personal Linux Infrastructure & Server Administration Project.
