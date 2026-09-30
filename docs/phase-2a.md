# Phase 2A — Manual and Safe Foundation

## Project

ELK + pfSense Cybersecurity Homelab

## Phase 2A Objective

Build and validate the foundational infrastructure before beginning Docker-based ELK automation.

Phase 2A is intentionally manual and conservative so that the existing Wazuh homelab remains protected.

## Completed Tasks

### Project Repository

- [x] Project directory created
- [x] Git repository initialized
- [x] Main branch created
- [x] Initial README created
- [x] `.gitignore` created
- [x] Initial Git commit created
- [x] GitHub repository created
- [x] GitHub remote configured
- [x] Initial commit pushed to GitHub
- [x] GitLab repository created
- [x] GitLab remote configured
- [x] Initial commit pushed to GitLab
- [x] Working tree verified clean

### Project Structure

The following directories were created:

```text
docs/
config/
docker/
logstash/
kibana/
elasticsearch/
scripts/

Documentation files:

docs/
├── architecture.md
├── network-design.md
└── phase-2a.md
pfSense
 pfSense CE installed
 pfSense VM created
 2 GB RAM allocated
 2 CPU cores allocated
 10 GB dynamic disk allocated
 WAN configured
 LAN configured
 OPT1 management interface configured
 LAN DHCP configured
 WebGUI access verified
 Default admin password changed
 OPT1 HTTPS management rule configured
 WAN firewall rules verified
 LAN firewall rules verified
pfSense Network Configuration
WAN
192.168.29.133/24
Gateway: 192.168.29.1
LAN
192.168.200.1/24
DHCP: 192.168.200.100–192.168.200.200
OPT1 Management
192.168.56.2/24
Windows Host Management
192.168.56.1/24
Endpoint Configuration
Debian

Existing Wazuh interface:

enp0s3
192.168.100.25/24

Project 2 interface:

enp0s8
192.168.200.100/24
Windows 7

Existing Wazuh interface:

192.168.100.17/24

Project 2 interface:

192.168.200.101/24
Wazuh Protection

The existing Wazuh environment remains separate.

The following network remains unchanged:

192.168.100.0/24

The Project 2 network is:

192.168.200.0/24

No Wazuh containers, Docker networks, or existing endpoint Wazuh interfaces were deleted or modified.

Connectivity Validation
Debian
 DHCP address received
 Debian → pfSense LAN
 Debian → Internet
 Debian DNS resolution
Windows 7
 DHCP address received
 Windows 7 → pfSense LAN
 Windows 7 → Internet
 Windows 7 DNS resolution
pfSense
 Debian DHCP lease visible
 Windows 7 DHCP lease visible
 LAN firewall verified
 WAN firewall verified
 OPT1 management access verified
Routing Notes

Debian currently has:

default via 192.168.100.1 dev enp0s3
default via 192.168.200.1 dev enp0s8 metric 100

The existing Wazuh/NAT route remains primary.

Windows 7 also has both network gateways available.

No default-route modification has been performed.

This is intentional to avoid disrupting Project 1.

Safety Rules

The following must not be performed during Project 2:

Do not delete Wazuh containers.
Do not delete Wazuh Docker volumes.
Do not modify the Wazuh Docker network.
Do not modify the existing Wazuh endpoint NIC configuration.
Do not change the Saif NatNetwork.
Do not disable the pfSense firewall globally.
Do not expose pfSense management through WAN.
Do not perform Docker system pruning.
Do not delete existing VirtualBox VMs without explicit review.
Phase 2A Status

Network foundation and repository foundation are operational.

Remaining Phase 2A work:

 Review final Git repository state
 Create final Phase 2A commit
 Push final Phase 2A documentation to GitHub
 Push final Phase 2A documentation to GitLab
 Confirm Phase 2A completion
Phase 2B

Phase 2B will begin only after Phase 2A is explicitly completed.

Planned Phase 2B work:

Docker ELK network
Elasticsearch deployment
Kibana deployment
Logstash deployment
Elastic Agent/log collection
pfSense log ingestion
Endpoint log ingestion
SIEM dashboards
Detection and correlation
Validation
Automation