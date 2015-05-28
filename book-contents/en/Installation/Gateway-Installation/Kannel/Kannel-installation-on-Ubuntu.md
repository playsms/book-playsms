# Kannel installation on Ubuntu

Prerequisites:

* You need Internet access
* You need to be root and gained access to Linux console
* Your Ubuntu or Debian must be configured correctly so that the `apt-get` will not fail

Below are steps required to install Kannel in Ubuntu or Debian:

1.  Install Kannel

    ```
    apt-get install kannel
    mkdir -p /var/log/kannel /var/run/kannel /var/spool/kannel/store
    chown -R kannel /var/log/kannel /var/run/kannel /var/spool/kannel/store
    usermod -a -G dialout kannel
    ```

2.  Edit `/etc/default/kannel` to activate smsbox

    ```
    sed -i 's/#START_SMSBOX/START_SMSBOX/' /etc/default/kannel
    ```

3.  Backup original kannel.conf

    ```
    cp /etc/kannel/kannel.conf /etc/kannel/kannel.conf.dist
    ```

4.  Download example `kannel.conf` and replace existing `/etc/kannel/kannel.conf`

    ```
    wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/contrib/kannel/kannel.conf
    cp kannel.conf /etc/kannel/
    ls -l /etc/kannel/
    ```

5.  Edit `/etc/kannel/kannel.conf`. Replace `http://CHANGE_THIS_TO_YOUR_PLAYSMS_URL`
    with your playSMS URL, for example with `http://localhost/playsms`

6.  Read the rest of `kannel.conf` and setup your Kannel.

    In the example `kannel.conf` you will see several option values with all uppercase, such as *KANNELADMIN_CHANGE_THIS*, you have to change them.
    Of course you need to understand how to configure `kannel.conf` properly, how to add modems and SMSCs when needed.
    
    Below URL is the user guide for understanding `kannel.conf`:
    `http://www.kannel.org/download/1.4.4/userguide-1.4.4/userguide.html`

7.  Only after you have configured `kannel.conf` to suit your needs and your setups then you may restart Kannel

    ```
    /etc/init.d/kannel restart
    ```

8. Verify Kannel installation

   ```
   ps ax | grep box
   netstat -lnpt
   tail -f /var/log/kannel/kannel.log
   ```
