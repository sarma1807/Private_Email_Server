## sendmail client (sends email)

on ` 192.168.1.121 hzd1 hzd1.OracleByExample.com ` <br>
login as ` root ` user

Modify the hosts file :
```
vi /etc/hosts
```

add following entries :
```
192.168.1.171 mysmtp mysmtp.OracleByExample.com
```

---

#### NOTE : this step will require VM to be able to connect to internet for downloading required packages.

Check if sendmail is already installed on the client VM :
```
rpm -qa | grep sendmail
```

Check for all the available sendmail related packages :
```
yum list *sendmail*
```

Install sendmail related packages :
```
yum install sendmail --assumeyes
yum install sendmail-cf --assumeyes
```

---

### configure sendmail

Modify the sendmail configuration file :
```
vi /etc/mail/sendmail.mc
```

add following entry :
```
define(`SMART_HOST', `mysmtp.OracleByExample.com')dnl
```

make/compile the sendmail configuration file :
```
/etc/mail/make
```

previous make will generate a new ` /etc/mail/sendmail.cf ` file.

verify the smtp configuration :
```
cat /etc/mail/sendmail.cf | grep DS | grep -v "#"
```

DISABLE sendmail to listen for remote email on port 25 : only allows local connections :
```
vi /etc/sysconfig/sendmail
```

add following entry :
```
DAEMON=no
```

---

commands to status/enable/start sendmail as service :
```
systemctl status sendmail.service
systemctl enable sendmail.service
systemctl start sendmail.service
```

---

send a test email :
```
echo "Subject: `hostname -s` sendmail test" | sendmail -v info@mysmtp.OracleByExample.com
```

