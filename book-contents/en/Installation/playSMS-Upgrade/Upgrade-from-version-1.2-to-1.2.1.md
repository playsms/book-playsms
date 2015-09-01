# Upgrade from version 1.2 to 1.2.1

We have a few steps below that must be followed sequentially to successfully upgrades an installed, 
unmodified, playSMS version 1.2 to playSMS version 1.2.1.

Essentially upgrades means that:

1. You backup old files and database
2. Then you get the new version and replace all old files
3. Then you upgrade the database with SQL upgrade file from new version

Skim this article from top to bottom before start. Follow them correctly and in order.

Let's start.

1.  Stop current playSMS daemon

    ```
    playsmsd stop
    playsmsd check
    ```

2.  Backup everything related to installed playSMS 1.2

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

3.  Copy files from playSMS version 1.2.1 to replace old files

    Download `playsms-1.2.1.tar.gz` from Sourceforge, visit [playSMS Download](http://playsms.org/download) for more information.
    
    Run below commands to extract downloaded playSMS and replace old files:

    ```
    tar -zxf playsms-1.2.1.tar.gz -C /usr/local/src
    ls -l /usr/local/src/
    cd /usr/local/src/playsms-1.2.1/
    cp -rR web/* /var/www/html/playsms
    cp daemon/linux/bin/playsmsd.php /usr/local/bin/playsmsd
    chmod 755 /usr/local/bin/playsmsd
    ```

6.  Upgrade DB

    SQL upgrade file is available on `playsms-1.2.1.tar.gz`.

    ```
    mysql -uroot -p playsms < db/playsms-upgrade_1.2_to_1.2.1.sql
    ```

7.  Start playSMS daemon, and make sure its started (PIDS are displayed)

    ```
    playsmsd /etc/playsmsd.conf start
    playsmsd /etc/playsmsd.conf check
    ```

8.  Verify installation after upgrade
