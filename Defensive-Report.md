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

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented.

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors

This alert is implemented as follows:
  - **Metric**: HTTP Response codes
  - **Threshold**: Any code over 400 (any error code) is among the top 5 response codes in the last 5 minutes
  - **Vulnerability Mitigated**: Brute force attack or a scan of some sort on the web server.
  - **Reliability**: High. If error codes are among the most common HTTP response codes, then something unusual is happening with the server.

#### HTTP Request Size Monitor
This alert is implemented as follows:
  - **Metric**: HTTP Request Bytes
  - **Threshold**: 6,000 Bytes over 1 minute (Originally 3,500, but that gave way to many false positives.)
  - **Vulnerability Mitigated**: Code injection, scanning, and/or DDOS
  - **Reliability**: Medium. If a DDOS attack is occuring, this will certainly trigger. It may also notice any of the more complicated code injection style attacks. But if traffic to the website goes up, this will also give us lots of false positives.

#### CPU Usage Monitor
This alert is implemented as follows:
  - **Metric**: CPU Usage
  - **Threshold**: above 50% for 5 minutes
  - **Vulnerability Mitigated**: DDOS attack, warning when the device is compromised.
  - **Reliability**: Medium-High. Will alert us when the machine is working abnormally hard. Might give some false positives, especially if we make the web-server do something rather intensive.

