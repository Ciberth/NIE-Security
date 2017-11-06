# PGP

## Interesting Commands

```

gpg --gen-key

# default (binary)
gpg --export -o export

# ascii
gpg --export -a -o export.txt


gpg --import export.txt
gpg --list-keys
gpg --delete-secret-keys name
gpg --delete-keys name

gpg --delete-secret-and-public-key name

gpg --edit-key key

# vb

gpg -o export.gpg --cipher-algo AES256 --encrypt export.txt

```

## External docu

- [gnupg.org](https://www.gnupg.org/gph/en/manual.html)
- [Default algos](https://security.stackexchange.com/questions/86305/what-is-the-default-cipher-algorithm-for-gnupg#86311)


# Labo zelf 

```
yum install gnupg -y

useradd gpg1
useradd gpg2
useradd gpg3
```

Switchen van console via rechter CTRL + F1, F2, F3

## Deel 1: Sleutelbeheer

### 1

```
su - gpg1

gpg --gen-key

> 1 (RSA and RSA)
> 2048
> 0
> y
> user_pgp2
> RSA&RSA
> azerty



gpg --list-keys
```

Passphrase = Voor private key te beveiligen (encrypteren)

Extra toetsaanslagen = voor meer entropie

Verschil is ander soort algoritme

### 2

voor gebruiker 1

```
# binair
gpg --export -o pgp1.gpg

# ascii
gpg --export -a -o pgp1.txt


```

via root shared folder

```
groupadd iedereen
usermod -a -G iedereen root
usermod -a -G iedereen pgp1
usermod -a -G iedereen pgp2
usermod -a -G iedereen pgp3

mkdir /iedereen
chgrp -R iedereen /iedereen
chmod -R 777 /iedereen

cp pgp1.txt /iedereen/pgp1.txt
...
```

### 3

```
# op user 1

gpg --import /iedereen/pgp2.txt
gpg --import /iedereen/pgp3.gpg

# verwijderen



```


```
gpg --import keyspgp1.txt
gpg --list-keys
gpg --delete-secret-keys name
gpg --delete-keys name
```

Bij verwijdering eerst private dan public ofwel via `gpg --delete-secret-and-public-key name`

### Vraag 4

```
gpg --edit-key key
> passwd
```


### Vraag 5

```
gpg --edit-key key
> trust
> 5
> y
> sign
> y
> passphrase
```

## Deel 2

### 1 

default cast5?

```
gpg -o bestand1.default --symmetric bestand1

gpg -o bestand1.aes256 --cipher-algo AES256 --symmetrric bestand1

gpg -o bestand2 --encrypt bestand2 # en interactief user_pgp2 kiezen


gpg -o bestand3.gpg --cipher-algo AES256 --encrypt bestand3

gpg --for-your-eyes-only --encrypt bestand4

gpg -a -o bestand5.gpg --symmetric bestand5

```


-d optie:

Decrypt the file given on the command line and write to stdout or file. If the decrypted file is signed, the signature is also verified. This command differs from the default operation, as it never writes to the filename which is included in the file and it rejects files which don't begin with an encrypted message.



```

gpg --output newfile --decrypt /iedereen/bestand1.def


# enkel note bij --for-your-eyes-only
```

file2:
gpg --decrypt file2.pgp

passphrase for secret key:

file3:
zelfde als file2

file4:
zelfde als file3
output toont ook:
gpg: note: sender requested "for-your-eyes-only"

file5:
zelfde als file 1
output toont ook:
gpg: WARNING: message was not intergrity protected

van user 3 krijg je: decryption failed: secret key not available

### 3


```

gpg -s -e bestand

gpg -s file # maakt een .sig of .asc bestand 

gpg -a -s file

# controleren van signed file

gpg --verify file.sig # en -e om oorspronkelijke file te krijgen


gpg --sign --encrypt /iedereen/p2file1.txt


gpg --verify /iedereen/p2file2.txt.asc

```

## Vraag 4

Met detached sigs blijft het origele bestand ongewijzigd:

```
gpg --output doc.sig --detach-sig doc
gpg --verify doc.sig doc
...
```


### vraag 5

```
gpg --clearsig naambestand

#geeft nen .asc

```

## deel 3

gpg --gen-key voor c 
gpg --gen-key voor b

gpg --import /weboftrust/user_c

gpg -o user_c_van_b --export c@email.com
gpg -o user_b --export user_b

