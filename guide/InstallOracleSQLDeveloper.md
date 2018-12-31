[![HitCount](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16.svg)](http://hits.dwyl.io/biagiopietro/OracleLaravelOnUbuntu16)
[![GitHub forks](https://img.shields.io/github/forks/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/network)
[![GitHub issues](https://img.shields.io/github/issues/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/issues)
[![GitHub license](https://img.shields.io/github/license/biagiopietro/OracleLaravelOnUbuntu16.svg)](https://github.com/biagiopietro/OracleLaravelOnUbuntu16/blob/master/LICENSE)
---

<h1 align="center">How to install and configure Oracle SQL Developer</h1>
<p align="center">
<sup>
<b>This guide is for only x64 system. (Tested on Ubuntu 16.04) </b>
</sup>
</p>


## Used files
* <a href = "http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html">sqldeveloper-18.1.0.095.1630-no-jre.zip</a>

## Installation
### Steps

1) Install Java Version ```JDK 8``` (in some installations this is a requirement instead of 1.7):
	```
	sudo add-apt-repository ppa:webupd8team/java
	sudo apt-get update
	sudo apt-get install oracle-java8-installer
	sudo update-alternatives --config java
	```
2)	Copy "sqldeveloper-18.1.0.095.1630-no-jre.zip" to /opt folder and unzip it, so:
    ```
	cd /opt
	sudo unzip sqldeveloper-*-no-jre.zip -d /opt/
	sudo chmod +x /opt/sqldeveloper/sqldeveloper.sh
	```
3) Linking over an in-path launcher for Oracle SQL Developer:
	```
	sudo ln -s /opt/sqldeveloper/sqldeveloper.sh /usr/local/bin/sqldeveloper
    ```
4) Edit "/opt/sqldeveloper/sqldeveloper.sh" and replace it's content to:
	```
	#!/bin/bash
	unset -v GNOME_DESKTOP_SESSION_ID
	cd /opt/sqldeveloper/sqldeveloper/bin
	./sqldeveloper "$@"
	```
5) Run SQL Developer:
	```
	sqldeveloper
	```
	#### Note
	When you run Sql Developer at the first time, you need to specify the path of JDK's folder. 
	In my computer, JDK stored at ```/usr/lib/jvm/java-1.7.0-openjdk-amd64``` 
	For Java 8 and Ubuntu 16+ ```/usr/lib/jvm/java-8-oracle```
6) Finally, create desktop application for easy to use:
	```
	cd /usr/share/applications/
	sudo vim sqldeveloper.desktop
	```
7) add this lines:
	```
	[Desktop Entry]
	Exec=sqldeveloper
	Terminal=false
	StartupNotify=true
	Categories=GNOME;Oracle;
	Type=Application
	Icon=/opt/sqldeveloper/icon.png
	Name=Oracle SQL Developer
	```
8) then run:
	```
	sudo update-desktop-database
	```
9) Finish!!!
 
## Configuration
### Steps
1) Open Oracle SQL Developer
2) Right click on ```Connections``` -> ```Add Connection```, then fill the fields:
	```
	Connection name:
	username: <some_name>
	password: <some_password>
	hostname: <some_ip>( or eg. localhost)
	port: 1521
	SID: xe
	```
3) Click on ```Test``` button and if it returns no errors then click on ```Connect```
4) Finish!!!




## Special Thanks
Special thanks to <a href="https://github.com/puffoCyano">PuffoCyano</a> for his help and <a href="https://stackoverflow.com/">StackOverflow</a> for replies.