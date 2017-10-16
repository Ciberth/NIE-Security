# Voorbereiding 17 oktober

# Opmerkingen vorige labo!

Op de .ssh mogen geen schrijfrechten voor de groep want anders kan een andere gebruiker zijn sleutel kopiëren in die van jou en zo hijacken. (dus nen chown 700)

## Laatste stukken SSH

### 4. Public Key Authentication

```
Naast wachtwoord-authenticatie kan je ook gebruikmaken van publieke-sleutel-authenticatie om in te loggen via SSH. Om dit te bekomen moeten de gebruikers zelf een sleutelpaar aanmaken en de sleutels op de juiste plaats kopiëren met de juiste naam. Er moeten daarnaast ook nog een aantal extra bestanden worden aangemaakt.

Stel dit in en test uit of je nu kan inloggen via de passeerzin.

Waarom wordt er een passeerzin gevraagd? Hoe kan je dit omzeilen?

> As you know, the advantage that the passphrase gives you is that if someone is able to read your private key, they are 'unable' to use it.

> This will prevent the passphrase prompt from appearing and set the key-pair to be stored in plaintext (which of course carries all the disadvantages and risks of that):

ssh-keygen -b 2048 -t rsa -f /tmp/sshkey -q -N ""
(vooral de combo -q en -N "" ) q voor silences en -N "" voor nieuwe lege passphrase
```

Todo voor implementatie:

1. ``PublicKeyAuthentication yes`` op de server en op de **client**.
2. Op **client** key maken: ``ssh-keygen -rsa -f $HOME/.ssh/id_rsa``.
3. De publieke key (id_rsa.pub) transferen naar server:  ``ssh-copy-id -i ~/.ssh/id_rsa.pub tiwi1@host``
4. Test new key with: ``ssh -i ~/.ssh/mykey user@host``

(als die ssh-copy-id nie lukt dan via scp en echo key >> ~/.ssh/authorized_keys)

[SSH.com](https://www.ssh.com/ssh/copy-id)


### 5. Port Forwarding

**Local**
Log in op de gateway-computer van jouw opstelling en zorg dat alle aanvragen op poort 8888 doorgestuurd worden naar poort 22 van een welbepaalde client-computer van een ander privaat netwerk.

```
ssh -L localport:remotehost:hostport user@hostname
ssh -L 8888:fermatVM:22 root@fermat
```

Je kan firewalls "ontwijken".


**Remote**
Veronderstel nu dat de computers binnen jouw privaat netwerk van buitenuit niet bereikbaar zijn!

Hoe kan je er voor zorgen dat de SSH-poort (poort 22) van je interne client beschikbaar wordt op poort 8888 van de gateway-computer? Test grondig uit of een toestel buiten jouw privaat netwerk een connectie kan maken met poort 8888 van jouw gateway en dat er op deze manier veilig kan worden ingelogd op de interne client.

```
ssh -R remoteport:host:hostport user@hostname
ssh -R 22:localhost:8888 root@fermat

(hier is fermatvm dan localhost en kan fermat via 8888 naar fermatvm 22 gaan)

```

Zo kan je van buitenaf toch aan je pc.


### 6. Bestandsbeheer

**sftp**
```
# Start session

sftp username@hostname

# Then you can use commands like: 
cd, chmod, chown, exit, get, put, rm


# Automatic retrievel mode

sftp myname@files.myhost.com:documents/portfolio.zip /tmp

```

[Sftp commandos](https://kb.iu.edu/d/akqg)
[Sftp en ssh](https://www.computerhope.com/unix/sftp.htm)

**scp**

```
Syntax:

scp <source> <destination>
To copy a file from B to A while logged into B:

scp /path/to/file username@a:/path/to/destination
To copy a file from B to A while logged into A:

scp username@b:/path/to/file /path/to/destination
```

[Bron](https://unix.stackexchange.com/questions/106480/how-to-copy-files-from-one-machine-to-another-using-ssh#106482)