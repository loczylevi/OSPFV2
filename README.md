# OSPFV2



## R1
```bash
interface GigabitEthernet0/0
ip address 192.168.1.254 255.255.255.0

interface Serial0/3/0
ip address 10.1.1.1 255.255.255.252

interface Serial0/3/1
ip address 10.1.2.1 255.255.255.252

router ospf 1
router-id 1.1.1.1
passive-interface GigabitEthernet0/0
network 192.168.1.0 0.0.0.255 area 0
network 10.1.1.0 0.0.0.3 area 0
network 10.1.2.0 0.0.0.3 area 0

```
## R3
```bash
!
interface GigabitEthernet0/0
 ip address 192.168.3.254 255.255.255.0

interface Serial0/3/0
 ip address 10.1.3.1 255.255.255.252
 clock rate 2000000
!
interface Serial0/3/1
 ip address 10.1.2.2 255.255.255.252
 clock rate 2000000
!
router ospf 1
 router-id 2.2.2.2
 log-adjacency-changes
 passive-interface GigabitEthernet0/0
 network 10.1.3.0 0.0.0.3 area 0
 network 10.1.2.0 0.0.0.3 area 0
!
```
_passive interface felé nem hirdet OSPFV hello üzeneteket_

## R2
```bash
!
interface GigabitEthernet0/0
 ip address 192.168.2.1 255.255.255.0
!
!
interface Serial0/3/0
 ip address 10.1.1.2 255.255.255.252
 clock rate 2000000
!
interface Serial0/3/1
 ip address 10.1.3.2 255.255.255.252
!
router ospf 1
 router-id 3.3.3.3
 log-adjacency-changes
default-information originate 
 network 10.1.1.0 0.0.0.3 area 0
 network 10.1.3.0 0.0.0.3 area 0
 network 192.168.2.0 0.0.0.255 area 0
!

```
_default-information originate hirdeti hogy ennél a router egyik lábánál van az internet_

## Check kód
```bash
sh ip route o
sh ip os nei
```

## Clear command
```bash
clear ip os pro
```


## Satic route
```bash
ip route 0.0.0.0 0.0.0.0 201.1.1.1 1
ip route 0.0.0.0 0.0.0.0 201.1.1.1 150
```
_A legvégén lévő egyes az  prioritás_
_150 esetén lebegő utvonalról beszélünk_
