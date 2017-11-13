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