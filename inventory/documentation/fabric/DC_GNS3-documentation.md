# DC_GNS3

# Table of Contents

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

# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| DC_GNS3 | l3leaf | leaf-1a | 192.168.255.61/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | l3leaf | leaf-1b | 192.168.255.62/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | l3leaf | leaf-2a | 192.168.255.63/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | l3leaf | leaf-2b | 192.168.255.64/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | l3leaf | leaf-3a | 192.168.255.65/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | l3leaf | leaf-4a | 192.168.255.67/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | l3leaf | leaf-9a-SVC | 192.168.255.69/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | spine | spine-1 | 192.168.255.51/24 | VEOS-LAB | Provisioned |
| DC_GNS3 | spine | spine-2 | 192.168.255.52/24 | VEOS-LAB | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | leaf-1a | Ethernet1 | spine | spine-1 | Ethernet1 |
| l3leaf | leaf-1a | Ethernet2 | spine | spine-2 | Ethernet1 |
| l3leaf | leaf-1a | Ethernet11 | mlag_peer | leaf-1b | Ethernet11 |
| l3leaf | leaf-1a | Ethernet12 | mlag_peer | leaf-1b | Ethernet12 |
| l3leaf | leaf-1b | Ethernet1 | spine | spine-1 | Ethernet2 |
| l3leaf | leaf-1b | Ethernet2 | spine | spine-2 | Ethernet2 |
| l3leaf | leaf-2a | Ethernet1 | spine | spine-1 | Ethernet3 |
| l3leaf | leaf-2a | Ethernet2 | spine | spine-2 | Ethernet3 |
| l3leaf | leaf-2a | Ethernet11 | mlag_peer | leaf-2b | Ethernet11 |
| l3leaf | leaf-2a | Ethernet12 | mlag_peer | leaf-2b | Ethernet12 |
| l3leaf | leaf-2b | Ethernet1 | spine | spine-1 | Ethernet4 |
| l3leaf | leaf-2b | Ethernet2 | spine | spine-2 | Ethernet4 |
| l3leaf | leaf-3a | Ethernet1 | spine | spine-1 | Ethernet5 |
| l3leaf | leaf-3a | Ethernet2 | spine | spine-2 | Ethernet5 |
| l3leaf | leaf-4a | Ethernet1 | spine | spine-1 | Ethernet7 |
| l3leaf | leaf-4a | Ethernet2 | spine | spine-2 | Ethernet7 |
| l3leaf | leaf-9a-SVC | Ethernet1 | spine | spine-1 | Ethernet9 |
| l3leaf | leaf-9a-SVC | Ethernet2 | spine | spine-2 | Ethernet9 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.31.1.0/24 | 256 | 28 | 10.94 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| leaf-1a | Ethernet1 | 172.31.1.1/31 | spine-1 | Ethernet1 | 172.31.1.0/31 |
| leaf-1a | Ethernet2 | 172.31.1.3/31 | spine-2 | Ethernet1 | 172.31.1.2/31 |
| leaf-1b | Ethernet1 | 172.31.1.5/31 | spine-1 | Ethernet2 | 172.31.1.4/31 |
| leaf-1b | Ethernet2 | 172.31.1.7/31 | spine-2 | Ethernet2 | 172.31.1.6/31 |
| leaf-2a | Ethernet1 | 172.31.1.1/31 | spine-1 | Ethernet3 | 172.31.1.0/31 |
| leaf-2a | Ethernet2 | 172.31.1.3/31 | spine-2 | Ethernet3 | 172.31.1.2/31 |
| leaf-2b | Ethernet1 | 172.31.1.5/31 | spine-1 | Ethernet4 | 172.31.1.4/31 |
| leaf-2b | Ethernet2 | 172.31.1.7/31 | spine-2 | Ethernet4 | 172.31.1.6/31 |
| leaf-3a | Ethernet1 | 172.31.1.1/31 | spine-1 | Ethernet5 | 172.31.1.0/31 |
| leaf-3a | Ethernet2 | 172.31.1.3/31 | spine-2 | Ethernet5 | 172.31.1.2/31 |
| leaf-4a | Ethernet1 | 172.31.1.1/31 | spine-1 | Ethernet7 | 172.31.1.0/31 |
| leaf-4a | Ethernet2 | 172.31.1.3/31 | spine-2 | Ethernet7 | 172.31.1.2/31 |
| leaf-9a-SVC | Ethernet1 | 172.31.1.1/31 | spine-1 | Ethernet9 | 172.31.1.0/31 |
| leaf-9a-SVC | Ethernet2 | 172.31.1.3/31 | spine-2 | Ethernet9 | 172.31.1.2/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 1.1.1.0/24 | 256 | 9 | 3.52 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC_GNS3 | leaf-1a | 1.1.1.11/32 |
| DC_GNS3 | leaf-1b | 1.1.1.12/32 |
| DC_GNS3 | leaf-2a | 1.1.1.11/32 |
| DC_GNS3 | leaf-2b | 1.1.1.12/32 |
| DC_GNS3 | leaf-3a | 1.1.1.11/32 |
| DC_GNS3 | leaf-4a | 1.1.1.11/32 |
| DC_GNS3 | leaf-9a-SVC | 1.1.1.11/32 |
| DC_GNS3 | spine-1 | 1.1.1.1/32 |
| DC_GNS3 | spine-2 | 1.1.1.2/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 2.2.2.0/24 | 256 | 7 | 2.74 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC_GNS3 | leaf-1a | 2.2.2.11/32 |
| DC_GNS3 | leaf-1b | 2.2.2.11/32 |
| DC_GNS3 | leaf-2a | 2.2.2.11/32 |
| DC_GNS3 | leaf-2b | 2.2.2.11/32 |
| DC_GNS3 | leaf-3a | 2.2.2.11/32 |
| DC_GNS3 | leaf-4a | 2.2.2.11/32 |
| DC_GNS3 | leaf-9a-SVC | 2.2.2.11/32 |
