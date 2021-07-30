## dovecot (imap/pop3) (allows email GUI client to pull email from server)

on ` 192.168.1.171 mysmtp mysmtp.OracleByExample.com ` <br>
login as ` root ` user

#### NOTE : this step will require VM to be able to connect to internet for downloading required packages.

Check if dovecot is already installed on the server :
```
dnf list --installed | grep dovecot
```

Check for all the available dovecot related packages :
```
dnf search *dovecot*
```

Install the dovecot package :
```
dnf install dovecot --assumeyes
```

---

### configure dovecot

Modify the dovecot configuration file :
```
vi /etc/dovecot/dovecot.conf
```

you might have to COMMENT OUT the existing parameter and add following parameter :
```
# * will allow dovecot to listen for incoming requests from all IPs ### :: is for IPv6
#listen = *, ::
listen = *
```

Modify the dovecot authentication configuration file :
```
vi /etc/dovecot/conf.d/10-auth.conf
```

you might have to COMMENT OUT the existing parameters and add following parameters :
```
#disable_plaintext_auth = yes
disable_plaintext_auth = no
# auth_mechanisms = plain
auth_mechanisms = plain login
```

Modify the dovecot mailbox configuration file :
```
vi /etc/dovecot/conf.d/10-mail.conf
```

you might have to COMMENT OUT the existing parameters and add following parameters :
```
mail_privileged_group = mail
mail_location = mbox:~/mail:INBOX=/var/spool/mail/%u
```

---

### dbadmin user - group assignment

assign mail group to dbadmin user
```
usermod --append --groups mail dbadmin
```

---

### start dovecot

commands to status/enable/start dovecot as service :
```
systemctl status dovecot.service
systemctl enable dovecot.service
systemctl start dovecot.service
```

dovecot log file :
```
/var/log/maillog
```

check if dovecot is running and listening on specific ip:port :
```
netstat -antp | egrep "Proto|dovecot"

# output :
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:993             0.0.0.0:*               LISTEN      1847/dovecot
tcp        0      0 0.0.0.0:995             0.0.0.0:*               LISTEN      1847/dovecot
tcp        0      0 0.0.0.0:110             0.0.0.0:*               LISTEN      1847/dovecot
tcp        0      0 0.0.0.0:143             0.0.0.0:*               LISTEN      1847/dovecot
#
```
