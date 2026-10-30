# Linux Server Hardening & Infrastructure Automation Lab

## Overview

A personal homelab project designed to simulate a small enterprise network infrastructure using Debian 13 virtual machines.

This project focuses on Linux server administration, network segmentation, firewall configuration, DNS management, SSH hardening, and infrastructure automation using Ansible.

The lab was built using VMware Workstation with three Debian 13 virtual machines acting as a Router Server, Internal Server (INT), and DMZ Server.

## Network Topology

The following diagram illustrates the network architecture of this homelab project.

![Network Topology](documentation/topoloy.png)

## Network Architecture

The infrastructure consists of three virtual machines:

| Server | Role | IP Address |
|---|---|---|
| Router Server | Routing, NAT, and Firewall | WAN, INT, DMZ interfaces |
| INT Server | BIND9 DNS, Ansible Controller | 10.0.1.11 |
| DMZ Server | Nginx Web Server | 10.0.2.11 |

### Network Segmentation

The network is divided into two internal segments:

| Network | Subnet | Gateway |
|---|---|---|
| INT | 10.0.1.0/24 | 10.0.1.254 |
| DMZ | 10.0.2.0/24 | 10.0.2.254 |

This separation allows internal services and externally exposed services to operate in different network segments.

## Technologies

- **Operating System:** Debian 13
- **Virtualization:** VMware Workstation
- **Firewall:** nftables
- **DNS Server:** BIND9
- **Remote Access:** OpenSSH
- **Automation:** Ansible
- **Web Server:** Nginx

## Implemented Features

### 1. Network Infrastructure

- Network segmentation using INT and DMZ networks.
- IPv4 forwarding and NAT configuration.
- Inter-network routing.
- Traffic filtering using nftables.
- Stateful firewall rules for established and related connections.

### 2. DNS Management

- Internal DNS server using BIND9.
- Custom internal DNS zone: `nusantara.id`.
- Internal hostname resolution for `web.nusantara.id`.
- DNS forwarding for external name resolution.

### 3. Server Security

- SSH key-based authentication using Ed25519.
- Disabled direct root SSH login.
- Disabled password-based SSH authentication.
- Disabled keyboard-interactive SSH authentication.
- SSH hardening applied to INT and DMZ servers.

### 4. Infrastructure Automation

- Ansible Controller hosted on the INT Server.
- Remote server management through SSH.
- Automated Nginx installation.
- Automated website deployment using Ansible Playbooks.

## Testing & Validation

The infrastructure was validated through connectivity tests, DNS queries, HTTP requests, SSH authentication tests, and Ansible automation.

| Test | Result |
|---|---|
| INT to Gateway connectivity | Passed |
| INT to DMZ connectivity | Passed |
| DNS resolution from INT | Passed |
| DNS resolution from DMZ | Passed |
| HTTP access using IP address | Passed |
| HTTP access using internal DNS | Passed |
| SSH key authentication from Windows to INT | Passed |
| SSH key authentication from Windows to DMZ | Passed |
| SSH password rejection on INT | Passed |
| Ansible connectivity | Passed |
| Nginx service status | Active |
| Nginx boot enablement | Enabled |

### Web Server Access

The deployed website can be accessed internally through:

- `http://10.0.2.11`
- `http://web.nusantara.id`

### Testing Documentation

Detailed test procedures and observed results are documented in:

[`documentation/testing-and-validation.md`](documentation/testing-and-validation.md)

## Repository Structure

```text
linux-server-hardening-lab/
├── ansible/
│   ├── deploy-website.yml
│   ├── install-nginx.yml
│   └── inventory.ini
├── dns/
│   ├── db.nusantara.id
│   └── named.conf.local
├── documentation/
│   ├── ansible-automation.md
│   ├── network-configuration.md
│   ├── security-configuration.md
│   ├── testing-and-validation.md
│   └── topoloy.png
├── firewall/
│   └── nftables.conf
├── ssh-hardening.conf/
│   └── 99-hardening.conf
└── README.md
```

## Current Limitations

- Router input and output firewall policies still use the `ACCEPT` default policy. Further hardening of traffic directed to and originating from the router is planned.
- Additional security testing and monitoring have not yet been implemented.
- Terminal screenshots and visual testing evidence will be added as project documentation is expanded.

## Future Improvements

- Implement stricter firewall policies for the router.
- Server monitoring and observability.
- Additional security testing.
- Backup and recovery automation.
- Further improvements to infrastructure automation.
- More comprehensive technical documentation.

## Project Status

**Status: Core Implementation Completed**

The core infrastructure has been implemented and tested, including network segmentation, routing, NAT, DNS integration, SSH hardening, firewall configuration, and Ansible-based web server deployment.

Further improvements are planned to strengthen security, monitoring, and automation.

## Author

Telecommunication Engineering Student

Diploma III (D3) Telecommunication Engineering student at Politeknik Elektronika Negeri Surabaya (PENS).

Interested in Linux System Administration, Network Infrastructure, Cybersecurity, and Cloud Computing.

This project was developed as part of my hands-on learning journey to explore Linux server administration, network engineering, infrastructure security, and automation.
