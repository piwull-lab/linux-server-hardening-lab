# Network Configuration
![Network Topology](topoloy.png)
## 1. Overview

This homelab implements a segmented network architecture using three Debian 13 virtual machines running on VMware Workstation.

The network is divided into three segments:

- WAN: Provides external network connectivity through VMware NAT.
- INT: Internal network for DNS services and infrastructure automation.
- DMZ: Isolated network for hosting web services.

## 2. Network Topology

```text
                  INTERNET
                      |
                 VMware NAT
                      |
                WAN: ens33
                192.168.204.130
                      |
               [ ROUTER SERVER ]
                   Debian 13
                      |
             +--------+--------+
             |                 |
          INT Network       DMZ Network
          10.0.1.0/24       10.0.2.0/24
             |                 |
        [INT SERVER]      [DMZ SERVER]
         10.0.1.11         10.0.2.11
             |                 |
        BIND9 DNS             Nginx
        Ansible             Web Server
        Controller
```

## 3. IP Addressing

| Device | Interface | IP Address | Network |
|---|---|---|---|
| Router | ens33 | 192.168.204.130/24 | WAN |
| Router | ens37 | 10.0.2.254/24 | DMZ |
| Router | ens38 | 10.0.1.254/24 | INT |
| INT Server | - | 10.0.1.11/24 | INT |
| DMZ Server | - | 10.0.2.11/24 | DMZ |

## 4. Network Gateway

- INT Server Default Gateway: 10.0.1.254
- DMZ Server Default Gateway: 10.0.2.254

The router acts as the default gateway for both internal network segments.

## 5. Network Segmentation

The INT and DMZ networks are separated into different subnets.

- INT Network: Hosts internal infrastructure services such as BIND9 DNS and Ansible Controller.
- DMZ Network: Hosts the Nginx web server.

Communication between network segments is controlled through firewall rules configured using nftables.

## 6. Network Services

| Service | Server | Purpose |
|---|---|---|
| DNS | INT Server | Internal domain resolution |
| Ansible | INT Server | Infrastructure automation |
| Nginx | DMZ Server | Web hosting |
| NAT | Router Server | Outbound internet connectivity |
| Firewall | Router Server | Network traffic filtering |

## 7. Validation

The following tests were performed:

- Verified connectivity between network segments.
- Verified router connectivity to the internet.
- Verified DNS resolution for web.nusantara.id.
- Verified HTTP access to the DMZ web server.
- Verified website access using the internal DNS hostname.

## 8. Conclusion

The network architecture successfully separates internal infrastructure services from public-facing web services within a virtualized environment.

The implementation provides a foundation for further Linux server hardening, network security testing, and infrastructure automation.
