# DC_FABRICS

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| DC_FABRICS | l3leaf | s1-brdr1 | 192.168.0.100/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s1-brdr2 | 192.168.0.101/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s1-leaf1 | 192.168.0.12/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s1-leaf2 | 192.168.0.13/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s1-leaf3 | 192.168.0.14/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s1-leaf4 | 192.168.0.15/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | spine | s1-spine1 | 192.168.0.10/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | spine | s1-spine2 | 192.168.0.11/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s2-brdr1 | 192.168.0.200/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s2-brdr2 | 192.168.0.201/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s2-leaf1 | 192.168.0.22/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s2-leaf2 | 192.168.0.23/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s2-leaf3 | 192.168.0.24/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | l3leaf | s2-leaf4 | 192.168.0.25/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | spine | s2-spine1 | 192.168.0.20/24 | cEOSLab | Provisioned | - |
| DC_FABRICS | spine | s2-spine2 | 192.168.0.21/24 | cEOSLab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | s1-brdr1 | Ethernet1 | mlag_peer | s1-brdr2 | Ethernet1 |
| l3leaf | s1-brdr1 | Ethernet2 | spine | s1-spine1 | Ethernet7 |
| l3leaf | s1-brdr1 | Ethernet3 | spine | s1-spine2 | Ethernet7 |
| l3leaf | s1-brdr1 | Ethernet4 | l3leaf | s2-brdr1 | Ethernet4 |
| l3leaf | s1-brdr1 | Ethernet5 | l3leaf | s2-brdr2 | Ethernet5 |
| l3leaf | s1-brdr1 | Ethernet6 | mlag_peer | s1-brdr2 | Ethernet6 |
| l3leaf | s1-brdr2 | Ethernet2 | spine | s1-spine1 | Ethernet8 |
| l3leaf | s1-brdr2 | Ethernet3 | spine | s1-spine2 | Ethernet8 |
| l3leaf | s1-brdr2 | Ethernet4 | l3leaf | s2-brdr2 | Ethernet4 |
| l3leaf | s1-brdr2 | Ethernet5 | l3leaf | s2-brdr1 | Ethernet5 |
| l3leaf | s1-leaf1 | Ethernet1 | mlag_peer | s1-leaf2 | Ethernet1 |
| l3leaf | s1-leaf1 | Ethernet2 | spine | s1-spine1 | Ethernet2 |
| l3leaf | s1-leaf1 | Ethernet3 | spine | s1-spine2 | Ethernet2 |
| l3leaf | s1-leaf1 | Ethernet6 | mlag_peer | s1-leaf2 | Ethernet6 |
| l3leaf | s1-leaf2 | Ethernet2 | spine | s1-spine1 | Ethernet3 |
| l3leaf | s1-leaf2 | Ethernet3 | spine | s1-spine2 | Ethernet3 |
| l3leaf | s1-leaf3 | Ethernet1 | mlag_peer | s1-leaf4 | Ethernet1 |
| l3leaf | s1-leaf3 | Ethernet2 | spine | s1-spine1 | Ethernet4 |
| l3leaf | s1-leaf3 | Ethernet3 | spine | s1-spine2 | Ethernet4 |
| l3leaf | s1-leaf3 | Ethernet6 | mlag_peer | s1-leaf4 | Ethernet6 |
| l3leaf | s1-leaf4 | Ethernet2 | spine | s1-spine1 | Ethernet5 |
| l3leaf | s1-leaf4 | Ethernet3 | spine | s1-spine2 | Ethernet5 |
| l3leaf | s2-brdr1 | Ethernet1 | mlag_peer | s2-brdr2 | Ethernet1 |
| l3leaf | s2-brdr1 | Ethernet2 | spine | s2-spine1 | Ethernet7 |
| l3leaf | s2-brdr1 | Ethernet3 | spine | s2-spine2 | Ethernet7 |
| l3leaf | s2-brdr1 | Ethernet6 | mlag_peer | s2-brdr2 | Ethernet6 |
| l3leaf | s2-brdr2 | Ethernet2 | spine | s2-spine1 | Ethernet8 |
| l3leaf | s2-brdr2 | Ethernet3 | spine | s2-spine2 | Ethernet8 |
| l3leaf | s2-leaf1 | Ethernet1 | mlag_peer | s2-leaf2 | Ethernet1 |
| l3leaf | s2-leaf1 | Ethernet2 | spine | s2-spine1 | Ethernet2 |
| l3leaf | s2-leaf1 | Ethernet3 | spine | s2-spine2 | Ethernet2 |
| l3leaf | s2-leaf1 | Ethernet6 | mlag_peer | s2-leaf2 | Ethernet6 |
| l3leaf | s2-leaf2 | Ethernet2 | spine | s2-spine1 | Ethernet3 |
| l3leaf | s2-leaf2 | Ethernet3 | spine | s2-spine2 | Ethernet3 |
| l3leaf | s2-leaf3 | Ethernet1 | mlag_peer | s2-leaf4 | Ethernet1 |
| l3leaf | s2-leaf3 | Ethernet2 | spine | s2-spine1 | Ethernet4 |
| l3leaf | s2-leaf3 | Ethernet3 | spine | s2-spine2 | Ethernet4 |
| l3leaf | s2-leaf3 | Ethernet6 | mlag_peer | s2-leaf4 | Ethernet6 |
| l3leaf | s2-leaf4 | Ethernet2 | spine | s2-spine1 | Ethernet5 |
| l3leaf | s2-leaf4 | Ethernet3 | spine | s2-spine2 | Ethernet5 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.30.11.0/24 | 256 | 24 | 9.38 % |
| 172.30.12.0/24 | 256 | 24 | 9.38 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| s1-brdr1 | Ethernet2 | 172.30.11.25/31 | s1-spine1 | Ethernet7 | 172.30.11.24/31 |
| s1-brdr1 | Ethernet3 | 172.30.11.27/31 | s1-spine2 | Ethernet7 | 172.30.11.26/31 |
| s1-brdr1 | Ethernet4 | 172.16.200.0/31 | s2-brdr1 | Ethernet4 | 172.16.200.1/31 |
| s1-brdr1 | Ethernet5 | 172.16.200.2/31 | s2-brdr2 | Ethernet5 | 172.16.200.3/31 |
| s1-brdr2 | Ethernet2 | 172.30.11.29/31 | s1-spine1 | Ethernet8 | 172.30.11.28/31 |
| s1-brdr2 | Ethernet3 | 172.30.11.31/31 | s1-spine2 | Ethernet8 | 172.30.11.30/31 |
| s1-brdr2 | Ethernet4 | 172.16.200.4/31 | s2-brdr2 | Ethernet4 | 172.16.200.5/31 |
| s1-brdr2 | Ethernet5 | 172.16.200.6/31 | s2-brdr1 | Ethernet5 | 172.16.200.7/31 |
| s1-leaf1 | Ethernet2 | 172.30.11.1/31 | s1-spine1 | Ethernet2 | 172.30.11.0/31 |
| s1-leaf1 | Ethernet3 | 172.30.11.3/31 | s1-spine2 | Ethernet2 | 172.30.11.2/31 |
| s1-leaf2 | Ethernet2 | 172.30.11.5/31 | s1-spine1 | Ethernet3 | 172.30.11.4/31 |
| s1-leaf2 | Ethernet3 | 172.30.11.7/31 | s1-spine2 | Ethernet3 | 172.30.11.6/31 |
| s1-leaf3 | Ethernet2 | 172.30.11.9/31 | s1-spine1 | Ethernet4 | 172.30.11.8/31 |
| s1-leaf3 | Ethernet3 | 172.30.11.11/31 | s1-spine2 | Ethernet4 | 172.30.11.10/31 |
| s1-leaf4 | Ethernet2 | 172.30.11.13/31 | s1-spine1 | Ethernet5 | 172.30.11.12/31 |
| s1-leaf4 | Ethernet3 | 172.30.11.15/31 | s1-spine2 | Ethernet5 | 172.30.11.14/31 |
| s2-brdr1 | Ethernet2 | 172.30.12.17/31 | s2-spine1 | Ethernet7 | 172.30.12.16/31 |
| s2-brdr1 | Ethernet3 | 172.30.12.19/31 | s2-spine2 | Ethernet7 | 172.30.12.18/31 |
| s2-brdr2 | Ethernet2 | 172.30.12.21/31 | s2-spine1 | Ethernet8 | 172.30.12.20/31 |
| s2-brdr2 | Ethernet3 | 172.30.12.23/31 | s2-spine2 | Ethernet8 | 172.30.12.22/31 |
| s2-leaf1 | Ethernet2 | 172.30.12.1/31 | s2-spine1 | Ethernet2 | 172.30.12.0/31 |
| s2-leaf1 | Ethernet3 | 172.30.12.3/31 | s2-spine2 | Ethernet2 | 172.30.12.2/31 |
| s2-leaf2 | Ethernet2 | 172.30.12.5/31 | s2-spine1 | Ethernet3 | 172.30.12.4/31 |
| s2-leaf2 | Ethernet3 | 172.30.12.7/31 | s2-spine2 | Ethernet3 | 172.30.12.6/31 |
| s2-leaf3 | Ethernet2 | 172.30.12.9/31 | s2-spine1 | Ethernet4 | 172.30.12.8/31 |
| s2-leaf3 | Ethernet3 | 172.30.12.11/31 | s2-spine2 | Ethernet4 | 172.30.12.10/31 |
| s2-leaf4 | Ethernet2 | 172.30.12.13/31 | s2-spine1 | Ethernet5 | 172.30.12.12/31 |
| s2-leaf4 | Ethernet3 | 172.30.12.15/31 | s2-spine2 | Ethernet5 | 172.30.12.14/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.0.255.0/24 | 256 | 8 | 3.13 % |
| 192.2.255.0/24 | 256 | 8 | 3.13 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC_FABRICS | s1-brdr1 | 192.0.255.9/32 |
| DC_FABRICS | s1-brdr2 | 192.0.255.10/32 |
| DC_FABRICS | s1-leaf1 | 192.0.255.3/32 |
| DC_FABRICS | s1-leaf2 | 192.0.255.4/32 |
| DC_FABRICS | s1-leaf3 | 192.0.255.5/32 |
| DC_FABRICS | s1-leaf4 | 192.0.255.6/32 |
| DC_FABRICS | s1-spine1 | 192.0.255.1/32 |
| DC_FABRICS | s1-spine2 | 192.0.255.2/32 |
| DC_FABRICS | s2-brdr1 | 192.2.255.7/32 |
| DC_FABRICS | s2-brdr2 | 192.2.255.8/32 |
| DC_FABRICS | s2-leaf1 | 192.2.255.3/32 |
| DC_FABRICS | s2-leaf2 | 192.2.255.4/32 |
| DC_FABRICS | s2-leaf3 | 192.2.255.5/32 |
| DC_FABRICS | s2-leaf4 | 192.2.255.6/32 |
| DC_FABRICS | s2-spine1 | 192.2.255.1/32 |
| DC_FABRICS | s2-spine2 | 192.2.255.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.0.254.0/24 | 256 | 6 | 2.35 % |
| 192.2.254.0/24 | 256 | 6 | 2.35 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC_FABRICS | s1-brdr1 | 192.0.254.9/32 |
| DC_FABRICS | s1-brdr2 | 192.0.254.9/32 |
| DC_FABRICS | s1-leaf1 | 192.0.254.3/32 |
| DC_FABRICS | s1-leaf2 | 192.0.254.3/32 |
| DC_FABRICS | s1-leaf3 | 192.0.254.5/32 |
| DC_FABRICS | s1-leaf4 | 192.0.254.5/32 |
| DC_FABRICS | s2-brdr1 | 192.2.254.7/32 |
| DC_FABRICS | s2-brdr2 | 192.2.254.7/32 |
| DC_FABRICS | s2-leaf1 | 192.2.254.3/32 |
| DC_FABRICS | s2-leaf2 | 192.2.254.3/32 |
| DC_FABRICS | s2-leaf3 | 192.2.254.5/32 |
| DC_FABRICS | s2-leaf4 | 192.2.254.5/32 |
