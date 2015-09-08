# Additional step for playSMS 1.3 installation

This is a special case, we may call it a bug in playSMS 1.3. The bug will cause playSMS (sendsmsd) unable to actually deliver SMS to gateways.
It was caused by a missing field in `playsms.sql` that is used during installation.

To fix playSMS 1.3 installation you need to insert an upgrade SQL file to your new playSMS 1.3 database.

Example, playSMS 1.3 source package was extracted to `/usr/local/src/playsms-1.3/` and playSMS 1.3 database is `playsms`, run below commands to fix the bug:

```
cd /usr/local/src/playsms-1.3/
mysql -uroot -p playsms < db/playsms-upgrade_1.2_or_1.2.1_to_1.3.sql
```
