# IPerfd
This how-to aims to start IPerf as a daemon.
## Prerequisite
Before making anything, you must install IPerf package:
sudo apt install iperf3

The operating system is Ubuntu server 18.04.4 LTS
## Installation
#### Download needed files
You need to download two files in your home directory:
```
cd ~
wget https://raw.githubusercontent.com/mikael-andre/IPerfd/master/iperfd.service
wget https://raw.githubusercontent.com/mikael-andre/IPerfd/master/iperfd
```
#### Copy files
Once downloaded, you have to copy init script in `/etc/systemd/system` and configuration file in `/etc/default`:
```
sudo cp -p iperfd.service /etc/systemd/system/iperfd.service
sudo cp -p iperfd /etc/default/iperfd
```
#### Give good rights
The init script needs excute rights:
```
chmod 664 /etc/systemd/system/iperfd.service 
```
#### Create log file
In order to log, you have to create a new log file in `/var/log` folder by the following command:
```
touch /var/log/iperfd.log
```
#### Reload Systemd
After giving theses privileges, you have to reload systemd
```
systemctl daemon-reload
```
#### Automatic start
Finaly, if you want init script to start on boot, you have to type this command
```
systemctl enable iperfd
```
## Verifications
By the same command, `systemctl status iperfd`, you can verify if IPerfd is started or stopped.
#### Started
```
root@lnx001:~# systemctl status iperfd
```
#### Stopped
```
root@lnx001:~# systemctl status iperfd
```
