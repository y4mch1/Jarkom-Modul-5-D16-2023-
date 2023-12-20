# Jarkom-Modul-5-D16-2023

**Praktikum Jaringan Komputer Modul 5 Tahun 2023**

## Author

| Nama                     | NRP        |
| ------------------------ | ---------- |
| Dicky Indra Kuncahyo     | 5025201250 |
| Widian Sasi Disertasiani | 5025211024 |

# Laporan Resmi

## Topologi

![topologi](https://media.discordapp.net/attachments/1170650328950124618/1186996963040833606/image.png?ex=65954811&is=6582d311&hm=f193fbd6d95276ae1f194dd8837ba6af7b6964e20e497f50c7837c3fb819c655&=&format=webp&quality=lossless&width=871&height=675)

## IP

![IP](https://media.discordapp.net/attachments/1170650328950124618/1187000541998489630/image.png?ex=65954b66&is=6582d666&hm=7a01a56be734283d389f2c5b0a0bf4da70ebc475e350a3cae40dd4a0459bab69&=&format=webp&quality=lossless&width=1440&height=366)

## CONFIGURASI

### Aura

``` C
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.199.0.21
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.199.0.17
	netmask 255.255.255.252

### Heiter
auto eth0
iface eth0 inet static
	address 192.199.0.22
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.199.8.1
	netmask 255.255.248.0

auto eth2
iface eth2 inet static
	address 192.199.4.1
	netmask 255.255.252.0
```

### Frieren

``` C
auto eth0
iface eth0 inet static
	address 192.199.0.18
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.199.0.13
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.199.0.9
	netmask 255.255.255.252
```

### Himmel

``` C
auto eth0
iface eth0 inet static
	address 192.199.0.10
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.199.2.1
	netmask 255.255.254.0

auto eth2
iface eth2 inet static
	address 192.199.0.129
	netmask 255.255.255.128
```

### Fern

``` C
auto eth0
iface eth0 inet static
	address 192.199.0.130
	netmask 255.255.255.128

auto eth1
iface eth1 inet static
	address 192.199.0.5
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.199.0.1
	netmask 255.255.255.252
```

### Sein (Web Server)

``` C
auto eth0
iface eth0 inet static
	address 192.199.4.2
	netmask 255.255.252.0
gateway 192.199.4.1
```

### Stark (Web Server)
 
```C
auto eth0
iface eth0 inet static
	address 192.199.0.14
	netmask 255.255.255.252
	gateway 192.199.0.13

Richter (DNS Server)
auto eth0
iface eth0 inet static
	address 192.199.0.6
	netmask 255.255.255.252
	gateway 192.199.0.5
```

### Revolte (DHCP Server)

```C
auto eth0
iface eth0 inet static
	address 192.199.0.2
	netmask 255.255.255.252
	gateway 192.199.0.1
```

### All Client

```C
auto eth0
iface eth0 inet dhcp
```

### ROUTING

Aura
``` C
#Kanan
route add -net 192.199.8.0 netmask 255.255.248.0 gw 192.199.0.22 #A9
route add -net 192.199.4.0 netmask 255.255.252.0 gw 192.199.0.22 #A10

#Bawah
route add -net 192.199.0.0 netmask 255.255.255.252 gw 192.199.0.18 #A1
route add -net 192.199.0.4 netmask 255.255.255.252 gw 192.199.0.18 #A2
route add -net 192.199.0.128 netmask 255.255.255.128 gw 192.199.0.18 #A3
route add -net 192.199.2.0 netmask 255.255.254.0 gw 192.199.0.18 #A4
route add -net 192.199.0.8 netmask 255.255.255.252 gw 192.199.0.18 #A5
route add -net 192.199.0.12 netmask 255.255.255.252 gw 192.199.0.18 #A6
```

Heiter (DHCP Relay)
```c
echo nameserver 192.168.122.1 > /etc/resolv.conf
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.199.0.21 #default

DHCP Relay
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

echo '
SERVERS="192.199.0.2"
INTERFACES="eth1 eth2"
OPTIONS=' > /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart

```
Frieren
``` c
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.199.0.17 #default
route add -net 192.199.0.0 netmask 255.255.255.252 gw 192.199.0.10 #A1
route add -net 192.199.0.4 netmask 255.255.255.252 gw 192.199.0.10 #A2
route add -net 192.199.0.128 netmask 255.255.255.128 gw 192.199.0.10 #A3
route add -net 192.199.2.0 netmask 255.255.254.0 gw 192.199.0.10 #A4
```
Himmel
```c
echo nameserver 192.168.122.1 > /etc/resolv.conf

route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.199.0.9 #default
route add -net 192.199.0.0 netmask 255.255.255.252 gw 192.199.0.130 #A1
route add -net 192.199.0.4 netmask 255.255.255.252 gw 192.199.0.130 #A2

DHCP Relay
apt-get update
apt-get install isc-dhcp-relay -y
service isc-dhcp-relay start

echo '
SERVERS="192.199.0.2"
INTERFACES="eth1 eth2"
OPTIONS=' > /etc/default/isc-dhcp-relay

echo '
net.ipv4.ip_forward=1' > /etc/sysctl.conf
service isc-dhcp-relay restart

Revolte (DHCP Server)
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-server -y
dhcpd --version

echo 'INTERFACES="eth0"' > /etc/default/isc-dhcp-server

echo '
subnet 192.199.0.0 netmask 255.255.255.252 {

}

# SchwerMountain

subnet 192.199.0.128 netmask 255.255.255.128 {
range 192.199.0.130 192.199.0.193;
option routers 192.199.0.129;
option broadcast-address 192.199.0.255;
option domain-name-servers 192.199.0.6;
default-lease-time 600;
max-lease-time 7200;
}

# LaubHills

subnet 192.199.2.0 netmask 255.255.254.0 {
range 192.199.2.2 192.199.3.1;
option routers 192.199.2.1;
option broadcast-address 192.199.3.255;
option domain-name-servers 192.199.0.6;
default-lease-time 600;
max-lease-time 7200;
}

# TurkRegion

subnet 192.199.8.0 netmask 255.255.248.0 {
range 192.199.8.2 192.199.11.255;
option routers 192.199.8.1;
option broadcast-address 192.199.15.255;
option domain-name-servers 192.199.0.6;
default-lease-time 600;
max-lease-time 7200;
}

# GrobeForest

subnet 192.199.4.0 netmask 255.255.252.0 {
range 192.199.4.2 192.199.6.1;
option routers 192.199.4.1;
option broadcast-address 192.199.7.255;
option domain-name-servers 192.199.0.6;
default-lease-time 600;
max-lease-time 7200;
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart

apt-get install isc-dhcp-server -y
dhcpd --version

echo 'INTERFACES="eth0"' > /etc/default/isc-dhcp-server

echo '

# A10

subnet 10.40.0.20 netmask 255.255.255.252 {
}

# A9

subnet 10.40.0.16 netmask 255.255.255.252 {
}

# SchwerMountain (A8)

subnet 10.40.0.128 netmask 255.255.255.128 {
range 10.40.0.130 10.40.0.193;
option routers 10.40.0.129;
option broadcast-address 10.40.0.255;
option domain-name-servers 10.40.0.18;
default-lease-time 600;
max-lease-time 7200;
}

# LaubHills (A7)

subnet 10.40.2.0 netmask 255.255.254.0 {
range 10.40.2.2 10.40.3.1;
option routers 10.40.2.1;
option broadcast-address 10.40.3.255;
option domain-name-servers 10.40.0.18;
default-lease-time 600;
max-lease-time 7200;
}
```

Fern
```c
echo nameserver 192.168.122.1 > /etc/resolv.conf
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.199.0.129 #default
```
