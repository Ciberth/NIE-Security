# Lesweek 9

(geen lesweek 8)
(op 22/11/2017)

### Vervolg XSS

**Three types of XSS:**
- non persistent 
- persistent
- DOM-based

Phishing is ook een klein stukje code op officiële website die opnieuw vraagt naar credentials (via klein frame oid). Voor gebruikers is dit minder transparant.

Gevolgen van XSS kunnen zeer ernstig zijn, zeker op lange termijn (bvb gebruikers die niemeer willen terug komen bvb)

### SQL injectie

Je gaat je HTTP request omvormen omdat je weet dat het omgezet wordt naar een SQL query.
In-house modules en code zijn vaak kwetsbaarder dan grote CMS'n.

### CSRF

Komt iets minder vaak voor maar is potentieel nog gevaarlekijker dan xss.
Victim gaat naar kwetsbare website.

Ander vb. 

Torrenting ; utorrent heeft ook webinterface waar je met GET requests dingen kan triggeren. Je kan je gui dus via restfull interfaces beheren. 

Browser ging naar slechte websites met daarin afbeeldingen met daarin Requests die op localhost iets gingen doen nl malware downloaden. 

**Limitation** zowel client actief runnen als toegang op forum om die images te zetten/en client binnen te trekken. 

Maar geen eigenlijk webservice nodig dus wel krachtig en ook krachtig om het van het standpunt is van wat u browser trust. 


### Defenses

Heel dit beveiliging verhaal is dus een argument om niet altijd aan in-house web dev te doen. Bovendien moet je je werkgever duidelijk maken dat een website maken niet een eenmalige taak is maar een continue!


### Sanitization

Vertrouw niet wat de gebruiker ingeeft. 
Bij tweede probleem is de slechte code slecht maar gaat de browser wel de code nog steeds het uitvoeren (browser kan da interpreteren).


## System

### Passwords

Nooit wachtwoord op slaan in plain text. Via hash! En daarom kan een bedrijf u uw wachtwoord niet geven.

### Brute-force attack

...

Iets wat in 1 taal veilig is, kan in een andere taal zeer onveilig zijn.


### Hash chains

Idee is da je hash terug kan vormen; idee is sequentiele hash reductie hash reductie hash reductie ; en enkel eerste en laatste w opgeslaan.

Met zeer weinig memory kan je enorm veel mogelijkheden opslaan.

password lookup process is dan in omgekeerde weg nie enkel hash reductie hash reductie maar iteraties hiervan 
veel minder tabellen en geheugen nodig. 

Salt is extra bit die deze methodes kan tegengaan. -> Goede beveiliging

Rainbow table attacks en dictionary attacks voelen dit

reductiefunctie zal rekening moete houden met de salt (per user) dus alle precomputed dingen van online zijn niet meer bruikbaar. Dus al dat werk moet je opnieuw manueel doen.

Salt is unencoded want die moet mee gehashed worden en het systeem moeten weten dat da salt is.

Vroeger ww hash in /etc/passwd nu in /etc/shadow


### Biometry

Zelf 1-eige tweelling heeft andere fingerprint


Fingerprint is niet revocable. Eens die gekend is dan kan iedereen da gebruiken.

### Security tokens

Kan fysisch zijn maar ook niet fysisch. Voordeel al u security dingen worden extern uitgevoerd. Alle berekeningen blijven op de token. Vaak 2FA. Bezit + kennis.
Nadeel ook blackboxes (bij biometry was da ook beetje) je weet niet echt altijd wat er under de hood zit/gebeurd.

