# Lesweek 12

(op 13/12/2017)


Gastsprekers:
- mooie herhaling
- vragenstelling van de eerste gastspreker gelijkaardig en inzichtsvragen

## Vervolg future evolutions

Meer transacties per blok dus fees zullen blijven stijgen. Je kan zelf kiezen hoeveel maar hoe duurder hoe sneller (bitcoinfees.info en bitcoinfees.earn.com).

Meer gebruikt als investeringsmiddel dan als transactiemiddel.

## IoT security


Argumentatie per use case. 
Communication probleem, bij 1000 devices hoe configureer je alles en communiceer je alles. 

LoRa -> groot bereik 5 a 15 km. En w gebruikt bij citywide deployments.

Aantal gateways (typisch op daken) en die zijn verbonde via een Server

Twee security aspecten:
- signal hidden in noice (spread spectrum)
- aes-128 NwkSKey (S staat voor session)



IoT devices moeten kunnen roamen dus verschillend netwerk.
Ze gebruiken verschillende network session key maar wel nog steeds dezelfde application session key (da moe lukken) en ook moet application session key moet aangepast kunnen worden.

Uit AppKey (ook gemaakt door manufacturer) kan sessie key afgeleid worden. AppKey is uniek maar network service kent dit niet dus kan dit niet lezen. Zie join requests & join completes & join accepts! Pas dan kan het interpret worden. Commisionning is een van de grote uitdagingen deze is mooie oplossing daarvoor.

Appkey is de geheime sleutel die enkel gebruikt w bij de joins, voor de rest niet.


## Quantum computing

Priem ontbinding is onmiddelijk achterhaald -> niet meer veilig.
Eliptische crummes zouden dan niet compromised zijn.

Quantum cryptografie bestaat wel en w al gebruikt.

De observatie beïnvloedt het deeltje zelf en da is het heel principe achter quantum cryptografie;

Foton is golf die zowel 1 als 0 kan voorstellen. 

Foton door filter dan krijg je foton met spin (afhankelijk van welke gebruikte filter). Maar door filter lock je dan 1 stand waardoor hij niet meer in alles tegelijk kan zijn. 

Gebruik je zelfde filter als ervoor -> blijft gelijk 100%
Gebruik je andere filter -> je weet niet meer wat het gaat zijn opsplitsing 50% 50%

We kunnen licht moduleren om data over te brengen (0n en 1n)

Bob weet niet welke filters Alice gebruikt heeft.

Heeft hij de juiste gebruikt geen probleem 100% juit
bij verkeerd 50% dat hij juist is.Daarna zegt Alice awel die en die en die waren verkeerd. 
Afluisteren kan maar de helft is verkeerd doordat je spin beïnvloedt dus het is onmiddelijk geweten!


Grootste nadeel:
- (voordeel) inherent veilig zolang onze fysica kennis niet kent
- verlies door medium (botsen op water molecules waardoor foton beïnvloedt w en spin ook)
- Optische vezels is gelimiteerd. 

Je kan ook quantum entanglement gebruiken; als je uit mekaar haalt en je doet wijziging op ene dan wijzig je ook de andere. 


## Opmerkingen examen

2 delen:
- gesloten boek (basiskennis)
- open boek (oefeningen en diepgaandere inzichtsvragen)

Waarom doet een protocol iets.

"Geef een aantal stappen in gesloten boek, leg uit waarom in openboek".

6 basis security goals! (confi, integrity, ... en bij elk protocol in welke mate voldoet het en waarom wrm wel wrm niet bij gesloten deel)

Laatste les niet te kennen (IoT, quantum) en legal aspects.


Perfect forward security
-> op regelmatige basis vorige sleutels wijzigen (zodat sessies veilig zijn)

Informatie in de geschiedenis heen mag u geen informatie geven

Bij IPsec -> altijd nieuwe field die berekend w


5 strategieen voor virussen om zich te verbergen
- vb zichzelf encrypteren
- in root sector  
- ... 

Waarom stuurt ssh de software versie door?
-> verschillende encryptiealgo (compatibiliteit)
-> sneller algoritmes voor te stellen (doorda je weet wa er ondersteund w)
-> je kan ook zegge ik wil enkel vanaf die versie communiceren door bugs 


Omgekeerde DES krijg je ook zelfde terug?


Wireshark trace
TLS
Session key/ ticket (handshake protocol) om later die sessie te resumen.
