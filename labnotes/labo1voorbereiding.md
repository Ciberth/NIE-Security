# Voorbereiding labo 1: Routing + DNS

## Overzicht

- [ ] Interfaces overal in orde?
- [ ] Gateway ok (route)?
- [ ] Pingen van
- [ ] this is an incomplete item

## Interfaces instellen

### Manueel

```
ifconfig eth1 192.128.1.1 netmask 255.255.255.0 up
ifconfig eth0 192.128.2.3 netmask 255.255.255.0 up
route add default gw 192.168.4.5 eth0
``` 

### Persistent

```
# Zie files /etc/sysconfig/network-scripts/ifcfg-eth0 

DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
NETMASK=255.255.255.0 # ofwel PREFIX=24
IPADDR=192.168.16.89
GATEWAY=192.168.16.8 # al dan niet gateway

```


## OSPF

```
# Config files zebra.conf en ospfd.conf 
# te vinden in /etc/quagga
# + vergeet niet met areas te werken 
# -> vaak area 0

sudo systemctl status/restart/enable zebra/ospfd

# routing niet vergeten op de gateway

# manueel
sudo echo 1 > /proc/sys/net/ipv4/ip_forward 

# persistent
net.ipv4.ip_forward = 1

# in /etc/sysctl.conf

```

### Zebra.conf

```
hostname name
password pass
enable password pass
interface lan0
!
interface lan1
!
```

### Ospfd.conf

```
hostname name
password pass
enable password pass
interface lan0
!
interface lan1
!
router ospf
  redistribute connected
  network 192.168.1.0/24 area 0.0.0.0
!
```


## DNS

### Algemeen

- De tools **named_checkconf** en **named-checkzone** kunnen hulp bieden!
- Zorg dat de rechten van de zone bestanden in orde zijn: ``chown named:named zone``.
- Gateways moeten toegevoegd worden in de ``/etc/named.conf`` file.
- Als er een slave is configureer deze goed met een **masters** en **type master** bij master.


### Voorbeelden

**DNS Master**
```
options {
    directory   "/var/named";
    dump-file   "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    memstatistics-file "/var/named/data/named_mem_stats.txt";
    allow-query     { any; };

    recursion yes;

    pid-file "/run/named/named.pid";
    empty-zones-enable no;
    forwarders { 192.168.16.8; };
};

logging {
        channel default_debug {
                syslog daemon;
                severity dynamic;
        };
};

zone "groep17.iii.hogent.be" IN {
    type master;
    file "groep17.iii.hogent.be";
    allow-transfer { 67.168.192.254; };
};


zone "67.168.192.in-addr.arpa" IN {
    type master;
    file "67.168.192.in-addr.arpa.dns";
    allow-transfer { 67.168.192.254; };
};
```

**DNS Slave**
```
options {
    directory   "/var/named";
    dump-file   "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    memstatistics-file "/var/named/data/named_mem_stats.txt";
    allow-query     { any; };
    recursion yes;
    pid-file "/run/named/named.pid";
    forwarders { 192.168.16.8; }; 
    empty-zones-enable no;
};

logging {
        channel default_debug {
                syslog daemon;
                severity dynamic;
        };
};

zone "groep17.iii.hogent.be" {
    type slave;
    file "groep17.iii.hogent.be";
    masters { 192.168.67.1; }; 
};

zone "67.168.192.in-addr.arpa" {
    type slave;
    file "67.168.192.in-addr.arpa";
    masters { 192.168.67.1; }; 
};

```

**Forward**
``/var/named/iets.x.y.z.be.dns``

```
$TTL 60
@   IN SOA  iets.x.y.z.be. thomas.clauwaert.ugent.be. (
                    1   ; serial
                    60  ; refresh
                    1H  ; retry
                    60  ; expire
                    3H ); minimum
        		IN  NS  pokemon
bulbasaur 		IN  A   192.168.1.1
charmander  	IN  A   192.168.1.2
squirtle   		IN  A   192.168.1.3
pikachu		  	IN  A   192.168.1.254

```

**Reverse**
```
$TTL 60
@   IN SOA  1.168.192 thomas.clauwaert.ugent.be. (
                    0   ; serial
                    60  ; refresh
                    1H  ; retry
                    60  ; expire
                    3H ); minimum
    IN  NS  pokemon.iets.x.y.z.be.
1   IN  PTR bulbasaur.iets.x.y.z.be.
2   IN  PTR charmander.iets.x.y.z.be.
3   IN  PTR squirtle.iets.x.y.z.be.
254 IN  PTR pikachu.iets.x.y.z.be.
```

Merk op dat op de clients er ook instellingen gewijzigd moeten worden zoals de hostname/

In ``/etc/resolv.conf``

```
nameserver 127.0.0.1
nameserver 192.168.67.1
options rotate
```