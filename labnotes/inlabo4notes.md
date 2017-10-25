# Labo VPN

## oplossing minitest ssh

op toestel 16.8
ssh -L 8888:albinovm.groep1.iii.hogent.be:22 root@albinoni.groep1.iii.hogent.be

ssh -p 8888 root@localhost

ofwel via remote

op albinoni als er geen firewall zou zitten

## inleiding vpn

modes:

Dit kan in transport mode (pakket wijzigen)
of in tunnel mode (inpakken in nieuw pakket)

dan ah voor authenticatie en esp voor encryptie (en ook authenticatie)





# voorbereiding
## Vraag 1

### Enkel esp voorbeeld 

```

spdflush;
flush;

add 192.168.65.1 192.168.76.1 esp 0x10001 -m transport -E des-cbc 0x3ffe05014819ffff
add 192.168.76.1 192.168.65.1 esp 0x10001 -m transport -E des-cbc 0x3ffe05014819ffff

spdadd 192.168.76.0/24 192.168.65.0/24 any -P in ipsec esp/transport//require;
spdadd 192.168.65.0/24 192.168.76.0/24 any -P out ipsec esp/transport//require;

```

### Enkel ah voorbeeld


```
flush;
spdflush;

add 192.168.65.1 192.168.76.1 ah 123456 -A hmac-sha1 "AH SA configuration!";
add 192.168.76.1 192.168.65.1 ah 123456 -A hmac-sha1 "AH SA configuration!";

spdadd 192.168.76.0/24 192.168.65.0/24 any -P in ipsec ah/transport//require;
spdadd 192.168.65.0/24 192.168.76.0/24 any -P out ipsec ah/transport//require;

```


## Vraag 2

### Eerst eps dan ah

```
flush;
spdflush;

add 192.168.65.1 192.168.76.1 esp 0x10001 -m transport -E des-cbc 0x3ffe05014819ffff;
add 192.168.65.1 192.168.76.1 ah 123456 -A hmac-sha1 "AH SA configuration!";

spdadd 192.168.76.0/24 192.168.65.0/24 any -P in ipsec esp/transport//require  ah/transport//require;
spdadd 192.168.65.0/24 192.168.76.0/24 any -P out ipsec esp/transport//require ah/transport//require;
```

### Eerst ah dan esp
(zal nie werken omdat je je ip header kwijt gaat zijn)


```
flush;
spdflush;

add 192.168.65.1 192.168.76.1 ah 123456 -A hmac-sha1 "AH SA configuration!";
add 192.168.65.1 192.168.76.1 esp 0x10001 -m transport -E des-cbc 0x3ffe05014819ffff;

spdadd 192.168.76.0/24 192.168.65.0/24 any -P in ipsec esp/transport//require  ah/transport//require;
spdadd 192.168.65.0/24 192.168.76.0/24 any -P out ipsec esp/transport//require ah/transport//require;
```


## Vraag 3

met mode -m van de tunnel