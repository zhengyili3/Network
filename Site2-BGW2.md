# Site2-BGW2# show ip int brief vrf all

IP Interface Status for VRF "default"(1)
Interface            IP Address      Interface Status
Lo0                  10.2.2.1        protocol-up/link-up/admin-up       
Lo1                  10.3.2.3        protocol-up/link-up/admin-up       
Lo100                10.10.0.2       protocol-up/link-up/admin-up       
Eth1/1               10.4.2.11       protocol-up/link-up/admin-up       
Eth1/2               10.4.2.9        protocol-up/link-up/admin-up       
Eth1/3               10.10.1.5       protocol-up/link-up/admin-up       
Eth1/4               10.10.1.7       protocol-up/link-up/admin-up       

IP Interface Status for VRF "management"(2)
Interface            IP Address      Interface Status
mgmt0                192.168.1.25    protocol-up/link-up/admin-up       

IP Interface Status for VRF "egress-loadbalance-resolution-"(3)
Interface            IP Address      Interface Status

IP Interface Status for VRF "green"(4)
Interface            IP Address      Interface Status
Vlan2300             forward-enabled protocol-up/link-up/admin-up   

# Site2-BGW2# show bgp l2vpn evpn summary 
BGP summary information for VRF default, address family L2VPN EVPN
BGP router identifier 10.2.2.1, local AS number 65333
BGP table version is 220, L2VPN EVPN config peers 4, capable peers 4
36 network entries and 51 paths using 13208 bytes of memory
BGP attribute entries [40/14720], BGP AS path entries [1/10]
BGP community entries [0/0], BGP clusterlist entries [4/16]

Neighbor        V    AS    MsgRcvd    MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
10.2.2.4        4 65333        473        450      220    0    0 07:17:07 5         
10.2.2.5        4 65333        465        448      220    0    0 07:15:01 5         
172.16.0.1      4 65222        479        449      220    0    0 07:17:34 10        
172.16.0.2      4 65222        481        450      220    0    0 07:18:51 10        

Neighbor        T    AS Type-1     Type-2     Type-3     Type-4     Type-5     Type-6     Type-7     Type-8     Type-12   
10.2.2.4        I 65333 0          3          0          0          2          0          0          0          0         
10.2.2.5        I 65333 0          3          0          0          2          0          0          0          0         
172.16.0.1      E 65222 0          6          2          0          2          0          0          0          0         
172.16.0.2      E 65222 0          6          2          0          2          0          0          0          0     

# Site2-BGW2(config)# show nve peers
Interface Peer-IP                                 State LearnType Uptime   Router-Mac       
--------- --------------------------------------  ----- --------- -------- -----------------
nve1      10.3.1.1                                Up    CP        07:20:22 n/a              
nve1      10.3.2.1                                Up    CP        07:18:56 52f7.4e2a.1b08   
nve1      10.3.2.2                                Up    CP        07:18:56 520f.0181.1b08   
nve1      10.10.0.1                               Up    CP        07:17:05 0200.0a0a.0001   

# Site2-BGW2(config)# show bgp l2vpn evpn
BGP routing table information for VRF default, address family L2VPN EVPN
BGP table version is 220, Local Router ID is 10.2.2.1
Status: s-suppressed, x-deleted, S-stale, d-dampened, h-history, *-valid, >-best
Path type: i-internal, e-external, c-confed, l-local, a-aggregate, r-redist, I-injected
Origin codes: i - IGP, e - EGP, ? - incomplete, | - multipath, & - backup, 2 - best2

   Network            Next Hop            Metric     LocPrf     Weight Path
Route Distinguisher: 65111:30001
*>e[2]:[0]:[0]:[48]:[5254.0083.eee7]:[0]:[0.0.0.0]/216
                      10.10.0.1                                      0 65222 65111 i
* e                   10.10.0.1                                      0 65222 65111 i
* e[2]:[0]:[0]:[48]:[5254.0083.eee7]:[32]:[192.168.11.10]/272
                      10.10.0.1                                      0 65222 65111 i
*>e                   10.10.0.1                                      0 65222 65111 i

Route Distinguisher: 65111:30002
*>e[2]:[0]:[0]:[48]:[5254.00df.c29d]:[0]:[0.0.0.0]/216
                      10.10.0.1                                      0 65222 65111 i
* e                   10.10.0.1                                      0 65222 65111 i
* e[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.10.0.1                                      0 65222 65111 i
*>e                   10.10.0.1                                      0 65222 65111 i

Route Distinguisher: 65111:50000
* e[5]:[0]:[0]:[24]:[192.168.11.0]/224
                      10.10.0.1                                      0 65222 65111 ?
*>e                   10.10.0.1                                      0 65222 65111 ?
* e[5]:[0]:[0]:[24]:[192.168.12.0]/224
                      10.10.0.1                                      0 65222 65111 ?
*>e                   10.10.0.1                                      0 65222 65111 ?

Route Distinguisher: 10.2.1.1:35068
* e[2]:[0]:[0]:[48]:[524b.c67b.1b08]:[0]:[0.0.0.0]/216
                      10.3.1.1                                       0 65222 65111 i
*>e                   10.3.1.1                                       0 65222 65111 i
* e[3]:[0]:[32]:[10.3.1.1]/88
                      10.3.1.1                                       0 65222 65111 i
*>e                   10.3.1.1                                       0 65222 65111 i

Route Distinguisher: 10.2.1.1:35069
* e[2]:[0]:[0]:[48]:[524b.c67b.1b08]:[0]:[0.0.0.0]/216
                      10.3.1.1                                       0 65222 65111 i
*>e                   10.3.1.1                                       0 65222 65111 i
* e[3]:[0]:[32]:[10.3.1.1]/88
                      10.3.1.1                                       0 65222 65111 i
*>e                   10.3.1.1                                       0 65222 65111 i

Route Distinguisher: 10.2.2.1:35068    (L2VNI 30001)
*>e[2]:[0]:[0]:[48]:[524b.c67b.1b08]:[0]:[0.0.0.0]/216
                      10.3.1.1                                       0 65222 65111 i
*>e[2]:[0]:[0]:[48]:[5254.0083.eee7]:[0]:[0.0.0.0]/216
                      10.10.0.1                                      0 65222 65111 i
*>i[2]:[0]:[0]:[48]:[5254.0087.8afc]:[0]:[0.0.0.0]/216
                      10.3.2.1                          100          0 i
*>l[2]:[0]:[0]:[48]:[52a1.26d5.1b08]:[0]:[0.0.0.0]/216
                      10.3.2.3                          100      32768 i
*>e[2]:[0]:[0]:[48]:[5254.0083.eee7]:[32]:[192.168.11.10]/272
                      10.10.0.1                                      0 65222 65111 i
*>e[3]:[0]:[32]:[10.3.1.1]/88
                      10.3.1.1                                       0 65222 65111 i
*>l[3]:[0]:[32]:[10.3.2.3]/88
                      10.3.2.3                          100      32768 i

Route Distinguisher: 10.2.2.1:35069    (L2VNI 30002)
*>e[2]:[0]:[0]:[48]:[524b.c67b.1b08]:[0]:[0.0.0.0]/216
                      10.3.1.1                                       0 65222 65111 i
*>i[2]:[0]:[0]:[48]:[5254.0074.e871]:[0]:[0.0.0.0]/216
                      10.3.2.2                          100          0 i
*>e[2]:[0]:[0]:[48]:[5254.00df.c29d]:[0]:[0.0.0.0]/216
                      10.10.0.1                                      0 65222 65111 i
*>l[2]:[0]:[0]:[48]:[52a1.26d5.1b08]:[0]:[0.0.0.0]/216
                      10.3.2.3                          100      32768 i
*>i[2]:[0]:[0]:[48]:[5254.0074.e871]:[32]:[192.168.12.11]/272
                      10.3.2.2                          100          0 i
*>e[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.10.0.1                                      0 65222 65111 i
*>e[3]:[0]:[32]:[10.3.1.1]/88
                      10.3.1.1                                       0 65222 65111 i
*>l[3]:[0]:[32]:[10.3.2.3]/88
                      10.3.2.3                          100      32768 i

Route Distinguisher: 10.2.2.2:4
* i[5]:[0]:[0]:[24]:[192.168.11.0]/224
                      10.3.2.1                 0        100          0 ?
*>i                   10.3.2.1                 0        100          0 ?

Route Distinguisher: 10.2.2.2:35068
*>i[2]:[0]:[0]:[48]:[5254.0087.8afc]:[0]:[0.0.0.0]/216
                      10.3.2.1                          100          0 i
* i                   10.3.2.1                          100          0 i

Route Distinguisher: 10.2.2.3:4
* i[5]:[0]:[0]:[24]:[192.168.12.0]/224
                      10.3.2.2                 0        100          0 ?
*>i                   10.3.2.2                 0        100          0 ?

Route Distinguisher: 10.2.2.3:35069
*>i[2]:[0]:[0]:[48]:[5254.0074.e871]:[0]:[0.0.0.0]/216
                      10.3.2.2                          100          0 i
* i                   10.3.2.2                          100          0 i
*>i[2]:[0]:[0]:[48]:[5254.0074.e871]:[32]:[192.168.12.11]/272
                      10.3.2.2                          100          0 i
* i                   10.3.2.2                          100          0 i

Route Distinguisher: 10.2.2.1:27001   (ES [0300.0000.00ff.3500.0309 0])
*>l[4]:[0300.0000.00ff.3500.0309]:[32]:[10.3.2.3]/136
                      10.3.2.3                          100      32768 i

Route Distinguisher: 10.2.2.1:4    (L3VNI 50000)
*>i[2]:[0]:[0]:[48]:[5254.0074.e871]:[32]:[192.168.12.11]/272
                      10.3.2.2                          100          0 i
*>e[2]:[0]:[0]:[48]:[5254.0083.eee7]:[32]:[192.168.11.10]/272
                      10.10.0.1                                      0 65222 65111 i
*>e[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.10.0.1                                      0 65222 65111 i
*>l[5]:[0]:[0]:[24]:[192.168.11.0]/224
                      10.3.2.3                 0        100          0 ?
*>l[5]:[0]:[0]:[24]:[192.168.12.0]/224
                      10.3.2.3                 0        100          0 ?
