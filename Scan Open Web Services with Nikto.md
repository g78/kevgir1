# Scanning open Web Service ports using Nikto

The Nmap scan in Step 1 identified a number of ports that were open for web services

#### Port 80
```
80/tcp    open  http        Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Kevgir VM
```

### Port 8080
```
8080/tcp  open  http        Apache Tomcat/Coyote JSP engine 1.1
| http-methods: 
|_  Potentially risky methods: PUT DELETE
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: Apache-Coyote/1.1
|_http-title: Apache Tomcat
```
### Port 80801
```
8081/tcp  open  http        Apache httpd 2.4.7 ((Ubuntu))
|_http-generator: Joomla! 1.5 - Open Source Content Management
| http-robots.txt: 14 disallowed entries 
| /administrator/ /cache/ /components/ /images/ 
| /includes/ /installation/ /language/ /libraries/ /media/ 
|_/modules/ /plugins/ /templates/ /tmp/ /xmlrpc/
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: Welcome to the Frontpage
```
### Port 9000
```
9000/tcp  open  http        Jetty winstone-2.9
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Jetty(winstone-2.9)
|_http-title: Dashboard [Jenkins]
```

To further enhance the results of the Nmap scan and enumerate further information we run a Nikto scan against each of the ports in turn

## Running the Scan

```
nikto -h 172.31.6.2
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          172.31.6.2
+ Target Hostname:    172.31.6.2
+ Target Port:        80
+ Start Time:         2017-07-27 16:10:51 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.7 (Ubuntu)
+ Server leaks inodes via ETags, header found with file /, fields: 0xec 0x52c8b6c4fbb0a 
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Apache/2.4.7 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 

+ Retrieved x-powered-by header: PHP/5.5.9-1ubuntu4.14
+ Uncommon header 'x-ob_mode' found, with contents: 0
+ OSVDB-3233: /icons/README: Apache default file found.
+ /phpmyadmin/: phpMyAdmin directory found
+ 8497 requests: 0 error(s) and 10 item(s) reported on remote host
+ End Time:           2017-07-27 16:37:11 (GMT-4) (1580 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

This scan gives us information on an OSVBD vulnerability and also the presence of a /phpmyadmin/ directory which can be used to attack the server

```
nikto -h 172.31.6.2:8080
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          172.31.6.2
+ Target Hostname:    172.31.6.2
+ Target Port:        8080
+ Start Time:         2017-07-27 16:42:19 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache-Coyote/1.1
+ Server leaks inodes via ETags, header found with file /, fields: 0xW/1895 0x1454530701000 
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ Allowed HTTP Methods: GET, HEAD, POST, PUT, DELETE, OPTIONS 
+ OSVDB-397: HTTP method ('Allow' Header): 'PUT' method could allow clients to save files on the web server.
+ OSVDB-5646: HTTP method ('Allow' Header): 'DELETE' may allow clients to remove files on the web server.
+ /: Appears to be a default Apache Tomcat install.
+ /examples/servlets/index.html: Apache Tomcat default JSP pages present.
+ OSVDB-3720: /examples/jsp/snp/snoop.jsp: Displays information about page retrievals, including other users.
+ Default account found for 'Tomcat Manager Application' at /manager/html (ID 'tomcat', PW 'tomcat'). Apache Tomcat.
+ /manager/html: Tomcat Manager / Host Manager interface found (pass protected)
+ /host-manager/html: Tomcat Manager / Host Manager interface found (pass protected)
nikto -h 172.31.6.2:9000
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          172.31.6.2
+ Target Hostname:    172.31.6.2
+ Target Port:        9000
+ Start Time:         2017-07-29 05:58:58 (GMT-4)
---------------------------------------------------------------------------
+ Server: Jetty(winstone-2.9)
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ Uncommon header 'x-jenkins-cli2-port' found, with contents: 59451
+ Uncommon header 'x-hudson-theme' found, with contents: default
+ Uncommon header 'x-jenkins-cli-port' found, with contents: 59451
+ Uncommon header 'x-jenkins-session' found, with contents: f5d64c90
+ Uncommon header 'x-ssh-endpoint' found, with contents: 172.31.6.2:41986
+ Uncommon header 'x-hudson-cli-port' found, with contents: 59451
+ Uncommon header 'x-jenkins' found, with contents: 1.647
+ Uncommon header 'x-instance-identity' found, with contents: MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAn8fNn04tBT9w9ORoD+NTk2wy9HcTQxM0W66be7ZrcMA51vPhc7KCSuOUkdY5aPwA2jwAerc/5l+Sd6REnYUwB81Uk54TlO0H+Q3qhcbCFm42VihVx3OsUeIUvGXum1JDioXml5YTPKCVLq/CGeIFfweyncQYuCIQhNUeWMOKX+o6sh4cCshFQZ/TdyKmUfeMvKS+Jl2nTDePHaMhvFv6jSNe2amafUjcU3QmyDRj0aOnwOME470UC91rclGyqcyRjUT4V7Tnc7WZ5i6jrYxZLfC6rArb4w9J464gtNL2VJLiW6/CKCUshV5Kmfa8j9H+chN4gd3i5eUmVsoELlAWYwIDAQAB
+ Uncommon header 'x-hudson' found, with contents: 1.395
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ OSVDB-5737: WebLogic may reveal its internal IP or hostname in the Location header. The value is "http://172.31.6.2:9000/".
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ DEBUG HTTP verb may show server debugging information. See http://msdn.microsoft.com/en-us/library/e8z01xdh%28VS.80%29.aspx for details.
+ Uncommon header 'x-you-are-in-group' found, with contents: 
+ Uncommon header 'x-required-permission' found, with contents: hudson.model.Hudson.Administer
+ Uncommon header 'x-you-are-authenticated-as' found, with contents: anonymous
+ Uncommon header 'x-permission-implied-by' found, with contents: hudson.model.Hudson.Administer
+ 7554 requests: 0 error(s) and 17 item(s) reported on remote host
+ End Time:           2017-07-29 06:29:19 (GMT-4) (1821 seconds)
---------------------------------------------------------------------------
+ /manager/status: Tomcat Server Status interface found (pass protected)
+ 7661 requests: 0 error(s) and 14 item(s) reported on remote host
+ End Time:           2017-07-27 17:06:35 (GMT-4) (1456 seconds)
---------------------------------------------------------------------------
```
This scan allows us to focus our energies on on tomcat exploits


```
nikto -h 172.31.6.2:8081
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          172.31.6.2
+ Target Hostname:    172.31.6.2
+ Target Port:        8081
+ Start Time:         2017-07-29 05:32:46 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.4.7 (Ubuntu)
+ Retrieved x-powered-by header: PHP/5.5.9-1ubuntu4.14
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Cookie 2837a59c63a65a4dec38297efe446470 created without the httponly flag
+ Server leaks inodes via ETags, header found with file /robots.txt, fields: 0x130 0x445ac694a2180 
+ Cookie 7c97a0247c3e642ace7069114ad93f42 created without the httponly flag
+ Entry '/administrator/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/cache/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/components/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/images/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/includes/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/language/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/libraries/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/media/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/modules/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/plugins/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/templates/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Entry '/tmp/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ Cookie 73317aa332813d7bac99f6815015cb66 created without the httponly flag
+ Entry '/xmlrpc/' in robots.txt returned a non-forbidden or redirect HTTP code (200)
+ "robots.txt" contains 14 entries which should be manually viewed.
+ IP address found in the 'location' header. The IP is "127.0.1.1".
+ OSVDB-630: IIS may reveal its internal or real IP in the Location header via a request to the /images directory. The value is "http://127.0.1.1:8081/images/".
+ OSVDB-39272: favicon.ico file identifies this server as: Joomla
+ Apache/2.4.7 appears to be outdated (current is at least Apache/2.4.12). Apache 2.0.65 (final release) and 2.2.29 are also current.
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ OSVDB-3092: /administrator/: This might be interesting...
+ OSVDB-3092: /includes/: This might be interesting...
+ OSVDB-3092: /logs/: This might be interesting...
+ Uncommon header 'x-ob_mode' found, with contents: 0
+ OSVDB-3092: /test.txt: This might be interesting...
+ OSVDB-3092: /tmp/: This might be interesting...
+ OSVDB-3233: /icons/README: Apache default file found.

+ /htaccess.txt: Default Joomla! htaccess.txt file found. This should be removed or renamed.
+ /administrator/index.php: Admin login page/section found.
+ /phpmyadmin/: phpMyAdmin directory found
+ 8514 requests: 0 error(s) and 36 item(s) reported on remote host
+ End Time:           2017-07-29 06:06:55 (GMT-4) (2049 seconds)
---------------------------------------------------------------------------

From here we can see that we have a Joomla administrative interface to exploit as well as numerous directories for us to visit e.g. `/logs/`


```
nikto -h 172.31.6.2:9000
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          172.31.6.2
+ Target Hostname:    172.31.6.2
+ Target Port:        9000
+ Start Time:         2017-07-29 05:58:58 (GMT-4)
---------------------------------------------------------------------------
+ Server: Jetty(winstone-2.9)
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ Uncommon header 'x-jenkins-cli2-port' found, with contents: 59451
+ Uncommon header 'x-hudson-theme' found, with contents: default
+ Uncommon header 'x-jenkins-cli-port' found, with contents: 59451
+ Uncommon header 'x-jenkins-session' found, with contents: f5d64c90
+ Uncommon header 'x-ssh-endpoint' found, with contents: 172.31.6.2:41986
+ Uncommon header 'x-hudson-cli-port' found, with contents: 59451
+ Uncommon header 'x-jenkins' found, with contents: 1.647
+ Uncommon header 'x-instance-identity' found, with contents: MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAn8fNn04tBT9w9ORoD+NTk2wy9HcTQxM0W66be7ZrcMA51vPhc7KCSuOUkdY5aPwA2jwAerc/5l+Sd6REnYUwB81Uk54TlO0H+Q3qhcbCFm42VihVx3OsUeIUvGXum1JDioXml5YTPKCVLq/CGeIFfweyncQYuCIQhNUeWMOKX+o6sh4cCshFQZ/TdyKmUfeMvKS+Jl2nTDePHaMhvFv6jSNe2amafUjcU3QmyDRj0aOnwOME470UC91rclGyqcyRjUT4V7Tnc7WZ5i6jrYxZLfC6rArb4w9J464gtNL2VJLiW6/CKCUshV5Kmfa8j9H+chN4gd3i5eUmVsoELlAWYwIDAQAB
+ Uncommon header 'x-hudson' found, with contents: 1.395
+ No CGI Directories found (use '-C all' to force check all possible dirs)
+ OSVDB-5737: WebLogic may reveal its internal IP or hostname in the Location header. The value is "http://172.31.6.2:9000/".
+ Web Server returns a valid response with junk HTTP methods, this may cause false positives.
+ DEBUG HTTP verb may show server debugging information. See http://msdn.microsoft.com/en-us/library/e8z01xdh%28VS.80%29.aspx for details.
+ Uncommon header 'x-you-are-in-group' found, with contents: 
+ Uncommon header 'x-required-permission' found, with contents: hudson.model.Hudson.Administer
+ Uncommon header 'x-you-are-authenticated-as' found, with contents: anonymous
+ Uncommon header 'x-permission-implied-by' found, with contents: hudson.model.Hudson.Administer
+ 7554 requests: 0 error(s) and 17 item(s) reported on remote host
+ End Time:           2017-07-29 06:29:19 (GMT-4) (1821 seconds)
---------------------------------------------------------------------------
```


