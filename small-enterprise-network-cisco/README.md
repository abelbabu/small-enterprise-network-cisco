# Small Enterprise Network Design & Implementation

**Cisco Packet Tracer Simulation**

## Overview

A small enterprise network designed and implemented in Cisco Packet
Tracer to practice core Cisco networking, network segmentation, routing,
security, remote management, and troubleshooting.

The final topology uses two Cisco 2911 routers, two Cisco 2960 switches,
four employee PCs, one admin PC, and one server.

## Network Architecture

The network is divided into separate VLANs:

  VLAN   Name         Network           Gateway
  ------ ------------ ----------------- --------------
  10     ADMIN        192.168.10.0/24   192.168.10.1
  20     EMPLOYEES    192.168.20.0/24   192.168.20.1
  30     SERVERS      192.168.30.0/24   192.168.30.1
  99     MANAGEMENT   192.168.99.0/24   192.168.99.1

WAN:

-   R1: `203.0.113.1/30`
-   ISP-R1: `203.0.113.2/30`
-   Simulated Internet destination: `8.8.8.8/32`

## End Devices

-   PC1 --- ADMIN / VLAN 10
-   PC0, PC2, PC3, PC4 --- EMPLOYEES / VLAN 20
-   SRV1 --- SERVER / VLAN 30
-   SW1 management SVI --- `192.168.99.2/24`
-   SW2 management SVI --- `192.168.99.3/24`

Employee PCs use DHCP. The server uses the static address
`192.168.30.10`.

## Technologies Implemented

-   IPv4 addressing and subnetting
-   VLAN segmentation
-   Access and trunk ports
-   IEEE 802.1Q trunking
-   Router-on-a-Stick
-   Inter-VLAN routing
-   DHCP
-   Static IP addressing
-   Default routing
-   NAT/PAT
-   Extended ACLs
-   SSHv2
-   SVI / Management VLAN
-   Switch port security
-   Sticky MAC addresses
-   Cisco IOS verification and troubleshooting

## Security

The project includes:

-   A dedicated management VLAN (VLAN 99)
-   SSHv2 for secure switch management
-   Extended ACL restricting employee-initiated traffic toward the Admin
    VLAN
-   Port security with a maximum of one MAC address per protected PC
    port
-   Sticky MAC learning
-   Basic device hardening with enable secret, password encryption, and
    MOTD banner

## Troubleshooting Performed

### NAT/PAT

NAT translations were initially absent because the LAN traffic entered
R1 through VLAN subinterfaces while NAT inside was not configured on
those subinterfaces.

The issue was corrected by applying `ip nat inside` to the LAN
subinterfaces. Internet connectivity was then verified with a ping to
`8.8.8.8` and `show ip nat translations`.

### ACL / ICMP

An initial employee-to-admin ACL also affected the return ICMP traffic
for an Admin-to-Employee ping.

The ACL was corrected by explicitly permitting ICMP echo-reply traffic.
After the change, Admin-to-Employee ping worked while Employee-initiated
traffic toward Admin remained restricted.

### Port Security

Port security was enabled on the PC-facing access ports using sticky MAC
learning and a maximum of one MAC address.

## Verification

The network was verified using Cisco IOS commands and end-device tests
including:

-   `show ip interface brief`
-   `show ip route`
-   `show ip dhcp binding`
-   `show ip nat translations`
-   `show ip access-lists`
-   `show vlan brief`
-   `show interfaces trunk`
-   `show port-security`
-   `show port-security address`
-   `show ip ssh`
-   Ping tests
-   SSH login tests

## Project Files

-   `packet-tracer/Small-Enterprise-Network.pkt` --- Cisco Packet Tracer
    project
-   `screenshots/topology.png` --- network topology
-   `documentation/` --- project documentation and evidence can be added
    here

## Learning Outcomes

This project provided hands-on practice with Cisco switching, routing,
VLAN segmentation, inter-VLAN communication, DHCP, NAT/PAT, ACL-based
traffic control, secure device management, Layer-2 security, and
structured network troubleshooting.

> This is a Cisco Packet Tracer simulation and does not represent
> production network administration experience.
