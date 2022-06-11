# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
_TODO: Fill out the information below._

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
_TODO: Fill out the details below. Include screenshots where possible._

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: _TODO: Insert `flag1.txt` hash value_
    - **Exploit Used**
      - wpscan was able to identify two users on the Word Press website hosted by the webserver.
        - wpscan –-url http://192.168.1.110/wordpress -eu
        - ![Wordpress Users](/images/wpscan-users.PNG)
      - Then, we simply
  - `flag2.txt`: flag2{fc3fd58dcdad9ab23faca6e9a36e851c
    - **Exploit Used**
      - _TODO: Identify the exploit used_
      - _TODO: Include the command run_
