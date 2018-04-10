# TFTP Server on Raspberry PI Documentation

Personal unfinished documentation of installing, configuring, and testing a TFTP server
on my raspberry pi.

**Links -**
* [tftpd-hpa Package(Server)](https://packages.debian.org/stretch/tftpd-hpa)
* [tftp-hpa Package(Client)](https://packages.debian.org/stretch/tftp-hpa)
* [RFC 1350 - TFTP Protocol](https://tools.ietf.org/html/rfc1350)

* [xinetd Package(Not being used)](https://packages.debian.org/stretch/xinetd)



Started off by running `sudo raspi-config` to open the Raspberry Pi Configuration and
navigate to the interfaces tab and enable SSH then reboot.

Rest of the operations were done over ssh and tftp.

Installed package with command -
`sudo apt-get install tftpd-hpa`

made a backup of /etc/default/tftpd-hpa before editing. 
Modifications- 
* Edited `TFTP_ADDRESS="192.168.1.17:69"`

Created a newtest.txt file with the results of ls -la / in /svr/tftp

**Successfully** transferred the file from another LAN attached machine.
```
$ tftp 192.168.1.17

tftp> get newtest.txt
tftp> quit
```
File aquired from tftp contained the correct contents - 
```
total 87
drwxr-xr-x  22 root root  4096 Apr 10 13:58 .
drwxr-xr-x  22 root root  4096 Apr 10 13:58 ..
drwxr-xr-x   2 root root  4096 Apr 10 02:52 bin
drwxr-xr-x   3 root root  2560 Dec 31  1969 boot
-rw-r--r--   1 root root     4 Nov 15  2016 debian-binary
drwxr-xr-x  15 root root  3560 Apr 10 14:00 dev
drwxr-xr-x 111 root root  4096 Apr 10 13:57 etc
drwxr-xr-x   3 root root  4096 Apr 10  2017 home
drwxr-xr-x  18 root root  4096 Apr 10 02:49 lib
drwx------   2 root root 16384 Apr 10  2017 lost+found
drwxr-xr-x   3 root root  4096 Apr 10  2017 man
drwxr-xr-x   3 root root  4096 Apr 10  2017 media
drwxr-xr-x   2 root root  4096 Apr 10  2017 mnt
drwxr-xr-x   7 root root  4096 Apr 10  2017 opt
dr-xr-xr-x 176 root root     0 Dec 31  1969 proc
drwx------   4 root root  4096 Apr 10 04:14 root
drwxr-xr-x  22 root root   780 Apr 10 14:00 run
drwxr-xr-x   2 root root  4096 Apr 10 02:56 sbin
drwxr-xr-x   3 root root  4096 Apr 10 14:08 srv
dr-xr-xr-x  12 root root     0 Dec 31  1969 sys
drwxrwxrwt  13 root root  4096 Apr 10 14:08 tmp
drwxr-xr-x  11 root root  4096 Apr 10  2017 usr
drwxr-xr-x  11 root root  4096 Apr 10  2017 var
```

Exploring getting it to work with xinetd. Have had no luck getting it to work properly
yet though. For now I will just manually start and stop the service when I need it-
`sudo service tftpd-hpa start`
`sudo service tftpd-hpa stop`

Using the below commands we can see if the server is correctly open once the service
Using the below commands we can see if the server is correctly open once the service
has been started -

`netstat -an|grep 69`
`netstat -a |grep tftp`