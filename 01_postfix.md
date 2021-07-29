## postfix server (receives email)

on ` 192.168.1.171 mysmtp mysmtp.OracleByExample.com ` <br>
login as ` root ` user

#### NOTE : this step will require VM to be able to connect to internet for downloading required packages.

Check if postfix is already installed on the server :
```
dnf list --installed | grep postfix
```

Check for all the available postfix related packages :
```
dnf search *postfix*
```

Install all the postfix related packages :
```
dnf install postfix* --assumeyes
```

---

### configure postfix

Backup the original configuration file :
```
cp /etc/postfix/main.cf /etc/postfix/main.cf_original
```

Modify the postfix configuration file :
```
vi /etc/postfix/main.cf
```

you might have to COMMENT OUT the existing parameters and add following parameters :
```
# RECEIVING MAIL : listen only on local network interface and reject from public ip addresses
inet_interfaces = 192.168.1.171

# TRUST AND RELAY CONTROL : Postfix "trusts" SMTP clients in the same IP subnetworks as the local machine
mynetworks_style = subnet
# you can also use custom subnetwork settings as following
# mynetworks = 168.100.189.0/28, 127.0.0.0/8

# make it run in PRIVATE ONLY network mode : turn off INTERNET MX lookups
relayhost = [host]

# custom banner displayed to email clients (such as sendmail)
smtpd_banner = $myhostname ESMTP $mail_name ($mail_version)
```

---

### start postfix

commands to status/start/stop postfix :
```
/usr/sbin/postfix status
/usr/sbin/postfix start
/usr/sbin/postfix stop
```

commands to status/enable/start postfix as service :
```
systemctl status postfix.service
systemctl enable postfix.service
systemctl start postfix.service
```

postfix log file :
```
/var/log/maillog
```

check if postfix is running and listening on specific ip:port :
```
netstat -antp | egrep "Proto|:25"

# output :
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 192.168.1.171:25        0.0.0.0:*               LISTEN      7731/master
```

---

### mailbox & aliases

#### ASSUMPTION : in this article, we assume that "dbadmin" user will receive emails

emails for "dbadmin" user will be stored in following file :
```
/var/spool/mail/dbadmin
```

alias can be configured to simulate email addresses such as ` info@mysmtp.OracleByExample.com ` or ` errors@mysmtp.OracleByExample.com ` or ` alerts@mysmtp.OracleByExample.com `.

Modify the aliases configuration file :
```
vi /etc/aliases
```

add following entries :
```
# alias: user[, user, user, ...]
alerts: dbadmin, sanjeev
errors: dbadmin, anilkm
info:   dbadmin
```

run following command to update aliases :
```
/usr/bin/newaliases
```

---

## disable NAT PORT for VM : 192.168.1.171 mysmtp mysmtp.OracleByExample.com
## this will stop all INTERNET traffic to mysmtp postfix server

---

### test connection to postfix :

on ` 192.168.1.121 hzd1 hzd1.OracleByExample.com `
```
curl 192.168.1.171:25

# output :
220 mysmtp.OracleByExample.com ESMTP Postfix (3.5.8)
# first line in the output is the pre-defined smtpd_banner
```