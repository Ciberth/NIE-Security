# Lesweek 1

(op 27/09/2017)

## Inleiding

- Test op 5/12
- Punten voor labosessies blijven behouden
- Voorbereidingen zijn cruciaal
- Theorie-examen: stuk open en stuk gesloten boek

**Interessante websites:**
- crypto.stackexchange.com
- krebsonsecurity.com
- schneier.com
- darkreading.com

## Chapter 1: Introduction 

### What comes to mind when you hear the term "Security"?

**Brainstorm**
- Bescherming van de gegevens van gebruikers
- Infrastructuurbescherming
- Mensen leren
- Veilig overschrijven
- Sociale netwerken + media
- Op politiek en militair niveau
- Privacy (Security dient om privacy te beschermen, maar ook dit is niet absoluut)

Het gaat niet enkel om technische aspecten!

### Starting with a secure computer

- Antivirus op smartphone!
- Tot enkele jaren was er de mythe dat er enkel virussen waren voor windows. Er is momenteel evenveel gevaar!
- Opleiden van eindgebruikers (ook de niet technische) om veilig te zijn.
- Hoe goed een systeem ook is, human error kan ervoor zorgen dat het systeem onveilig is.

**The user remains a security risk!**
Zie bvb "vaak veranderen van wachtwoord" + "lack of knowledge"


### Social networks

- Wees er u van bewust dat alles wat je deelt kan gebruikt worden in social engineering.
- Faken van identiteit, uit naam van de CEO mails versturen is een techniek.
- "Your identity" is worth $5 on the black market.
- Moeilijke balans tussen privacy en wat je wil delen op sociale netwerken.

### Niemand is veilig

- Apple naaktfoto's -> via fake AP en redirect om terug in te loggen.
- M. Zuckerburg ook gehacked geweest. Zelfde ww voor linkedIn en facebook.

### Privacy vs security

- George Orwell - 1984 (geschreven in 1949) veel van uitgekomen.
- True speak is ook iets gelijkaardigs (alternative facts). (Media onbetrouwbaar maken) Gevaarlijk!
- Waar is de grens tussen computer criminaliteit.
- Er zijn er ook die zeggen "alles wat encrypted is, moet weg". Omdat dit gebruikt kan worden door terroristen en dergelijke. ~ China
- Het bezoeken van gevaarlijke sites is niet altijd gelijk aan slechte intenties hebben.
- NSA is niet de enige.
- Snowden was een IT consultant die veel dingen kreeg/inkijk had zonder dat dat de bedoeling was.
- "Wie bewaakt de bewakers?" (Latijnse quote)

### Zijn bedrijven altijd beter? En wat met media?

- Meestal gelukkig wel maar zeker niet altijd!
- Like's op andere websites en ze kunnen dus perfect volgen welke websites je volgt. Fb weet dus alles van je surfgedrag. 
- Uber - weet waar je zit.
- Media doet enorm veel! Wees kritisch.


### Niet alles is onomkeerbaar 

- Extra security maatregelen zorgen voor een daling in fraudegevallen.

### Future trends: bitcoin

- Methode: Cryptografische methodes / hashes 
- Het is een munt maar nog niet overal gezien als legale munt.
- Pieken zijn te verklaren door instabiele regimes. 
- Aantal dalingen zijn te verklaren door bvb China waar het niet meer legaal is. "Het is niet controleerbaar"
- Voor zo'n grote investeringen moet je bewust zijn van de politieke aspecten.

### Future trends: blockchains

- Veel andere toepassingen.

### Future trends: cyber warfare

- Schade veroorzaken.
- Vb. Stuxnet - nucleair programma enorm veel schade (miljoenen) aangericht.
- Petya (ransomware): Ukrain - vooral kritische infrastructuur. Vb. permanent deleten van files. Eigenaardig dat een ransomware zoveel schade aanricht en in theorie weinig opbrengt.

### Future trends: IoT

...


### Impact van data breaches

- Ashley Madison (ethical hacking)
- DNC email leak (political), ook bij de franse verkiezingen zijn er aanwijzigingen. 
- IoT botnet Mirai netwerk. Ip cameras, routers, ... -> open source gemaakt.
- WannaCry (ransomware)


### Waarom is security nodig

- Informatie heeft waarde
- Kan gestolen zijn
- ...
- Moeilijk in te schatten hoeveel "oude files" voor u waard zijn.
- Availability kan grote impact hebben.


### Overzicht van de cursus

- Chapter 1: Introduction
- Chapter 2: Basic concepts
- Chapter 3: Network and communication security
- Chapter 4: Encryption algorithms
- Chapter 5: Software and systems security
- Chapter 6: Intrusion detection
- Chapter 7: Future trends
- Chapter 8: Legal aspects
- Chapter 9: Guest speakers



## Chapter 2: Basic concepts

!! Security goals & protocols combinatie vraag is een belangrijke vraag op het examen voor inzicht in beide!
Dus gegeven een security protocol, aan welk model voldoet die?

**Network security model**

### Confidentiality

Alice gaat bericht sturen naar Bob, Carol of Trudy willen het onderscheppen, soms een derde partij (thrusted).

**Data confidentiality** = data can only be read by those who are allowed to read that data. 

Een "aanval" kan actief zijn of passief (eavesdropping). Als Carol het kan lezen dan is er geen confidentialiteit meer. 

Als Carol het niet meer kan lezen maar wel nog kan zien dat Alice iets stuurt naar Bob is traffic flow niet ok maar confidentialiteit wel. 

### Authenticatie

**Authenticatie** = je hebt de juiste gegevens om in te loggen
Dit is niet het zelfde als **identificatie** (hier is garandeer je dat dit de persoon in kwestie is).

**Attribute authentication** -> vb prof die op minerva iets kan aanpassen ; studenten niet. 

**Data-origin authentication** -> aantonen dat de data inderdaad van een specifieke bron afkomstig is. 

Op het model -> Carol die zich voordoet als Alice. In dit geval is Alice niet geauthenticeerd. Oplossing is bvb security tokens.


### Access control and authorisation 

...

### Data integriteit

= de data is niet gewijzigd. Maw er is niets verwijderd/toegevoegd/...
+ je weet wnr het bericht niet geldig is.

Op model -> "stel je moet betalen, wel betaal aan nen anderen" of "betaal meerdere keren"

Oplossing: security token + seq. no.

### Non-repudiation

Verloochening. Je kan niet verloochenen dat een bepaald bericht verstuurd of ontvangen is. 

### Availabilitiy

Bvb. Carol gaat overmatig veel berichten sturen zodat bericht van Alice niet meer zichtbaar is.
Als Carol vanuit meerdere bronnen stuurt is het veel moeilijker! (Distributed)

### Attacks

Passief: eavesdropping + traffic analysis
Actief: DoS + replay + hijacking + ...

**Soorten:**
- Brute force
- Crypt
- ...


**Categories:**
- Ciphertext only
- Known plaintext
- Chosen plaintext
- Chosen ciphertext
- Chosen text

**Hoe veilig kan je het systeem maken?**
Je streeft in principe altijd naar het zodanig lang maken voor te kraken zoda als het lukt het dan niet meer interessant/relevant is. 


### Symmetric encryption

Zender en ontvanger gebruiken dezelfde sleutel --> vaak voor confidentialiteit/authentiteit.

Example: Caesar Cipher

GCUA VQ DTGCM - easy to break (shiften over 2)

!!Weet dat die advanced methods (des, 3 des, aes, twofish....) weten wat/welke symmetrisch/assymmetrisch zijn.


### Assymmetric encryption

Public key bob en eigen Private key bob

Grote voordeel is dat er geen uitwisseling meer moet zijn (Bob zet zijn publieke key online)
Nadeel is dat het systeem complexer is en veel trager. Het is niet geschikt voor grote bestanden te encrypteren.

1024 bits RSA is lager in security dan de 128 bits AES!! 

Alles wat ge-encrypt is met private sleutel kan ge-decrypt worden met publieke sleutel. 
Dus Alice stuurt dan weet bob da het van alice is, maar er is geen garantie dat enkel bob dit leest want iedereen kan ontcijferen. 

Wel authentication maar geen confidentiality.

Vb'n van assym: RSA, EIGamal, ECC, Diffie Hellman, ...

### Hash-functies

"Lange key wordt gemapt op korte hash" interessant bij check digits, error codes en natuurlijk security.

Message digest = hash code

Birthday-attack!

**MAC** = Message integration codes
... 
gedeelde key om hash te maken vaak in combinatie met protocolen


-> Test yourself!!