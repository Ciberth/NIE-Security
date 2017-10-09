# Voorbereiding labo 2: SSH

## Afwerken DNS ?

[ ] Zone files toekennen aan named: ``chown named:named zonefile``
[ ] Hostnames: ``hostnamectl set-hostname --static <name>.groep26.iii.hogent.be``
[ ] ``/etc/resolv.conf checken:``
```
nameserver 127.0.0.1
nameserver 192.168.76.1
options rotate
```

## SSH cheatsheet

### Server stuff

Locatie: ``/etc/ssh/sshd_config`` 
Locatie voor public keys: ``/etc/ssh/ssh_known_hosts``


### Client stuff

Server toevoegen bij known hosts (?): ``/etc/.ssh/known_hosts``
Config in: ``~/.ssh/ssh_config``
Uitwisselen van publieke key is via: ``ssh-keyscan``



### Local forwarding

**Doel:** Dingen die anders geblokkeerd worden toch door de firewall laten bvb.
``ssh -L localport:remotehost:hostport user@hostname``
Waarschijnlijk iets in den trend van: ssh -L 1234:fermatvm:22 root@fermat
> Poor man's vpn


### Remote forwarding

**Doel:** From home to work
``ssh -R remoteport:host:hostport user@hostname``
Dus: ssh -R 1234:fermatvm:22 root@fermat
of bij fermatvm = localhost denk ik

Dus fermat kan nu via zijn eigen 1234 poort verbinden naar fermatvm poort 22 (ssh) 


### scp

```
Syntax:

scp <source> <destination>
To copy a file from B to A while logged into B:

scp /path/to/file username@a:/path/to/destination
To copy a file from B to A while logged into A:

scp username@b:/path/to/file /path/to/destination
```

[Bron](https://unix.stackexchange.com/questions/106480/how-to-copy-files-from-one-machine-to-another-using-ssh#106482)