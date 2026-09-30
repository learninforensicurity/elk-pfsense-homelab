# Project 2 Network Design

## Networks

| Network | Purpose | Gateway |
|---|---|---|
| 192.168.29.0/24 | Home LAN / pfSense WAN | 192.168.29.1 |
| 192.168.200.0/24 | ELK/pfSense lab LAN | 192.168.200.1 |
| 192.168.56.0/24 | pfSense management | 192.168.56.2 |

## pfSense

- WAN: 192.168.29.133/24
- LAN: 192.168.200.1/24
- OPT1: 192.168.56.2/24
- LAN DHCP: 192.168.200.100-192.168.200.200

## Project 2 Endpoints

### Debian

- Wazuh NIC: 192.168.100.25
- Project 2 NIC: 192.168.200.100

### Windows 7

- Wazuh NIC: 192.168.100.17
- Project 2 NIC: 192.168.200.101

### Windows Host

- Management: 192.168.56.1

## Network Separation

The existing 192.168.100.0/24 Wazuh network is retained and has not been modified.

The Project 2 lab uses the separate 192.168.200.0/24 network through pfSense.

## Validation

- Debian → pfSense LAN: PASS
- Windows 7 → pfSense LAN: PASS
- Debian → Internet: PASS
- Windows 7 → Internet: PASS
- Windows 7 → DNS through pfSense: PASS
- pfSense DHCP leases for Debian and Windows 7: PASS