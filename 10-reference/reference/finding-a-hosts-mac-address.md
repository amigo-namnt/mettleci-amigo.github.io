# Finding a Host's MAC Address

> [!WARNING]
> Customers who are using MettleCI as part of an IBM entitlement **do not** need to supply their MAC address so can safely ignore this page.

Customer’s licensing MettleCI directly from Data Migrators may be issued with a license tied to the MAC address of your development environment’s DataStage Engine which you’ll need to provide when ordering your MettleCI software.

A MAC (media access control) address is a unique identifier assigned to a network interface controller in a host machine. It is normally formatted as 6 double-character hexadecimal numbers with colon or hyphen delimiters (`XX:XX:XX:XX:XX:XX` or `XX-XX-XX-XX-XX-XX`).

*   [Windows Hosts](#windows-hosts)
*   [Unix Hosts](#unix-hosts)
*   [AIX Hosts](#aix-hosts)

# Windows Hosts

You Windows host’s MAC address is described as the `Physical Address` of your Ethernet adapter when using the Windows `ipconfig /all` command:

```
C:\Users\John>ipconfig /all

Windows IP Configuration

   Host Name . . . . . . . . . . . . : EC2AMAZ-0D2DTLJ
   Primary Dns Suffix  . . . . . . . :
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : ap-southeast-2.ec2-utilities.amazonaws.com
                                       ap-southeast-2.compute.internal

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : ap-southeast-2.compute.internal
   Description . . . . . . . . . . . : AWS PV Network Device #0
   Physical Address. . . . . . . . . : 02-26-32-AF-A8-7A   <-------------- YOUR MAC ADDRESS
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::a8b4:4209:833f:65b7%5(Preferred)
   IPv4 Address. . . . . . . . . . . : 172.31.9.230(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.240.0
   Lease Obtained. . . . . . . . . . : Wednesday, April 8, 2020 10:52:40 AM
   Lease Expires . . . . . . . . . . : Wednesday, April 8, 2020 12:52:41 PM
```

# Unix Hosts

As the root user (or user with appropriate permissions) you can use the command `ifconfig -a` on **Linux** to determine your MAC address. From the displayed information, find **eth0** (this is the default first Ethernet adapter). The number ***may*** appear next to a test label `HWaddr`.

```
$> sudo ifconfig -a
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
	options=1203<RXCSUM,TXCSUM,TXSTATUS,SW_TIMESTAMP>
	inet 127.0.0.1 netmask 0xff000000
	inet6 ::1 prefixlen 128
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
	nd6 options=201<PERFORMNUD,DAD>
gif0: flags=8010<POINTOPOINT,MULTICAST> mtu 1280
stf0: flags=0<> mtu 1280
bridge0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	options=63<RXCSUM,TXCSUM,TSO4,TSO6>
	ether 82:dc:5a:23:b0:00                <--------- YOUR MAC ADDRESS
	Configuration:
		id 0:0:0:0:0:0 priority 0 hellotime 0 fwddelay 0
		maxage 0 holdcnt 0 proto stp maxaddr 100 timeout 1200
		root id 0:0:0:0:0:0 priority 0 ifcost 0 port 0
		ipfilter disabled flags 0x0
	member: en1 flags=3<LEARNING,DISCOVER>
	        ifmaxaddr 0 port 12 priority 0 path cost 0

```

# AIX Hosts

On AIX environments, use the `lscfg` command:

```
 # lscfg -vl ent0
  ent0             U7H5F.001.FCD8675-P1-T9  2-Port 10/100/1000 Base-TX PCI-X Adapter (14532868)
      2-Port 10/100/1000 Base-TX PCI-X Adapter:
        Network Address.............000E418C0D3A      <--------- YOUR MAC ADDRESS
        ROM Level.(alterable).......XX0000
        Hardware Location Code......U7H5F.001.FCD8675-P1-T9
  PLATFORM SPECIFIC000E418C0D3A
  Name:  ethernet
    Node:  ethernet@1
    Device Type:  network
    Physical Location: U7H5F.001.FCD8675-P1-T9

```

Or you may see results similar to this

```
 lscfg -vpl ent0
  ent0             U8286.42A.210486W-V3-C14-T1  Virtual I/O Ethernet Adapter (l-lan)
        Network Address.............962886198E0E           <--------- YOUR MAC ADDRESS
        Displayable Message.........Virtual I/O Ethernet Adapter (l-lan)
        Hardware Location Code......U8286.42A.210486W-V3-C14-T1
  PLATFORM SPECIFIC
  Name:  l-lan
    Node:  l-lan@3000000e
    Device Type:  network
    Physical Location: U8286.42A.210486W-V3-C14-T1

```

Your MAC address is the “Network Address” and you will have to put the colons in yourself when using it to request your license (000E418C0D3A becomes 00:0E:41:8C:0D:3A in this example)