# Project 2 — ELK + pfSense Homelab Architecture

## Objective

Build a resource-conscious cybersecurity SIEM lab using the Elastic Stack and pfSense.

The lab is designed to remain separate from the existing Wazuh environment while allowing the same endpoint VMs to participate in both projects.

## Core Components

### pfSense

pfSense provides:

- Firewalling
- Routing
- NAT
- DHCP
- DNS forwarding/resolution
- Network segmentation

### Elastic Stack

The planned SIEM stack consists of:

- Elasticsearch
- Logstash
- Kibana
- Elastic Agent / log collectors

The Elastic Stack will run using Docker on the Windows host.

## Network Architecture

```text
                         Home LAN
                      192.168.29.0/24
                             |
                             | WAN
                             |
                     pfSense WAN
                     192.168.29.133
                             |
                  +----------+----------+
                  |                     |
                  |                     |
          Project 2 LAN             Management
       192.168.200.0/24          192.168.56.0/24
                  |                     |
             pfSense LAN            pfSense OPT1
             192.168.200.1          192.168.56.2
                  |                     |
          +-------+-------+             |
          |               |             |
       Debian           Windows 7    Windows Host
     .200.100           .200.101       .56.1

 Endpoint Dual-NIC Design

The existing Wazuh network remains separate.

Debian
enp0s3 → 192.168.100.25 → Wazuh network
enp0s8 → 192.168.200.100 → Project 2 network
Windows 7
Adapter 1 → 192.168.100.17 → Wazuh network
Adapter 2 → 192.168.200.101 → Project 2 network
Network Isolation

The Wazuh network uses:

192.168.100.0/24

The Project 2 lab uses:

192.168.200.0/24

These are separate networks.

The existing Wazuh Docker and VirtualBox networking must not be modified as part of Project 2.

Management Access

pfSense OPT1 provides dedicated management access from the Windows host:

Windows Host
192.168.56.1
      |
      | HTTPS 443
      |
pfSense OPT1
192.168.56.2

The management firewall rule permits HTTPS access from the Windows host to the pfSense OPT1 address.

Resource-Conscious Design

The lab is designed to minimize additional VM resource consumption.

The Elastic Stack will use Docker rather than a dedicated Elasticsearch, Kibana, or Logstash VM.

The pfSense VM uses:

2 GB RAM
2 CPU cores
10 GB dynamically allocated disk
Current Verified Network State
pfSense
WAN: 192.168.29.133/24
LAN: 192.168.200.1/24
OPT1: 192.168.56.2/24
LAN DHCP: 192.168.200.100–192.168.200.200
Debian
Wazuh NIC: 192.168.100.25
Project 2 NIC: 192.168.200.100
Windows 7
Wazuh NIC: 192.168.100.17
Project 2 NIC: 192.168.200.101
Windows Host
pfSense management interface: 192.168.56.1
Validation Completed
Debian → pfSense LAN: PASS
Windows 7 → pfSense LAN: PASS
Debian → Internet: PASS
Windows 7 → Internet: PASS
Windows 7 → DNS through pfSense: PASS
Debian → DNS: PASS
pfSense DHCP lease for Debian: PASS
pfSense DHCP lease for Windows 7: PASS
pfSense WebGUI from Windows host: PASS
OPT1 HTTPS management rule: PASS
Routing Considerations

Debian currently has two default routes:

192.168.100.1 → enp0s3
192.168.200.1 → enp0s8

The existing 192.168.100.1 route remains the primary route.

Windows 7 also has both the existing Wazuh-network gateway and the new pfSense gateway available.

No default-route changes have been made because the existing Wazuh networking must remain stable.

Project Separation
Project 1
Wazuh HA Homelab
192.168.100.0/24
Project 2
ELK + pfSense Homelab
192.168.200.0/24

Project 2 must not modify or delete Project 1 resources.

Future Expansion

Planned capabilities include:

pfSense firewall log collection
Endpoint telemetry
Logstash pipelines
Elasticsearch indexing
Kibana dashboards
SIEM detection rules
Security event correlation
Alerting
Additional security monitoring components
Design Principle

The lab will be built incrementally.

Phase 2A focuses on:

Network foundation
pfSense
VirtualBox networking
Endpoint connectivity
Git/GitHub/GitLab
Documentation
Safe validation

Phase 2B will focus on:

Docker-based Elastic Stack deployment
Configuration
Log collection
SIEM integration
Automation
Validation    