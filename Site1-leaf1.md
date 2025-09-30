##### Site1-Leaf1# show ip int brief vrf all

IP Interface Status for VRF "default"(1)
Interface            IP Address      Interface Status
Lo0                  10.2.1.4        protocol-up/link-up/admin-up       
Lo1                  10.3.1.3        protocol-up/link-up/admin-up       
Eth1/1               10.4.1.0        protocol-up/link-up/admin-up       
Eth1/2               10.4.1.4        protocol-up/link-up/admin-up       

IP Interface Status for VRF "management"(2)
Interface            IP Address      Interface Status
mgmt0                192.168.1.11    protocol-up/link-up/admin-up       

IP Interface Status for VRF "egress-loadbalance-resolution-"(3)
Interface            IP Address      Interface Status

IP Interface Status for VRF "green"(4)
Interface            IP Address      Interface Status
Vlan2300             forward-enabled protocol-up/link-up/admin-up       
Vlan2301             192.168.11.1    protocol-up/link-up/admin-up   

##### Site1-Leaf1# show bgp l2vpn evpn summary 
BGP summary information for VRF default, address family L2VPN EVPN
BGP router identifier 10.2.1.4, local AS number 65111
BGP table version is 79, L2VPN EVPN config peers 2, capable peers 2
13 network entries and 18 paths using 4732 bytes of memory
BGP attribute entries [18/6624], BGP AS path entries [1/10]
BGP community entries [0/0], BGP clusterlist entries [4/16]

Neighbor        V    AS    MsgRcvd    MsgSent   TblVer  InQ OutQ Up/Down  State/PfxRcd
10.2.1.2        4 65111        483        449       79    0    0 07:17:42 5         
10.2.1.5        4 65111        482        448       79    0    0 07:17:13 5         

Neighbor        T    AS Type-1     Type-2     Type-3     Type-4     Type-5     Type-6     Type-7     Type-8     Type-12   
10.2.1.2        I 65111 0          4          0          0          1          0          0          0          0         
10.2.1.5        I 65111 0          4          0          0          1          0          0          0          0     

##### Site1-Leaf1# show nve peers
Interface Peer-IP                                 State LearnType Uptime   Router-Mac       
--------- --------------------------------------  ----- --------- -------- -----------------
nve1      10.3.1.1                                Up    CP        07:19:24 n/a              
nve1      10.3.1.2                                Up    CP        07:19:24 5205.58e4.1b08   
nve1      10.10.0.1                               Up    CP        06:23:06 0200.0a0a.0001   

##### Site1-Leaf1# show bgp l2vpn evpn
BGP routing table information for VRF default, address family L2VPN EVPN
BGP table version is 79, Local Router ID is 10.2.1.4
Status: s-suppressed, x-deleted, S-stale, d-dampened, h-history, *-valid, >-best
Path type: i-internal, e-external, c-confed, l-local, a-aggregate, r-redist, I-injected
Origin codes: i - IGP, e - EGP, ? - incomplete, | - multipath, & - backup, 2 - best2

   Network            Next Hop            Metric     LocPrf     Weight Path
Route Distinguisher: 65111:30001
* i[2]:[0]:[0]:[48]:[5254.0087.8afc]:[0]:[0.0.0.0]/216
                      10.10.0.1                         100          0 65222 65333 i
*>i                   10.10.0.1                         100          0 65222 65333 i

Route Distinguisher: 65111:30002
* i[2]:[0]:[0]:[48]:[5254.0074.e871]:[32]:[192.168.12.11]/272
                      10.10.0.1                         100          0 65222 65333 i
*>i                   10.10.0.1                         100          0 65222 65333 i

Route Distinguisher: 10.2.1.1:35068
* i[2]:[0]:[0]:[48]:[524b.c67b.1b08]:[0]:[0.0.0.0]/216
                      10.3.1.1                          100          0 i
*>i                   10.3.1.1                          100          0 i

Route Distinguisher: 10.2.1.3:4
* i[5]:[0]:[0]:[24]:[192.168.12.0]/224
                      10.3.1.2                 0        100          0 ?
*>i                   10.3.1.2                 0        100          0 ?

Route Distinguisher: 10.2.1.3:35069
* i[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.3.1.2                          100          0 i
*>i                   10.3.1.2                          100          0 i

Route Distinguisher: 10.2.1.4:35068    (L2VNI 30001)
*>i[2]:[0]:[0]:[48]:[524b.c67b.1b08]:[0]:[0.0.0.0]/216
                      10.3.1.1                          100          0 i
*>l[2]:[0]:[0]:[48]:[5254.0083.eee7]:[0]:[0.0.0.0]/216
                      10.3.1.3                          100      32768 i
*>i[2]:[0]:[0]:[48]:[5254.0087.8afc]:[0]:[0.0.0.0]/216
                      10.10.0.1                         100          0 65222 65333 i
*>l[2]:[0]:[0]:[48]:[5254.0083.eee7]:[32]:[192.168.11.10]/272
                      10.3.1.3                          100      32768 i

Route Distinguisher: 10.2.1.4:4    (L3VNI 50000)
*>i[2]:[0]:[0]:[48]:[5254.0074.e871]:[32]:[192.168.12.11]/272
                      10.10.0.1                         100          0 65222 65333 i
*>i[2]:[0]:[0]:[48]:[5254.00df.c29d]:[32]:[192.168.12.10]/272
                      10.3.1.2                          100          0 i
*>l[5]:[0]:[0]:[24]:[192.168.11.0]/224
                      10.3.1.3                 0        100      32768 ?
*>i[5]:[0]:[0]:[24]:[192.168.12.0]/224
                      10.3.1.2                 0        100          0 ?