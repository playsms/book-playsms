# Using install script

Install playSMS using install script `install-playsms.sh`.

Please note that before following below steps you need to cover all steps required in [Requirements setup on Ubuntu](Requirements-setup-on-Ubuntu.md).

Please also note that the current official release is **playSMS version 1.3** and we will use that.

1.  Login as `root` or become `root`

    ```
    sudo su -
    ```

2.  Extract playSMS package and go there (For example in /usr/local/src)

    ```
    tar -zxf playsms-1.3.tar.gz -C /usr/local/src
    ls -l /usr/local/src/
    cd /usr/local/src/playsms-1.3/
    ```

3.  Copy install.conf.dist to install.conf and edit install.conf

    Read install.conf and make changes to suit your system configuration

    ```
    cp install.conf.dist install.conf
    nano install.conf
    ```

4.  Run installer script

    ```
    ./install-playsms.sh
    ```

5.  Configure rc.local to get playsmsd started on boot

    Look for rc.local on /etc, /etc/init.d, /etc/rc.d/init.d

    When you found it edit that rc.local and put:

    `/usr/local/bin/playsmsd start`

    on the bottom of the file (before exit if theres an exit command).

    This way playsmsd will start automatically on boot.

6.  If you're using playSMS version 1.3 there are additional steps you need to do.
    
    Please follow additional steps as explained in [this page](Additional-step-for-playSMS-1.3-installation.md).

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
