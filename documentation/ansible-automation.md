# Ansible Automation

## Overview

Ansible is used as a configuration management and automation tool in this lab.

The INT Server acts as the Ansible Controller, while the DMZ Server acts as the Managed Node.

## Infrastructure

| Component | Configuration |
|---|---|
| Ansible Controller | INT Server |
| Controller IP | 10.0.1.11 |
| Managed Node | DMZ Server |
| Managed Node IP | 10.0.2.11 |
| Remote User | adminlab |
| Connection | SSH Public Key Authentication |

## Implemented Automation

### 1. Nginx Installation

The `install-nginx.yml` playbook automates:
- Package cache updates.
- Nginx installation.
- Nginx service startup.
- Nginx service enablement.

### 2. Website Deployment

The `deploy-website.yml` playbook automates:
- Creation of the website index file.
- Deployment of custom HTML content.
- File ownership and permission configuration.

## Validation

The following tests were performed:
- Ansible connectivity test using the ping module.
- Successful execution of the Nginx installation playbook.
- Successful execution of the website deployment playbook.
- Website accessibility through HTTP.

## Result

Ansible successfully managed the DMZ Server remotely from the INT Server using SSH key-based authentication.
