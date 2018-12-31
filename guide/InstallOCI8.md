[![HitCount](http://hits.dwyl.io/biagiopietro/LicenseDialog.svg)](http://hits.dwyl.io/biagiopietro/LicenseDialog)
[![GitHub forks](https://img.shields.io/github/forks/biagiopietro/LicenseDialog.svg)](https://github.com/biagiopietro/LicenseDialog/network)
[![GitHub issues](https://img.shields.io/github/issues/biagiopietro/LicenseDialog.svg)](https://github.com/biagiopietro/LicenseDialog/issues)
[![GitHub license](https://img.shields.io/github/license/biagiopietro/LicenseDialog.svg)](https://github.com/biagiopietro/LicenseDialog/blob/master/LICENSE)
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

1) mkdir /opt/oracle
2) move the "instantclient-basic-linux.x64-12.1.0.2.0.zip" and "instantclient-sdk-linux.x64-12.1.0.2.0.zip" into /opt/oracle
3) cd /opt/oracle
4) unzip /opt/oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip
5) unzip /opt/oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip
6) ln -s /opt/oracle/instantclient_12_2/libclntsh.so.12.1 /opt/oracle/instantclient_12_2/libclntsh.so
7) ln -s /opt/oracle/instantclient_12_2/libocci.so.12.1 /opt/oracle/instantclient_12_2/libocci.so
8) echo /opt/oracle/instantclient_12_2 > /etc/ld.so.conf.d/oracle-instantclient
9) ldconfig
10) apt-get install php-dev php-pear build-essential libaio1
11) pecl install oci8
12) When you are prompted for the Instant Client location, enter the following: instantclient,/opt/oracle/instantclient_12_2
13) apt-get install php7.2-fpm
14) echo "extension = oci8.so" >> /etc/php/7.2/fpm/php.ini
15) echo "extension = oci8.so" >> /etc/php/7.2/cli/php.ini
16) Check if the extension is enabled, so run php -m | grep 'oci8' and If you see "oci8", its works!
17) service php7.1-fpm restart

### Note
* If you see warnings or errors please remove php*-xml and install it again, so:
    1) apt-get purge php*-xml 
    2) apt-get autoremove php*-xml
    3) apt-get install php-xml php7.1-xml
			

## Special Thanks
Special thanks to <a href="https://github.com/puffoCyano">PuffoCyano</a> for his help and <a href="https://stackoverflow.com/">StackOverflow</a> for replies.