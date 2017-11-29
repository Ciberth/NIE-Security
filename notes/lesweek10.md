# Lesweek 10

(op 29/11/2017)

# Vervolg secure systems
## Trusted OS
= "veilig genoeg"

Er worden bepaalde security policies gedefineerd en we hebben er vertrouwen in dat deze enforced worden. En men gaat er dan van uit dat dat voldoende is.

### Policies

vb.
Unclassified > restricted > confidential > secret > top secret

Toegangsaccess -> compartments.

Onderzoeker -> R&D
Accountant -> financiële zaken
Manager -> beide

Discretionary vs Mandatory access control vs Role-based access control

Mandatory : admin kiest auth. Het is dus verplicht om altijd regels of labels toe te kennen aan informatie


RBAC meest gebruikt en is zelfde als MAC maar dan voor groepen/roles.

**TCB** = alles wa nodig is om u os veilig te maken (zowel software als hardware). 

Echt veilige systemen hebben een compact security kernel met daarbovenop een os. 

### Disk encryption

Vooral tegen fysiek verlies van de harde schijf. 
Op filesysteem level krijgt deze een add-on om folders te encrypteren. Je breidt het dus uit. Nadeel is dat de meta-data vaak niet mee encrypted wordt. Toegangsrechten, tijdstippen...

Full disk -> echt alles w encrypted, zelf tijdelijke bestanden in het geheugen is beschermd.
Nog niet per se echt veilig. Cold boot attacks (onmiddelijke restart na afsluiten), key loggers...

**Plausible denial** -> "als iemand u verplicht om een passwd in te typen; kan je een ander ww ingeven die een andere partitie gaat laden om zo te kunne zeggen ah nee keb die files nie staan".

Trusted platform module -> kijken of er geen hardware is toegevoegd

(einde secure systems)

# Secure Software

## Malware

Malware is niet per se hetzelfde als een virus. 

### vb Logic bomb

Stukje software dat zal geactiveerd worden mits aan bepaalde voorwaarde voldaan is.

### Backdoor

Gebruikt om traditionele authenticatie vormen te ontwijken. Soms met opzet in software gestoken voor gemak (godmode).

Verschillende soort backdoors. 

### Mydoom worm

Botnet spam 

### Trojan horse

### Spyware

Vroeger was da voor antivirussen beetje een discussie of het ongewenst was of nie en zo kwamen er rechtspraken.


Eeuwige discussie tss wat is spyware en gebruiksgemak.

...

Eerste malware in 1971 "the creeper".
First Trojan horse 1975 "animal game".

...

## Software cracking

...

# Chapter 6: intrusion detection


"Wat is een aanval?" -> is nen poortscan een aanval?
Allemaal onduidelijk.

AD in principe nutteloze noice maar is het nutteloos - nee je bent wijzer geworden.


ID = intern 
voor bvb als er iemand toch voorbij firewall geraakt is
nuttig maar eigenlijk te laat

Idealiter dus beide


merk op de false negatives en false positives (statistiek)


Audit data -> grote differentiatie tss vendors en dat combineren moeilijk en lastig is.

Je kan ook ID op pc zelf zetten (vergaand). 
Data verzamelen van het netwerk is het alternatief. 

User heeft dan geen impact op de performantie, en de aanvaller kan niet zo makkelijk wijzigen + is ook crossplatform en je kan info verkrijgen die op host niveau niet altijd beschikbaar is.
Vraagt natuurlijk wel wat overhead op het netwerk. Het heeft vaak ook moeite met encrypted pakket of custom applicatiepakketen. Dus vaak zowel host logs als netwerk logs verzamelen.


