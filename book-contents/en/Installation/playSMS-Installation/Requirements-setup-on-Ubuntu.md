# Requirements setup on Ubuntu

Prior to playSMS installation the server must be prepared by installing playSMS required applications.

In this tutorial the preparation is done for Ubuntu with LAMP stack.

1.  Upgrade

    ```
    apt-get update
    apt-get upgrade
    ```

2.  Install LAMP stack and some PHP extensions

    ```
    apt-get install apache2 libapache2-mod-php5 mysql-server php5 php5-cli php5-mysql php5-mcrypt php5-gd php5-imap php5-curl
    ```

3.  Enable `mcrypt` extension manually:

    ```
    php5enmod mcrypt
    ```

4.  Restart `apache2`

    ```
    service apache2 restart
    ```

5.  Browser `http://localhost` and see if the web server is serving

6.  Download playSMS package from `https://sourceforge.net/projects/playsms/files/playsms/` and save it or upload it to the server
