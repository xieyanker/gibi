# gibi(Get Interface By IP)
A simple shell which can get interface by IP

### How to install

```shell
wget https://raw.githubusercontent.com/xieyanker/gibi/main/gibi
chmod +x gibi
cp gibi /usr/local/bin/
```

### How to use

You can user `gibi $ip` to find the `interface` name by `ip`.

```shell
[root@master1 ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 52:54:00:1b:d9:45 brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.101/24 brd 192.168.122.255 scope global noprefixroute eth0
       valid_lft forever preferred_lft forever
    inet6 fd00::20c:29ff:fe9f:52be/120 scope global
       valid_lft forever preferred_lft forever
    inet6 fe80::5054:ff:fe1b:d945/64 scope link
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:31:b1:59:ad brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:31ff:feb1:59ad/64 scope link
       valid_lft forever preferred_lft forever
4: cni0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether f6:d8:8e:0b:66:cf brd ff:ff:ff:ff:ff:ff
    inet 10.85.0.1/16 brd 10.85.255.255 scope global cni0
       valid_lft forever preferred_lft forever
    inet6 1100:200::1/24 scope global
       valid_lft forever preferred_lft forever
    inet6 fe80::f4d8:8eff:fe0b:66cf/64 scope link
       valid_lft forever preferred_lft forever
5: veth897078f3@if3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master cni0 state UP group default
    link/ether da:d2:ca:90:e2:8b brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::d8d2:caff:fe90:e28b/64 scope link
       valid_lft forever preferred_lft forever
[root@master1 ~]#
[root@master1 ~]# gibi 127.0.0.1
lo
[root@master1 ~]#
[root@master1 ~]# gibi 192.168.122.101
eth0
[root@master1 ~]#
[root@master1 ~]# gibi fd00::20c:29ff:fe9f:52be
eth0
[root@master1 ~]#
[root@master1 ~]# gibi fe80::5054:ff:fe1b:d945
eth0
[root@master1 ~]#
[root@master1 ~]# gibi 172.17.0.1
docker0
[root@master1 ~]#
[root@master1 ~]# gibi fe80::42:31ff:feb1:59ad
docker0
[root@master1 ~]#
[root@master1 ~]# gibi fe80::d8d2:caff:fe90:e28b
veth897078f3
[root@master1 ~]#
```

### Common question

##### 1. Can not find the interface by ip

```shell
[root@master1 ~]# gibi 192.168.0.1
Can not find the interface by ip 192.168.0.1, please retry with the correct ip!
Example: gibi 192.168.122.101
[root@master1 ~]#
```

Please ensure the ip your passed exists on your os.

```shell
ip a | grep $ip
```

##### 2. Only one ip can be passed

```shell
[root@master1 ~]# gibi 192.168.122.101
eth0
[root@master1 ~]#
[root@master1 ~]# gibi 192.168.122.101 127.0.0.1
Only one ip can be passed!!!
Example: gibi 192.168.122.101
[root@master1 ~]#
```

The `gibi` can only find the interface by one ip now.

