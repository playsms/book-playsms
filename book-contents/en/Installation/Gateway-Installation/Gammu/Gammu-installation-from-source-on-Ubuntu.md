# Gammu installation from source on Ubuntu

Here we have 10 steps that you need to follow one step at a time and in order.

Please stop, do not continue to the next step, and post questions in playSMS Forum when you experienced difficulties or found error during following this manual.

Let's start.

1.  Make sure you have root access

    ```
    sudo su -
    ```

2.  Install required packages for building Gammu from source in Ubuntu

    ```
    apt-get install libcurl4-openssl-dev libusb-1.0-0-dev libbluetooth-dev libmysqlclient-dev cmake
    ```

3.  Download Gammu, navigate to Gammu source package file location and extract
   
    Download `gammu-1.36.2.tar.bz2` from http://wammu.eu and save it in `/usr/local/src`
   
    ```
    cd /usr/local/src
    wget -c wget -c http://dl.cihar.com/gammu/releases/gammu-1.36.2.tar.bz2
    tar -jxf gammu-1.36.2.tar.bz2
    ```

4.  Enter extracted Gammu source package directory and compile Gammu

    ```
    cd gammu-1.36.2
    ./configure
    make
    make test
    make install
    ldconfig
    ```
    
    Note:
    
    - Do not forget to run `ldconfig`

5.  Create required directories

    ```
    mkdir -p /var/log/gammu /var/spool/gammu/{inbox,outbox,sent,error}
    ```
    
    Note:
    
    - The directory names are case-sensitive

6.  Setup Gammu spool directories owner and permission

    In this example your webserver's user and group is `www-data`
   
    ```
    chown www-data:www-data -R /var/spool/gammu/*
    ```
    
    You can also set files and folders permission to world-writable
    
    ```
    chmod 777 -R /var/spool/gammu/*
    ```

7.  Get example of `gammu-smsdrc` from playSMS package and copy to `/etc/`

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

8.  Get `gammu_smsd_start` and `gammu_smsd_stop` scripts from playSMS package and copy to `/usr/local/bin`

    ```
    wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/contrib/gammu/linux/gammu_smsd_start
    wget -c https://raw.githubusercontent.com/antonraharja/playSMS/master/contrib/gammu/linux/gammu_smsd_stop
    cp gammu_smsd_start gammu_smsd_stop /usr/local/bin
    chmod +x /usr/local/bin/gammu_smsd*
    ls -l /usr/local/bin/gammu_smsd*
    ```
    
    Note:
   
    - Do not forget to set executable permission to those files (`chmod +x`)
    - You might also want to put `/usr/local/bin/gammu_smsd_start` in `/etc/rc.local` to get `gammu-smsd` started on boot

9.  Run `gammu_smsd_start` to start `gammu-smsd`

    ```
    gammu_smsd_start
    ```

10. Verify if `gammu-smsd` is running

    ```
    ps ax | grep -v grep | grep gammu-smsd
    ```
    
    Monitor Gammu smsd log file:
    
    ```
    tail -f /var/log/gammu/smsd.log
    ```
