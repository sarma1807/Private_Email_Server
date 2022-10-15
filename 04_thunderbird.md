## thunderbird (email client on Windows box)

on ` 192.168.1.21 winbox winbox.OracleByExample.com ` <br>
this is the windows machine which we will use for thunderbird

Modify the hosts file :
```
c:\Windows\System32\drivers\etc\hosts
```

add following entries :
```
192.168.1.171 mysmtp mysmtp.OracleByExample.com
```

---

download and install thunderbird email client from :
#### https://www.thunderbird.net/en-US/

```
start thunderbird and cancel initial configuration wizard.


configure email :
         name : dbadmin
email address : dbadmin@mysmtp.OracleByExample.com
     password : <provide password>
     # HINT : we configured this password as "ILovePlayStation" in first step during "postfix" configuration

click "continue"

protocol : IMAP

security certificate : confirm security exception


password related security settings :

server settings -> security settings ->
       connection security   : starttls
       authentication method : normal password
```

---

if everything goes well, we should see something similar to following :

![Thunderbird_01.jpg](https://github.com/sarma1807/Private_Email_Server/blob/main/Screenshots/Thunderbird_01.jpg) <br><br>

