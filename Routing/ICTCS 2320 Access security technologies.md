
![[Pasted image 20260227221132.png]]
Kali
````r
sysctl -w net.ipv6.conf.all.disable_ipv6=0 
sysctl -w net.ipv6.conf.all.forwarding=1

ip addr add 2001:db8:bad::1/64 dev eth0 
ip addr add fe80::bad/64 dev eth0 scope link


`````



ALS1B

```r
access-list ipv6 IP6DENY deny ipv6 any any 
! 

interface 1/1/3-1/1/7 
apply access-list ipv6 IP6DENY in 
apply access-list ipv6 IP6DENY out 
!


NN46-ALS1(config)# dhcpv4-snooping 
NN46-ALS1(config)# vlan 32
!
dhcpv4-snooping 
NN46-ALS1(config-vlan-32)# int 1/1/1-1/1/2
NN46-ALS1(config-if-<1/1/1-1/1/2>)# dhcpv4-snooping trust


NN46-ALS1(config)# access-list ipv6 IP6DENY
NN46-ALS1(config-acl-ipv6)# deny ipv6 any any
NN46-ALS1(config-acl-ipv6)# ^C

NN46-ALS1(config-acl-ipv6)# ^C

NN46-ALS1(config-acl-ipv6)# ex
NN46-ALS1(config)# interface 1/1/3-1/1/7
NN46-ALS1(config-if-<1/1/3-1/1/7>)#  apply access-list ipv6 IP6DENY in
NN46-ALS1(config-if-<1/1/3-1/1/7>)#     apply access-list ipv6 IP6DENY out
NN46-ALS1(config-if-<1/1/3-1/1/7>)# ex
NN46-ALS1(config)# dhcpv4-snooping 
NN46-ALS1(config)# vlan 32
NN46-ALS1(config-vlan-32)# dhcpv4-snooping 
NN46-ALS1(config-vlan-32)# int 1/1/1-1/1/2
NN46-ALS1(config-if-<1/1/1-1/1/2>)# dhcpv4-snooping trust
NN46-ALS1(config-if-<1/1/1-1/1/2>)# ex
NN46-ALS1(config)# port-access port-security enable 
NN46-ALS1(config)# port-access event-log 
% Command incomplete.
NN46-ALS1(config)# port-access event-log client 
NN46-ALS1(config)# int 1/1/3-1/1/7
NN46-ALS1(config-if-<1/1/3-1/1/7>)# port-access allow-flood-traffic disable 
wn 6-ALS1(config-if-<1/1/3-1/1/7>)# port-access security violation action shutdow
NN46-ALS1(config-if-<1/1/3-1/1/7>)# port-access port-security 
NN46-ALS1(config-if-portsecurity)# enable 
NN46-ALS1(config-if-portsecurity)# client-limit 1
NN46-ALS1(config-if-portsecurity)# ex
NN46-ALS1(config-if-<1/1/3-1/1/7>)# ex
NN46-ALS1(config)# int 1/1/3-1/1/7
NN46-ALS1(config-if-<1/1/3-1/1/7>)# dhcpv4-snooping max-bindings 1
NN46-ALS1(config-if-<1/1/3-1/1/7>)# ex
NN46-ALS1(config)# ex
% Ambiguous command.
NN46-ALS1(config)# ex
% Ambiguous command.
NN46-ALS1(config)# 




```


