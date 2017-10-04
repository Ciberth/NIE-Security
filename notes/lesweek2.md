# Lesweek 2

(op 4/10/2017)

(Chapter 3)

## Inleiding (Network model)

**Mogelijke problemen**

- Network security vs system security (chapter 5).
- Sniffer
- Router hack

Hierdoor moet er beveiliging zijn op meerdere niveau's. 

**Hoe hoger je op de laag zit, hoe minder er ge-encrypteerd is.**
(Wel hoe "makkelijker" het gebruik)


## SSH (Secure Shell)

- Applicatielaag protocol
- Je gaat van laptop een connectie opzetten en die encrypteren
- Je kan ook ssh'n naar een router terwijl die eigenlijk geen applicatielaag heeft (lijkt beetje raar)
- Voorganger was telnet (het is echt achterhaalt) = alles plain text
- Ssh kan ook gebruikt worden voor tunnels op te zetten
- X-session forwarding = grafische omgeving van remote server binnen te trekken
- Symmetrische encryptie met minimaal 128 bit keys
- Nieuwe security algoritmes toevoegen is mogelijk (groot voordeel aan ssh)

Bestaat uit 3 blokken:
* transport layer protocol
* user authentication protocol
* connection protocol

SSH werkt dus wel boven de transportlaag! Sommige zijn optioneel (je moet niet per se authentication zijn)

### SSH transport layer protocol

== boven transportlaag!

* Server authentication, confidentiality and integrity
* Compression (optional)
* Bovenop *betrouwbare* transportlaag (vb. TCP)

Pas na tcp connectie kan het protocol beginnen.
Versies doorsturen is relevant voor bvb bugs / verschillende versies van ssh / bepaalde security algos of encryptiemethodes die mogelijk nog niet gekend zijn door een partij.


Client stuurt SSH_MSG_KEXINIT (Key Exchange Init). De client kan kiezen welke protocollen hij eerst wil en de server zal sequentieel alles afgaan en als het matcht gebruikt men die.

Service request definieert welke dienst de client wil van de server.

De encryptie is vanaf newkeys dus vlak voor service request (daarvoor is het plaintext).
Je kan er toch voor zorgen dat dit veilig is zie straks.


**Binary packet protocol**

Twee redenen waarom Padding w toegevoegd:
- Veelvoud van de blokgrootte
- Traffic analyse vermoeilijken omdat het er anders "uit gehaald zou kunnen worden".

Seq # worden standaard op nul geinitialiseerd

aes128 is veiliger dan 3des(168) triple des is eigenlijk minst veilige


Meerdere verschillende functionaliteiten (x-session, commandlines) zullen over dezelfde lijn gebeuren om performantieredenen. Dus dezelfde zaken worden hergebruikt.


Elke keer als je een nieuwe sessie opzet worden er nieuwe sleutels aangemaakt. Men wil niet dat sleutels hergebruikt worden. Op die manier is een sessie die gepakt is geen probleem voor later.

- Diffie Helman
- server wordt geauthenticeert via publieke sleutel
- die publieke sleutel wordt ook gebruikt voor signatures

Nadeel is dus wel dat er wat gebeurt aan logica nog voor er authenticatie is (kan gebruikt worden voor dos-attacken). Er bestaan algo's die authenticatie al gebeuren vanaf softwareversion exchange ipv ssh_msg_kexinit.


### User authentication protocol

3 mogelijkheden:
* public key
* password
* host based


In de failure zit er meer informatie met methodes bvb. Client stuurt daarna weer met de gekozen methodes
daarna ofwel "keb nog gerief nodig" ofwel "ge zijt geauth".

Verschil tss password en host based. -> Clients moeten publieke sleutel hebben. 

### SSH Connection protocol

Ieder kanaal is configureerbaar, ze worden wel allemaal encrypt. 
Je kan bvb kiezen voor compressie, maximale snelheid, bloksnelheid (soms wil je snelle interactie voor bvb interactieve shell,...)


### SSH port forwarding (vpn functionaliteit)

Omvormen van een onveilige connectie naar een veilige.
2 varianten locaal en remote port forwarding

Local port forwarding is meest gebruikte.

werk naar home en vanuit home naar yahoo
vereiste firewall moet ssh toelaten 

ssh'n naar home

```
-L (local port forwarding)

ssh -L 9001:yahoo.com:80 home

en dan surfen naar localhost:9001
```
stel bij ftp dan geef je je credentials nog steeds vanop work in
nadeel is da home systeem moet aan staan (poor man's vpn)

```
Banned pc dus je stuurt nu eigenlijk nog een nieuwe ssh connectie door

```

Alternatief is remote port forwarding

```
vanaf home naar work maar commando begint vanaf werk pc
dus je zegt eerder ik ga dingen voor u doorsturen
dus vanaf work:

ik ssh naar home en alles wat er gestuurd wordt vanaf home naar 9001 zal ik sturen naar intranet:80

ssh -R 9001:intra-site.com:80 home
``` 

Een van de grote nadelen is als je naar eender welke site wil surfen dan is alternatief **socks proxy**

Dynamic port forwarding

```
SOCKS proxy
ssh -D 9001 home
```


TCP -> no IP address roaming ondersteund!


## Exchanging keys

Binnen ssh moete sleutels uitgewisseld worden.

Meest eenvoudige is out of band maar minder geschikt voor bedrijven.

Doel is telkens het afspreken van een sleutel die beide partijen en die toch nie makkelijk is voor anderen.

**Diffie-Hellman** = mathematisch probleem

3 is primitieve wortel module 7
men kan heel moeilijk voorspellen in welke volgorde ze gaan komen
dus tot welke macht moet je generator verheffen om 4 uit te komen -> zeer moeilijk

oud maar veelgebruikt protocol


Alic en bob voorbeeld

Publieke sleutel Alice: 5^6 mod 23 
Publieke sleutel Bob: 5^15 mod 23

Wat is de gedeelde sleutel : 2

In praktijk grote waarde van a, b en p

Grote zwakheid van Diffie-Hellman = man in the middle attack

Problemen

Berekeningen zijn complex -> gevoelig voor DOS attacks 


Ephemeral DH -> altijd nieuwe keys bij elke sessie.

publieke methodes -> dure berekeningen 


### KDC

"het maken van symmetrische encryptie outsorcen naar een betrouwbare derde partij"

KDC beslist wie mag spreken me wie.
Je hebt master key (per user 1 key naar kdc) en sessie key voor communicatie naar endevices.

N1 is om aan te tonen dat het "nu" gegenereerd is (replay te vermijden) (nonce?)

wat is de bedoeling van 4 en 5 -- bedoelt voor authenticatie

in 4 toont aan dat bob wel degelijk bob is en 5 da ze wel degelijk alice is

improved -> 1 message kan een groot verschil maken

inzicht hierin hebben!

### Asymmetric encryption

public available directory = server waar men sleutel gaat registreren

iedereen die will communiceren moet hier eerst aan vragen en om die stap te vermijden is de PKI er gekomen men wil eigenlijk een centraal punt vermijden. 


Meestal minder CA's dan end-user. Je moet dus maar een paar ca's vertrouwen en nie miljoenen gebruikers
Ra's -> voor load te verspreiden.


CA hierarchy

Ca's vertrouwen van andere Ca's

hoe lager in de hierarchy hoe korter de geldigheidsdatum

### X.509 authentication