# Upgrade from version 1.0-rc4 to 1.0

We have 8 steps to follow to successfully upgrade an installed unmodified playSMS version 1.0-rc4 to 1.0.

Follow them correctly and in order.

1.  Stop current playSMS daemon

    ```
    playsmsd stop
    playsmsd check
    ```

2.  Backup everything related to installed playSMS 1.0-rc4

    Backup playSMS database:
    - playSMS DB as SQL file, example DB name is `playsms`:
    
      ```
      mysqldump -u root -p --add-drop-table playsms > playsms.sql
      ```
      
      Note that option `--add-drop-table` above is important, do not miss it.
    
    Backup playSMS files and folders:
    - playSMS daemon script at `/usr/local/bin/playsmsd`
    - playSMS daemon config at `/etc/playsmsd`
    - playSMS files at web folder `/var/www/playsms`
    
    WARNING:
    - Backup process is very important
    - Do not continue if you have any hesitation
    - Ask a lot if you have doubt
    - You must make sure that you know how to restore them

3.  Install playSMS version 1.0 in the same server with the same DB and the same web folder

    playSMS version 1.0 installation manual is available from [previous chapter](../playSMS-Installation/README.md).
    
    This step requires you to install playSMS version 1.0 on top of installed playSMS 1.0-rc4, that means old database, files and folders will be replaced with the new one.

4.  Stop playSMS daemon

    ```
    playsmsd stop
    playsmsd check
    ```

5.  Re-insert your backup playSMS DB sql file (DB sql file dump from previous installation) to the same DB

    ```
    mysql -uroot -p playsms < playsms.sql
    ```

6.  Upgrade DB

    - Get DB upgrade SQL from GitHub repository
    
      ```
      wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/db/playsms-upgrade_1.0-rc4_to_1.0.sql
      ```

    - re-insert that upgrade DB file into current playSMS DB
    
      ```
      mysql -uroot -p playsms < ./playsms-upgrade_1.0-rc4_to_1.0.sql
      ```

7.  Start playSMS daemon

    ```
    playsmsd start
    playsmsd check
    ```

8.  Verify installation after upgrade
