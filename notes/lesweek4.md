# Lesweek 4

(op 18/10/2017)


## Intermezzo: Krack-attack

"Foute implementatie"

Binnen wpa2 is er een uitwisseling tussen station en ap. En die AP ga bericht sturen naar station die da moet encrypteren (forward handshake). Op zich ok. Maar er was een functie die ge meer dan 1 keer kon oproepen. En het station ging opnieuw een bericht encrypteren en opsturen.

Een aanval kan het eerste bericht opnieuw en opnieuw sturen. Om zo de boodschappen voorspelbaar maken. 
Een station mag dus nie meer dan 1 keer beantwoorden en vanaf nul initaliseren (die nose)

Meeste zijn al gepatched. Veel van die android devices worden spijtig genoeg nie snel geupdate. 

Mooi vb van systeem da intrisiek veilig is, maar toch nog holes heeft. 
Normaal is er bufferperiode bij patches maar openbsd heeft zich daar niet aan gehouden.

Routers zijn op zich zelf nie kwetsbaar, het zijn de clients.

## Data link layer: WEP & WPA

Groter gevaar bij wifi vandaar: WEP & WPA.

Wrm data link security nodig... (dia 4)

CAM
Door switches in hub te veranderen verzadig je het netwerk zwaarder. 
Al het verkeer kan je ook sniffen wat anders nie over u poort gestuurd w.

ARP spoofing

DHCP starvation

A hidden node problem/attack

Stel a wil naar b sturen 
en na sensen zal hij naar b sturen
c kan nie lezen da a al stuurt en dus b krijgt beide tegelijk
opl: rts/cts

**Hoe kan je dit systeem als aanvaller misbruiken:**  
als aanvaller zou je cts kunne sturen en zegge da hij continu "bezet" is en de legitieme gaan wachten tot het medium vrij is maar als jij cts blijft herhalen dan gaan anderen zelf nie meer proberen en is het dus wa down. 

WEP werd gepromoot als grote stap voorwaards en da was het ook maar zeer snel was duidelijk dat dit niet veilig was. Dan is WPA gekomen maar die was tijdelijk en dan WPA2. 


### WEP

Auhtenticatie in de vorm van een gedeelde sleutel. 

**Mooie examenvraag**: geef verbeterpunten voor WEP protocol. 

Dia 11: de eerste VIER zaten in wep en de laatste twee zijn er in wpa bijgekomen


Authentication using ssid was da u ssid nie aan het sturen da hij er was. Dus client moest zelf probe sturen.
Probleem is da u initiele bericht (probe) in plain text gestuurd w en dus als iemand sniffed ziet hem het al. 

MAC address filtering

op luchthavens vaak nog gedaan 
maar onveilig tegen mac spoofing. 

Problemen:

key was zeer klein

WPA authentication

Supplicant (client) - authenticator (ap) - authentication server (men wil afzondering dus los van ap)

Protocollen bouwen verder op mekaar zie EAP-TLS


## Firewalls

Wat: 
- controleren welke diensten toegankelijk zijn 
- controleren van users
- gedrag gaan controleren

Opletten: niet veilig tegen zaken die er rond kunnen (opzetten ap)

3 types: packet filtering + crcuit level + proxy

Hoe hoger hoe beter de beveiling maar hoe hoger de overhead.


Firewall gaat ieder ip pakket inspecteren. 
Filter rules ..

Grootste nadeel is dat het zeer beperkt is. 

stateful inspection 

vooral interessant waar je eigenlijk niet op voorhand weet welke poorten gebruikt gaan worden

time out bij tcp (udp heeft sowieso time out)


### Circuit level gateway

"relay at tcp level"

### SOCKS

firewalls omzeilen (china)

(ook proxy)

### Application level gateway aka proxy

applicatie specifiek 
die gaat enkel verkeer toelaten als je eerst naar de proxy gaat
interne communicatie gaat naar proxy


sql injecties kunnen deteceert worden
debug dingen

inkomende mail scannen (dus groot voordeel)
grootste nadeel is dat het veel complexer is

niet alle software kan omgaan met proxies (proprietary) email en browsing da wel maar matlab bvb niet

Firewall op wat voor soort device zet je dat? - vaak pc vast bastion

Waarom 2 poorten ipv 1 poort

ip spoofing is een groot probleem dus als er een lokaal intranet ip binnenkomt via internet dan kan je da al blokken

+ veel strengere rules voor internet dan intranet

screened subnet firewall p26 en DMZ


personal firewalls

interne gebruikers zijn vaak het grootste risico


Volgend hoofdstuk (4)

# 4. Encryption Algorithms

### Steganography

verschil met cryptografie
(stegano gaat het verbergen, cryptografie gaat het nie per se verbergen maar anders tonen)

eens u systeem bekend is, is het niets meer waard
bij cryptografie is het bekend en dat is ok

watermarking is nie makkelijk deelbaar
behalve als je weet welke distributie 
technieken eerder ter illustratie

### Cryptografie

Mono alfabetische

ceasar cipher
(4 bit sleutel)

Willekeurige shuffle is al een eerste improvement

grotere sleutel dus das veiliger maar onze taal is voorspelbaar (veel voorkomende letters)


zoveel mogelijk entropie generen

entropie is een eenheid voor de chaos/onvoorspelbaarheid


bij die eerste eerder lage entropie
en bij da tweede een entropie van 1 
en daaruit volgt de polyalfabetische substitie

alberti cipher


digraph 



