## Private Email Server

---

### Problem/Requirement

When running multiple virtual machines in a private lab or home network, we should be able to send emails such as alert notifications from those virtual machines to a private email server.

This is required when configuring monitoring scripts or products such as Prometheus AlertManager.

On Linux ...

---

### Solution

We can use following software packages on Linux to configure a Private Email Server.

```
postfix server      : receives email
sendmail client     : sends email
dovecot (imap/pop3) : allows email GUI client to pull email from server
thunderbird         : email client on Win0dows box
```

---

### My Machines

```
# mysmtp virtual machine will run postfix & dovecot
192.168.1.171 mysmtp mysmtp.OracleByExample.com

# hzd1 virtual machine will be the sendmail client
192.168.1.121 hzd1 hzd1.OracleByExample.com

# winbox is the host machine - will run thunderbird
192.168.1.21 winbox winbox.OracleByExample.com

```

---

![Private_Email_Server_00_Arch.jpg](https://github.com/sarma1807/Private_Email_Server/blob/main/Screenshots/Private_Email_Server_00_Arch.jpg) <br><br>

---

### Latest Verification

```
# 15-October-2022
# this is working properly with following software versions :

Linux OS : CentOS Stream release 9 (5.14.0-171.el9.x86_64)
postfix.x86_64     2:3.5.9-19.el9    @appstream
curl.x86_64        7.76.1-19.el9     @anaconda
libcurl.x86_64     7.76.1-19.el9     @anaconda
sendmail.x86_64    8.16.1-10.el9     @appstream
dovecot.x86_64     1:2.3.16-7.el9    @appstream
Thunderbird 102.3.3 (64-bit)
```
