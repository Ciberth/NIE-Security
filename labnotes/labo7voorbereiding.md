# Voorbereiding PAM

In etc/pam.conf staat een configuratiefile maar het is beter om in /etc/pam.d/ files te maken met verschillende configuraties in modules.

## Waar bevinden zich de PAM-modules?

``/etc/pam.d``

## Waar bevinden zich de configuratiebestanden?

``/etc/security`` of ``/lib/security`` of ``/lib64/security``

## Welke PAM-module wordt gebruikt voor het controleren van de login-gegevens aan de hand van de /etc/passwd-file?

[pam_localuser.so](http://www.linux-pam.org/Linux-PAM-html/sag-pam_localuser.html) (?)

## Welke PAM-module kan je gebruiken om de sterkte van wachtwoorden te checken?

[pam_cracklib.so](http://www.linux-pam.org/Linux-PAM-html/sag-pam_cracklib.html)



## Bekijk de inhoud van deze file en beschrijf het authenticatieproces.

```
#%PAM-1.0
# This file is auto-generated.
# User changes will be destroyed the next time authconfig is run.
auth        required      pam_env.so
auth        sufficient    pam_unix.so nullok try_first_pass
auth        requisite     pam_succeed_if.so uid >= 500 debug
auth        required      pam_deny.so

account     required      pam_unix.so
account     sufficient    pam_succeed_if.so uid < 500 quiet
account     required      pam_permit.so

password    requisite     pam_cracklib.so try_first_pass retry=3
password    sufficient    pam_unix.so md5 shadow nullok try_first_pass use_authtok
password    required      pam_deny.so

session     required      pam_limits.so
session     required      pam_unix.so
```

### Module types

**AUTH:**
> Instructs application to prompt the user for identification such as password. It may set credentials and alsy grant privileges.

**ACCOUNT:**
> Checks password aging, limit access, may be used to limit system access based on system resources.

**PASSWORD:**
> Stacked with auth module. Responsible for updating the user authentication token, often a password.

**SESSION:**
> Provide functions before and after session.

### Control flags

**Required:**
> Must return success. Even if false, execution still continues.

**Requisite:**
> Failure terminates execution.

**Optional:**
> Optional

**Sufficient:**
> If this succeeds, all others in the stack are ignored. 

### PAM standard arguments

**Debug**
> Additional information to syslog.

**No_warn**
> No warning

**Use_first_pass**
> Will use password from previous module. 

**Try_first_pass**
> Same as above but it will prompt one time (for the user to retry) if it fails.

- auth:
	* pam_env: setting/unsetting environment variables
	* pam_unix: traditional password authentication
	* pam_succeed_if: test account characteristics (hier: is uid groter of gelijk aan 500)
	* pam_deny: deny access
- account:
	* pam_unix
	* pam_succeed_if (hier: uid kleiner dan 500)
	* pam_permit: permit access
- password:
	* pam_cracklib: checks the password against dictionary words (hier: Retry:: Prompt user at most 3 times before returning with error. The default is 1.)
	* pam_unix
	* pam_deny
- sesion:
	* pam_limits: limit resources
	* pam_unix

## Bronnen

[Linux-pam](http://www.linux-pam.org/Linux-PAM-html/Linux-PAM_SAG.html)


# In labo

## PAM: Pluggable authentication modules

**Wijziging is onmiddelijk van start**

-> /lib/security
-> /etc/pam.d/...
--> per service -> 1 bestand (login, sshd, racoon, ...)


```
useradd wim
passwd wim

chage -l wim

vim /etc/passwd
vim /etc/shadow


system-auth # komt veel voor, kan op andere distributies andere naam hebben


# zeer handig

cat * | grep -rn "securetty" # of dus beter

grep -rn "nologin" * 

```

Doen we da open dan zien we vier grote blokken

Lijn per lijn uitgevoerd (stapel)

Het is niet omdat je authenticeerd bent da je automatisch sessie mag openen.

Kijk zeker naar man pages man pam_unix en dan zie **module types provided**.

Bij time is da bvb enkel account (pam_time)

Checks kan je doen via pam_succeed_if module.

pam_mount bestaat ook bvb als gebruiker inlogt dan moet je iets mounten en die heeft dan returnwaarde of het gelukt is of niet.

Eerste kolom

- auth -> authenticate
- password
- account
- session

Tweede kolom

- required -> regel is verplicht, is er nie voldaan dan wordt toegang geweigerd maar hij gaat die andere modules wel doorlopen.
- requisite -> zelfde als required maar hij stopt 
- sufficient -> vanaf je hieraan voldoet ist ok
- optional -> optioneel
- of zelf defineren via vierkante haakjes bvb. [success=1 default=ignore]


required -> nodig ga door
requisite -> nodig, stop
sufficient -> voledoende stop
optional -> optioneel


Je eindigt met een pam_permit of pam_den bij auth, account, password.

Voor debug informatie:
``journalctl -f -l SYSLOG_FACILYT=10``

check via ``cat /etc/passwd``

```
groupadd -g 900 group900
groupadd -g 2000 groep2000
useradd -g 2000 -u 2000 pam2000
useradd -g 900 -u 900 pam900
passwd pam2000
passwd pam900

yum install pamtester -y
```




## Opdrachten

### 1. Configureer PAM zodat de meeste modules debug-informatie wegschrijven.
In welk(e) bestand(en) komt deze informatie terecht?

In ``/etc/pam.d/system-auth`` bij alle modules debug parameter toevoegen. Bij systemd blijkbaar debug=1
Loggen via ``journal -f -l SYSLOG_FACILITY = 10``.


### 2. Pas de configuratie aan zodat een gebruiker 5 kansen krijgt om een aanvaardbaar nieuw wachtwoord in te geven bij het wijzigen van zijn wachtwoord.

Kijk naar welke service je aanpast, hier passwd > als je cat doet dan zie je da system-auth gebruikt wordt dus is het best om die zaken daar dan in te steken!

Retry op 5 gezet

```
...
password requisite pam_pwquality.so try_first_pass local_users_only retry=5 ...
...

Dan testen door in te loggen als pam2000 > passwd > huidig ww en dan 5 zever dingen
Je krijgt "passwd: Have exhausted maximum number of retries for service."
```


### 3. Pas het systeem aan zodat gebruikers met uid > 1000 niet kunnen inloggen en die met een uid < 1000 wel. Test uit met de nieuw aangemaakte gebruikers.

```
(al de rest bij auth in commentaar)
auth required pam_env.so debug
auth required pam_unix.so nullok try_first_pass debug
auth required pam_succeed_if.so uid <= 1000 debug
auth required pam_permit.so debug

...

```

### 4. Bij systeemonderhoud is het wenselijk dat niet-root-gebruikers zich voor een bepaalde tijd niet kunnen aanmelden; pas dit toe voor ssh en voor login. Zorg er bovendien voor dat gebruikers die toch proberen in te loggen een passende boodschap te zien krijgen.

Zie ``man pam_nologing`` en maak dus file ``/etc/nologin``.

```
echo "systeemonderhoud, enkel toegang voor root" > /etc/nologin

# ik deed niets buiten de nologin file en da werkte al zoals gewenst
# idee is echter volgende regel in sshd en in login povenaan steken
auth required pam_nologin

```

### 5. Configuraar PAM zodat gebruiker pam1 enkel kan inloggen vanop de computer van je collega.

via /etc/access.conf 
daarin zet je

+:pam900:192.186.76.2
-:pam900:ALL

en dan in sshd

auth requisite pam_access.so accessfile=/etc/access.conf debug


### 6.

cp /etc/securetty /etc/securetty.bak

alles in commentaar zetten; behalve tty4


### 7.

In
/etc/pam.d/sshd  en /etc/pam.d/login aanpassen:
```

account   required   pam_time.so
```

/etc/security/time.conf aanpassen:
```

# services ; ttys ; users ; times

login;*;*;Th1000-1200
sshd;*;*;Th1000-1200


# login ; tty* & !ttyp* ; * ; Th1000-1200


```

### 8. 

/etc/security/time.conf aanpassen:
```
sshd ; * ; pam900 | pam2000 ; MoFr0000-2400
login; * ; pam900 | pam2000 ; MoFr0000-2400

# loging ; * ; pam* ; TuWe
# loging ; * ; pam* ; !TuWe

```


### 9.

Er wordt gekeken naar module other.
Hierin staan 4 stacks elk required met elk een deny.
