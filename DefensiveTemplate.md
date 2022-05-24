# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology
_TODO: Fill out the information below._

The following machines were identified on the network:
- Capstone
  - **Operating System**: Linux
  - **Purpose**: Alert testing
  - **IP Address**: 192.168.1.105
- Kali Machine
  - **Operating System**: Kali linux (Debian)
  - **Purpose**: Atacking machine with Pen Test toolset built in
  - **IP Address**: 192.168.1.90
- Target 1
  - **Operating System**: Linux
  - **Purpose**: Vulnerable machine to be exploited
  - **IP Address**: 192.168.1.110
- Target 2
  - **Operating System**: Linux
  - **Purpose**: Vulnerable machine to be exploited
  - **IP Address**: 192.168.1.105
- Elk VM 
  - **Operating System**: Linux with ELK stack installed
  - **Purpose**: SIEM to help SOC team identify malicous activity 
  - **IP Address**: 192.168.1.100

### Description of Targets

The target of this attack was: `Target 1` @ 192.168.1.110

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors

Alert 1 is implemented as follows:
  - **Metric**: HTTP 400 Responses
  - **Threshold**: 1000 errors last 5 mins
  - **Vulnerability Mitigated**: Bruteforcing Logins and Directories
  - **Reliability**: High. Generally normal users aren'tcreating 400 errors on webpages a 1000 times a minute. A broken Crawler could potentially do this   in the wild. 

#### CPU Usage Monitor
Alert 2 is implemented as follows:
  - **Metric**: CPU usage percentage
  - **Threshold**: 50% of CPU last 5 minutes
  - **Vulnerability Mitigated**: Hacker running reverse shells, scripts, and malware on the machine. 
  - **Reliability**: Medium. Can generate alerts from normal activity but is still good to have these alerts since they will likely triggered along with normal syetm processes that are resource intensive. Most likely can be 

#### HTTP Request Size Monitor
Alert 3 is implemented as follows:
  - **Metric**: Http request size in Bytes
  - **Threshold**: sum of request greater than 3500 last 1 minutes
  - **Vulnerability Mitigated**: Identify Cross Site Scripting acitvity, DDOS attacks, and Buffer Overflow. 
  - **Reliability**: Low Reliability. Normal traffic such as downnloading a normal file can trigger this alert. Still beneficial to have since it can help identify malicouse traffic when there are other indicators oif compromise occuring simultaneously. 

_TODO Note: Explain at least 3 alerts. Add more if time allows._

### Going Further 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:

Target 1:
- Weak Passwords and Brute Forcing 
  - **Patch**: Set Minimum password requirements, set password reset intervals, and timeout between attempts or lockout after certain number of attempts.
  - **Why It Works**: Makes it longer and harder for password cracking and brute forcing software to guess passwords. 
- Access control problems for files containing sensitive information 
  - **Patch**: Change file permisions so www user doesn't have any permission to view documents with sensitive info 
  - **Why It Works**: Prevents web pages viewers to have open source information on how to hack the company 
- Priveledge Escalation: www user can run python as root without password
  - **Patch**: 2 options: first option take away the ability to run python as root user. Second option if python run as root isn't optional then require a password to use sudo. 
  - **Why It Works**: Mitigates the ability to run python as root fromm www user. Anyone trying to brute force the password of www user will be reported into the system logs. 

Target 2:
- Outdated PHPmailer Version exploitable by backdoor exploit 
  - **Patch**: Update PHPmailer version and monitor alerts for malicouse activity 
  - **Why It Works**: Updates address known CVEs and  nulifys the exploit
- Excessive open source information on version and exploits on wb pages
  - **Patch**: move file off web server and update file permissions
  - **Why It Works**: makes it harder for a hacker to enumerate the machine
-  User Defined Dynamic Library Priveledge Escalation using exploit E-DB:1518 https://www.exploit-db.com/exploits/1518
  - **Patch**:  Mysql is outdated and needs to be updated to the latest version
  - **Why It Works**: The update patches MySQL to prevent the exploit from working
