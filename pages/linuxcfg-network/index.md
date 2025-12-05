---
layout: page
title: Шпаргалка по настройке сети в linux
---

## база
```no-line-numbers
ip a    #проверить какой ip
ip r    #проверить какой шлюз
ip a add <ip_addr/mask> dev <interface>    #временно добавляет IP
ip route add default via <gw_ip> dev <interface>        #временно добавляет дефолтный маршрут
ip route replace default via <gw_ip> dev <interface>    #временно заменяет дефолтный маршрут

```

днс

```no-line-numbers
nano /etc/resolv.conf
```

```no-line-numbers
nameserver 8.8.8.8
```

время

```no-line-numbers
systemctl status systemd-timesyncd
systemctl status chrony
systemctl status ntpd

```

```no-line-numbers
timedatectl set-timezone Europe/Moscow
```

### поднять\опустить интерфейс

используя "ip"

```no-line-numbers
# ip link set dev eth0 up
# ip link set dev eth0 down
```

используя "ifconfig"

```no-line-numbers
# /sbin/ifconfig eth0 up
# /sbin/ifconfig eth0 down
```




## - - - Конфиги - - -

## настройка сети в Debian 13

юнит

```no-line-numbers
sudo systemctl status networking
```

конфиг тут:

```no-line-numbers
sudo nano /etc/network/interfaces
```

dns тут:

```no-line-numbers
nano /etc/resolv.conf
```

## настройка сети в Ubuntu 20.04.6 LTS

конфиг тут:

```no-line-numbers
/etc/netplan/50-cloud-init.yaml
```

смотрим какие есть сетевые интерфейсы

команда:

```no-line-numbers
ip a
```
вывод:

```no-line-numbers
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:d0:01:00 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.55/24 brd 192.168.1.255 scope global dynamic eth0
       valid_lft 81438sec preferred_lft 81438sec
    inet6 fe80::215:5dff:fed0:100/64 scope link
       valid_lft forever preferred_lft forever
```

видим, что есть некий **eth0** его и вписываем в **/etc/netplan/50-cloud-init.yaml** к примеру так выглядит настройка **eth0** с включенным DHCP и **ens224** с статичным ip. Параметр **optional: true** позволяет избежать долгой загрузки ОС в некоторых случаях

```no-line-numbers
network:
    ethernets:
#        enp0s3:
        eth0:
            dhcp4: true
            optional: true
           # addresses: [192.168.1.55/24, ]
        ens224:
            addresses: [192.168.1.77/24, ]
    version: 2

```


## настройка сети в Centos 8

конфиг тут:

```no-line-numbers
nano /etc/sysconfig/network-scripts/ifcfg-ens32
```

содержание

```no-line-numbers
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=no
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens32
UUID=3d0227d7-615f-4a25-ba56-db66822f0e0f
DEVICE=ens32
ONBOOT=yes
IPADDR=192.168.1.55
PREFIX=24

```




