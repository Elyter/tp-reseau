# TP2 : Ethernet, IP, et ARP

🌞 **Mettez en place une configuration réseau fonctionnelle entre les deux machines**

```
❯ ifconfig
bridge102: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	options=3<RXCSUM,TXCSUM>
	ether 82:65:7c:1e:b8:66 
	inet 10.37.129.2 netmask 0xffffff00 broadcast 10.37.129.255
	inet6 fe80::8065:7cff:fe1e:b866%bridge102 prefixlen 64 scopeid 0x1a 
	inet6 fdb2:2c26:f4e4:1::1 prefixlen 64 
	Configuration:
		id 0:0:0:0:0:0 priority 0 hellotime 0 fwddelay 0
		maxage 0 holdcnt 0 proto stp maxaddr 100 timeout 1200
		root id 0:0:0:0:0:0 priority 0 ifcost 0 port 0
		ipfilter disabled flags 0x0
	member: vmenet1 flags=3<LEARNING,DISCOVER>
	        ifmaxaddr 0 port 21 priority 0 path cost 0
	nd6 options=201<PERFORMNUD,DAD>
	media: autoselect
	status: active
```
```
parallels@ubuntu-linux-22-04-desktop:~$ cd /etc/netplan/
parallels@ubuntu-linux-22-04-desktop:/etc/netplan$ sudo vi 00-installer-config.yaml
parallels@ubuntu-linux-22-04-desktop:/etc/netplan$ sudo netplan apply
```

🌞 **Prouvez que la connexion est fonctionnelle entre les deux machines**

```
❯ ping 10.37.129.10
PING 10.37.129.10 (10.37.129.10): 56 data bytes
64 bytes from 10.37.129.10: icmp_seq=0 ttl=64 time=0.860 ms
64 bytes from 10.37.129.10: icmp_seq=1 ttl=64 time=0.675 ms
64 bytes from 10.37.129.10: icmp_seq=2 ttl=64 time=0.662 ms
64 bytes from 10.37.129.10: icmp_seq=3 ttl=64 time=0.695 ms
^C
--- 10.37.129.10 ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.662/0.723/0.860/0.080 ms
```

```
parallels@ubuntu-linux-22-04-desktop:/etc/netplan$ ping 10.37.129.2
PING 10.37.129.2 (10.37.129.2) 56(84) bytes of data.
64 bytes from 10.37.129.2: icmp_seq=1 ttl=64 time=0.338 ms
64 bytes from 10.37.129.2: icmp_seq=2 ttl=64 time=0.451 ms
64 bytes from 10.37.129.2: icmp_seq=3 ttl=64 time=0.341 ms
64 bytes from 10.37.129.2: icmp_seq=4 ttl=64 time=0.469 ms
^C
--- 10.37.129.2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3063ms
rtt min/avg/max/mdev = 0.338/0.399/0.469/0.060 ms
```

🌞 **Wireshark it**

[Capture packet ping](ping.pcapng)

# II. ARP my bro

🌞 **Check the ARP table**

```
❯ arp -a
? (10.37.129.10) at 0:1c:42:f9:18:97 on bridge102 ifscope [bridge]
```

```
parallels@ubuntu-linux-22-04-desktop:/etc/netplan$ arp -a
? (10.37.129.2) à 82:65:7c:1e:b8:66 [ether] sur enp0s5
```

```
❯ arp -a
? (10.33.19.254) at 0:c0:e7:e0:4:4e on en0 ifscope [ethernet]
```
🌞 **Manipuler la table ARP**

```
❯ sudo arp -a -d
10.33.17.52 (10.33.17.52) deleted
10.33.18.68 (10.33.18.68) deleted
10.33.19.254 (10.33.19.254) deleted
224.0.0.251 (224.0.0.251) deleted
❯ arp -a
? (10.33.17.52) at ba:d4:52:5:4b:42 on en0 ifscope [ethernet]
? (10.33.19.254) at 0:c0:e7:e0:4:4e on en0 ifscope [ethernet]
```
```
❯ ping 10.37.129.10
PING 10.37.129.10 (10.37.129.10): 56 data bytes
64 bytes from 10.37.129.10: icmp_seq=0 ttl=64 time=1.180 ms
64 bytes from 10.37.129.10: icmp_seq=1 ttl=64 time=0.697 ms
64 bytes from 10.37.129.10: icmp_seq=2 ttl=64 time=0.715 ms
^C
--- 10.37.129.10 ping statistics ---
3 packets transmitted, 3 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.697/0.864/1.180/0.224 ms
❯ arp -a
? (10.33.16.15) at 3e:da:c8:2a:ea:5e on en0 ifscope [ethernet]
? (10.33.16.112) at 9e:f9:61:57:1:7a on en0 ifscope [ethernet]
? (10.33.17.52) at ba:d4:52:5:4b:42 on en0 ifscope [ethernet]
? (10.33.18.66) at 3a:d2:4d:6a:dc:e6 on en0 ifscope [ethernet]
? (10.33.18.102) at 94:8:53:46:75:d3 on en0 ifscope [ethernet]
? (10.33.19.254) at 0:c0:e7:e0:4:4e on en0 ifscope [ethernet]
? (10.37.129.10) at 0:1c:42:f9:18:97 on bridge102 ifscope [bridge]
? (224.0.0.251) at 1:0:5e:0:0:fb on en0 ifscope permanent [ethernet]
❯ 
```
🌞 **Wireshark it**

[Trames arp](arp.pcapng)

🦈 **PCAP qui contient les trames ARP**

# III. DHCP you too my brooo

🌞 **Wireshark it**

[Trames DHCP](dhcp.pcapng)

🦈 **PCAP qui contient l'échange DORA**
