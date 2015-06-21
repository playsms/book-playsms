# Requirements setup on Ubuntu

Prior to playSMS installation the server must be prepared by installing playSMS required applications.

In this tutorial the preparation is done for Ubuntu with LAMP stack.

1.  Upgrade

    ```
    apt-get update
    apt-get upgrade
    ```

2.  Install LAMP stack, and some PHP extensions

    ```
    apt-get install apache2 mysql-server php5 php5-cli php5-mysql php5-gd php5-curl php5-imap php5-mcrypt
    ```

3.  Start `apache2`

    ```
    service apache2 restart
    ```

4.  Browser `http://localhost` and see if the web server is serving
