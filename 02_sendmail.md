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
dnf list --installed | grep sendmail
```

Check for all the available sendmail related packages :
```
dnf search sendmail
```

Install sendmail related packages :
```
dnf install sendmail* --assumeyes
```

Verify - after installing sendmail packages :
```
sample output :

# dnf list --installed | grep sendmail
sendmail.x86_64               8.16.1-11.el9           @appstream
sendmail-cf.noarch            8.16.1-11.el9           @appstream
sendmail-doc.noarch           8.16.1-11.el9           @appstream
#
```

---

### configure sendmail

Modify the sendmail configuration file :
```
vi /etc/mail/sendmail.mc
```

add following entry at the end of the file :
```
define(`SMART_HOST', `mysmtp.OracleByExample.com')dnl
```

verify following entry :
```
cat /etc/mail/sendmail.mc | grep -i SMART_HOST

# expected output should contain 2 entries, similar to following :
dnl define(`SMART_HOST', `smtp.your.provider')dnl
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

# expected output should contain 1 entry, similar to following :
DSmysmtp.OracleByExample.com
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
systemctl start  sendmail.service
```

---

send a simple test email (without email body) :
```
echo "Subject: `hostname -s` sendmail test" | sendmail -v info@mysmtp.OracleByExample.com
```

send a simple test email (with email body) :
```
echo -e "From: info@mysmtp.OracleByExample.com\nTo: info@mysmtp.OracleByExample.com\nSubject: `hostname -s` sendmail test\nContent-Type: text/html\n\nMore detailed message goes here ..." | sendmail -v info@mysmtp.OracleByExample.com
```

