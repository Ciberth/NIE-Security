# Lesweek 11

(op 06/12/2017)


# Vervolg intrusion detection

Audit logs = van de systemen, poorten, pings, enz. Vaak worden ze gecombineerd om inzicht te krijgen in de activiteiten van de gebruikers.

## Practical approaches

### Statistical approach

Alles wat afwijkt van normaal gedrag is verdacht. Kan wijzen op malware, een aanval...
Het probleem is dat dit vaak **false positives** gaat geven!

### Rule-based approach

Hier gaat men definieren wat alleszins niet mag. X aantal poorten scannen is niet toegestaan bvb. 
Nadeel is dat dit vrij outdated kan zijn en dat je dus achterop de feiten loopt. 



## Statistical detection 

Men gaat gebruikerspatronen bekijken en definieren wat we van de gebruiker verwachten om zo te kijken of alles ok is of niet.
Het definieren van thresholds (bvb na 5 keer verkeerd inloggen wordt je account geblokkeerd of als de login tijd minder is dan 2 seconden dan is het wellicht nen bot -> negeren). 

Voordeel: vrij eenvoudig toe te passen maar het typisch gedrag van een netwerkadmin =/= programmeur =/= accountant.

Er bestaat ook een **profiel gebaseerde aanpak** dan gaat men op basis van het profiel regels toegepasseerd (in de praktijk meer gedaan). 

Nog verder is **anomaly detection**. Hierin gaat men het typisch gedrag van het systeem definieren. Ipv gebruikers zijn het hier dus systemen. 

Groot voordeel
- kan om het even welke aanval detecteren
- updatebaar

Nadeel
- te veel false positives
- geen idee wat of waarom alleen da er iets was (relatief weinig kennis en men moet nog zelf zoeken)


-> Opgebouwd via statistische methodes. 

Markov ketens = toestanden definieren met probiliteiten. 

Neurale netwerken doen het goed. Die moet je ook niet continu opnieuw modeleren maar traint op bestaande dataset. 


## Rule based 

- misuse detection
- burglar (wat mag een eindgebruiker doen en wat niet)


### Misuse Detection

= Penetration identification 

Vaak platformspecifiek (nadeel) en kan cpu intensief zijn (alle rules moeten gecheckt worden) -> real time detectie is beperkt.

Te vergelijken met antivirus. 


### Burglar alarms
eigenlijk een variant van misuse detection

Bij elke wijziging aan het netwerk moet dit aangepast worden (nadeel). Vooral bij jonge bedrijven is dit vaak lastig. 


### Hybride approaches

Commerciële producten zijn vaak hybride. 


### Privacy

Veel landen hebben strenge wetgeving. 
- Geen persoonlijke informatie opslaan die de gewoontes kunnen afleiden. 
- Data mag je verzamelen die niet privacy gerelateerd is en als je er niet kan uit afleiden wie die user is. 
- Packet headers mag je inspecteren
- Packet contents das al moeilijker, maar zoeken naar bepaalde strings da mag wel. 
- Mails lezen mag niet (ook geen werkmails). 
- (Recht op privemails versturen via werkemail). 


## Honeypots

Fake systeem voor aanvallers zodat ze dat systeem eerst aanvallen. Informatie verkrijgen hoe aanvallers te werk gaan. En je kan zo detecteren/monitoren terwijl je je kritische systemen wel nog veilig stelt.
Vaak nen VM maar da heeft vaak verdachte zaken (generic namen voor printers, geen pings...)


## Limitations

Ze kunnen geen software bugs oplossen. Geen alternatief voor updates.
Als u data encrypted is, kan je ook veel moeilijker analyseren. 



# Chapter 7: Future Evolutions

## Cryptocurrency and block chains

Cryptocurrency = variant van virtuele currency maar niet omgekeerd.

Gaat gebruik maken van cryptografische methodes. 

Groot verschil met traditioneel geld = volledig gedecentraliseerd (visa is gecentraliseerd bvb, traditioneel geld - centrale bank)

Bitcoin is het bekendste voorbeeld. 

Silk Road = plaats op the dark web. Bitcoin is niet anoniem, iedereen die bitcoin heeft, heeft een identiteit. Maar dat is een virtuele identiteit. Dus de link met de echte persoon is niet gekend.
Men denkt dikwijls dat het onlinkbaar is maar het is zeker niet onmogelijk om te weten te komen wie eigenaar is van bitcoins. 

Bitcoin stijgt in waarde - maar aantal transacties blijft relatief gelijk. 

Vaak is een crash gelinkt met politieke zaken. 

Er zit ook een vote systeem in voor wijzigingen van het bitcoin protocol -> gedecentraliseerd 

Heel het netwerk checkt ook of je die munt wel mocht spenderen. 

"Ledger" -> publiek beschikbaar en kan verified worden door iedereen die bitcoin protocol gebruikt. 

Mooie Examenvraag: availability bij bitcoin.  

Eigen bitcoin hash met publieke sleutel van den anderen en dat ondertekenen met eigen private sleutel. Dan in ledger kijken of 1 gesigned is en bedoelt is voor 2. We kunnen steeds verifieren of een transactie gebeurd is. 

Zo kan je ook zien hoe de bitcoinen geevolueerd zijn (hoe ze van A naar B naar C zijn gegaan).

1 transactie kan soms meerdere transactie omvatten (tss haakjes)

Transactie wordt gehahsed met publieke sleutel nieuwe eigenaar en getekend door private sleutel van oude eigenaar.

Minen:
De gevonden nonce w gebruikt om de vorige transactie te lokken zodat daarna die opnieuw gebruikt kan worden. 

Als bitcoins op zijn moet je wel nog iets vinden om miners te laten minen voor u transacties te laten verifieren. Incentives. Block (1mb) is nu wa te klein om alles op te vangen van 10 min (?) nu kiest men de die die meeste fee hebben. Nieuwe eigenaar moet dan langer wachten op zijn geld. 

Bij tie breken de nonce hash waarde die dichter bij 0 zit krijgt voorrang. 

Blockchain is niet zo geschikt voor snelle transacties
pas na 6 time periodes (6 keer tien min) weet de pizza owner of het ok is. 

Ecologische impact - eigenlijk niet te verantwoorden (persoonlijk). Geen ethische investering.


alternatives:
- randomized
- coin age (sparen)
- velocity (dynamisch systeem voor dagelijkse interacties)
- voting based

veel bitcoins zijn al verdwenen.



Block chain technologie in andere disciplines!!
- voting
- dns
- ...