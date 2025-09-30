# Site2-Leaf2# show ip int brief vrf all

IP Interface Status for VRF "default"(1)
Interface            IP Address      Interface Status
Lo0                  10.2.2.3        protocol-up/link-up/admin-up       
Lo1                  10.3.2.2        protocol-up/link-up/admin-up       
Eth1/1               10.4.2.2        protocol-up/link-up/admin-up       
Eth1/2               10.4.2.4        protocol-up/link-up/admin-up       

IP Interface Status for VRF "management"(2)
Interface            IP Address      Interface Status
mgmt0                192.168.1.22    protocol-up/link-up/admin-up       

IP Interface Status for VRF "egress-loadbalance-resolution-"(3)
Interface            IP Address      Interface Status

IP Interface Status for VRF "green"(4)
Interface            IP Address      Interface Status
Vlan2300             forward-enabled protocol-up/link-up/admin-up       
Vlan2302             192.168.12.1    protocol-up/link-up/admin-up  

# Site2-Leaf2# show bgp l2vpn evpn summary 
BGP summary information for VRF default, address family L2VPN EVPN
BGP router identifier 10.2.2.3, local AS number 65333
BGP table version is 76, L2VPN EVPN config peers 2, capable peers 2
14 network entries and 19 paths using 4992 bytes of memory
BGP attribute entries [19/6992], BGP AS path entries [1/10]
BGP community entries [0/0], BGP clusterlist entries [4/16]

Neighbor        V    AS    MsgRcvd    MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
10.2.2.4        4 65333        484        448       76    0    0 07:17:10 5         
10.2.2.5        4 65333        482        446       76    0    0 07:14:24 5         

Neighbor        T    AS Type-1     Type-2     Type-3     Type-4     Type-5     Type-6     Type-7     Type-8     Type-12   
10.2.2.4        I 65333 0          4          0          0          1          0          0          0          0         
10.2.2.5        I 65333 0          4          0          0          1          0          0          0          0         

# Site2-Leaf2# show nve peers
Interface Peer-IP                                 State LearnType Uptime   Router-Mac       
--------- --------------------------------------  ----- --------- -------- -----------------
nve1      10.3.2.1                                Up    CP        07:18:56 52f7.4e2a.1b08   
nve1      10.3.2.3                                Up    CP        07:18:56 n/a              
nve1      10.10.0.2                               Up    CP        06:22:10 0200.0a0a.0002 

# Site2-Leaf2# show bgp l2vpn evpn
BGP routing table information for VRF default, address family L2VPN EVPN
BGP table version is 76, Local Router ID is 10.2.2.3
Status: s-suppressed, x-deleted, S-stale, d-dampened, h-history, *-valid, >-best
Path type: i-internal, e-external, c-confed, l-local, a-aggregate, r-redist, I-injected
Origin codes: i - IGP, e - EGP, ? - incomplete, | - multipath, & - backup, 2 - best2

   Network            Next Hop            Metric     LocPrf     Weight Path
Route Distinguisher: 65333:30001
*>i[2]:[0]:[0]:[48]:[5254.0083.eee7]:[32]:[192.168.11.10]/272
                      10.10.0.2                         100          0 65222 65111 i
* i                   10.10.0.2                         100          0 65222 65111 i

Route Distinguisher: 65333:30002
* i[2]:[0]:[0]:[48]:[5254.00df.c29d]:[0]:[0.0.0.0]/216
                      10.10.0.2                         100          0 65222 65111 i
*>i                   10.10.0.2                         100          0 65222 65111 i
*>i[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.10.0.2                         100          0 65222 65111 i
* i                   10.10.0.2                         100          0 65222 65111 i

Route Distinguisher: 10.2.2.1:35069
* i[2]:[0]:[0]:[48]:[52a1.26d5.1b08]:[0]:[0.0.0.0]/216
                      10.3.2.3                          100          0 i
*>i                   10.3.2.3                          100          0 i

Route Distinguisher: 10.2.2.2:4
* i[5]:[0]:[0]:[24]:[192.168.11.0]/224
                      10.3.2.1                 0        100          0 ?
*>i                   10.3.2.1                 0        100          0 ?

Route Distinguisher: 10.2.2.3:35069    (L2VNI 30002)
*>l[2]:[0]:[0]:[48]:[5254.0074.e871]:[0]:[0.0.0.0]/216
                      10.3.2.2                          100      32768 i
*>i[2]:[0]:[0]:[48]:[5254.00df.c29d]:[0]:[0.0.0.0]/216
                      10.10.0.2                         100          0 65222 65111 i
*>i[2]:[0]:[0]:[48]:[52a1.26d5.1b08]:[0]:[0.0.0.0]/216
                      10.3.2.3                          100          0 i
*>l[2]:[0]:[0]:[48]:[5254.0074.e871]:[32]:[192.168.12.11]/272
                      10.3.2.2                          100      32768 i
*>i[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.10.0.2                         100          0 65222 65111 i

Route Distinguisher: 10.2.2.3:4    (L3VNI 50000)
*>i[2]:[0]:[0]:[48]:[5254.0083.eee7]:[32]:[192.168.11.10]/272
                      10.10.0.2                         100          0 65222 65111 i
*>i[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.10.0.2                         100          0 65222 65111 i
*>i[5]:[0]:[0]:[24]:[192.168.11.0]/224
                      10.3.2.1                 0        100          0 ?
*>l[5]:[0]:[0]:[24]:[192.168.12.0]/224
                      10.3.2.2                 0        100      32768 ?
