Intended way to solve rorito CTF box

basic info
```
level:- easy
type:- linux
IP:- 192.168.33.16
```
Port scan:-

```
┌─[shark@shark]─[~/box]
└──╼ $nmap -sC -sV  192.168.33.16
Starting Nmap 7.80 ( https://nmap.org ) at 2020-10-21 13:23 IST
Nmap scan report for 192.168.33.16
Host is up (0.00047s latency).
Not shown: 996 filtered ports
PORT   STATE  SERVICE  VERSION
20/tcp closed ftp-data
21/tcp open   ftp      vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:192.168.33.1
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp open   ssh      OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 15:58:ce:44:24:b1:8e:39:1b:b4:3b:a0:61:a8:fa:c1 (RSA)
|   256 0b:99:80:ff:eb:70:ef:e4:a4:6d:59:f8:ec:80:e5:d1 (ECDSA)
|_  256 d4:bd:fa:e1:3a:b6:2b:b0:55:3b:7c:5b:07:17:24:b6 (ED25519)
80/tcp open   http     Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 40.62 seconds
```
from the port scan we get to know there is a  Apache httpd 2.4.29 on port 80 navigating to that...

![image](https://github.com/5h4rk-lab/solutions_of_5h4rk/blob/master/apache.png)

<br>
lets find out wether there is any directorys avilable on web site running gobuster scan gives you... 

![image](https://github.com/5h4rk-lab/solutions_of_5h4rk/blob/master/gobuster.png)

after moving to `/publications` directory you will find an PDF which looks like empty but not so didnt get? let me show


![image](https://github.com/5h4rk-lab/solutions_of_5h4rk/blob/master/hidden.png)

select the entair pdf and copy it to any text editor it says

```
Hey ! you reached here noice.Have you been trolled or you are going to be trolled depends on the situation huh.
There is an old   saying that "privacyismythmyfriend007#" ~By 0xnairSometimes some sayings can be helpful.
```

okay now lets goo onn and enumurate ftp

```
ftp> ls -al
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 ftp      ftp          4096 Oct 21 06:03 .
drwxr-xr-x    3 ftp      ftp          4096 Oct 21 06:03 ..
-rw-r--r--    1 ftp      ftp          5929 Oct 21 05:55 .0xnair.zip
226 Directory send OK.
ftp> get .0xnair.zip
local: .0xnair.zip remote: .0xnair.zip
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for .0xnair.zip (5929 bytes).
226 Transfer complete.
5929 bytes received in 0.01 secs (758.7523 kB/s)
ftp> pwd
257 "/pub/user/troll/public/access/.0xnair" is the current directory
ftp> 
```
going through every folder you will wind an hidden folder name .0xnair which has a file name 0xnair.zip <br>
lets download that and unzip it but this is a password protected file lets crack it using `fcrackzip` <br>
