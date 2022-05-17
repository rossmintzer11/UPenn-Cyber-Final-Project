# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
_TODO: Fill out the information below._

Nmap scan results for each machine reveal the below services and OS details:

```bash
$ nmap -sC -sV 192.168.1.110
  # TODO: Insert scan output
```

This scan identifies the services below as potential points of entry:
- Target 1
  - SSH on Port 22 verison 6.7p1
  - HTTP Apache Server on Port 80  version 2.4.10  
  - RPC on Port 111 
  - SMBD on Port 139 version 3.x -4.x
  - SMBD on Port 445 version 4.2.14

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
  -  flag1{b9bbcb33e11b80be759c4e844862482d} 
    - Used google inspect element to find the flag hidden in the code
      - _TODO: Identify the exploit used_
      - _TODO: Include the command run_
  - `flag2.txt`: flag2{fc3fd58dcdad9ab23faca6e9a36e581c}
    - **Exploit Used**
      - WPSCAN to Enumerate Use
      - WPSCAN -url 192.168.1.110 --enumerate u
      - found user Michael
      -screenshot
      - Used  basic Brute force to SSH into Michael's user
      - Weak Password used (michael)
      ''' bash
      ssh michael@192.168.1.110
      '''
