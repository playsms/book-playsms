# Additional step for playSMS 1.3 installation

This is a special case, we may call it a bug in playSMS 1.3, we have 2 bugs.

## 1st bug

The bug will cause playSMS (sendsmsd) unable to actually deliver SMS to gateways.
It was caused by a missing field in `playsms.sql` that is used during installation.

To fix playSMS 1.3 installation you need to insert an upgrade SQL file to your new playSMS 1.3 database.

Example, playSMS 1.3 source package was extracted to `/usr/local/src/playsms-1.3/` and playSMS 1.3 database is `playsms`. Run below commands to fix this bug:

```
cd /usr/local/src/playsms-1.3/
mysql -uroot -p playsms < db/playsms-upgrade_1.2_or_1.2.1_to_1.3.sql
```

## 2nd bug

The bug will cause your Kannel not receiving delivery reports due to empty `dlr-mask`.

To fix this you need to download Kannel gateway's `fn.php` from Github and replace yours.

Example, your playSMS is installed in `/var/www/html/playsms`. Run below commands to fix this bug:

```
wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/web/plugin/gateway/kannel/fn.php
cp fn.php /var/www/html/playsms/plugin/gateway/kannel/fn.php
playsmsd restart
playsmsd check
```
