fufix
=====
A Mailserver installer for **Debian and Debian based distributions**. 
This installer is permanently **tested on Debians stable branch** but is reported to run on newer branches, too. Debian Squeeze (old-stable) is not supported.

## Introduction
A summary of what software is installed with which features enabled.
**System setup**
* Setting the Hostname & Fully Qualified Domain Name
* Timezone adjustment
* Automatically generated passwords with high complexity
* Self-signed SSL certificate for all supported services
* Nginx (+php5-fpm) installation with a site for Postfixadmin (SSL only, based on BetterCrypto)
* MySQL installation as backend for mail service
* DNS check via Google DNS to verify PTR and A Record
* Free Rsyslog from mail logs (mail.* only)

**Postfix**
* Submission activated (TCP/587)
* SMTPS disabled
* Require TLS Authentification
* Included ZEN blocklist
* Spam- and virus protection by [FuGlu Mail Content Scanner](http://www.fuglu.org)  with ClamAV and Spamassassin backend: Reject infected mails (<v0.2: delete), mark spam and move to "Junk"
* SSL based on BetterCrypto (but no definition of "high" ciphers for compatibility reasons)

**Dovecot**
* Default mailboxes to subscribe to automatically (Inbox, Sent, Drafts, Trash, Junk - SPECIAL-USE RFC 6154 tags)
* Sieve/ManageSieve (TCP/4190)
* Global sieve filter: Prefix spam with "[SPAM]" and move to "Junk"
* (IMAP) quotas
* LMTP (resident daemon)
* SSL based on BetterCrypto

**Postfixadmin**
* Automatic superuser configuration
* Full quota support
* "config.local.php" preconfigured

## Before you start
**Please remove any web- and mail service** running on your server. I recommend using a clean Debian minimal installation.
Remember to purge Debians default MTA Exim4:
```
apt-get purge exim4*
``` 
