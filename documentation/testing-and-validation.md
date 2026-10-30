# Testing and Validation

## Overview

This document records the validation results of the Linux Server Hardening Lab running on Debian 13 virtual machines.

## 1. Network Connectivity Testing

| Source | Destination | Result |
|---|---|---|
| INT Server | 10.0.1.254 | Successful |
| INT Server | 10.0.2.11 | Successful |

Packet loss: 0% for both tests.

## 2. DNS Testing

DNS resolution was tested from both INT and DMZ networks using:

`dig @10.0.1.11 web.nusantara.id`

Results:
- DNS query status: NOERROR
- Authoritative answer: Yes
- Resolved IP address: 10.0.2.11
- Query time: 0 msec (as reported by dig)

Both INT and DMZ servers successfully resolved the internal domain.

## 3. Web Server Testing

HTTP connectivity was tested using:

- `curl http://10.0.2.11`
- `curl http://web.nusantara.id`

Results:
- HTTP content successfully retrieved.
- Custom HTML page displayed correctly.
- Nginx successfully served the website.

## 4. SSH Hardening Testing

SSH key authentication was tested from the Windows host.

Results:
- Windows to INT Server: Successful.
- Windows to DMZ Server: Successful.
- Password authentication to INT Server: Rejected.

The password authentication test returned:

`Permission denied (publickey).`

## 5. Ansible Automation Testing

Ansible connectivity was tested using:

`ansible -i inventory.ini dmz -m ping`

Result: SUCCESS, with `pong` returned by the managed node.

Nginx service status was checked remotely using Ansible.

Result: `active`

Nginx boot enablement was also checked remotely.

Result: `enabled`

## 6. Overall Result

The lab successfully demonstrates:

- Network segmentation between INT and DMZ.
- Inter-network routing and firewall filtering.
- Internal DNS using BIND9.
- Nginx web server deployment.
- SSH key-based authentication and hardening.
- Remote server management using Ansible.

The main network, DNS, web server, SSH key authentication, and Ansible validation tests were successful.
