# Upgrade from version 1.0 to 1.1

We have 9 steps below that must be followed sequentially to successfully upgrades an installed, unmodified, playSMS version 1.0 to playSMS version 1.1.

Essentially upgrades means that:

1. You backup old files and database (get the database SQL file)
2. Then you remove old files
3. Then you install new version, in the same path and same database
4. Then you re-insert old backup database SQL file from step 1
5. Then you upgrade the database with SQL upgrade file from new version

Skim this article from top to bottom before start. Follow them correctly and in order.

Let's start.

1.  Stop current playSMS daemon

    ```
    playsmsd stop
    playsmsd check
    ```

2.  Backup everything related to installed playSMS 1.0

    Backup playSMS database:
    - playSMS DB as SQL file, example DB name is `playsms`:
    
      ```
      mysqldump -u root -p --add-drop-table playsms > playsms.sql
      ```
      
      Please note that the option `--add-drop-table` above is very important, **do not miss it**.
    
    Backup playSMS files and folders:
    - playSMS daemon script at `/usr/local/bin/playsmsd`
    - playSMS daemon config at `/etc/playsmsd`
    - playSMS files at web folder `/var/www/html/playsms`
    
    WARNING:
    - Backup process is very important
    - Do not continue if you have any hesitation
    - Ask a lot if you have doubt
    - You must make sure that you know how to restore them

3.  Remove all old playSMS files at web folder

    In this example the old playSMS web folder is `/var/www/html/playsms`

    ```
    cd /var/www/html/playsms
    ls -l
    rm -rf *
    ```
    
    WARNING: 
    - Prior to running above `rm -rf *` command you must make sure that you have the backup
    - And also make sure that you type the command correctly in the correct location

4.  Install playSMS version 1.1 in the same server with the same DB and the same web folder

    Stop here for a while, relax, its going to take sometime.
    
    Please remember that you are currently upgrading, not just installing, therefore after playSMS 1.1 installation you need to comeback here and continue to step 5 and the rest.

    playSMS version 1.1 installation manual is available from [previous chapter](../playSMS-Installation/README.md).
    
    This step requires you to install playSMS version 1.1 on top of installed playSMS 1.0, that means old database, files and folders will be replaced with the new one.

5.  Stop playSMS daemon, and make sure its stopped (no PIDS shown)

    ```
    playsmsd stop
    playsmsd check
    ```

6.  Re-insert your backup playSMS DB sql file (DB sql file dump from previous installation) to the same DB

    ```
    mysql -uroot -p playsms < playsms.sql
    ```

7.  Upgrade DB

    - Get DB upgrade SQL from GitHub repository
    
      ```
      wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/db/playsms-upgrade_1.0_to_1.1.sql
      ```

    - re-insert that upgrade DB file into current playSMS DB
    
      ```
      mysql -uroot -p playsms < ./playsms-upgrade_1.0_to_1.1.sql
      ```

8.  Start playSMS daemon, and make sure its started (PIDS are displayed)

    ```
    playsmsd start
    playsmsd check
    ```

9.  Verify installation after upgrade
