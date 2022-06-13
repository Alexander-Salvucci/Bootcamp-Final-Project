# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- ELK
  - **Operating System**: Linux
  - **Purpose**: Collecting logs, Kibana dashboard
  - **IP Address**:192.168.1.100
- Kali
  - **Operating System**: Linux
  - **Purpose**:Penetration Testing
  - **IP Address**:192.168.1.90
- Target 1
  - **Operating System**: Linux
  - **Purpose**:Target server. A vulnerable WordPress server.
  - **IP Address**:192.168.1.110
- Capstone
  - **Operating System**: Linux
  - **Purpose**:Testing alerts
  - **IP Address**:192.168.1.105


### Description of Targets


The target of this attack was: `Target 1` (IP: 192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors
_TODO: Replace `Alert 1` with the name of the alert._

Alert 1 is implemented as follows:
  - **Metric**: HTTP Response error codes
  - **Threshold**: 400 over 5 minutes
  - **Vulnerability Mitigated**: Brute force attack or a scan of some sort on the web server.
  - **Reliability**: High. Will almost never false positive as web-server never recieves this much traffic, unless under attack.

#### HTTP Request Size Monitor
Alert 2 is implemented as follows:
  - **Metric**: HTTP Request Bytes
  - **Threshold**: 4000 Bytes over 1 minute
  - **Vulnerability Mitigated**: Code injection, scanning, and/or DDOS
  - **Reliability**: Medium. If a DDOS attack is occuring, this will certainly trigger. It may also notice any of the more complicated code injection style attacks. But if traffic to the website goes up, this will also give us lots of false positives.

#### CPU Usage Monitor
Alert 3 is implemented as follows:
  - **Metric**: CPU Usage
  - **Threshold**: above 50% for 5 minutes
  - **Vulnerability Mitigated**: DDOS attack, warning when the device is compromised.
  - **Reliability**: Medium-High. Will alert us when the machine is working abnormally hard. Might give some false positives, especially if we make the web-server do something rather intensive.


### Suggestions for Going Further (Optional)
_TODO_: 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 2
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 3
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
