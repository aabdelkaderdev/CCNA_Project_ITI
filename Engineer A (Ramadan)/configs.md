## BSE-SW-Core-1-ALEX
A2.1 ! building the LACP on SW1
en
conf t

int r f0/2-3
channel-pro lacp
channel-group 1 mode active
switchport mode trunk
no shut
exit

sh etherchannel summary

A2.2 ! classfying ports as trunk/access ports
int r f0/1-8
switchport mode trunk
exit
end

sh interfaces trunk
! in the screenshot we can see the f0/1 is not shown  because its down yet, and f0/2,3 are not shown because they are now a logically one port because of etherchannel so they are P01 !


A2.3 ! making the vtp server
vtp mode server
vtp domain Alex
vtp password Alex
vtp version 2

! creatign the vlans
vlan 10
name Adminstration

vlan 20
name HR

vlan 30
name Clinical_Services

vlan 40
name IP_Camera

vlan 50
name Access_Control

vlan 60
name Internal_Servers


vlan 70
name DMZ_Public_Web_Server

end
sh vlan brief 

A2.6 ! making STP primary
en
conf t

spanning-tree vlan 10,20,30,40,50,60,70 root primary

end
show spanning-tree

A2.8 ! SVI and default route
en
conf t

int vlan 10
ip add 172.16.1.4 255.255.255.240
exit

ip default-gateway 172.16.1.1

end

show ip interface vlan 10
sh running | include default-gateway




A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config









## BSE-SW-Core-1-ALEX
A2.1! building the LACP on SW2
en
conf t

int r f0/2-3
channel-pro lacp
channel-group 1 mode active
switchport mode trunk
no shut
exit

sh etherchannel summary

A2.2! classfying ports as trunk/access ports
int r f0/1-8
switchport mode trunk
exit
end

sh interfaces trunk
! in the screenshot we can see the f0/1 is not shown  because its down yet, and f0/2,3 are not shown because they are now a logically one port because of etherchannel so they are P01!


A2.3 ! making the vtp server
vtp mode server
vtp domain Alex
vtp password Alex
vtp version 2

! creatign the vlans
vlan 10
name Adminstration

vlan 20
name HR

vlan 30
name Clinical_Services

vlan 40
name IP_Camera

vlan 50
name Access_Control

vlan 60
name Internal_Servers


vlan 70
name DMZ_Public_Web_Server

end
sh vlan brief 

A2.6 ! making STP primary
en
conf t

spanning-tree vlan 10,20,30,40,50,60,70 root secondary

end
show spanning-tree

A2.8 ! SVI and default route
en
conf t

int vlan 10
ip add 172.16.1.5 255.255.255.240
exit

ip default-gateway 172.16.1.1

end

show ip interface vlan 10
sh running | include default-gateway






A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config



## BSE-SW-Admin-ALEX
A2.4 ! creating the vtp clients
en
conf t

vtp mode client
vtp domain Alex
vtp password Alex
vtp version 2

end
sh vtp status
sh vlan brief

A2.5 ! make the access ports and add the vlans to it
en
conf t

int r f0/3-4
switchport mode access
switchport access vlan 10
exit

end
sh vlan brief

A2.7 ! portfast and bpdugurad and shutdown unused ports
en
conf t

int r f0/3-4
spanning-tree portfast
spanning-tree bpduguard enable
exit
end

show spanning-tree interface f0/3 detail
show spanning-tree interface f0/4 detail


! shutting down unused interfaces
conf t
int r f0/5-24,g0/1-2
shutdown
exit
end


sh interfaces status

A2.8 ! SVI and default route
en
conf t

int vlan 10
ip add 172.16.1.6 255.255.255.240
exit
ip default-gateway 172.16.1.1

end

show ip interface vlan 10
sh running | include default-gateway







A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config








## BSE-SW-HR-ALEX
A2.4 ! creating the vtp clients
en
conf t

vtp mode client
vtp domain Alex
vtp password Alex
vtp version 2

end
sh vtp status
sh vlan brief

A2.5 ! make the access ports and add the vlans to it
en
conf t

int r f0/3-4
switchport mode access
switchport access vlan 20
exit

end
sh vlan brief


A2.7 ! portfast and bpdugurad and shutdown unused ports
en
conf t

int r f0/3-4
spanning-tree portfast
spanning-tree bpduguard enable
exit
end

show spanning-tree interface f0/3 detail
show spanning-tree interface f0/4 detail


! shutting down unused interfaces
conf t
int r f0/5-24,g0/1-2
shutdown
exit
end

sh interfaces status





A2.8 ! SVI and default route
en
conf t

int vlan 10
ip add 172.16.1.7 255.255.255.240
exit
ip default-gateway 172.16.1.1
end

show ip interface vlan 10

sh running | include default-gateway






A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config






## BSE-SW-Clinical-ALEX
A2.4 ! creating the vtp clients
en
conf t

vtp mode client
vtp domain Alex
vtp password Alex
vtp version 2

end
sh vtp status
sh vlan brief


A2.5 ! make the access ports and add the vlans to it
en
conf t

int r f0/3-4
switchport mode access
switchport access vlan 30
exit

end
sh vlan brief


A2.7 ! portfast and bpdugurad and shutdown unused ports
en
conf t

int r f0/3-4
spanning-tree portfast
spanning-tree bpduguard enable
exit
end

show spanning-tree interface f0/3 detail
show spanning-tree interface f0/4 detail


! shutting down unused interfaces
conf t
int r f0/5-24,g0/1-2
shutdown
exit
end

sh interfaces status






A2.8 ! SVI and default route
en
conf t

int vlan 10
ip add 172.16.1.8 255.255.255.240
exit
ip default-gateway 172.16.1.1

end

show ip interface vlan 10
sh running | include default-gateway


A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config


## BSE-SW-ELV-ALEX
A2.4 ! creating the vtp clients
en
conf t

vtp mode client
vtp domain Alex
vtp password Alex
vtp version 2

end
sh vtp status
sh vlan brief

A2.5 ! make the access ports and add the vlans to it
en
conf t

int r f0/3
switchport mode access
switchport access vlan 40
exit

int r f0/4
switchport mode access
switchport access vlan 50
exit


end
sh vlan brief

A2.7 ! portfast and bpdugurad and shutdown unused ports
en
conf t

int r f0/3-4
spanning-tree portfast
spanning-tree bpduguard enable
exit
end

show spanning-tree interface f0/3 detail
show spanning-tree interface f0/4 detail


! shutting down unused interfaces
conf t
int r f0/5-24,g0/1-2
shutdown
exit
end

sh interfaces status




A2.8 ! SVI and default route
en
conf t

int vlan 10
ip add 172.16.1.9 255.255.255.240
exit

ip default-gateway 172.16.1.1

end

show ip interface vlan 10

sh running | include default-gateway








A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config





## BSE-SW-Server-ALEX
A2.4 ! creating the vtp clients
en
conf t

vtp mode client
vtp domain Alex
vtp password Alex
vtp version 2

end
sh vtp status
sh vlan brief


A2.5 ! make the access ports and add the vlans to it
en
conf t

int r f0/3-5
switchport mode access
switchport access vlan 60
exit

int r f0/6
switchport mode access
switchport access vlan 70
exit


end
sh vlan brief


A2.7 ! portfast and bpdugurad and shutdown unused ports
en
conf t

int r f0/3-6
spanning-tree portfast
spanning-tree bpduguard enable
exit
end

show spanning-tree interface f0/3 detail
show spanning-tree interface f0/4 detail
show spanning-tree interface f0/5 detail
show spanning-tree interface f0/6 detail


! shutting down unused interfaces
conf t
int r f0/7-24,g0/1-2
shutdown
exit
end

sh interfaces status

A2.8 ! SVI and default route
en
conf t

int vlan 10
ip add 172.16.1.10 255.255.255.240
exit

ip default-gateway 172.16.1.1

end

show ip interface vlan 10

sh running | include default-gateway





A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config







## BSE-R1-ALEX
A3.1 ! applying no shut and IP between the routers
en
conf t

int  g0/0
ip add 172.16.1.34 255.255.255.252
no shut
exit

int g0/1
no shut
exit


A3.2 ! Creating subinterfaces per vlan for inter-vlan routing
en
conf t

int g0/1.10
encap dot1Q 10
ip add 172.16.1.2 255.255.255.240
no shut
exit

int g0/1.20
encap dot1Q 20
ip add 172.16.0.194 255.255.255.224
no shut
exit

int g0/1.30
encap dot1Q 30
ip add 172.16.0.2 255.255.255.128
no shut
exit

int g0/1.40
encap dot1Q 40
ip add 172.16.0.130 255.255.255.192
no shut
exit

int g0/1.50
encap dot1Q 50
ip add 172.16.0.226 255.255.255.224
no shut
exit

int g0/1.60
encap dot1Q 60
ip add 172.16.1.18 255.255.255.248
no shut
exit

int g0/1.70
encap dot1Q 70
ip add 172.16.1.26 255.255.255.248
no shut
exit


A3.3 ! configure HSRB Active with R1 and standby R2 with preempt
en
conf t


int g0/1.10
standby 10 ip 172.16.1.1
standby 10 prio 110
standby 10 preempt


int g0/1.20
standby 20 ip 172.16.0.193
standby 20 prio 110
standby 20 preempt


int g0/1.30
standby 30 ip 172.16.0.1
standby 30 prio 110
standby 30 preempt


int g0/1.40
standby 40 ip 172.16.0.129
standby 40 prio 110
standby 40 preempt


int g0/1.50
standby 50 ip 172.16.0.225
standby 50 prio 110
standby 50 preempt

int g0/1.60
standby 60 ip 172.16.1.17
standby 60 prio 110
standby 60 preempt



int g0/1.70
standby 70 ip 172.16.1.25
standby 70 prio 110
standby 70 preempt
exit
end

sh standby

A3.6 ! add ip helper to vlan sub interfaces
en
conf t

int g0/1.10
ip helper-address 172.16.1.20

int g0/1.20
ip helper-address 172.16.1.20

int g0/1.30
ip helper-address 172.16.1.20

int g0/1.40
ip helper-address 172.16.1.20

int g0/1.50
ip helper-address 172.16.1.20

int g0/1.60
ip helper-address 172.16.1.20

int g0/1.70
ip helper-address 172.16.1.20
exit
end



A4.1 ! internal ospf and passive interfaces
en
conf t

router ospf 1
router-id 1.1.1.1


net 172.16.1.0 0.0.0.15 area 1
net 172.16.0.192 0.0.0.31 area 1
net 172.16.0.0 0.0.0.127 area 1
net 172.16.0.128 0.0.0.63 area 1
net 172.16.0.224 0.0.0.31 area 1
net 172.16.1.16 0.0.0.7 area 1
net 172.16.1.24 0.0.0.7 area 1
net 172.16.1.32 0.0.0.3 area 1


passive-interface g0/1.10
passive-interface g0/1.20
passive-interface g0/1.30
passive-interface g0/1.40
passive-interface g0/1.50
passive-interface g0/1.60
passive-interface g0/1.70
end



A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config


A5.10 ! shutting down the interface on R1 to see R2 turn to active
en
conf t

int g0/1
shut

!bringing the interface up again and seeing the R1 takes active role again because of preempt

int g0/1
no shut

## BSE-R2-ALEX
A3.1 ! applying no shut and IP between the routers
en
conf t

int  g0/0
ip add 172.16.1.38 255.255.255.252
no shut
exit

int g0/1
no shut
exit

A3.2 ! Creating subinterfaces per vlan for inter-vlan routing
en
conf t

int g0/1.10
encap dot1Q 10
ip add 172.16.1.3 255.255.255.240
no shut
exit

int g0/1.20
encap dot1Q 20
ip add 172.16.0.195 255.255.255.224
no shut
exit

int g0/1.30
encap dot1Q 30
ip add 172.16.0.3 255.255.255.128
no shut
exit

int g0/1.40
encap dot1Q 40
ip add 172.16.0.131 255.255.255.192
no shut
exit

int g0/1.50
encap dot1Q 50
ip add 172.16.0.227 255.255.255.224
no shut
exit

int g0/1.60
encap dot1Q 60
ip add 172.16.1.19 255.255.255.248
no shut
exit

int g0/1.70
encap dot1Q 70
ip add 172.16.1.27 255.255.255.248
no shut
exit



A3.3 ! configure HSRB Active with R1 and standby R2 with preempt
en
conf t


int g0/1.10
standby 10 ip 172.16.1.1
standby 10 prio 90
standby 10 preempt


int g0/1.20
standby 20 ip 172.16.0.193
standby 20 prio 90
standby 20 preempt


int g0/1.30
standby 30 ip 172.16.0.1
standby 30 prio 90
standby 30 preempt


int g0/1.40
standby 40 ip 172.16.0.129
standby 40 prio 90
standby 40 preempt


int g0/1.50
standby 50 ip 172.16.0.225
standby 50 prio 90
standby 50 preempt

int g0/1.60
standby 60 ip 172.16.1.17
standby 60 prio 90
standby 60 preempt



int g0/1.70
standby 70 ip 172.16.1.25
standby 70 prio 90
standby 70 preempt
exit
end

sh standby brief




A3.6 ! add ip helper to vlan sub interfaces
en
conf t

int g0/1.10
ip helper-address 172.16.1.20

int g0/1.20
ip helper-address 172.16.1.20

int g0/1.30
ip helper-address 172.16.1.20

int g0/1.40
ip helper-address 172.16.1.20

int g0/1.50
ip helper-address 172.16.1.20

int g0/1.60
ip helper-address 172.16.1.20

int g0/1.70
ip helper-address 172.16.1.20
exit
end



A4.1 ! internal ospf and passive interfaces
en
conf t

router ospf 1
router-id 2.2.2.2

net 172.16.1.0 0.0.0.15 area 1
net 172.16.0.192 0.0.0.31 area 1
net 172.16.0.0 0.0.0.127 area 1
net 172.16.0.128 0.0.0.63 area 1
net 172.16.0.224 0.0.0.31 area 1
net 172.16.1.16 0.0.0.7 area 1
net 172.16.1.24 0.0.0.7 area 1
net 172.16.1.36 0.0.0.3 area 1


passive-interface g0/1.10
passive-interface g0/1.20
passive-interface g0/1.30
passive-interface g0/1.40
passive-interface g0/1.50
passive-interface g0/1.60
passive-interface g0/1.70
end

A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config






## BSE-EDGE-ALEX
A3.1 ! applying no shut and IP between the routers
en
conf t

int  g0/0
ip add 172.16.1.33 255.255.255.252
no shut
exit

int g0/1
ip add 172.16.1.37 255.255.255.252
no shut
exit

int s0/0/0
ip add 200.200.200.2 255.255.255.252
no shut
exit

int s0/0/1
ip add 172.16.1.41 255.255.255.252
no shut
exit


A4.1 ! internal ospf and passive interfaces
en
conf t

router ospf 1
router-id 3.3.3.3

conf  t
router ospf 1
no net 172.16.1.32 0.0.0.3 area 0
no net 172.16.1.36 0.0.0.3 area 0
no net 200.200.200.0 0.0.0.3 area 0
net 172.16.1.40 0.0.0.3 area 0

net 172.16.1.32 0.0.0.3 area 1
net 172.16.1.36 0.0.0.3 area 1
net 200.200.200.0 0.0.0.3 area 1

end

A4.3 ! default route and default-orignate to isp efault-information originate advertises the default route only when EDGE-ALEX already has a default route in its routing table. !
en
conf t

ip route 0.0.0.0 0.0.0.0 200.200.200.1

router ospf 1
default-information originate

end


A4.4 ! config PAT that permits the private ips of alex and cairo
en
conf t


ip access-list standard NAT-PRIVATE-NETWORKS
permit 172.16.1.0 0.0.0.15
permit 172.16.0.192 0.0.0.31
permit 172.16.0.0 0.0.0.127
permit 172.16.0.128 0.0.0.63
permit 172.16.0.224 0.0.0.31
permit 172.16.1.16 0.0.0.7
permit 172.16.1.24 0.0.0.7
 
 
permit 192.168.1.0 0.0.0.63
permit 192.168.1.64 0.0.0.15
permit 192.168.1.80 0.0.0.7
exit

int r g0/0-1
ip nat inside

int s0/0/1
ip nat inside

int s0/0/0
ip nat outside
exit


ip nat inside source list NAT-PRIVATE-NETWORKS interface serial0/0/0 overload

end


A5.7 - 9 ! configuring ssh and enable secert and vty lines
en
conf t

ip domain-name bse.alex
enable secret bse123
username admin privilege 15 secret admin123
crypto key generate rsa
1024

ip ssh version 2
line vty 0 4
login local
transport input ssh
exit

service password-encryption
banner motd #Unauthorized access is strictly prohibited!#


! creating the acl that allows only adminstrators only to ssh
ip access-list standard SSH-ACCESS
permit 172.16.1.0 0.0.0.15
exit

line vty 0 4
access-class SSH-ACCESS in

end

copy running-config startup-config


