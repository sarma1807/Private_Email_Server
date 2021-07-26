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
thunderbird         : email client
```

---

