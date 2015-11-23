# Make Fail2ban with blocklist.de better
Idea from http://wiki.kvs1.de/doku.php?id=pimp-fail2ban-with-blocklist.de


Most admins have http://www.fail2ban.org/ in use to protect their servers.
To get more power out of fail2ban you can combine it with http://blocklist.de

## New jail for fail2ban
```
[ssh-blocklist]
 
enabled  = true
port     = ssh
filter   = blocklist
logpath  = /var/log/blocklist.log
maxretry = 1
bantime  = 86400
action   = %(action_)s
```
* Monitor ssh port and uses the filter blocklist with the logfile blocklist.log.
* All found IPs will be blocked after 1 attempt for 1 day.


## New filter for fail2ban
```
# Fail2Ban configuration file
 
[Definition]
 
# Option:  failregex
# Notes.:  regex to match the password failures messages in the logfile. The
#          host must be matched by a group named "host". The tag "<HOST>" can
#          be used for standard IP/hostname matching and is only an alias for
#          (?:::f{4,6}:)?(?P<host>[\w\-.^_]+)
# Values:  TEXT
#
failregex = ^ *: *<HOST>$
 
# Option:  ignoreregex
# Notes.:  regex to ignore. If this regex matches, the line is ignored.
# Values:  TEXT
#
ignoreregex = 
```

## Get the IPs
```
run blocklist.de-update.sh from Terminal
```

## Restart service
```
service fail2ban restart
```
