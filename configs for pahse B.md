## Router edge alex
B5 ! setting ftp on the router
en
bse123
conf t
ip ftp username  BSEALEX
ip ftp password  BSEALEX
end

copy running-config ftp
172.16.1.22

## SW1 core alex
B5 ! setting ftp on the router
en
bse123
conf t
ip ftp username  BSEALEX
ip ftp password  BSEALEX
end

copy running-config ftp
172.16.1.22


## B7 copy running configs to startup configs on all devices
en
bse123
copy running-config startup-config 

## Router edege alex 
B.3 ! truning on AAA on vty lines while also keeping the local userame / password for failur scenarios
en
bse123
conf t



tacacs-server host 172.16.1.21
tacacs-server key bse123
aaa new-model
aaa authentication login default group tacacs+ local
line vty 0 4
login authentication default
exit

aaa authentication login CONSOLE local
line con 0
login authentication CONSOLE
exit


## SW1 core alex
B.3 ! truning on AAA on vty lines while also keeping the local userame / password for failur scenarios

en
bse123
conf t

tacacs-server host 172.16.1.21
tacacs-server key bse123
aaa new-model
aaa authentication login default group tacacs+ local
line vty 0 4
login authentication default
exit

aaa authentication login CONSOLE local
line con 0
login authentication CONSOLE
exit

## edge router cairo
B.3 ! truning on AAA on vty lines while also keeping the local userame / password for failur scenarios

en
bse123
conf t

tacacs-server host 172.16.1.21
tacacs-server key bse123
aaa new-model
aaa authentication login default group tacacs+ local
line vty 0 4
login authentication default
exit

aaa authentication login CONSOLE local
line con 0
login authentication CONSOLE
exit


## SW1 core cairo
B.3 ! truning on AAA on vty lines while also keeping the local userame / password for failur scenarios

en
bse123
conf t

tacacs-server host 172.16.1.21
tacacs-server key bse123
aaa new-model
aaa authentication login default group tacacs+ local
line vty 0 4
login authentication default
exit

aaa authentication login CONSOLE local
line con 0
login authentication CONSOLE
exit




# port security
conf t
interface range fa0/3-4
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation restrict

end
sh port-se

