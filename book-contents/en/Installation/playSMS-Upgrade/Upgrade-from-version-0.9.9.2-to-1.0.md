playSMS Upgrade
===============

# Upgrade from version 0.9.9.2 to 1.0


1.  Stop current playSMS daemon

    ```
    playsmsd stop
    playsmsd check
    ```

2.  Backup everything related to installed playSMS 0.9.9.2

    Backup these items:
    - playSMS DB as SQL file, example DB name is `playsms`:
    
      ```
      mysqldump -u root -p --add-drop-table playsms > playsms.sql
      ```
      
    - playSMS daemon at `/usr/local/bin/playsmsd`
    - playSMS daemon config at `/etc/playsmsd`
    - playSMS files at web folder `/var/www/playsms`
    
    WARNING:
    - Backup process is very important
    - Do not continue if you have any hesitation
    - Ask a lot if you have doubt
    - You must make sure that you know how to restore

3.  Remove all old playSMS files at web folder

    ```
    cd /var/www/playsms
    rm -rf .
    ```
    
    WARNING: 
    - Prior to running above `rm -rf .` command you must make sure that you have the backup
    - And also make sure that you type the command correctly and in order

4.  Install playSMS version 1.0 in the same server with the same DB and the same web folder

    Installation manual is available from [previous chapter](../playSMS-Installation/README.md).

5.  Stop playSMS daemon

    ```
    playsmsd stop
    playsmsd check
    ```


6.  Re-insert your backup playSMS DB sql file to the same DB

    ```
    mysql -uroot -p playsms < playsms.sql
    ```

7.  Upgrade DB

    - Get DB upgrade SQL from GitHub repository
    
      ```
      wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/db/playsms-upgrade_0.9.9.2_to_1.0.sql
      ```

    - re-insert that upgrade DB file into current playSMS DB
    
      ```
      mysql -uroot -p playsms < ./playsms-upgrade_0.9.9.2_to_1.0.sql
      ```

8.  Start playSMS daemon

    ```
    playsmsd start
    playsmsd check
    ````

9.  Verify installation after upgrade
