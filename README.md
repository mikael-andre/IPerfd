# IPerfd
This how-to aims to start IPerf as a daemon.
## Prerequisite
Before making anything, you must install IPerf package:
```
sudo apt install iperf3
```

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
● iperfd.service - IPerf daemon
   Loaded: loaded (/etc/systemd/system/iperfd.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2020-04-22 19:30:23 UTC; 5s ago
  Process: 5912 ExecStartPost=/bin/sleep 1 (code=exited, status=0/SUCCESS)
  Process: 5902 ExecStart=/usr/bin/iperf3 --verbose --server --daemon --bind $IP_ADDRESS --port $PORT --logfile $LOG_FILE --pidfile $PID_FILE (code=exited, status=0/SUCCESS)
 Main PID: 5905 (iperf3)
    Tasks: 1 (limit: 2353)
   CGroup: /system.slice/iperfd.service
           └─5905 /usr/bin/iperf3 --verbose --server --daemon --bind 172.16.1.1 --port 5201 --logfile /var/log/iperfd.log --pidfile /var/run/iperfd.pid

Apr 22 19:30:22 lnx001.ibreizh.lan systemd[1]: Starting IPerf daemon...
Apr 22 19:30:23 lnx001.ibreizh.lan systemd[1]: Started IPerf daemon.
```
#### Stopped
```
root@lnx001:~# systemctl status iperfd
● iperfd.service - IPerf daemon
   Loaded: loaded (/etc/systemd/system/iperfd.service; enabled; vendor preset: enabled)
   Active: inactive (dead) since Wed 2020-04-22 19:31:32 UTC; 5s ago
  Process: 5912 ExecStartPost=/bin/sleep 1 (code=exited, status=0/SUCCESS)
  Process: 5902 ExecStart=/usr/bin/iperf3 --verbose --server --daemon --bind $IP_ADDRESS --port $PORT --logfile $LOG_FILE --pidfile $PID_FILE (code=exited, status=0/SUCCESS)
 Main PID: 5905 (code=exited, status=1/FAILURE)

Apr 22 19:30:22 lnx001.ibreizh.lan systemd[1]: Starting IPerf daemon...
Apr 22 19:30:23 lnx001.ibreizh.lan systemd[1]: Started IPerf daemon.
Apr 22 19:31:32 lnx001.ibreizh.lan systemd[1]: Stopping IPerf daemon...
Apr 22 19:31:32 lnx001.ibreizh.lan systemd[1]: Stopped IPerf daemon.
```
