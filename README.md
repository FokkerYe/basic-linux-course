# basic-linux-course
Lesson for beginner Student
#ifconfig  ============(Check my NIC Card Info)
#ifconfig eth0
#ifconfig eth0 up (up/down)
# ifconfig etho down (up/down)
#ifup eth0
#ifdown eth0
#ifconfig eth0 192.168.0.1 netmask 255.255255.0 (temporaily assign IP)
#ifconfig eth0:1 192.168.56.0.1 255.255.255.0 ( virtual Ip)
#route add default gw 192.168.0.254  (default route)
# route -F (route table command)
#route -nF
# netstat -nr
======================================================
Static IP
vi /etc/sysconfig/network-scripts/ifcfg-enp0s3 (redhat base)
ONBOOT=yes
BOOTPROTO="satatic"
IPADDR=10.10.10.10
NETMASK=255.255.255.0
GATEWAY=10.10.10.1
DNS1=8.8.8.8
DNS2=8.8.4.4
systemctl restart NetworkManager
 cp ifcfg-enp0s3 ifcfg-enp0s3:1 ( virtual IP)
----------------------------------------------
(ubuntu base,Debian base)
&sudo -i
/lib/systemd/syste/
systemctl restart NetworkManager
#nano /etc/network/interfaces 
auto eth0
iface eth0 inet static
address 192.168.0.1
netmask 255.255.255.0
gateway 192.168.0.254
dns-nameservers 8.8.8.8 8.8.4.4
-------------------------------------

auto eth0:0
ifcace eth0:0 inet static
address 200.200.200.1
netmask 255.255.255.0
gateway 200.200.200.254 
----------------------------------

auto eth1
iface eth1 inet dhcp 
# /etc/init.d/networking restart (or) systemctl restart networking
==========================================================
Ubuntu 20.1
#sudo -i
#cd /etc/netplan/
ls
#nano 01-network-manager-all.yaml
ethernets:
enp0s3:
dhcp4: yes
ctrl+o
ctrl+x
#netplan apply
-----
nano 01-network-manager-all.yaml
ethernets:
enp0s3:
dhcp4: no
dhcp6: no
address: [200.200.200/24]
gateway: 200.200.200.1
nameservers:
addresses: [8.8.8.8, 8.8.4.4]
ctrl+o 
ctrl+x
netplan apply
***************************************
systemctl start/stop/restart servicename
systemctl enable/disable servicename
**********----------------**********=======================================================
nmcli (NetworkManager)
#nmcli -t -f RUNNING gerneral (check Running)
#nmcli dev status (check the attached network interfaces on our system)
#nmcli connection show (check active connnection on the device)
#nmcli dev show (list all the available device)
#nmcli -t dev show (-t, -terse: when want the output to be very brief and very few words)
#nmcli -f DHCP4 dev show (To print device list with field DHCP4)
nmcli c s
nmcli -t dev show
#nmcli con down enp0s3
#nmcli con up enp0s3

******************************************************
nmcli network ip change (ifconfig)
** nmcli con mod enp0s3 ipv4.method manual
nmcli con mod enp0s3 ipv4.addresses 10.10.10.10/8
nmcli con mod enp0s3 ipv4.gateway 10.10.10.100
nmcli con mod enp0s3 ipv4.dns "8.8.8.8 8.8.4.4"
systemctl restart NetworkManager
systemctl restart network

***nmcli con mod enp0s3 ipv4.method manual ipv4.addresses 10.10.10.10/8 ipv4.gateway 10.10.10.100 ipv4.dns "8.8.8.8 8.8.4.4"
-----------------------------------------------------------------------------------------------------

nmcli con add conn-name LAN2 type ethernet ifname enp0s3 ipv4.method manual ipv4.addresses 10.10.10.10/8 ipv4.gateway 10.10.10.100 ipv4.dns "8.8.8.8 8.8.4.4"(virtual ip)
*nmcli con s
*nmcli con up LAN2 (or) enp0s3
* nmcli con show  (or) * nmcli con show
*nmcli con del LAN2
*nmcli con show
------------------------------------------------------------------------------
*************************************************
**nmcli con mod enp0s3 ipv4.method auto (DHCP cliend up)

===============================================

Ping (Packet InterNet Groper)
ping -w timein seconds hostname/ip
ping -w 3 facebook.com
ping -c 5 facebook.comm
ping -s packetsize hostname/ip
ping -s 300 facebook.com
ping -f hostname-ip (flooding (or) Non-stop)

-----------------------------
