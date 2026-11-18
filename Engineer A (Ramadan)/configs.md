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

spanning-tree vlan 10,30,40,50,60,70 root primary

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

spanning-tree vlan 10,30,40,50,60,70 root secondary

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

