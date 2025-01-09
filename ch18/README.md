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

### Networking with TCP/IP

The basic building block for any network based on UNIX hosts is the *Transmission Control Protocol/Internet Protocol (TCP/IP)* suite, which includes three protocols even though only two appear in the name.
*User Datagram Protocol (UDP)* is a connectionless protocol.

In TCP/IP, all data travels via IP packets, which is why addresses are referred to as *IP addresses*.

Ubuntu and Networking

[Linux USB Project](http://www.linux-usb.org/)

Other graphical network clients for use with Linux

* [Nmap](http://nmap.org/)
* [Netcat](http://nc110.sourceforge.net/)
* [Wireshark](http://www.wireshark.org/)
* [tcpdump](http://www.tcpdump.org/)
* 
#### TCP/IP Addressing

Internet IP addresses (also known as *public* IP addresses). Internet IP addresses are assigned (for the United States and some other hosts) by the American Registry for Internet Numbers ([ARIN](http://www.arin.net/)). ARIN assigns *Internet service providers (ISPs)* one or more blocks of IP addresses, while the ISPs can then assign to their subscribers.

A TCP/IP address is expressed as a series of four decimal numbers: a 32-bit value expressed in a format known as dotted-decimal format, such as 192.168.0.1. Each set of numbers is known as an *octet) (eight 1s and 0s, such as 10000000 to represent 128) and ranges from 0 to 255.

There are three classes of networks:

* Class A - Consists of networks with the first octet ranging from 1 to 126. There are only 126 Class A networks, each composed of up to 16,777,214 hosts. No host portion of an address can be all 0s or 255s. The 10. network is reserved for local network use, and the 127. network is reserved for the loopback address, 127.0.0.1. This address does not appear and is not accessible on your LAN.

* Class B - Consists of networks defined by the first two octets, with the first ranging from 128 to 191. The 128. network is also reserved for local network use. Therea rea 16,382 Class B networks, each with 65,534 possible hosts.

* Class C - Cosnists of a network defined by the first three octets with the first ranging from 192 to 223. The 192. network is another that is reserved for local network use. Therea are a possible 2,097,150 Class C networks of up to 254 hosts each.

The 0 address is used for network-to-network broadcasts. Also note that there are two other classes of networks, Classes D and E. Class D networks are reserved for multicast addresses and are not for use by network hosts. Class E addresses are deemed experimental and thus are not open for public addressing.

These classes are standard, but a *netmask* also determines what class your network is in. Common netmasks for the different c lasses are as follows:

* Class A - 255.0.0.0
* Class B - 255.255.0.0
* Class C - 255.255.255.0

Limits of IPv4 Addressing

The IPv4 address scheme is based on32-bit numbering and limits the number of available IP addresses to about 4.1 billion. Many companies and organizations (particularly in the United States) were assigned very large blocks of IP addresses in the early stages of growth of the Internet, which has left a shortage of "open" addresses. The Internet might run out of available addresses.

To solve this problem, a newer scheme named IP version 6 (IPv6) is being implemented. It uses a much larger addressing solution that is based on 128-bit addresses.

Migrtation to IPv6 is slow in coming, however, because many computer operating systems, software, hardware, firmware, and users are in the IPv4 mindset. Supporting IPv6 requires rewriting many network utilities, portions of operating systems currently in use, and firmware in routing and firewall hardware.

#### Using IP Masquerading in Ubuntu

Three blocks of IP addresses are reserved for use on internal networks and hosts not directly connected to the Internet. The address ranges are from 10.0.0.0 to 10.255.255.255, or 1 Class A network; from 172.16.0.0 to 172.31.255.255, or 16 Class B networks, and from 192.168.0.0 to 192.168.255.255, 256 Class C networks. use these IP addresses when building a LAN for your business or home. Which class you choose can depend on the number of hosts on your network.

#### Ports

Most servers on your network perform more than one task. For example, web servers often have to serve both standard and secure pages.

```
cat /etc/services
...
ftp		21/tcp
fsp		21/udp		fspd
ssh		22/tcp				# SSH Remote Login Protocol
telnet		23/tcp
smtp		25/tcp		mail
http		80/tcp		www		# WorldWideWeb HTTP
pop3		110/tcp		pop-3		# POP version 3
```

### IPv6 Basics

As IPv6 receives greater acceptance and use, this understanding shoul be adequate to help you transition between the two, even if specific issues are not addressed in the chapter.

IPv6 supports 3.4 x 10^38 addresses. We don't need NAT in IPv6 to translate IP addresses as packets pass through a routing device, as there are an adequate number of IP addresses available.

IPv6 allows us to go back to the easier-to-configure peer-to-peer style of Internet networking originally conceived of and used in the 1980s. This creates routing tables that are much smaller because fewere subroutes need to be generated.

Useful featuers that IPv6 includes:

* Address autoconfiguration (RFC2462)
* Anaycast addresses ("one-out-of-many")
* Mandatory multicast addresses
* IPsec (IP Security)
* Simplified header structure
* Mobile IP
* IPv6-to-IPv4 transition mechanisms

IPv6 addresses are created using eight sets of numbers, like this:

`2603:7080:9603:e32e:ce0:8865:ecb1:f9a2`

Each of the eight sectiosn is made of a four-digit number in hexadecimal.
Eachs set of 4 hex digits represents 16 bits or numbers 0-65535.

Often an address has long substrings of all zeros; the longest and first run of all-zero sections is abbreviated as a double colon (::)> Because :: is variable in length, it can be used only once per address.

It is also possible to write the last 32 bits of an IPv6 address using the well-known IPv4 format. Forexample, 2002::10.0.0.1 corresponds to the long form 2002:0000:0000:0000:0000:0000:0a00:0001.

In IPv6, the first 48 bits are for Internet routing (network addressing).

the 16 bits from the 49th to the 54th are for defining subnets:

The last 64 bits are for device (interface) IDs.

Speical-use, reserved IPv6 addresses:

* ::1/128 is the loopback address
* ::/128 is the unspecified address
* ::IPv4-address/96 are the IPv4-compatible addresses.
* 2001:db8::/32 are the documentation addresses. They are used for documentation purposes such as user manuals, RFCs and so on.
* ::0 is the default unicast route address.
* ff00::/8 are multicast addresses.

### Network Organization

Properly organizing your network addressing process grows more difficult as the size of your network grows.

#### Subnetting

Within Class A and B networks, there can be separate networks called *subnets*. Subnets are considered part of the host portion of an address for network class definitions. For example, in the 128. Class B network, you can have one computer with address 128.10.10.10 and anotehr with address 128.10.200.20; these computers are on the same network. Because of this, communication between the two computers requires either a router or a switch. Subnets can be helpful for separating workgroups within a company.

Often subnets c an be used to separate workgroups that have no real need to interact with or to shield from other groups' information passing among members of a specific workgroup.

Subnet use also enables your network to grow beyond 254 hosts and share IP addresses.
With proper routing configuration, users might not even know they are on a different subnet from their co-workers.

Another common use for subnetting is with networks that cover a wide geographic area.

#### Subnet Masks

TCP/IP uses subnet masks to show which part of an IP address is the network portion and which part is the host. Subnet masks are usually referred to as *netmasks*. For a pure Class A network, the netmask is 255.0.0.0; for a Class B network, the netmask is 255.255.0.0; and for a Class C network, the netmask is 255.255.255.0. 
You can also use netmasks to deviate from the standard classes.

By using customized netmasks, you can subnet your network to fit your needs.

See *Sam's Teach Yourself TCP/IP Network Administration in 21 Days*, Day 6, "The Art of Subnet Masking".

[Linux Network Administrator's Guide](http://www.tldp.org/LDP/nag2/index.html)

#### Broadcast, Unicast, and Multicast Addresssing

Information can get to systems through three types of addresses: unicast, multicast, and broadcast.

* **Unicast** - Sends information to one specific host. Unicast addresses are used for Telnet, FTP, SSH or any other information needs to be shared in a one-to-one exchange of information.

* **Multicasting** - Broadcasts information to groups of computers sharing an application, such as a video conferencing client or an online gaming application. All the machiens participating in the conference or game require the same information at precisely the same time to be effective.

* **Broadcasting** - Transmits information to all the hosts on a network or subnet. *Dynamic Host Configuration Protocol (DHCP) uses broadcast messages when the DHCP client looks for a DHCP server to get its network settigns, and *Reverse Address Resolution Protocol (RARP) uses broadcast messages tfor hardware address-to-IP address resolution. Broadcast messages use .255 in all the host octets of the networ IP address. (10.2.255.255 broadcasts to every host in your class B network).

### Hardware Devices for Networking

#### Network Interface Cards

Each NIC has a unique address (the hardware address, known as Media Access Control [MAC] address), which identifies that NIC.
A MAC address looks similar to this: 00:60:08:8F:5A:D9.

* DHCP - Dynamic Host Configuration Protocol
* Address Resolution Protocol (ARP)
* Reverse Address Resolution Protocol (RARP)

##### Token Ring

##### 10BASE-t

##### 100BASE-T

##### 1000BASE-T

##### Fiber-Optic and Gigabit Ethernet

##### Wireless Network Interfaces

#### Network capable

3 Types of Network cable

1. coaxial
2. UTP
3. Fiber

##### Unshielded Twisted Pair

* Category 1 (Cat1)
* Category 2 (Cat2)
* Category 3 (Cat3)
* Category 4 (Cat4)
* Category 5 (Cat5)
* Category 6 (Cat6)

##### Fiber Optic cable

#### Hubs and Switches

Number of connections (ports): 4, 8, 16, 24, and 48

#### Routers and Bridges

##### Bridges

##### Routers

#### Initializing New Network Hardware

Device file in the `/dev` directory.

If you do not use automatic hardware detection and configuration, you can initialize network hardware by doing the following:

* Manually editing the `/etc/modprobe.conf` file
* Manually loading or unloading the new device's kernel module with the `modprobe` command

##### Editing the `/etc/modprobe.conf` File

##### Using `modprobe` to Manually Load Kernel Modules

`sudo modprobe 8139too`

`dmesg`


#### Using Network Configuration Tools

To configure a network client host using the command line, you can use a combination of commands or edit specific files under the `/etc` directory.

Ubuntu's grapical tool: `nm-connection-editor`

For anyone new to networking, using the `nm-connection-editor` graphical tool is the way to go.

##### Command-Line Network Interface Configuration

`ifconfig`

```
$ ip route
default via 192.168.1.1 dev enp6s0 proto dhcp metric 100 
169.254.0.0/16 dev enp6s0 scope link metric 1000 
192.168.1.0/24 dev enp6s0 proto kernel scope link src 192.168.1.150 metric 100 
```


`ifconfig` is used to configure a network interface. You can use it to do the following:

* Active or deactive your NIC or change your NIC's mode
* Change your machine's IP address, netmask, or broadcast address
* Create an IP alias to allow more than one IP address on your NIC
* Set a destination address for a point to point connection

`ifconfig [network device] options`

ifconfig options

* Create alias
* Change IP address
* Change the netmask
* Change the broadcast
* Take interface down
* Bring interface down
* SET NIC promiscuous
* Set multicasting mode
* Enable or disable

To deactivate

`sudo ifconfig eth0 down`

To configure and activate and bring up the `eth0` interface with a specific IP address

`sudo ifconfig eth0 192.168.2.9 netmask 255.255.255.0 up`


Activate the interface according to a defined hostname:

`sudo ifconfig eth0 catcat.fakeurl.com up`

Get information about all your network interfaces:

`sudo ip addr show`

Assign an IP address to a specific interface:

`sudo ip addr add 192.168.2.9 dev eth1`

To remove an assigned IP address:

`sudo ip addr del 192.168.2.9 dev eth1`

Enable a network interface:

`sudo ip link set eth1 up`

Disable a network interface:

`sudo ip link set eth1 down`

Check the routing table:

`sudo ip route show`

To add a static route:

`sudo ip route add 10.10.30.0/24 via 192.168.50.100 dev eth0`

Remove a static route:

`sudo ip route del 10.10.30.0/24

To add a default gateway:

`sudo ip route add default via 192.168.36.100`

```
$ ip route
default via 192.168.1.1 dev enp6s0 proto dhcp metric 100 
169.254.0.0/16 dev enp6s0 scope link metric 1000 
192.168.1.0/24 dev enp6s0 proto kernel scope link src 192.168.1.150 metric 100 
```

`netstat`

netstat options

* -g
* -i
* -s
* -v
* -c
* -e
* -C

#### Network Configuration Files

* /etc/hosts
* /etc/services
* /etc/nsswitch.conf
* /etc/resolve.conf
* /etc/host.conf

##### Adding Hosts to `/etc/hosts`

##### Service Settings in `/etc/services`

##### Using `/etc/nsswitch.conf` After Changing Naming Services

##### Setting a Name Server with `/etc/resolv.conf`

##### Setting DNS Search Order with `/etc/host.conf`

#### Using Graphical Configuration Tools

### Dynamic Host Configuration Protocol (DHCP)

Setting name server entries in `/etc/resolv.conf`


#### How DHCP Works

* Network subnet/host address - Enables host to connect to the network at will
* Subnet/hostname - Enables the specified host to connect to the subnet
* Subnet/hardware address -Enables specific client to connect to the network after getting the hostname from the DHCP

#### Activating DHCP at Installation and Boot Time

See: `/etc/network/interfaces`

DHCP settings: `/etc/dhcp/dhclient.conf`

```
$ sudo dhclient
[sudo] password for dstevenson: 
RTNETLINK answers: File exists
```

#### DHCP Software Installation and Configuration

##### DHCP `dhclient`

DHCP is automatically enabled when you install Ubuntu.

`dhclient.conf` options

* timeout time;
* retry time;
* select-timeout time;
* reboot time;
* renew date;

See the `dhclient.conf` man page for more information on additional settings.

##### DHCP Server

#### Using DHCP to Configure Network Hosts

* Setting the domain name
* Setting DNS servers
* Setting the default and maximum lease times

#### Other Uses for DHCP