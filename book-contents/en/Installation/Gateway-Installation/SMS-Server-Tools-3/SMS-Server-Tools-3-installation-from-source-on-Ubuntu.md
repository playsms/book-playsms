# SMS Server Tools 3 installation from source on Ubuntu

In this tutorial we will be using SMS Server Tools 3 version [3.1.15](http://smstools3.kekekasvi.com/packages/smstools3-3.1.15.tar.gz) source package.

Here we have 10 steps that you need to follow one step at a time and in order.

Please stop, do not continue to the next step, and post questions in playSMS Forum when you experienced difficulties or found error during following this manual.

Let's start.

1.  Make sure you have root access

    ```
    sudo su -
    ```

2.  Install required packages for building SMS Server Tools 3 from source in Ubuntu

    ```
    apt-get install build-essential
    ```

3.  Get source package and extract it

    Download `smstools3-3.1.15.tar.gz` from http://smstools3.kekekasvi.com and save it in `/usr/local/src`

    ```
    cd /usr/local/src
    wget -c http://smstools3.kekekasvi.com/packages/smstools3-3.1.15.tar.gz
    tar -zxvf smstools3-3.1.15.tar.gz
    ```

4.  Enter the extracted source codes directory and execute make to compile followed by installing smstools3

    ```
    cd smstools3
    make
    make install
    ```

5.  Create required directories

    ```
    mkdir -p /var/log/sms/stats
    mkdir -p /var/spool/sms/{checked,failed,incoming,outgoing,sent,modem1,modem2}
    ```
    
    Note:
    
    - The directory names are case-sensitive

6.  Setup SMS Server Tools 3 spool directories owner and permission

    In this example your webserver's user and group is `www-data`
   
    ```
    chown www-data:www-data -R /var/spool/sms
    ```
    
    You can also set files and folders permission to world-writable
    
    ```
    chmod 777 -R /var/spool/sms
    ```

7.  Get example of `smsd.conf` and copy to `/etc/`

    ```
    mv /etc/smsd.conf /etc/smsd.conf.dist
    wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/contrib/smstools/smsd.conf
    cp smsd.conf /etc/
    ```
    
    Note:
   
    - Before continue to the next step you have to take a look at `/etc/smsd.conf` and edit the file accordingly
    - You may need to adjust queues and modems options
    - Mostly you do not need to change other options but queues and modems
    - Do not change the file or directory paths
    
    Important:
    
    - Modem name must be the same as SMSC name in playSMS

8.  Run SMS Server Tools 3

    ```
    /etc/init.d/sms3 start
    ```

10. Verify if SMS Server Tools 3 is running

    ```
    ps ax | grep -v grep | grep smsd
    ```
    
    Monitor SMS Server Tools 3 log file:
    
    ```
    tail -f /var/log/smsd.log
    ```
