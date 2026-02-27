![[Pasted image 20260227221005.png]]


interface Ethernet 2
ipv6 enable 
ipv6 address fe80::46:1 link-local


interface Ethernet 3
ipv6 enable 
ipv6 address fe80::46:3 link-local

interface loopback0
ipv6 enable 
ipv6 address 2001:db8:46::3/128 

global prefix
interface Ethernet 3
ipv6 enable 
ipv6 address 2001:db8:46:2::1/64

ip route 
ipv6 route 2001:db8:46::1/128 Ethernet 1 fe80::46:1
ipv6 route 2001:db8:46::2/128 Ethernet 1 fe80::46:2

ipv6 route 2001:db8:46::3/128 Ethernet 2 fe80::46:3

ipv6 route 2001:db8:46:3::/64  Ethernet 2 fe80::46:3