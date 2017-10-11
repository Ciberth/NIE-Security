# Lesweek 3

(op 11/10/2017)

test 28 november

### ... Limitations of (en verder)

er zijn wel wat gebreken in die certificaten, er zijn exetnsies toegevoegd om die gebreken aan te vullen

vb. attributen en constraints

"critical flag" is niet echt vast gedefinieerd, allemaal zeer **vaag**.
Verschillende extensies zijn ontwikkeld door verschillende personen en door die vaagheid zijn ze soms overlappend in functionaliteit. 

> certificaten omvatten soms te veel

vb. als u email is veranderd moet je nieuw certificaat aanvragen

subsets zijn gemaakt zoals bvb PKIX daarin staat wat er verplicht is en dergelijke.

België gebruikt een iso standaard naar europese normen.


## Transport layer security

TLS/SSL

TLS is ontwikkelt om alle verkeer te encryptere.
Waar ssh typisch w gebruikt om dingen veilig door te sturen (shell, ftp, ...) gaat TLS specifiek meer verkeer encrypteren. 

TLS is ook meer generiek ontwikkeld, meerdere soorten tcp verkeer. SSH heeft andere functionaliteiten zoals multiplexing die TLS niet heeft.

TLS heeft standaard geen user authentication 

FTP-TLS is ook niet gelijk aan SFTP

Dus vaak een licht verschillend doel maar in principe vrij gelijkaardig.

"is resumable" wil eigenlijk zeggen kunne we deze sessie later opnieuw gebruiken (da kan die startup sneller maken en is een verschil met ssh)



aan te raden leg ze naast elkaar om te vergelijken

handshake protocol zie slides

pas na fase 4 spreekt men van een beveiligde verbinding (?)

hier bij tls wordt eerst mac toegevoegd en dan pas encryptie bij ssh is dit omgekeerd.


in praktijk zal men vaak een dynamisch proces starten omdat je moet wachten met encrypteren tot alles binnen is

Je begint met kleine pakketjes en langzaam groter (google doet da ook)


"random waardes" zijn moeilijk te bepalen
random generators zijn vaak iets of wa voorspelbaar (seed nodig en da kan vanalles zijn, cpu load, aantal muisclicks sinds x min, boottime in seconden)

heartbeat...

TLS is iets efficienter dan ssh
tls is er geen random padding die toegevoegd wordt wat het decrypteren iets makkelijker zou maken in theorie

**latency!** minstens 2 keer 56ms kwijt (2 round trip times) er is een speedup mogelijk je kan een sessie resumen


naar geheugen toe is da nie te doen voor de server (niet schaalbaar en alles in geheugen houden kan nie) 

server maakt ticket en de sessie wordt bij de client opgeslaan

dus **sessie management** zit bij de **client** dus een stuk schaalbaarder en de overhead w gereduceerd. 


een andere speed up is false start (als je nog geen sessie hebt) er wordt uitwisseling gedaan
men gaat er van uit da het meestal al lukt dus men gaat van de eerste keer die clientexchange ook al doorsturen "men gaat er van uit dat het goe zal lopen" dus in de 112 ms is er ook al data vertuurd


grootste nadeel is omgaan met proxies

ofwel gaat local proxy als endpoint fungeren voor tls systeem (minder veilig eigenlijk door die proxy zeker als het privaat netwerk is)

als men sessies opslaat dan moeten al die sessies ook gesynct worden en dezelfde keys hebben en op dezelfde manier geupdate w

zeer vaak worden intermediate authorities ook toegevoegd (zijn certificaten) zo bespaar je de client een roundtrip (dns resolve, ... ) Belangrijk om voldoende certificaten toe te voegen om speed ups toe te laten. 

"Moet je de root certificate toevoegen"? Nee die zijn meestal gekend in os of browser. Zorg er ook voor dat de certificaten niet te uitgebreid zijn. 




## Network layer: IPsec & vpn

Hoe kunnen we ip pakketen veilig encrypteren?
Is da wel zinvol is de transportlaag nie voldoende?

vaak zijn aanvallen op ip basis
- ip spoofing 
- dos attacks



mode 1 over internet
mode 2 van server naar client (dus binnen een privaat netwerk bvb altijd in combinatie met andere protocollagen erboven)


transportmode - want ip adres blijft behouden

mutable fields -> time to live bvb die inhoudt moet kunnen wijzigen

esp = encapsulating security payload - die gaat encryptie uitvoeren die niet aanwezig was bij de ah header


### Examenvraag: 
**als ge esp gebruikt heeft het dan nog zin ah te gebruiken?**
waarom zou esp toch met ah gecombineerd moeten worde
```
je hebt idd authenticatie van de header maar je hebt geen authenticatie van u eerste ip header dus op ip niveau is spoofing nog steeds mogelijk
```

### VPN

IPSec & VPN zijn die hetzelfde?
Niet hetzefde maar wel verwant

vpn = secure tunnel van site naar site
kan geimplementeerd als ipsec maar nie noodzakelijk



l2tp heeft zelf geen encryptie en w gecombineerd met ipsec
