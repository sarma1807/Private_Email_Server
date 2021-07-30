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

click "continue"

protocol : IMAP

security certificate : confirm security exception


password related security settings :

server settings -> security settings ->
       connection security   : starttls
       authentication method : normal password
```
