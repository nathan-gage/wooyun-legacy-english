# WEAK-PASSWORD Vulnerability Analysis

> Automatically extracted on 2026-01-23 18:57
> Sample count: 15


> Total case count: 15

## High-Frequency Parameters
```
  id: 2 occurrences
  dir: 1 occurrence
  systemID: 1 occurrence
```


### Attack Pattern Distribution
```
  weak password: 11 occurrences
  disclosure: 4 occurrences
  execution: 1 occurrence
  upload: 1 occurrence
```


## Representative Case Titles

- Using predecessors' experience to compromise 14 million floating-population records in a certain province
  Vulnerability type: backend weak password
- At least 8 sites in a 58.com business have weak passwords, leading to getshell again (can roam the intranet again)
  Vulnerability type: service weak password
- A certain organization's public platform has WebLogic and login weak passwords (leaks large amounts of internal information; shell possible)
  Vulnerability type: backend weak password
- Beidou precision agriculture integrated service weak password can schedule and monitor agricultural machinery
  Vulnerability type: backend weak password
- Weak password on a State Grid site (large amounts of resident payment data \ apparently can control users' power supply)
  Vulnerability type: backend weak password
- A certain organization has a security vulnerability in department and company product standard setting (involving ministry-level users)
  Vulnerability type: backend weak password
- A certain organization's unified authentication platform has a security vulnerability
  Vulnerability type: backend weak password
- One weak password on SouFun leaks 50,000 property-listing details
  Vulnerability type: backend weak password
- Weak password in Ocean's King integrated archive query system
  Vulnerability type: infrastructure weak password
- One weak password at a home-appliance manufacturer leaks sensitive information (arbitrary file deletion)
  Vulnerability type: backend weak password
- A certain organization's cluster data center has a telecom vendor Tecal E6000 MM blade-server WEB weak password leading to telnet command execution
  Vulnerability type: service weak password
- A certain organization's backend has a weak password #ten thousand student records leaked #serious leak of confidential materials#
  Vulnerability type: backend weak password
- One backend weak password on Parents Network
  Vulnerability type: service weak password
- A certain organization has a SQL vulnerability
  Vulnerability type: infrastructure weak password
- Weak password and arbitrary file upload in an urban rail transit engineering survey management information system
  Vulnerability type: backend weak password

## High-Frequency Payload Patterns
```
orm.jsp, WebLogic weak password 12345678 exists; after login, a WAR package can be deployed, and traces of a predecessor's webshell were found.
```
