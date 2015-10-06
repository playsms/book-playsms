# Using install script

Install playSMS using install script `install-playsms.sh`.

Please note that before following below steps you need to cover all steps required in [Requirements setup on Ubuntu](Requirements-setup-on-Ubuntu.md).

Please also note that the current official release is **playSMS version 1.3.1** and we will use that.

1.  Extract playSMS package and go there (For example in /usr/local/src)

    ```
    sudo tar -zxf playsms-1.3.1.tar.gz -C /usr/local/src
    ls -l /usr/local/src/
    cd /usr/local/src/playsms-1.3.1/
    ```

2.  Copy install.conf.dist to install.conf and edit install.conf

    Read install.conf and make changes to suit your system configuration

    ```
    sudo cp install.conf.dist install.conf
    sudo nano install.conf
    ```

3.  Run installer script

    ```
    sudo ./install-playsms.sh
    ```

4.  Configure `rc.local` to get playsmsd started on boot

    Look for `rc.local` on `/etc`, `/etc/init.d` or `/etc/rc.d/init.d`

    When you found it edit that `rc.local` and put:

    `/usr/local/bin/playsmsd start`

    on the bottom of the file (before exit if theres an exit command).

    This way playsmsd will start automatically on boot.

Note:

* After successful installation, please run command `ps ax` and see if playsmsd is running

  ```
  ps ax | grep playsms
  4069 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd /etc/playsmsd.conf schedule
  4071 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd /etc/playsmsd.conf dlrssmsd
  4073 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd /etc/playsmsd.conf recvsmsd
  4075 pts/12  S    0:00 /usr/bin/php -q /usr/local/bin/playsmsd /etc/playsmsd.conf sendsmsd
  ```

* Run several checks

  ```
  sudo playsmsd status
  sudo playsmsd check
  ```

* Stop here and review your installation steps when playsmsd is not running
* Consider to ask question in playSMS forum when you encountered a problem
* If all seems to be correctly installed you may try to login from web browser

  ```
  URL                    : http://[your web server IP]/playsms/
  Default admin username : admin
  Default admin password : admin
  ```
