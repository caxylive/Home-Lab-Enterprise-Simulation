# Initial Configuration

```Bash
root@proxmox:~# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enx00e04c36001d: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master vmbr0 state UP group default qlen 1000
    link/ether 00:e0:4c:36:00:1d brd ff:ff:ff:ff:ff:ff
3: wlp0s20f3: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 70:a8:d3:25:34:33 brd ff:ff:ff:ff:ff:ff
4: vmbr0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 00:e0:4c:36:00:1d brd ff:ff:ff:ff:ff:ff
    inet 10.118.1.254/24 scope global vmbr0
       valid_lft forever preferred_lft forever
    inet6 fe80::2e0:4cff:fe36:1d/64 scope link 
       valid_lft forever preferred_lft forever
```
