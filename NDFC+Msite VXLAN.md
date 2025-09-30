# Introduction
This document describes how to configure Nexus 9000v VXLAN EVPN Multisite deployment with NDFC.


# Prerequisites
## Requirements

Cisco recommends that you have knowledge of these topics:
NDFC

Multi-Site VXLAN EVPN

CML simulator

## Components Used
1. CML 2.8
2. Virtual Nexus Dashboard 3.2.2f
3. NDFC 12.2.3
4. N9000v 10.5(3f)


# Configure
## Network Diagram
![image](https://github.com/zhengyili3/Network/blob/main/CML/Topo.png)

## High Level Steps
1. Create 3 Fabrics (2 "Data Center VXLAN EVPN" + 1 "Mutli-Site External Network")
2. Create MSD and move previous 3 fabrics into MSD
3. Create external Fabric
4. Create VRF/Network and attach them to Leaf switches.

## Configurations
### 1/ Connect Nexus9000v OOB to NDFC
1. CML and NDFC are installed on same esxi host.
2. CML external connecter "OOB-Bridge" bridge to Nexus Dashboard Management vmnic.
3. Connect all Nexus9000v mgmt ports and "OOB-Bridge" to OOB Switch.

### 2/ Create 2 "Data Center VXLAN EVPN" fabric on NDFC
#### 2.1 Define "Fabric Name" & "Fabric Type" and fill in "Genernal Parameters" such as BGP AS number,Fabric Interface Numbering, Underlay Protocol and Anycast Gateway MAC
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/1.png)

Fabric interface are links connected between leaf and spine switches.
Underlay Routing Protocol is used to setup leaf-spine connectivity.
Anycast Gateway MAC address is the server default gateway mac address.

#### 2.2 Define Reolication 
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/2.png)

Replication Mode for BUM traffic, we can use Multicast or Ingress Replication.
Chose Spine RR size

#### 2.3 Define Underlay Protocols
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/3.png)

Define 2 loopback ports, one for underlay routing protocol and another for VTEP source.

#### 2.4 Define Resources
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/4.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/5.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/6.png)

Underlay Routing Loopback IP Range: Used to underlay neighbor setup.
Underlay VTEP loopback IP Range: Used to setup nve peers.
Layer 2 VXLAN VNI Range: These are the VNIDs which  mapped to Vlans
Layer 3 VXLAN VNI Range: These are the Layer 3 VNIDs that mapped to layer 3 VNI Vlan to nn-segment

#### 2.5 Add Switch and Change Switch Role
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/add%20switch.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/add%20switch2.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/7.png)

Change switch role and "Recalculate and Deploy"

#### 2.6 Change interface access policy
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/edit%20interface.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/edit%20interface2.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/Site1/edit%20interface3.png)
We are using CSR1000v connect to Server Leaf, so configure e1/3 as access port.

#### 2.7 Refer previous steps create Site-2.

### 3/ Create ISN Fabric
#### 3.1 Create new fabric type "Multi-Site External Network" 
![image](https://github.com/zhengyili3/Network/blob/main/CML/ISN/1.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/ISN/2.png)

#### 3.2 Change ISN role to "Core Router"
![image](https://github.com/zhengyili3/Network/blob/main/CML/ISN/3.png)

#### 3.3 Create Loopback0 on both ISN nodes.
![image](https://github.com/zhengyili3/Network/blob/main/CML/ISN/5.png)
Create loopback 0 per ISN device, used for "Centralized_To_Route_Server" server list.
ISN1 172.31.0.1/32
ISN2 172.31.0.2/32

 
### 4/ Create VXLAN EVPN Multi-Site fabric "MSD"
#### 4.1 Create new fabric type "VXLAN EVPN Multi-Site"
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/1.png)
#### 4.2 Define DCI Type
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/2.png)

"Multi-Site Overlay IFC Deplioyment Method" contain 3 method:
1. "Manual": Requires explicit creation and management of overlay IFCs between border gateways or route servers.
2. "Direct_To_BGWS": Useful for straightforward topologies where BGWs connect directly to each other.
3. "Centralized_To_Route_Server": BGWs form overlay BGP connections to the route server(s), which act as a central point for inter-site routing.

#### 4.3 Define msite resource
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/3.png)

#### 4.4 Move Site-1&Site-2&ISN into MSD
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/3-2-1.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/3-2-2.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/3-2-3.png)


#### 4.5 Create multisite underlay links
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/4.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/5.png)

Edit other links between BGW and ISN.
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/5-4.png)

#### 4.6 Recalculate and Deploy
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/11.png)

### 5/ Create VRF
#### 5.1 Create VRF
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/12-1.png)

#### 5.2 Attach VRF to Leafs and BGWs
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/12.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/14.png)

#### 5.3 Create Network
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/15.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/16.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/18.png)

#### 5.4 Attach Networks to Server Leaf
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/19-2.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/20.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/21.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/22.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/23.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/24.png)

Attach vlan 2300 to Site1&Site2 Leaf1 e1/3. Same steps attach vlan 2301 to Site1&Site2 Leaf2 e1/3

#### 5.5 Attach Networks to BGWs
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/27.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/28.png)
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/29.png)

### 6/ Final Topology
![image](https://github.com/zhengyili3/Network/blob/main/CML/msite/final.png)

# Verify

Host IP addresses
Site1-Host1: 192.168.11.10
Site1-Host2: 192.168.12.10
Site1-Host1: 192.168.11.11
Site2-Host2: 192.168.12.11


## 1. Intra-Site Ping
```
cisco@Site1-Host1:~$ ping 192.168.12.10 -c 5
PING 192.168.12.10 (192.168.12.10) 56(84) bytes of data.
64 bytes from 192.168.12.10: icmp_seq=1 ttl=62 time=10.5 ms
64 bytes from 192.168.12.10: icmp_seq=2 ttl=62 time=11.3 ms
64 bytes from 192.168.12.10: icmp_seq=3 ttl=62 time=10.2 ms
64 bytes from 192.168.12.10: icmp_seq=4 ttl=62 time=12.1 ms
64 bytes from 192.168.12.10: icmp_seq=5 ttl=62 time=7.35 ms

--- 192.168.12.10 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4007ms
rtt min/avg/max/mdev = 7.346/10.289/12.069/1.610 ms
```

## 2. Inter-Site Ping
```
cisco@Site1-Host1:~$ ping 192.168.11.11 -c 5
PING 192.168.11.11 (192.168.11.11) 56(84) bytes of data.
64 bytes from 192.168.11.11: icmp_seq=1 ttl=64 time=25.5 ms
64 bytes from 192.168.11.11: icmp_seq=2 ttl=64 time=21.2 ms
64 bytes from 192.168.11.11: icmp_seq=3 ttl=64 time=22.9 ms
64 bytes from 192.168.11.11: icmp_seq=4 ttl=64 time=23.6 ms
64 bytes from 192.168.11.11: icmp_seq=5 ttl=64 time=29.3 ms

--- 192.168.11.11 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4008ms
rtt min/avg/max/mdev = 21.161/24.474/29.329/2.792 ms


cisco@Site1-Host1:~$ ping 192.168.12.11 -c 5
PING 192.168.12.11 (192.168.12.11) 56(84) bytes of data.
64 bytes from 192.168.12.11: icmp_seq=1 ttl=60 time=26.4 ms
64 bytes from 192.168.12.11: icmp_seq=2 ttl=60 time=28.9 ms
64 bytes from 192.168.12.11: icmp_seq=3 ttl=60 time=23.4 ms
64 bytes from 192.168.12.11: icmp_seq=4 ttl=60 time=27.0 ms
64 bytes from 192.168.12.11: icmp_seq=5 ttl=60 time=35.0 ms

--- 192.168.12.11 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 23.423/28.131/34.982/3.845 ms
```