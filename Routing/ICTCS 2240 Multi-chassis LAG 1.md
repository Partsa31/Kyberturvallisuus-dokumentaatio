
![[Pasted image 20260203135226.png]]


DLS1
```r
vlan 4046
   name MLAG_PEERLINK
   trunk group MLAG
!
!
interface Vlan4046
   no autostate
   ip address 10.46.46.1/24
!

interface Ethernet 6-7
   description MLAG Peer-Link
   channel-group 4046 mode active
   no shutdown
!

interface Port-Channel4046
   switchport access vlan 4046
!

spanning-tree mode none
!

mlag configuration 
domain-id BLOCK1
local-interface vlan 4046
peer-address 10.46.46.2
peer-link Port-Channel 4046

vlan 8
name ACCESS
!
interface Port-Channel112
	switchport mode trunk
	mlag112
!
interface eth4
channel-group 112 mode active
no shutdown
!

interface eth5
channel-group 112 mode active
no shutdown
!
int vlan8
ip address 10.46.108.254/24
!
int vlan 8
isis enable LAN
isis passive
!
interface vxlan 1
vxlan source-interface loopback0
vxlan vlan 8 vni 1008
vxlan flood vtep 192.168.46.2
!

ip virtual-router mac-address 02:00:00:00:00:46
interface vlan 8
ip virtual-router address 10.46.108.1


```

DLS2
```r
vlan 4046
   name MLAG_PEERLINK
   trunk group MLAG
!
!
interface Vlan4046
   no autostate
   ip address 10.46.46.2/24
!

interface Ethernet 6-7
   description MLAG Peer-Link
   channel-group 4046 mode active
   no shutdown
!

interface Port-Channel4046
   switchport access vlan 4046
!

spanning-tree mode none
!

mlag configuration 
domain-id BLOCK1
local-interface vlan 4046
peer-address 10.46.46.1
peer-link Port-Channel 4046
!
vlan 8
name ACCESS
!
interface Port-Channel122
	switchport mode trunk
	mlag112
!
interface eth4
channel-group 122 mode active
no shutdown
!

interface eth5
channel-group 122 mode active
no shutdown
!
int vlan8
ip address 10.46.108.253/24
!
int vlan 8
isis enable LAN 
isis passive
!
interface vxlan 1
vxlan source-interface loopback0
vxlan vlan 8 vni 1008
vxlan flood vtep 192.168.46.1
!

ip virtual-router mac-address 02:00:00:00:00:46
interface vlan 8
ip virtual-router address 10.46.108.1


```


DLS3
```r
vlan 4046
   name MLAG_PEERLINK
   trunk group MLAG
!
!
interface Vlan4046
   no autostate
   ip address 10.46.46.3/24
!

interface Ethernet 6-7
   description MLAG Peer-Link
   channel-group 4046 mode active
   no shutdown
!

interface Port-Channel4046
   switchport access vlan 4046
!

spanning-tree mode none
!

mlag configuration 
domain-id BLOCK2
local-interface vlan 4046
peer-address 10.46.46.4
peer-link Port-Channel 4046
!
vlan 8
name ACCESS
!
interface Port-Channel212
	switchport mode trunk
	mlag212
!
interface eth4
channel-group 212 mode active
no shutdown
!

interface eth5
channel-group 212 mode active
no shutdown
!
int vlan8
ip address 10.46.208.254/24
!
int vlan 8
isis enable LAN 
isis passive
!
interface vxlan 1
vxlan source-interface loopback0
vxlan vlan 8 vni 1008
vxlan flood vtep 192.168.46.4
!

ip virtual-router mac-address 02:00:00:00:00:46
interface vlan 8
ip virtual-router address 10.46.108.1




```
DLS4
```r
vlan 4046
   name MLAG_PEERLINK
   trunk group MLAG
!
!
interface Vlan4046
   no autostate
   ip address 10.46.46.4/24
!

interface Ethernet 6-7
   description MLAG Peer-Link
   channel-group 4046 mode active
   no shutdown
!

interface Port-Channel4046
   switchport access vlan 4046
!

spanning-tree mode none
!

mlag configuration 
domain-id BLOCK2
local-interface vlan 4046
peer-address 10.46.46.4
peer-link Port-Channel 4046
!
vlan 8
name ACCESS
!
interface Port-Channel222
	switchport mode trunk
	mlag222
!
interface eth4
channel-group 222 mode active
no shutdown
!

interface eth5
channel-group 222 mode active
no shutdown
!
int vlan8
ip address 10.46.208.253/24
!
int vlan 8
isis enable LAN isis passive
!
interface vxlan 1
vxlan source-interface loopback0
vxlan vlan 8 vni 1008
vxlan flood vtep 192.168.46.2
!

ip virtual-router mac-address 02:00:00:00:00:46
interface vlan 8
ip virtual-router address 10.46.108.1



```
ALS1

```r

vlan 8
name ACCESS
!
interface lag 112
	no shutdown
	no routing 
	vlan trunk native 1
	vlan trunk allowed all
	lacp mode passive
	
!
interface 1/1/1-1/1/2
	no shutdown
	lag 112

!
!
int 1/1/3
no routing 
no shutdown
vlan access 8
!
```
ALS2
```r

vlan 8
name ACCESS
!
interface lag 122
	no shutdown
	no routing 
	vlan trunk native 1
	vlan trunk allowed all
	lacp mode passive
!

interface 1/1/1-1/1/2
	no shutdown
	lag 122

!
int 1/1/3
no routing 
no shutdown
vlan access 8
!
```

ALS3
```r
vlan 8
name ACCESS
!
interface lag 212
	no shutdown
	no routing 
	vlan trunk native 1
	vlan trunk allowed all
	lacp mode passive
!


interface 1/1/1-1/1/2
	no shutdown
	lag 212
!

int 1/1/3
no routing 
no shutdown
vlan access 8
!
```
ALS4
```r
vlan 8
name ACCESS
!
interface lag 222
	no shutdown
	no routing 
	vlan trunk native 1
	vlan trunk allowed all
	lacp mode passive
!

!
interface 1/1/1-1/1/2
	no shutdown
	lag 222

!
int 1/1/3
no routing 
no shutdown
vlan access 8
!
```