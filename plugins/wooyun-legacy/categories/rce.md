# RCE Vulnerability Analysis

> Automatically extracted on 2026-01-23 18:57
> Sample count: 3


> Total case count: 3

### High-Frequency Parameters
```
  repo: 1 occurrence
  apkpackagename: 1 occurrence
  error: 1 occurrence
  packagename: 1 occurrence
  intent: 1 occurrence
```

### Representative Cases

#### wooyun-2015-0145365
**The Android version of a certain search engine's input method has a vulnerability allowing remote information retrieval and user-behavior control (can maliciously push content, and targets can be found within a 4G network, etc.)**
- Parameters: `repo, apkpackagename, error, packagename, intent`
- Payload: `oreign Address         State       PID/Program namet`

#### wooyun-2014-048949
**114 Website Navigation (app) command execution**
- Payload: `org/papers/548<script>function execute(cmdArgs) {ret`

#### wooyun-2011-01334
**Remote ActiveX overflow 0-day in an e-commerce IM tool on a certain e-commerce platform**
- Payload: `<script>var buffer = '';while (buffer.length < 1111) buff`

---


### Attack Pattern Distribution
```
  execution: 3 occurrences
```


## Representative Case Titles

- LoL Duowan Box APP remote command execution vulnerability
  Vulnerability type: remote code execution
- dolphin zero APP remote code execution vulnerability
  Vulnerability type: remote code execution
- Feiyuxing router arbitrary command execution allows ROOT control of the router
  Vulnerability type: remote code execution

## High-Frequency Payload Patterns
```
org/papers/548my android system is 4.1.2function execute(cmdA
```
