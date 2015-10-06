# Upgrade to playSMS version 1.3.1

We have a few steps below that must be followed sequentially to successfully upgrades an installed, unmodified, 
playSMS version 1.1, 1.2, 1.2.1 or 1.3 to playSMS version 1.3.1.

Please note that upgrade instructions in this article are not compatible with playSMS 1.0 and before.

Essentially upgrades means that:

1. You backup old files and database
2. Then you get the new version and replace all old files
3. Then you upgrade the database with SQL upgrade file from new version

Skim this article from top to bottom before start. Follow them correctly and in order.

Let's start.

1.  Stop current playSMS daemon

    ```
    sudo playsmsd stop
    sudo playsmsd check
    ```

2.  Backup everything related to installed playSMS 1.1, 1.2, 1.2.1 or 1.3

    Backup playSMS database:
    - playSMS DB as SQL file, example DB name is `playsms`:
    
      ```
      mysqldump -u root -p --add-drop-table playsms > playsms.sql
      ```
      
      Please note that the option `--add-drop-table` above is very important, **do not miss it**.
    
    Backup playSMS files and folders:
    
    - playSMS daemon script is `/usr/local/bin/playsmsd`
    - playSMS daemon config is `/etc/playsmsd.conf`
    - playSMS files are located at web folder `/var/www/html/playsms`
    
    WARNING:
    
    - Backup process is very important
    - Do not continue if you have any hesitation
    - Ask a lot if you have doubt
    - You must make sure that you know how to restore them

3.  Copy files from playSMS version 1.3.1 to replace old files

    Download `playsms-1.3.1.tar.gz` from Sourceforge, visit [playSMS Download](http://playsms.org/download) for more information.
    
    Run below commands to extract downloaded playSMS and replace old files:

    ```
    sudo tar -zxf playsms-1.3.1.tar.gz -C /usr/local/src
    ls -l /usr/local/src/
    cd /usr/local/src/playsms-1.3.1/
    sudo cp -rR web/* /var/www/html/playsms
    sudo cp daemon/linux/bin/playsmsd.php /usr/local/bin/playsmsd
    sudo chmod 755 /usr/local/bin/playsmsd
    ```

6.  Upgrade DB

    SQL upgrade file is available on `playsms-1.3.1.tar.gz`.

    If you upgrade from playSMS 1.1 to 1.3.1:

    ```
    mysql -uroot -p playsms < db/playsms-upgrade_1.1_to_1.3.1.sql
    ```

    If you upgrade from playSMS 1.2 or 1.2.1 to 1.3.1:

    ```
    mysql -uroot -p playsms < db/playsms-upgrade_1.2_or_1.2.1_to_1.3.1.sql
    ```

    If you upgrade from playSMS 1.3 to 1.3.1:

    ```
    mysql -uroot -p playsms < db/playsms-upgrade_1.3_to_1.3.1.sql
    ```

7.  Start playSMS daemon, and make sure its started (PIDS are displayed)

    ```
    playsmsd /etc/playsmsd.conf start
    playsmsd /etc/playsmsd.conf check
    playsmsd /etc/playsmsd.conf version
    ```

8.  Verify installation after upgrade
