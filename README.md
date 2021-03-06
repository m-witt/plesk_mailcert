# plesk_mailcert
Version 1.06

Copies Plesk LetsEncrypt CERT to Mailservers and Webmin

The script MAILCERT is used if you secured your plesk server also with an LetsEncrypt certificate, Example: server.mydomain.tld
WARNING! This is experimental and only tested on Debian/Ubuntu Systems at this time. Make sure you have backed up your PEM files before usage

Supported:
- Plesk 12.5
- Debian
- Postfix
- Dovecot
- Courier
- Webmin
- Qmail

Usage:
- Install the LetsEncrypt Plesk Extension: https://github.com/plesk/letsencrypt-plesk
- Add a webspace with your plesk hostname and secure it with as LetsEncrypt certificate
- Edit /etc/mailcert/mailcert.cfg or set your certificate's hostname via command variable.
- Run it manually or set up cron job. 
**Example:** `@hourly /root/plesk-certupdate/mailcert -r -s myserver.net > /dev/null`
``` 
Usage: mailcert [-v : Version Check] [-r : Run Certificate Check] [-h: Display Help]
 -v : Checks if a newer version of this script is available.
 -s example.com : Sets the hostname via command line.
 -r : Runs the script. If running in a cron job you will need to run this argument.
 -h : Displays this help page.
```

Remarks:
The MAILCERT Script try's to get the actual PEM File from the vhost. This file is changed after each renewal of the LetsEncrypt certificate. If the file exists, it will be copied to the known default pem file of the services.
At this time:
- Dovecot: /etc/dovecot/private/ssl-cert-and-key.pem
- Postfix: /etc/postfix/postfix_default.pem 
- Courier IMAP: /usr/share/imapd.pem
- Courier POP3: /usr/share/pop3d.pem
- Webmin: /etc/webmin/miniserv.pem
- Qmail: /var/qmail/control/servercert.pem
