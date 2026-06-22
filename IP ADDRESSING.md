
# Routing & Protocols Implementation
* **OSPF Area 0 Backbone:** Configured on **R1, R2, R3, and R4** to manage internal transit routing efficiently across the campus network. R1 features a `passive-interface` on its local LAN side to limit unnecessary multicast hello packets.
* **RIPv2 Edge Domain:** Configured on **R5** for a lightweight, classless routing footprint on the branch edge.
* **Mutual Route Redistribution:** Implemented on **R4 (ASBR)**. OSPF subnets are seamlessly redistributed down into the RIP process, and RIP metrics are translated dynamically back into the OSPF backbone.
* **Automated Device Provisioning:** **R1** is deployed as a local **DHCPv4 Server** managing the `LAN1` address pool autonomously.

---

# IP Addressing & Infrastructure Documentation

| Device | Interface | IP Address | Subnet Mask | CIDR | Default Gateway | Description / Role |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **R1** | Gig0/0 | 192.168.10.1 | 255.255.255.0 | /24 | N/A | Gateway for Branch LAN 10 (DHCP Pool active) |
| | Gig0/1 | 192.168.1.1 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R2 |
| **R2** | Gig0/0 | 192.168.20.1 | 255.255.255.0 | /24 | N/A | Gateway for LAN 20 |
| | Gig0/1 | 192.168.1.2 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R1 |
| | Gig0/2 | 192.168.2.1 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R3 |
| **R3** | Gig0/0 | 192.168.30.1 | 255.255.255.0 | /24 | N/A | Gateway for LAN 30 |
| | Gig0/1 | 192.168.2.2 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R2 |
| | Gig0/2 | 192.168.3.1 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R4 |
| **R4** | Gig0/0 | 192.168.40.1 | 255.255.255.0 | /24 | N/A | Gateway for LAN 40 |
| *(ASBR)*| Gig0/1 | 192.168.3.2 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R3 (OSPF Boundary) |
| | Gig0/2 | 192.168.4.1 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R5 (RIPv2 Boundary) |
| **R5** | Gig0/0 | 192.168.50.1 | 255.255.255.0 | /24 | N/A | Gateway for Branch LAN 50 |
| | Gig0/1 | 192.168.4.2 | 255.255.255.252 | /30 | N/A | Point-to-Point WAN Link to R4 |
| **PC1** | Fa0 | *DHCP Assigned* | 255.255.255.0 | /24 | 192.168.10.1 | Dynamic Client inside LAN 10 Pool |
| **PC2** | Fa0 | 192.168.20.2 | 255.255.255.0 | /24 | 192.168.20.1 | Static Host Assignment |
| **PC3** | Fa0 | 192.168.30.2 | 255.255.255.0 | /24 | 192.168.30.1 | Static Host Assignment |
| **PC4** | Fa0 | 192.168.40.2 | 255.255.255.0 | /24 | 192.168.40.1 | Static Host Assignment |
| **PC5** | Fa0 | 192.168.50.2 | 255.255.255.0 | /24 | 192.168.50.1 | Static Host Assignment |