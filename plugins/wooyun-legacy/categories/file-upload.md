# FILE-UPLOAD Vulnerability Analysis

> Automatically extracted on 2026-01-23 18:57
> Sample count: 11


> Total case count: 11

## High-Frequency Parameters
```
  Connector: 1 occurrence
```


### Attack Pattern Distribution
```
  upload: 6 occurrences
  getshell: 3 occurrences
  weak password: 1 occurrence
  execution: 1 occurrence
  traversal: 1 occurrence
```


## Representative Case Titles

- Shanghai Metro has an arbitrary file upload vulnerability allowing shell access
  Vulnerability type: file upload leading to arbitrary code execution
- A certain organization has a security vulnerability: collaborative portal FCK file upload to getshell
  Vulnerability type: file upload leading to arbitrary code execution
- Misconfiguration on a computer manufacturer's site leads to unauthorized access and backend administration (shell possible)
  Vulnerability type: file upload leading to arbitrary code execution
- A certain organization's education cloud platform arbitrary file upload leads to GETSHELL
  Vulnerability type: file upload leading to arbitrary code execution
- Arbitrary file upload on a Duowan subsite
  Vulnerability type: file upload leading to arbitrary code execution
- Yibido upload vulnerability leads to website compromise
  Vulnerability type: file upload leading to arbitrary code execution
- Arbitrary command execution vulnerability on a Rongzicheng subsite
  Vulnerability type: file upload leading to arbitrary code execution
- Getshell in a certain organization's trade-association system / involves nearly 200 bank-related entities / affects intranet security
  Vulnerability type: file upload leading to arbitrary code execution
- Aopeng Training Network backend weak password allows getshell
  Vulnerability type: file upload leading to arbitrary code execution
- Traversal in a SouFun backend system allows getshell
  Vulnerability type: file upload leading to arbitrary code execution
- Upload vulnerability on the employment office's official website at a certain organization causes multiple school sites, including the main site server, to be controlled
  Vulnerability type: file upload leading to arbitrary code execution

## High-Frequency Payload Patterns
```
ort="java.util.*,java.io.*"%><%out.println("Hello Wo
```
