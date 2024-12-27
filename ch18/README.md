# Ubuntu Unleashed, 2019 Edition

## Chapter 18: Networking

### Laying the Foundation: The `localhost` Interface

`localhost` interface, sometimes called the *loopback interface*.

```
$ ip address show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
```

`ifconfig` is deprecated

```
$ ifconfig
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 19452  bytes 2120081 (2.1 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 19452  bytes 2120081 (2.1 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```