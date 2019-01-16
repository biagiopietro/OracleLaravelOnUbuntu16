[![HitCount](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16.svg)](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16)
[![GitHub forks](https://img.shields.io/github/forks/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/network)
[![GitHub issues](https://img.shields.io/github/issues/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/issues)
[![GitHub license](https://img.shields.io/github/license/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/blob/master/LICENSE)
---

<h1 align="center">How to install oci8</h1>
<p align="center">
<sup>
<b>This guide is for only x64 system. (Tested on Ubuntu 16.04) </b>
</sup>
</p>


## Used files
* <a href = "https://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html">instantclient-basic-linux.x64-12.1.0.2.0.zip</a>
* <a href = "https://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html">instantclient-sdk-linux.x64-12.1.0.2.0.zip</a>

## Steps

1) Create oracle directory
    ```
    mkdir /opt/oracle
    ```
2) Move ```instantclient-basic-linux.x64-12.1.0.2.0.zip``` and ```instantclient-sdk-linux.x64-12.1.0.2.0.zip``` into /opt/oracle
3) Move into oracle directory
    ```
    cd /opt/oracle
    ```
4) Unzip ```instantclient-basic-linux.x64-12.1.0.2.0.zip``` file
    ```
    unzip /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip
    ```
5) Unzip ```instantclient-sdk-linux.x64-12.1.0.2.0.zip``` file
    ```
    unzip /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip
    ``` 
6) Make link between files
    ```
    ln -s /opt/oracle/instantclient_12_2/libclntsh.so.12.1 /opt/oracle/instantclient_12_2/libclntsh.so
    ```
7) Make link between files
    ```
    ln -s /opt/oracle/instantclient_12_2/libocci.so.12.1 /opt/oracle/instantclient_12_2/libocci.so
    ```
8) Copy this line ```/opt/oracle/instantclient_12_2``` into ```oracle-instantclient```
    ```
    echo /opt/oracle/instantclient_12_2 > /etc/ld.so.conf.d/oracle-instantclient
    ```
9) Configure dynamic linker run-time bindings 
    ```
    ldconfig
    ```
10) Install php, build-essential and libaio1 
    ```
    apt-get install php-dev php-pear build-essential libaio1
    ```
11) Install oci8
    ```
    pecl install oci8
    ```
12) When you are prompted for the Instant Client location, enter the following: 
    ```
    instantclient,/opt/oracle/instantclient_12_2
    ```
13) Install ```php7.2-fpm```
    ```
    apt-get install php7.2-fpm
    ```
14) Copy in append this line ```extension = oci8.so``` into ```/etc/php/7.2/fpm/php.ini```
    ```
    echo "extension = oci8.so" >> /etc/php/7.2/fpm/php.ini
    ```
15) Copy in append this line ```extension = oci8.so``` into ```/etc/php/7.2/cli/php.ini```
    ```
    echo "extension = oci8.so" >> /etc/php/7.2/cli/php.ini
    ```
16) Check if the extension is enabled
    ```
    php -m | grep 'oci8'
    ```
    and if you see ```oci8```, its works!
17) Restart ```php7.1-fpm``` service
    ```
    service php7.1-fpm restart
    ```

### Note
* If you see warnings or errors please remove ```php*-xml``` and install it again, so:
   ```
    apt-get purge php*-xml 
    apt-get autoremove php*-xml
    apt-get install php-xml php7.1-xml
   ```
			

## Special Thanks
Special thanks to <a href="https://github.com/puffoCyano">PuffoCyano</a> for his help and <a href="https://stackoverflow.com/">StackOverflow</a> for replies.
