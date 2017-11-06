# Voorbereiding sendmail

## Wat is de padnaam van het configuratiebestand van Sendmail?

Sendmail leest van ``/etc/mail/sendmail.cf`` maar als sysadmin pas je ``/etc/mail/sendmail.mc`` aan (macrobestand). Deze maakt de .cf. Zie H7.

## Welke aanpassingen zijn er nodig aan de DNS-instellingen om berichten te kunnen versturen naar jouw domein?

Een A-record voor alle hosts en een MX-record voor alle mailservers.

Vb:
```
$TTL 1h
$ORIGIN example.com.
@ IN SOA ns1.example.com. admin.example.com. (
2014062401
12h
15m
2w
2h
)
      IN    NS   ns1.example.com.
1w    IN    MX   10 mail.example.com.
ns1   IN    A    10.0.0.23
mail  IN    A    10.0.0.24
www   IN    A    10.0.0.27


Bron: http://www.slashroot.in/mx-record-dns-explained-example-configurations
```

## Waar vind je de logs van Sendmail op Fedora20?

``/var/log/maillog`` of ik vermoed ``journalctl -u sendmail``

## Hoe wordt de configuratie-file bruikbaar gemaakt voor de sendmail-deamon?

``/etc/mail/sendmail.cf`` via macro ``/etc/mail/sendmail.mc``

Daaron op eerste lijn: ``include(`/usr/share/sendmail-cf/m4/cf.m4')``

```
/etc/init.d/sendmail restart

# of 

systemctl restart sendmail
```



## Wat moet je aanpassen om te zorgen dat alle post verstuurd naar voornaam.familienaam@jouwdomein.iii.hogent.be terechtkomt bij gebruiker tiwi1?

Meerdere manieren mogelijk! Alias, forward, address mappings (virtuser) dit laatste in:
```
# in sendmail.mc
FEATURE(`virtusertable')

# in /etc/mail/virtusertable
voornaam.famnilienaam@jouwdomein.iii.hogent.be

# in /etc/mail/local-host-names:
jouwdomein.iii.hogent.be
makemap hash virtusertable.db < virtusertable

systemctl restart sendmail
```



## Wat moet je aanpassen in de configuratie zodat berichten afkomtstig uit een ander domein dan het jouwe tegengehouden worden? Berichten versturen naar andere domeinen moet evenwel nog wel mogelijk zijn.


```
/etc/mail/access aanpassen:
	localhost	OK
	domain	REJECT
makemap hash /etc/mail/access.db < /etc/mail/access
/etc/mail/sendmail.mc: FEATURE(`access_db')
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf

```
