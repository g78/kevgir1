# Enumerate the machine using nmap
```
nmap -p 0-65535 -T5 -O -A 172.31.6.2

Starting Nmap 7.01 ( https://nmap.org ) at 2017-08-07 11:47 EDT
Warning: 172.31.6.2 giving up on port because retransmission cap hit (2).
Nmap scan report for 172.31.6.2
Host is up (0.17s latency).
Not shown: 65518 closed ports
PORT      STATE SERVICE     VERSION
25/tcp    open  ftp         vsftpd 3.0.2
|_smtp-commands: SMTP: EHLO 530 Please login with USER and PASS.
80/tcp    open  http        Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Kevgir VM
111/tcp   open  rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      44128/udp  mountd
|   100005  1,2,3      51052/tcp  mountd
|   100021  1,3,4      39076/tcp  nlockmgr
|   100021  1,3,4      46434/udp  nlockmgr
|   100024  1          40871/tcp  status
|   100024  1          58632/udp  status
|   100227  2,3         2049/tcp  nfs_acl
|_  100227  2,3         2049/udp  nfs_acl
139/tcp   open  netbios-ssn Samba smbd 3.X (workgroup: CANYOUPWNME)
445/tcp   open  netbios-ssn Samba smbd 3.X (workgroup: CANYOUPWNME)
1322/tcp  open  ssh         OpenSSH 6.6.1p1 Ubuntu 2ubuntu2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 17:32:b4:85:06:20:b6:90:5b:75:1c:6e:fe:0f:f8:e2 (DSA)
|   2048 53:49:03:32:86:0b:15:b8:a5:f1:2b:8e:75:1b:5a:06 (RSA)
|_  256 3b:03:cd:29:7b:5e:9f:3b:62:79:ed:dc:82:c7:48:8a (ECDSA)
2049/tcp  open  nfs         2-4 (RPC #100003)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      44128/udp  mountd
|   100005  1,2,3      51052/tcp  mountd
|   100021  1,3,4      39076/tcp  nlockmgr
|   100021  1,3,4      46434/udp  nlockmgr
|   100024  1          40871/tcp  status
|   100024  1          58632/udp  status
|   100227  2,3         2049/tcp  nfs_acl
|_  100227  2,3         2049/udp  nfs_acl
6379/tcp  open  redis       Redis key-value store
8080/tcp  open  http        Apache Tomcat/Coyote JSP engine 1.1
| http-methods: 
|_  Potentially risky methods: PUT DELETE
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: Apache-Coyote/1.1
|_http-title: Apache Tomcat
8081/tcp  open  http        Apache httpd 2.4.7 ((Ubuntu))
|_http-generator: Joomla! 1.5 - Open Source Content Management
| http-robots.txt: 14 disallowed entries 
| /administrator/ /cache/ /components/ /images/ 
| /includes/ /installation/ /language/ /libraries/ /media/ 
|_/modules/ /plugins/ /templates/ /tmp/ /xmlrpc/
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Welcome to the Frontpage
9000/tcp  open  http        Jetty winstone-2.9
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Jetty(winstone-2.9)
|_http-title: Dashboard [Jenkins]
39076/tcp open  nlockmgr    1-4 (RPC #100021)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      44128/udp  mountd
|   100005  1,2,3      51052/tcp  mountd
|   100021  1,3,4      39076/tcp  nlockmgr
|   100021  1,3,4      46434/udp  nlockmgr
|   100024  1          40871/tcp  status
|   100024  1          58632/udp  status
|   100227  2,3         2049/tcp  nfs_acl
|_  100227  2,3         2049/udp  nfs_acl
39445/tcp open  mountd      1-3 (RPC #100005)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      44128/udp  mountd
|   100005  1,2,3      51052/tcp  mountd
|   100021  1,3,4      39076/tcp  nlockmgr
|   100021  1,3,4      46434/udp  nlockmgr
|   100024  1          40871/tcp  status
|   100024  1          58632/udp  status
|   100227  2,3         2049/tcp  nfs_acl
|_  100227  2,3         2049/udp  nfs_acl
40871/tcp open  status      1 (RPC #100024)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      44128/udp  mountd
|   100005  1,2,3      51052/tcp  mountd
|   100021  1,3,4      39076/tcp  nlockmgr
|   100021  1,3,4      46434/udp  nlockmgr
|   100024  1          40871/tcp  status
|   100024  1          58632/udp  status
|   100227  2,3         2049/tcp  nfs_acl
|_  100227  2,3         2049/udp  nfs_acl
42088/tcp open  ssh         Apache Mina sshd 0.8.0 (protocol 2.0)
| ssh-hostkey: 
|_  2048 97:bb:2c:13:54:2f:88:0d:00:c6:80:24:30:d6:29:54 (RSA)
48050/tcp open  unknown
51052/tcp open  mountd      1-3 (RPC #100005)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      44128/udp  mountd
|   100005  1,2,3      51052/tcp  mountd
|   100021  1,3,4      39076/tcp  nlockmgr
|   100021  1,3,4      46434/udp  nlockmgr
|   100024  1          40871/tcp  status
|   100024  1          58632/udp  status
|   100227  2,3         2049/tcp  nfs_acl
|_  100227  2,3         2049/udp  nfs_acl
60107/tcp open  mountd      1-3 (RPC #100005)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2,3,4        111/tcp  rpcbind
|   100000  2,3,4        111/udp  rpcbind
|   100003  2,3,4       2049/tcp  nfs
|   100003  2,3,4       2049/udp  nfs
|   100005  1,2,3      44128/udp  mountd
|   100005  1,2,3      51052/tcp  mountd
|   100021  1,3,4      39076/tcp  nlockmgr
|   100021  1,3,4      46434/udp  nlockmgr
|   100024  1          40871/tcp  status
|   100024  1          58632/udp  status
|   100227  2,3         2049/tcp  nfs_acl
|_  100227  2,3         2049/udp  nfs_acl
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port48050-TCP:V=7.01%I=7%D=8/7%Time=59888C98%P=x86_64-pc-linux-gnu%r(DN
SF:SVersionBindReq,36,"Unrecognized\x20protocol:\x20\0\x06\x01\0\0\x01\0\0
SF:\0\0\0\0\x07version\x04bind\0\0\x10\0\x03\n")%r(DNSStatusRequest,24,"Un
SF:recognized\x20protocol:\x20\0\0\x10\0\0\0\0\0\0\0\0\0\n");
Aggressive OS guesses: Linux 2.6.32 (91%), Linux 3.11 - 4.1 (91%), Linux 3.2 - 3.8 (91%), Linux 3.8 (91%), IPFire 2.11 firewall (Linux 2.6.32) (91%), WatchGuard Fireware 11.8 (90%), Linux 3.1 - 3.2 (90%), Linux 2.6.18 - 2.6.22 (89%), Linux 2.6.35 (89%), IGEL UD3 thin client (Linux 2.6) (89%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: CANYOUPWNME, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Unix (Samba 4.1.6-Ubuntu)
|   Computer name: canyoupwnme
|   NetBIOS computer name: CANYOUPWNME
|   Domain name: 
|   FQDN: canyoupwnme
|_  System time: 2017-08-07T18:53:31+03:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_smbv2-enabled: Server supports SMBv2 protocol

TRACEROUTE (using port 587/tcp)
HOP RTT       ADDRESS
1   168.63 ms 172.27.232.1
2   168.78 ms 172.31.6.2

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 340.53 seconds
```

# Step 2. Refine the Results:
Using the results of this scan we can further enumerate the identified services, ports and access points
- Run Nikto scan on all open Web Ports
- Run SMB Scan



