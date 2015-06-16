# Gammu installation via apt-get on Ubuntu

Here we have 6 steps that you need to follow one step at a time and in order.

Please stop, do not continue to the next step, and post questions in playSMS Forum when you experienced difficulties or found error during following this manual.

1.  Make sure you have root access
    
    ```
    sudo su -
    ```

2.  Install Gammu via `apt-get`

    ```
    apt-get install gammu-smsd
    ```

3.  Create required directories

    ```
    mkdir -p /var/log/gammu /var/spool/gammu/{inbox,outbox,sent,error}
    ```
    
    Note:
    
    - The directory names are case-sensitive

4.  Setup Gammu spool directories owner and permission

    In this example your webserver's user and group is `www-data`
   
    ```
    chown www-data:www-data -R /var/spool/gammu/*
    ```
    
    You can also set files and folders permission to world-writable
    
    ```
    chmod 777 -R /var/spool/gammu/*
    ```

5.  Get example of `gammu-smsdrc` from playSMS package and copy to `/etc/`

    ```
    wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/contrib/gammu/linux/gammu-smsdrc
    cp gammu-smsdrc /etc/
    ```
    
    Note:
   
    - Before continue to the next step you have to take a look at `/etc/gammu-smsdrc` and edit the file accordingly
    - Try to identify your modem by running `gammu --config /etc/gammu-smsdrc identify`
    - You may need to adjust the `port` and `connection` options
    - Mostly you do not need to change other options
    - Do not change the file or directory paths

6.  Run gammu-smsd

    ```
    /etc/init.d/gammu-smsd start
    ```
