# Without install script

Install playSMS by following step-by-step:

1. Login as `root`

2.  Extract playSMS package and go there (For example in /usr/local/src)

    ```
    tar -zxf playsms-1.0.tar.gz -C /usr/local/src
    ls -l /usr/local/src/
    cd /usr/local/src/playsms-1.0/
    ```

3.  Run getcomposer.sh

    ```
    ./getcomposer.sh
    ```

    You may see the following warning, that can safely be ignored:
    ```
    Warning: Ambiguous class resolution, "PEAR_ErrorStack" was found in both "/usr/local/src/playsms-1.0/web/lib/composer/vendor/pear/pear/PEAR/ErrorStack.php" and "/usr/local/src/playsms-1.0/web/lib/composer/vendor/pear/pear/PEAR/ErrorStack5.php", the first will be used.
    ```

4.  Create playSMS web root, log, lib and set ownership to user www-data or web server user

    Assumed that your web root is `/var/www` and your web server user is `www-data`

    ```
    mkdir -p /var/www/playsms /var/log/playsms /var/lib/playsms
    chown -R www-data /var/www/playsms /var/log/playsms /var/lib/playsms
    ```

    Please note that there are Linux distributions using `apache` as web server user instead of `www-data`

    Also note that there are Linux distributions set `/var/www/html` as web root instead of `/var/www`

5.  Copy files and directories inside `web` directory to playSMS web root and set ownership to web server user

    ```
    cp -R web/* /var/www/playsms
    chown -R www-data /var/www/playsms
    ```

6.  Setup database (import database)

    ```
    mysqladmin -u root -p create playsms
    cat db/playsms.sql | mysql -u root -p playsms
    ```

7.  Copy config-dist.php to config.php and then edit config.php

    ```
    cp /var/www/playsms/config-dist.php /var/www/playsms/config.php
    vi /var/www/playsms/config.php
    ```

    Please read and fill all fields with correct values

8.  Enter daemon/linux directory, copy files and folder inside

    ```
    cp daemon/linux/etc/playsmsd.conf /etc/playsmsd.conf
    cp daemon/linux/bin/playsmsd /usr/local/bin/playsmsd
    ```

9.  Just to make sure every paths are correct, please edit /etc/playsmsd.conf

    ```
    vi /etc/playsmsd.conf
    ```

    Make sure that `PLAYSMS_PATH` is pointing to a correct playSMS installation path (in this example to /var/www/playsms)

    Also Make sure that `PLAYSMS_BIN` is pointing to a correct playSMS daemon scripts path (in this example to /usr/local/bin)

10. Start playsmsd now from Linux console, no need to reboot

    ```
    playsmsd start
    ```

11. Configure rc.local to get playsmsd started on boot

    Look for rc.local on /etc, /etc/init.d, /etc/rc.d/init.d

    When you found it edit that rc.local and put:

    `/usr/local/bin/playsmsd start`

    on the bottom of the file (before exit if theres an exit command).

    This way playsmsd will start automatically on boot.

Note:

* After successful installation, please run command `ps ax` and see if playsmsd is running

  ```
  ps ax | grep playsms
  4069 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd schedule
  4071 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd dlrssmsd
  4073 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd recvsmsd
  4075 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd sendsmsd
  ```

* Run several checks

  ```
  playsmsd status
  playsmsd check
  ```

* Stop here and review your installation steps when playsmsd is not running
* Consider to ask question in playSMS forum when you encountered a problem
* If all seems to be correctly installed you may try to login from web browser

  ```
  URL                    : http://[your web server IP]/playsms/
  Default admin username : admin
  Default admin password : admin
  ```
