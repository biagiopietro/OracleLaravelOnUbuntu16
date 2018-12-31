[![HitCount](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16.svg)](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16)
[![GitHub forks](https://img.shields.io/github/forks/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/network)
[![GitHub issues](https://img.shields.io/github/issues/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/issues)
[![GitHub license](https://img.shields.io/github/license/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/blob/master/LICENSE)
---

<h1 align="center">How to enable oci8 in Laravel</h1>
<p align="center">
<sup>
<b>This guide is for only x64 system. (Tested on Ubuntu 16.04) </b>
</sup>
</p>


## Used files
* <a href = "http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html">oracle-xe-11.2.0-1.0.x86_64.rpm.zip</a>

## Steps
1) Copy the downloaded file (oracle-xe-11.2.0-1.0.x86_64.rpm.zip)
2) Move to home directory and paste it.
    ```
    cd $HOME   
    ``` 
3) Unzip using the command:
    ```
    unzip oracle-xe-11.2.0-1.0.x86_64.rpm.zip 
    ```
4) Install required packages using the command:
    ```
    sudo apt-get install alien libaio1 unixodbc
    ```
5) Enter into the Disk1 folder using command:
    ```
    cd Disk1/
    ```
6) Convert RPM package format to DEB package format (that is used by Ubuntu) using the command:
    ```
    sudo alien --scripts -d oracle-xe-11.2.0-1.0.x86_64.rpm
    ```
7) Create the required chkconfig script using the command:
    ```
    sudo pico /sbin/chkconfig
    ```
   The pico text editor is started and the commands are shown at the bottom of the screen. Now copy and paste the following into the file and save:
    ```     
    #!/bin/bash
    # Oracle 11gR2 XE installer chkconfig hack for Ubuntu
    file=/etc/init.d/oracle-xe
    if [[ ! `tail -n1 $file | grep INIT` ]]; then
        echo >> $file
        echo '### BEGIN INIT INFO' >> $file
        echo '# Provides: OracleXE' >> $file
        echo '# Required-Start: $remote_fs $syslog' >> $file
        echo '# Required-Stop: $remote_fs $syslog' >> $file
        echo '# Default-Start: 2 3 4 5' >> $file
        echo '# Default-Stop: 0 1 6' >> $file
        echo '# Short-Description: Oracle 11g Express Edition' >> $file
        echo '### END INIT INFO' >> $file
    fi
    update-rc.d oracle-xe defaults 80 01
    ```
8) Change the permission of the chkconfig file using the command:
    ```
    sudo chmod 755 /sbin/chkconfig
    ```
9) Set kernel parameters. Oracle 11gR2 XE requires additional kernel parameters which you need to set using the command:
    ```
    sudo pico /etc/sysctl.d/60-oracle.conf
    ```
10) Copy the following into the file and save:
    ```
    # Oracle 11g XE kernel parameters 
    fs.file-max=6815744  
    net.ipv4.ip_local_port_range=9000 65000  
    kernel.sem=250 32000 100 128 
    kernel.shmmax=536870912 
    ```
11) Verify the change using the command:
    ```
    sudo cat /etc/sysctl.d/60-oracle.conf 
    ```
12) You should see what you entered earlier. Now load the kernel parameters:
    ```
    sudo service procps start
    ```
13) Verify the new parameters are loaded using:
    ```
    sudo sysctl -q fs.file-max
    ```
    You should see the file-max value that you entered earlier.
14) Set up /dev/shm mount point for Oracle. Create the following file using the command:
    ```
    sudo pico /etc/rc2.d/S01shm_load
    ```
15) Copy the following into the file and save.
    ```
    #!/bin/sh
    case "$1" in
    start)
        mkdir /var/lock/subsys 2>/dev/null
        touch /var/lock/subsys/listener
        rm /dev/shm 2>/dev/null
        mkdir /dev/shm 2>/dev/null
    *)
        echo error
        exit 1
        ;;
    
    esac 
    ```    
16) Change the permissions of the file using the command:
    ```
    sudo chmod 755 /etc/rc2.d/S01shm_load
    ``` 
17) Now execute the following commands:
    ```
    sudo ln -s /usr/bin/awk /bin/awk 
    sudo mkdir /var/lock/subsys 
    sudo touch /var/lock/subsys/listener
    ```
18) Reboot your PC!
19) Move again into
    ```
    cd Disk1/
    ```
20) Install the oracle DBMS using the command:
    ```
    sudo dpkg --install oracle-xe_11.2.0-2_amd64.deb
    ```
21) Configure Oracle using the command:
    ```
    sudo /etc/init.d/oracle-xe configure 
    ```
    * When is required please insert the port number suggested in []
    * Then you have to insert a password 
    * Confirm the password
    * Choose if you want to start on boot the oracle database
22) Setup environment variables by editing your .bashrc file:
    ```
    pico ~/.bashrc
    ```
23) Add the following lines to the end of the file:
    ```
    export ORACLE_HOME=/u01/app/oracle/product/11.2.0/xe
    export ORACLE_SID=XE
    export NLS_LANG=`$ORACLE_HOME/bin/nls_lang.sh`
    export ORACLE_BASE=/u01/app/oracle
    export LD_LIBRARY_PATH=$ORACLE_HOME/lib:$LD_LIBRARY_PATH
    export PATH=$ORACLE_HOME/bin:$PATH
    ```
24) Load the changes by executing your profile:
    ```
    . ~/.bashrc
    ```
25) Start the Oracle 11gR2 XE:
    ```
    sudo service oracle-xe start
    ```
26) Add user <YOURUSERNAME> to group dba using the command:
    ```
    sudo usermod -a -G dba <YOURUSERNAME>
    ```   
27) Start the Oracle XE 11gR2 server using the command:
    ```
    sudo service oracle-xe start
    ```
28) Start command line shell as the system admin using the command:
    ```
    sqlplus sys as sysdba
    ```
    Enter the password that you gave while configuring Oracle earlier. 
    You will now be placed in a SQL environment that only understands SQL commands.
29) Create a regular user account in Oracle using the SQL command:
    ```
    create user <USERNAME> identified by <PASSWORD>;
    ```
    Replace USERNAME and PASSWORD with the username and password of your choice. 
    Please remember this username and password.
    #### Note
    If you had error executing the above with a message about resetlogs, then execute the following SQL command and try again:
        ```
        alter database open resetlogs;
        ```   
30) Grant privileges to the user account using the SQL command:
    ```
    grant connect, resource to <USERNAME>;
    ```
    Replace USERNAME and PASSWORD with the username and password of your choice.
    Please remember this username and password.
31) Exit the sys admin shell using the SQL command:
    ```
    exit;
    ```
32) Start the commandline shell as a regular user using the command:
    ```
    sqlplus
    ```
    Now, you can run sql commands...
33) Finish!!!

### Note
* If you see warnings or errors please remove php*-xml and install it again, so:
    ```
    apt-get purge php*-xml 
    apt-get autoremove php*-xml
    apt-get install php-xml php7.1-xml
    ```
			

## Special Thanks
Special thanks to <a href="https://github.com/puffoCyano">PuffoCyano</a> for his help and <a href="https://stackoverflow.com/">StackOverflow</a> for replies.