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