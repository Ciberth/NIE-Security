# Lesweek 7

(geen lesweek 6)
(op 08/11/2017)

# Modern Cryptography

## HASH algorithms

**Verschil encryptie algos**
Bij encryptie algo's zijn er hier grotere blokken en sleutels.
Bij hash heb je ook niet per se een sleutel nodig maar heel belangrijk ze moeten beter bestand zijn tegen sleutelattacks.

Minder rondes dan bvb DES of AES en daardoor iets performanter. 

Bekendste zijn MD5, SHA-1...

### SHA-1

Net zoals AES opgenomen in standaarden en door NIST competenties verkozen.

512 bits nodig voor 160 bits hash value, iets veiliger maar trager dan md5 (denk ik)

### SHA-2

Grotere blokgrotes en langere hash waardes maar trager dan SHA-1.

Still not yet widely used -> Prof toch niet zo zeker van. Overal staat da maar toch oude bronnen. Pure encryptie algo's evolueren maar traag.

De SHA-512, de 512 staat voor de hashgrootte.

ROTR1 is rotatie naar rechts met 1 bit dan xor rotatierechts 8 bits xor shift rechts 7 bits

Met weinig bits wijziging toch grote hashfunctie wijziging!


### SHA-3

Keccak gekozen en werkt volledig anders. Het is ook parameteriseerbaar. Veiliger en sneller dan SHA-2.


## MAC algoritmes

Kan enkel gelezen worden door 1 ontvanger.
Zowel authentication + integrity in 1 functie.


### CBC-MAC

Tweede blok gaat afhangen van de eerste blok. Dus laatste blok hangt af van alles daarvoor.

Grootste nadeel: weinig flexibiliteit van de grootte van je mac (heel beperkt). Ander nadeel is niet ontwikkeld voor collision maar wel voor encryptie.

Ook futureproof.

### HMAC 

Eerste ding op slide p 153 -> unsafe omdat we bij eerste iets te weten komen over key als we message weten of in tweede da we bij de key iets kunnen toevoegen.

opad en ipad = grote hamilltonafstand dus afstand tss bits is maximaal

Wordt gebruikt bij IPSEC en TLS in de praktijk. Ook sneller dan CBC


# Chapter 6: Software & system security

## PGP

Iedere zender en ontvanger heeft publieke en private sleutel. 

PGP kan o.a. gebruikt worden voor authenticatie

(r64) -> 3 bits worden 4 bits.

Vroeger werden soms enters en tabs vervormd door spaties fzo via R64 is alles uniform. 

Twee schemas voor confidentialiteit en voor authenticatie oefen voor examen.

Eerst authenticatie en dan confidentiality en anders omgekeerd.

Twee time stamps zijn verschillend. Onderste is wanneer hij aangemaakt is en tweede wanneer hij signed is!!

Symmetrische sleutel w geencrypteerd voor de encrypte van het pgp pakket.

Een sleutel is betrouwbaar als hij getekend is door genoeg andere, ofwel door 1 persoon die we altijd vertrouwen ofwel door 3 die we meestal vertrouwen en het path tussenin mag maximaal 5 zijn.


Enkel owner kan public key revoction doen, dan moet je ondertekende revoke request versturen als eigenaar maar dit kan wel enige tijd duren!


## S/MIME

RFC 822 en SMTP ondersteunden geen multimedia en speciale characters en S/MIME is dan ontwikkeld om da op te vangen.

S staat voor security.

Clear-signed is interessant als de andere client S/MIME nie ondersteunt voor hem nog te kunnen lezen. Dus das wel voordeel tov pgp omda je dan client-onafhankelijk kan blijven. 

Vrij flexibel. 

## Web applications

Firewalls laten meestal http verkeer door. Er is soort perceptie http moet doorgelaten worden maar het is alles behalve onshculdig. HTTPS beschermt eveneens niet tegen bufferoverflows. 

### Misconfigurations

### Client-side controls

### Direct object reference

### XSS

Bij 1e vb slide moet je op de link klikken!

Persistente versies bestaan ook. 

Hier mikt men op bezoekers en niet op de hosts van de server!

Laatste vb is een DOM attack. Hier is eigenlijk de client kwetsbaar. De browser had niet mogen weergeven wat de fout was maar enkel er is een fout! Net zoals bij ww/user combo.