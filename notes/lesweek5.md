# Lesweek 5

(op 25/10/2017)

## Herhaling vorige week + verder gaan met

Zijn zeer lang nuttig geweest (enigma wo2) maar met de komst van de computer zijn deze ook maar minder en minder bruikbaar. 

### Transposition cipher

Inverteren van de zin of het woord of ook wel de ScyTale

hier weer opnieuw niet meer zo veilig door de pc maar als je niet weet wat encryptie is dan is dit wel een eenvoudig systeem om te maken/encrypteren en toch vrij robuust.


### Rail Fence cipher

Grid maken en geschrankt alles opzetten.

"Hoeveel bits je hier hebt, de encryptiesleutel van het systeem" 
De sleutelgrootte zegt typisch iets over het aantal combinaties, hier: maximaal 4 nodig (aantal rijen is 3).
Dit is dus relatief makkelijk te kraken via brute force.

### Columnar Transposition cipher

Je gaat kolom lezen en je krijgt key die zal zeggen welke kolom je eerst gaat lezen


Nadeel: ze gaan bepaalde stukken van je woord niet verbergen "departed" de ... ed 


### Nadelen

substitiutie frequentieanalyse
transposition annagramming

oplossing is beide combineren na elkaar

### Rotor driven approaches

Enigma en dergelijke 


Al die oude manieren gingen er van uit dat je niet wist hoe het systeem werkte.
Hier wist je wel dat de vijand een encryptiesleutel had en de methode zelf was relatief publiek. Maar zelf als de encryptiemethode niet meer geheim is dan nog kan de aanvaller het niet echt makkelijk decrypteren.


## Moderne cryptografie

Systemen die computationeel veilig zijn

block cipher vs stream cipher (bit per bit gaan encryptere) deze laatste worden minder gebruikt maar is nog steeds nuttig. Audio/video streams. Of bvb internet of things. Of sensoren in autos

S-boxing en P-boxing (Feistel Cipher)

Het hele process moest publiek geweten zijn en toch nog veilig zijn. Nen xor op basis van een functie (op basis van een sleutel)

meerdere sleutels + gekend process

De substititues - xor's
en de transposities van links naar rechts
en dat doe je n rondes na mekaar


diffusie = als je 1 karakter wijzigt moet dat veel invloed hebben op u cipher
confusion = statische analyse zo moeilijk mogelijk maken

### DES & 3-DES

Eerste gestandaardiseerde encryptiemanier/implementatie.
Nsa heeft de beveiliging al gereduceert. Door die specifieke groottes kon de nsa makkelijker kraken.

8 nutteloze bits bij de key (pariteitsbits)

Begrijpen voor examen!

merk op de subkey zelf zijn maar 48 bits ipv 64/56. Waarom!

We beginnen met een permutatie om de sleutel nog onvoorspelbaarder te maken (wegnemen van voorspelbaarheid)
Sommige sleutels zijn verboden in des 

"er zijn een aantal sleutels die niet veilig zijn in des, kan je zo 1 vinden en waarom zou die niet veilig zijn?" --> antwoord omdat het ongewijzigd uit die permutatie komt!!


soms 1 shift, soms 2 ook weer om die voorspelbaarheid te voorkomen.

Die e-box gaat onze 32 bit expanderen tot 48 zodat er geXORt kan worden met die sleutel.

Basicly input dupliceren


s-box

IN: 8 maal 6 bits
OUT: 8 maal 4 bits

hardware implementatie
die zes bits worden gezien als een soort adres



11 (eerste en laaste) is 3 -> derde kolom
0100 )> de vierde kolom en dus is de output 4 en al die outputs staan voorgesteld door iets da in 4 bits kan voorgesteld worden


p-box is permutatie
(elke ronde is dezelfde)

de uitkomst wordt nog eens geXORt met de linkerkant 


Meeste data bestaat uit meerdere blokken van 64 bit en da zijn die andere
electronic code book
cbc (chaining)
...


grootste nadeel: heel veel informatie over de oorspronkelijke wordt behouden (de structuur dus) 

Information leakage 

CBC: er is ook een IV = initialisiatie vector die wordt gebruikt zodat de eerste mapping onvoorspelbaar w
(zo kan je de headers niemeer achterhalen bij een IP pakket fzo)


nadeel: 1 bit error zorgt voor volledige misvat op 1 blok en genereert ook 1 bit error in de volgende blok

s-bit

stream cipher eigenlijk we willen bijna bit per bit werken (dus byte per byte xorn)

bij cbc werd je plaintext geencrypteerd en gedecrypteerd maar bij s-bit cfb dient u ciphertext als input en plaintext als output (dus het zelfde schema w gebruikt voor encryptie/decryptie)

Examen: gegeven encryptie stel decryptie op


s-bit output feedback

grote voordeel zit bij bit errors (hier heb je maar 1 blok) bij het vorige nam je de fouten telkens mee (zeer interessant voor systemen met packetloss)


CTR 

werkt met een counter die altijd opgeteld w 
zie slides


Deze methodes worden ook gebruikt bij AES en andere symmetrische

de sleutelgrootte vergelijken tussen twee systemen zegt neits


DES nog veiliger maken -> DES meerdere keren na elkaar

triple des werkt met 3 verschillende sleutels

DES is zwaar achterhaald maar zeker niet nutteloos

DES is gemaakt voor hardware, software implementaties zijn zeer inefficient

### AES

- Rijndael algoritme
- wel veilig

geschikt voor hard- en software implementaties


## Assymetric

### RSA

De twee originele priemgetallen terugvinden is moeilijk!

### Elliptic Curve Cryptografie

ook veilig naar de toekomst toe (quantumcomputing)

a = generator	

de dot operatie gaat zeer snel en als je de eindsituatie weet kan je heel moeilijk afweten welke weg alles heeft afgelegd

sneller en veiliger dan rsa
mogelijk nadeel: nsa heeft hier wel inpact gehad, den RNG kan een backdoor hebben

diffie hellman = elke sessie maakt nieuwe sleutels aan