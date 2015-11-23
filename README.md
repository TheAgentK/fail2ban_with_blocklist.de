# Make Fail2ban with blocklist.de better
Idea from http://wiki.kvs1.de/doku.php?id=pimp-fail2ban-with-blocklist.de


Most admins have http://www.fail2ban.org/ in use to protect their servers.
To get more power out of fail2ban you can combine it with http://blocklist.de

## New jail for fail2ban
```
[ssh-blocklist]
...
```
see [jail.local](jail.local)
* Monitor ssh port and uses the filter blocklist with the logfile blocklist.log.
* All found IPs will be blocked after 1 attempt for 1 day.


## New filter for fail2ban
```
# Fail2Ban configuration file
 
[Definition]
...
```
see [blocklist.conf](blocklist.conf)

## Get the IPs
```
./blocklist.de-update.sh
```
run [blocklist.de-update.sh](blocklist.de-update.sh) from Terminal

## Restart service
```
service fail2ban restart
```

## Cron job
Call the script each hour to fetch the last IP list for SSH
```
0 * * * * $PATH_TO_FILE$/blocklist.de-update.sh ssh 3600
```

## Monitoring
```
tail -f /var/log/auth.log /var/log/fail2ban.log
```
