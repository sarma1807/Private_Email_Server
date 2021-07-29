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
thunderbird         : email client on Windows box
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
