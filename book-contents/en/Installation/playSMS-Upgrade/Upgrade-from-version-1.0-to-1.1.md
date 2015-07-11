# Upgrade from version 1.0 to 1.1

We have 7 steps below that must be followed sequentially to successfully upgrades an installed, unmodified, playSMS version 1.0 to playSMS version 1.1.

Essentially upgrades means that:

1. You backup old files and database
2. Then you get the new version and replace all old files
3. Then you remove unused plugins
4. Then you upgrade the database with SQL upgrade file from new version

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

3.  Copy files from playSMS version 1.1 to replace old files

    Download `playsms-1.1.tar.gz` from Sourceforge, visit [playSMS Download](http://playsms.org/download) for more information.
    
    Run below commands to extract downloaded playSMS and replace old files:

    ```
    tar -zxf playsms-1.1.tar.gz -C /usr/local/src
    ls -l /usr/local/src/
    cd /usr/local/src/playsms-1.1/
    cp -rR web/* /var/www/html/playsms
    cp daemon/linux/bin/playsmsd /usr/local/bin
    ```

4.  Remove unused plugins

    ```
    cd /var/www/html/playsms
    rm -rf plugin/gateway/gnokii
    rm -rf plugin/gateway/msgtoolbox
    ```

5.  Upgrade DB

    SQL upgrade file is available on `playsms-1.1.tar.gz`.

    ```
    mysql -uroot -p playsms < /usr/local/src/playsms-1.1/db/playsms-upgrade_1.0_to_1.1.sql
    ```

6.  Start playSMS daemon, and make sure its started (PIDS are displayed)

    ```
    playsmsd start
    playsmsd check
    ```

7.  Verify installation after upgrade
