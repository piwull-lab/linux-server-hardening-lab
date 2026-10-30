![Network Topology](topology.png)
# Security Configuration

## 1. Overview

This document describes the security mechanisms implemented in the Linux Server Hardening Lab.

The main objective is to control network traffic, secure remote administration, and restrict communication between internal network segments.

## 2. Firewall Configuration

The router server uses nftables to filter network traffic.

Implemented configurations:

- IPv4 forwarding enabled.
- NAT masquerading for INT and DMZ networks.
- Forward chain uses a default DROP policy.
- Established and related connections are allowed.
- Outbound HTTP and HTTPS traffic is permitted.
- DNS traffic is permitted for internal servers.
- NTP traffic is permitted for time synchronization.
- Specific INT-to-DMZ and DMZ-to-INT traffic is allowed based on service requirements.

## 3. SSH Hardening

SSH security configurations are applied to INT Server and DMZ Server.

Configuration file:

`/etc/ssh/sshd_config.d/99-hardening.conf`

Implemented settings:

| Configuration | Value | Purpose |
|---|---|---|
| PermitRootLogin | no | Disable direct root login |
| PubkeyAuthentication | yes | Enable SSH public key authentication |
| PasswordAuthentication | no | Disable password-based SSH authentication |
| KbdInteractiveAuthentication | no | Disable keyboard-interactive authentication |
| PermitEmptyPasswords | no | Reject empty passwords |

SSH access was tested using key-based authentication.

## 4. Network Segmentation

The infrastructure separates internal services and web services into two different networks.

- INT Network: Contains DNS and Ansible services.
- DMZ Network: Contains the Nginx web server.

Traffic between these networks is restricted through firewall rules on the router server.

## 5. Access Control

The firewall controls communication between network segments based on source, destination, interface, protocol, and port.

Examples include:

- INT-to-DMZ SSH access for server administration.
- INT-to-DMZ HTTP access for web service testing.
- DMZ-to-INT DNS access for internal domain resolution.
- Restricted forwarding between INT and DMZ.

## 6. Security Validation

The following security configurations were validated:

- SSH key-based authentication.
- Root SSH login disabled.
- Password-based SSH authentication disabled.
- Firewall forwarding policy set to DROP.
- Network connectivity tested according to firewall rules.

## 7. Current Limitations

The router's input and output firewall chains still use ACCEPT policies.

Therefore, the router itself has not yet undergone complete firewall hardening.

Additional improvements may include:

- Restricting access to router management services.
- Implementing monitoring and logging.
- Performing additional firewall testing.
- Reviewing unnecessary exposed services.

## 8. Conclusion

The lab implements basic Linux server hardening and network traffic control through nftables and OpenSSH security configurations.

These measures provide a foundation for further infrastructure security improvements.
