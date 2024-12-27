# Ubuntu Unleashed, 2019 Edition

## Chapter 18: Networking

### Laying the Foundation: The `localhost` Interface

`localhost` interface, sometimes called the *loopback interface*.

#### Checking for the Availability of the Loopback Interface 

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

#### Configuring the Loopback Interface Manually

The `localhost interface's IP address is specified in a text configuration file that is used by Ubuntu to keep records of various network-wide IP addresses. The file is called `/etc/hosts`.

```
$ cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	dstevensonlinux1

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

You might hear or read about terms such as `localhost`, *loopback*, and *dummy interface*;
all these terms refer to the use of the IP address 127.0.0.1.
The term *loopback interface* is used because, to Linux networking drivers, it looks as though the machine is talking to a network that consists of only one machine; the kernel sends network traffic to and from itself on the same computer.

Each networked Ubuntu machine on a LAN uses this same IP address for its `localhost`.

You can use `sudo` and edit the `/etc/hosts` file to add the `localhost` entry if it doesn't exist.

```
sudo ip addr add 127.0.0.1/24 dev lo
sudo ip route add 127.0.0.1/24 dev lo
```

Use the `ip` command as shown previously to test the interface.

### Checking connections with `ping`, `traceroute` and `mtr`

```
$ ping -c 3 localhost
PING localhost (127.0.0.1) 56(84) bytes of data.
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.047 ms
64 bytes from localhost (127.0.0.1): icmp_seq=2 ttl=64 time=0.038 ms
64 bytes from localhost (127.0.0.1): icmp_seq=3 ttl=64 time=0.040 ms

--- localhost ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2048ms
rtt min/avg/max/mdev = 0.038/0.041/0.047/0.003 ms
```

```
$ ping6 -c 3 ::1
PING ::1(::1) 56 data bytes
64 bytes from ::1: icmp_seq=1 ttl=64 time=0.051 ms
64 bytes from ::1: icmp_seq=2 ttl=64 time=0.044 ms
64 bytes from ::1: icmp_seq=3 ttl=64 time=0.044 ms

--- ::1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2049ms
rtt min/avg/max/mdev = 0.044/0.046/0.051/0.003 ms
```

Three tools that are usefulfor checking a network:

* ping/ping6
* traceroute/traceroute6
* mtr

A network timeout while you're using any of these tools indicates that there is a connectivity problem.

```
$ ping -c 3 google.com
PING google.com(lga34s40-in-x0e.1e100.net (2607:f8b0:4006:824::200e)) 56 data bytes
64 bytes from lga34s40-in-x0e.1e100.net (2607:f8b0:4006:824::200e): icmp_seq=1 ttl=116 time=25.6 ms
64 bytes from lga34s40-in-x0e.1e100.net (2607:f8b0:4006:824::200e): icmp_seq=2 ttl=116 time=22.9 ms
64 bytes from lga34s40-in-x0e.1e100.net (2607:f8b0:4006:824::200e): icmp_seq=3 ttl=116 time=23.5 ms

--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 22.917/24.012/25.579/1.136 ms
```

The second tool, `traceroute` (along with its IPv6 version traceroute6), tracks the route that packets take on an IP network from the local computer to the network host specified.
The `traceroute6` tool is intended for use with IPv6, although it isn't necesssary unless you want to force the command to trace using only IPv6 - otherwise `traceroute` tries to resolve the name given and automatically uses whichever protocol is most appropriate.

```
traceroute google.com
 1  Linksys01376.rochester.rr.com (192.168.1.1)  0.445 ms  0.422 ms  0.396 ms
 2  * * *
 3  lag-63.hnrtnyaf02h.netops.charter.com (24.58.232.213)  23.395 ms  34.729 ms  34.511 ms
 4  lag-46.mcr11rochnyei.netops.charter.com (24.58.49.64)  11.944 ms  13.822 ms  12.079 ms
 5  lag-28.rcr01rochnyei.netops.charter.com (24.58.32.74)  13.823 ms  13.666 ms  14.000 ms
 6  lag-25-10.chcgildt87w-bcr00.netops.charter.com (66.109.6.116)  26.366 ms lag-415-10.chcgildt87w-bcr00.netops.charter.com (66.109.6.2)  26.338 ms lag-15-10.chcgildt87w-bcr00.netops.charter.com (66.109.6.72)  26.288 ms
 7  72.14.212.162 (72.14.212.162)  53.294 ms syn-024-030-200-185.inf.spectrum.com (24.30.200.185)  26.017 ms 72.14.212.162 (72.14.212.162)  25.990 ms
 8  * * *
 9  142.251.60.12 (142.251.60.12)  26.162 ms 142.251.60.202 (142.251.60.202)  26.046 ms 142.251.60.204 (142.251.60.204)  29.142 ms
10  192.178.249.234 (192.178.249.234)  22.974 ms 192.178.249.208 (192.178.249.208)  25.767 ms 192.178.249.232 (192.178.249.232)  23.892 ms
11  142.251.234.31 (142.251.234.31)  25.433 ms 142.251.234.67 (142.251.234.67)  25.378 ms 192.178.99.91 (192.178.99.91)  26.958 ms
12  142.251.69.178 (142.251.69.178)  35.321 ms 216.239.57.137 (216.239.57.137)  33.753 ms  33.790 ms
13  142.251.69.63 (142.251.69.63)  34.490 ms 216.239.62.194 (216.239.62.194)  33.069 ms 142.251.69.171 (142.251.69.171)  32.953 ms
14  192.178.106.163 (192.178.106.163)  34.520 ms 192.178.106.19 (192.178.106.19)  33.361 ms 192.178.106.21 (192.178.106.21)  32.912 ms
15  142.251.65.115 (142.251.65.115)  32.998 ms 142.251.65.113 (142.251.65.113)  32.843 ms  32.841 ms
16  lga34s36-in-f14.1e100.net (142.250.80.110)  33.793 ms  33.918 ms  33.767 ms
```

The third tool, `mtr`, combines the functionality of `ping` and `traceroute` and gives you a live display of the data as it runs, as shown in this example.

