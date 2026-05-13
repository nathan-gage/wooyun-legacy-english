# admin internal partSystemWeak Credentialsanddefault auth interface command specialitemscheck test method plan

## 1. itemsdirectory approx description

### 1.1 check testTarget

 for admin single characters internal part manage manageSystemadvancelinesWeak Credentialsanddefault auth interface command specialitemsSecureassess assess, cover coverthe followingSystemtype:

| Systemtype | type product | Risk Level |
|---------|---------|---------|
| OA companySystem | cause remote A6/A8/ micro E-Cology/wild reach OA/daysdynamic power/ | High |
| itemSystem | Coremail/Exchange/Zimbra/Winmail | High |
| VPN Gateway | deep information server SSL VPN/Sangfor VPN/as USG/ | Critical |
| Bastion Host | /JumpServer/ / | Critical |
| Databasemanage manage | phpMyAdmin/Navicat Web/DBeaver/DBMS self with manage manage interface | Critical |
| Networkset prepare | transaction change machine/route device/defense manage manage interface | High |
| inbetween item/operations | Tomcat Manager/WebLogic Console/Zabbix/Grafana | High |

### 1.2 check testScopeandAuthorization

- **mustObtain**: method certificate pageAuthorizationcertificate(cover)/IP/URL resource asset clear single/check testTime WindowConfirm
- **check test constraint **:onlyinAuthorizationScopeinternal advancelines, not advancelinesBrute Force(only testWeak Credentials/default auth interface command array combine), not forge complete businessinjudge
- **lock set policy strategy**:check test firstConfirmeachSystemAccount Lockoutpolicy strategy, control makeAttempttimesnumber, avoid trigger initiate lock set

---

## 2. default auth interface commandDictionarycome source

### 2.1 company openDictionaryresource source

| come source | Address/Path | Description |
|------|----------|------|
| **SecLists** | `github.com/danielmiessler/SecLists/tree/master/Passwords/Default-Credentials` | business boundary most all default auth credential according collect, include route device/ Header/Web Applicationetc. |
| **DefaultCreds-cheat-sheet** | `github.com/ihebski/DefaultCreds-cheat-sheet` | by commerce/productCategoryofdefault auth interface command rate check table, include Python check queryTool |
| **CISA Known Default Passwords** | CISA method initiate deploy | nationalNetworkSecureglobal maintain protectofalready notify default auth interface command list |
| **RouterPasswords** | `routerpasswords.com` | Networkset prepare default auth interface commandDatabase |
| **Kali self withDictionary** | `/usr/share/wordlists/` | include `rockyou.txt`/`common-passwords.txt` etc. |
| **fuzzdb** | `github.com/fuzzdb-project/fuzzdb/tree/master/wordlists-user-passwd` | testuseWeak CredentialsDictionary |
| **WooYun history history vulnerability library** | cloudImage/version exist | large quantity national assetSystemdefault auth interface command real actualCase |

### 2.2 national assetSystemspecialusedefault auth interface command integer manage

requires for admin commonuseproduct mobile tool integer manage, the followingasHighfrequency default auth interface command:

#### OA System

```
# cause remote OA (Seeyon)
system / system
audit-admin / seeyon123456
group-admin / 123456
seeyon / 123456
A8 / seeyon

# micro OA (E-Cology)
sysadmin / 1
admin / admin
SecurityAdmin / SecurityAdmin@123

# wild reach OA
admin / (Blank Password)
admin / admin00

# OA
admin / admin
```

#### VPN set prepare

```
# deep information server SSL VPN
admin / admin
Admin / Admin123

# as USG defense
admin / Admin@123
admin / Huawei@123

# set prepare
admin / admin
admin / ruijie
```

#### Bastion Host

```
# Bastion Host
admin / admin123
shterm / shterm

# JumpServer
admin / admin
admin / ChangeMe

# Bastion Host
admin / admin
```

#### Database

```
# MySQL
root / (Blank Password)
root / root
root / 123456
root / mysql

# SQL Server
sa / (Blank Password)
sa / sa
sa / 123456

# Oracle
sys / change_on_install
system / manager
scott / tiger

# PostgreSQL
postgres / postgres
postgres / 123456

# Redis
(No Authentication)
(Password) 123456 / redis / foobared
```

#### inbetween itemandoperationsTool

```
# Tomcat Manager
tomcat / tomcat
admin / admin
manager / manager

# WebLogic
weblogic / weblogic
weblogic / weblogic123

# Zabbix
Admin / zabbix

# Grafana
admin / admin
```

#### Networkset prepare wilduse

```
admin / admin
admin / 123456
admin / password
cisco / cisco
enable / (Empty)
```

### 2.3 self createDictionarypolicy strategy

remove default auth interface command external, need check testthe followingWeak Credentialsmode:

1. **Top Weak Credentials**:`123456`/`admin`/`password`/`12345678`/`abc123`/`000000`/`1qaz2wsx`/`qwerty`
2. **single characters related key**:single characters name + common seen after (such as `zwfwzx@123`/`govunit2024`)
3. **Username=Password**:`zhangsan/zhangsan`/`admin/admin`
4. **Username+simple single change change**:`zhangsan123`/`zhangsan@123`/`Zhangsan1!`
5. ** copy/ degree array combine**:`Unit@2025`/`Admin2025!`/`P@ssw0rd2025`
6. **key sequence list**:`1qaz2wsx`/`qwer1234`/`!QAZ2wsx`
7. **mobile numbercode**:common seen 11 charactersmobile number(such asif canObtainUsermobile numberlist)

---

## 3. check testToolmatrix matrix

### 3.1 audit coreTool

| Tool | Purpose | protocol protocol/scenario scene | Notes |
|------|------|----------|------|
| **Hydra** | Networkservice expose power check test | SSH, FTP, RDP, SMB, MySQL, MSSQL, POP3, IMAP, HTTP-Form, VNC etc. | support holdConcurrencycontrol make/code manage |
| **Medusa** | andlinesNetworkLogincheck test | SSH, FTP, HTTP, MySQL, MSSQL, SMB, VNC etc. | model block ize, line process set |
| **Ncrack** | HighrateNetworkAuthentication decode | SSH, RDP, FTP, HTTP, Telnet etc. | Nmap out product |
| **CrackMapExec (NetExec)** | Windows/AD domain environment environment | SMB, WinRM, MSSQL, LDAP, RDP | check test domainWeak Credentials select |
| **super levelWeak CredentialsCheckTool** | national asset image izeTool | SSH, RDP, MySQL, MSSQL, FTP, SMB etc. | intext boundary page, suitable combine national internal environment environment |
| **Fscan** | Internal Network combineScan | PortScan + Weak Credentialscheck test one body ize | Go compile write, singleFile, Internal Network device |
| **SNETCracker** | national assetWeak Credentialsaudit plan | SSH, RDP, MySQL, FTP, SMB, Redis, MongoDB etc. | Windows GUI, operation simple |

### 3.2 Web Applicationspecialuse

| Tool | Purpose |
|------|------|
| **Burp Suite (Intruder)** | HTTP table singleWeak Credentialscheck test, support hold Cookie/Token handle manage |
| **PKAV HTTP Fuzzer** | national asset HTTP Weak CredentialsTool, support holdCAPTCHAIdentifyInterface |
| **self set define Python Script** | for special set OA/VPN LoginInterfacecompile write(seenSection 4) |

### 3.3 Databasespecialuse

| Tool | Purpose |
|------|------|
| **DBPwAudit** | Databaseinterface command audit plan(MySQL, MSSQL, Oracle) |
| **odat** | Oracle Databaseattack attackTool, include default auth interface command check test model block |
| **redis-cli** | Redis Unauthorized AccessinvolvingWeak Credentialscheck test |

### 3.4 Tool

| Tool | Purpose |
|------|------|
| **Nmap** | PortDiscoverandserviceIdentify(first setStep) |
| **Masscan** | large scale modelPortfast rateScan |
| **EHole (hole)** | specified patternIdentify, fast rateIdentifyresource asset forshouldofproduct/ commerce |
| **TideFinger** | national asset Web specified patternIdentify |

---

## 4. self dynamic izeScript route

### 4.1 integer body architecture structure

```
+---------------------------------------------+
| Weak Credentialscheck test self dynamic ize framework architecture |
+-------------+-----------+-------------------+
| Phase 1 | Phase 2 | Phase 3 |
| resource assetDiscover | specified patternIdentify | Weak Credentialscheck test |
| Nmap/ | EHole/ | Hydra/self set define |
| Masscan | specified pattern library | Script/Fscan |
+-------------+-----------+-------------------+
| Phase 4: Resultremit totalandreport generate complete |
+---------------------------------------------+
```

### 4.2 Phase 1:resource assetDiscoverandPortScan

```python
#!/usr/bin/env python3
"""
Phase 1: based onAuthorization IP list advancelinesPortScan, Identifyopen release service
"""
import subprocess
import json
import csv

def scan_targets(ip_file, output_dir):
 """
 forAuthorization IP listExecutePortScan
 """
 # common seen manage manageServerinterface
 target_ports = [22, # SSH
 23, # Telnet
 80, # HTTP
 443, # HTTPS
 1433, # MSSQL
 1521, # Oracle
 3306, # MySQL
 3389, # RDP
 5432, # PostgreSQL
 5900, # VNC
 6379, # Redis
 8080, # HTTP-Alt / Tomcat
 8443, # HTTPS-Alt
 8888, # manage manage interface common seenPort
 9090, # WebLogic / manage manageConsole
 27017, # MongoDB]
 ports_str = ",".join(str(p) for p in target_ports)

 cmd = ["nmap", "-sV", "-sC",
 "-p", ports_str,
 "-iL", ip_file,
 "-oA", f"{output_dir}/scan_result",
 "--open",
 "-T3", # control makeScanrate degree, avoid impact response business]
 subprocess.run(cmd, check=True)

def parse_nmap_results(xml_file):
 """
 decode Nmap XML output out, provide take IP:Port:Service map map
 Return: [{"ip": "x.x.x.x", "port": 22, "service": "ssh", "product": "OpenSSH"},...]
 """
 import xml.etree.ElementTree as ET
 tree = ET.parse(xml_file)
 results = []
 for host in tree.findall(".//host"):
 ip = host.find(".//address[@addrtype='ipv4']").get("addr")
 for port in host.findall(".//port"):
 state = port.find("state").get("state")
 if state == "open":
 service = port.find("service")
 results.append({
 "ip": ip,
 "port": int(port.get("portid")),
 "protocol": port.get("protocol"),
 "service": service.get("name", "unknown") if service is not None else "unknown",
 "product": service.get("product", "") if service is not None else "",
 })
 return results
```

### 4.3 Phase 2:specified patternIdentifyandDictionarymatch config

```python
#!/usr/bin/env python3
"""
Phase 2: root according service specified pattern match config forshouldofdefault auth interface commandDictionary
"""

# service->Dictionarymap map scale rule
SERVICE_DICT_MAP = {
 "ssh": ["dict/ssh_default.txt", "dict/common_weak.txt"],
 "ftp": ["dict/ftp_default.txt", "dict/common_weak.txt"],
 "rdp": ["dict/rdp_default.txt", "dict/common_weak.txt"],
 "mysql": ["dict/mysql_default.txt"],
 "mssql": ["dict/mssql_default.txt"],
 "oracle": ["dict/oracle_default.txt"],
 "redis": ["dict/redis_default.txt"],
 "mongodb": ["dict/mongodb_default.txt"],
 "vnc": ["dict/vnc_default.txt"],
 "telnet": ["dict/telnet_default.txt", "dict/network_device_default.txt"],
}

# Web product specified pattern->Dictionarymap map
WEB_PRODUCT_DICT_MAP = {
 "seeyon": "dict/web/seeyon_default.txt",
 "ecology": "dict/web/weaver_default.txt",
 "tongda": "dict/web/tongda_default.txt",
 "coremail": "dict/web/coremail_default.txt",
 "tomcat": "dict/web/tomcat_default.txt",
 "weblogic": "dict/web/weblogic_default.txt",
 "zabbix": "dict/web/zabbix_default.txt",
 "grafana": "dict/web/grafana_default.txt",
 "jumpserver": "dict/web/jumpserver_default.txt",
 "sangfor": "dict/web/sangfor_default.txt",
 "phpmyadmin": "dict/web/phpmyadmin_default.txt",
}

def match_dict(service_info):
 """
 root accordingScanResultmatch config combine suitableofDictionaryFile
 """
 service = service_info["service"].lower()
 product = service_info.get("product", "").lower()

 dicts = []

 # service level match config
 if service in SERVICE_DICT_MAP:
 dicts.extend(SERVICE_DICT_MAP[service])

 # Web product level match config(HTTP/HTTPS servicerequiresadvance one step specified patternIdentify)
 if service in ("http", "https", "http-proxy"):
 for keyword, dict_file in WEB_PRODUCT_DICT_MAP.items():
 if keyword in product:
 dicts.append(dict_file)
 if not dicts:
 dicts.append("dict/web/generic_web_default.txt")

 return dicts
```

### 4.4 Phase 3:Weak Credentialscheck testExecute

```python
#!/usr/bin/env python3
"""
Phase 3: debug degreeWeak Credentialscheck test any service
"""
import subprocess
import time
import logging

logger = logging.getLogger("weak_pwd_checker")

# all global rate rate control make:avoid trigger initiateAccount Lockout
MAX_ATTEMPTS_PER_ACCOUNT = 3 # eachAccountmost largeAttempttimesnumber
REQUEST_INTERVAL = 2 # eachtimesAttemptbetween isolate()
MAX_THREADS = 4 # Concurrencyline process number

def check_network_service(target_ip, port, service, user_file, pass_file):
 """
 useuse Hydra check testNetworkserviceWeak Credentials
 """
 service_map = {
 "ssh": "ssh",
 "ftp": "ftp",
 "rdp": "rdp",
 "mysql": "mysql",
 "mssql": "mssql",
 "vnc": "vnc",
 "telnet": "telnet",
 "smb": "smb",
 "redis": "redis",
 }

 hydra_service = service_map.get(service)
 if not hydra_service:
 logger.warning(f"not support holdofservice type: {service}")
 return None

 cmd = ["hydra",
 "-L", user_file, # UsernameDictionary
 "-P", pass_file, # PasswordDictionary
 "-s", str(port), # Port
 "-t", str(MAX_THREADS), # line process number
 "-W", str(REQUEST_INTERVAL), # etc.pending between isolate
 "-f", # toNo. oneValidcredential according that is stop
 "-o", f"results/{target_ip}_{port}_{service}.txt",
 f"{target_ip}",
 hydra_service,]

 logger.info(f"check test {target_ip}:{port} ({service})")
 result = subprocess.run(cmd, capture_output=True, text=True, timeout=300)
 return parse_hydra_output(result.stdout)

def check_web_login(url, product_type, dict_file):
 """
 useuse requests check test Web Applicationdefault auth interface command
 support hold handle manageCAPTCHA/CSRF Token etc.
 """
 import requests

 results = []
 session = requests.Session()
 session.verify = False

 # add Dictionary:format mode username:password
 with open(dict_file) as f:
 creds = [line.strip().split(":", 1) for line in f if ":" in line]

 for username, password in creds:
 try:
 # 1. ObtainLoginpage(take CSRF Token / Cookie)
 login_page = session.get(url, timeout=10)

 # 2. root according product type structure forgeLoginRequest
 login_data = build_login_request(product_type, username, password, login_page)

 # 3. SendLoginRequest
 resp = session.post(login_data["url"],
 data=login_data["data"],
 headers=login_data.get("headers", {}),
 timeout=10,
 allow_redirects=False,)

 # 4. determine judgeLoginResult
 if is_login_success(product_type, resp):
 results.append({
 "url": url,
 "username": username,
 "password": password,
 "product": product_type,
 })
 logger.warning(f"[!] DiscoverWeak Credentials: {url} -> {username}:{password}")

 time.sleep(REQUEST_INTERVAL)

 except Exception as e:
 logger.error(f"check test abnormal common {url}: {e}")

 return results

def build_login_request(product_type, username, password, login_page):
 """
 root accordingDifferentproduct structure forgeLoginRequest
 this requires for each type product single independent suitable config
 """
 from bs4 import BeautifulSoup
 import re

 # wilduse CSRF Token provide take
 soup = BeautifulSoup(login_page.text, "html.parser")
 csrf_token = ""
 csrf_input = soup.find("input", {"name": re.compile(r"csrf|token|_token", re.I)})
 if csrf_input:
 csrf_token = csrf_input.get("value", "")

 # by product type part initiate
 if product_type == "seeyon":
 return {
 "url": login_page.url.rsplit("/", 1)[0] + "/seeyon/rest/authentication/ucpcLogin",
 "data": {"login_username": username, "login_password": password},
 }
 elif product_type == "ecology":
 return {
 "url": login_page.url.rsplit("/", 1)[0] + "/ecology/login/checkLogin.jsp",
 "data": {"loginid": username, "userpassword": password, "csrf": csrf_token},
 }
 elif product_type == "tongda":
 import hashlib
 pwd_md5 = hashlib.md5(password.encode()).hexdigest()
 return {
 "url": login_page.url.rsplit("/", 1)[0] + "/logincheck.php",
 "data": {"UNAME": username, "PASSWORD": pwd_md5},
 }
 #... other product suitable config...
 else:
 # wildusetable singleSubmit
 form = soup.find("form")
 action = form.get("action", "") if form else ""
 inputs = {}
 if form:
 for inp in form.find_all("input"):
 name = inp.get("name", "")
 if "user" in name.lower():
 inputs[name] = username
 elif "pass" in name.lower() or "pwd" in name.lower():
 inputs[name] = password
 elif inp.get("value"):
 inputs[name] = inp["value"]
 return {"url": action or login_page.url, "data": inputs}

def is_login_success(product_type, response):
 """
 determine judgeLoginwhetherSuccess(requiresroot according product suitable config)
 """
 # wildusedetermine judge logic logic
 fail_keywords = ["Failure", "error", "error", "fail", "invalid", "incorrect", "wrong"]

 # 302 skip transfer wild common table showLoginSuccess
 if response.status_code in (301, 302):
 location = response.headers.get("Location", "").lower()
 if "login" not in location and "error" not in location:
 return True

 # 200 Responseinnot includeFailurekeywords
 if response.status_code == 200:
 body = response.text.lower()
 if not any(kw in body for kw in fail_keywords):
 # needcheck whether there isSuccessidentifier identify
 success_keywords = ["Success", "welcome", "dashboard", "index", "main", "home"]
 if any(kw in body for kw in success_keywords):
 return True

 return False
```

### 4.5 Phase 4:Resultremit total

```python
#!/usr/bin/env python3
"""
Phase 4: remit totalAllcheck testResult, generate complete reportData
"""
import json
import csv
from datetime import datetime

def aggregate_results(result_dir):
 """
 remit totalAllcheck testResult
 """
 findings = []

 # TraversalAllResultFile
 #... decode Hydra output out/Web check test output out...

 # byRisk Levelrank sequence
 risk_order = {"Critical": 0, "High": 1, "in": 2, "Low": 3}
 findings.sort(key=lambda x: risk_order.get(x.get("risk", "in"), 2))

 return findings

def calculate_risk(finding):
 """
 risk assess level logic logic
 """
 service = finding.get("service", "")
 password = finding.get("password", "")

 # Bastion Host/VPN/Databasedefault auth interface command -> Critical
 if service in ("jumpserver", "shterm", "vpn", "mysql", "mssql", "oracle", "redis"):
 return "Critical"
 # Blank Password -> Critical
 if not password or password == "(Empty)":
 return "Critical"
 # OA/ itemSystemdefault auth interface command -> High
 if service in ("seeyon", "ecology", "tongda", "coremail", "exchange"):
 return "High"
 # wilduseWeak Credentials(such as 123456)-> High
 if password in ("123456", "admin", "password", "root"):
 return "High"
 return "in"

def export_csv(findings, output_file):
 """
 Export CSV format modeResult
 """
 fieldnames = ["sequence number", "IPAddress", "Port", "service/System", "Username", "Password", "Risk Level", "Discovertime between"]
 with open(output_file, "w", newline="", encoding="utf-8-sig") as f:
 writer = csv.DictWriter(f, fieldnames=fieldnames)
 writer.writeheader()
 for i, finding in enumerate(findings, 1):
 writer.writerow({
 "sequence number": i,
 "IPAddress": finding["ip"],
 "Port": finding["port"],
 "service/System": finding["service"],
 "Username": finding["username"],
 "Password": finding["password"],
 "Risk Level": finding["risk"],
 "Discovertime between": finding.get("timestamp", datetime.now().isoformat()),
 })
```

### 4.6 one key operatelinesScript

```bash
#!/bin/bash
# weak_pwd_audit.sh - Weak Credentialscheck test primary controlScript
# usemethod:./weak_pwd_audit.sh <AuthorizationIPlistFile>

set -euo pipefail

IP_FILE="${1:?usemethod: $0 <ip_list.txt>}"
WORK_DIR="./audit_$(date +%Y%m%d_%H%M%S)"
mkdir -p "$WORK_DIR"/{scan,results,report}

echo "[*] Phase 1: PortScan..."
nmap -sV -p 22,23,80,443,1433,1521,3306,3389,5432,5900,6379,8080,8443,9090,27017 \
 -iL "$IP_FILE" -oA "$WORK_DIR/scan/nmap_result" --open -T3

echo "[*] Phase 2: specified patternIdentify..."
# Canselect: Call EHole Identify Web product
#./EHole finger -l "$IP_FILE" -json "$WORK_DIR/scan/finger.json"

echo "[*] Phase 3: Weak Credentialscheck test..."
# NetworkserviceBatchcheck test (Fscan one body ize)./fscan -hf "$IP_FILE" -pwdf dict/common_weak.txt -o "$WORK_DIR/results/fscan_result.txt" -t 4 -time 2

# orpart serviceCall Hydra
while IFS=, read -r ip port service; do
 case "$service" in
 ssh|ftp|rdp|mysql|mssql|vnc|telnet|redis)
 hydra -L "dict/${service}_users.txt" -P "dict/${service}_default.txt" \
 -s "$port" -t 4 -W 2 -f \
 -o "$WORK_DIR/results/${ip}_${port}.txt" \
 "$ip" "$service" || true;;
 esac
done < "$WORK_DIR/scan/service_list.csv"

echo "[*] Phase 4: generate complete report..."
python3 generate_report.py "$WORK_DIR/results/" "$WORK_DIR/report/"

echo "[+] check test complete, report characters for: $WORK_DIR/report/"
```

---

## 5. check test flow processandinject meaning eventitems

### 5.1 identifier accurate operation business flow process

```
1. first period accurate prepare(1-2days)
 +-- Obtaincertificate pageAuthorization
 +-- collect collect resource asset clear single(IP/URL/Systemname name/negative person)
 +-- ConfirmeachSystemAccount Lockoutpolicy strategy
 +-- accurate prepare check test environment environment(Toolpart deploy/Dictionaryinteger manage)
 +-- and methodConfirmcheck testTime Window(create protocolNon-tool operation time between)

2. resource asset manage(0.5days)
 +-- PortScanConfirmopen release service
 +-- Web specified patternIdentifyConfirmproduct type
 +-- integer manage IP:Port:service:product map map table

3. Dictionarysuitable config(0.5days)
 +-- root according product type match config default auth interface commandDictionary
 +-- supplement topup single characters related keyWeak Credentials(single characters name etc.)
 +-- ConfirmEachTargetofAttempttimesnumber above limit

4. check testExecute(1-3days)
 +-- NetworkserviceWeak Credentialscheck test(SSH/RDP/DBetc.)
 +-- Web Applicationdefault auth interface command check test(OA/VPN/ itemetc.)
 +-- Networkset prepare manage manage interface check test
 +-- real timeRecordDiscoverResult

5. ResultValidate(0.5days)
 +-- person toolConfirmeach one conditionWeak CredentialsDiscover(rank remove error report)
 +-- assess assess each conditionDiscoverofreal actual risk
 +-- intercept image take cert

6. report compile write(1days)
 +-- by model template output out check test report
```

### 5.2 Secureinject meaning eventitems

1. **rate rate control make**:EachAccountmost manyAttempt 3 times, between isolate notLowfor 2, avoid trigger initiateAccount Lockout
2. **Time Window**:audit core businessSystemcreate protocolinNon-tool operation time between(such as 22:00-06:00)check test
3. **should connect system**:check test period between protect holdand method operations person wild information wild, out current abnormal common standalone that is stop
4. **LogRecord**:Allcheck test operationmusthasCompleteLog(time between/Target/operation/Result)
5. **DataSecure**:DiscoverofWeak Credentialsinformation add secretStorage, report only pass recursive toAuthorizationconnect collect person
6. **not do after **:DiscoverWeak Credentialsafter onlyValidateCanLogin, not advancelinesany after continue operation(not readData/not provide permission)

---

## 6. report model template

### 6.1 report result structure

```
 page
 - report name name:XXsingle characters internal partSystemWeak CredentialsspecialitemsSecurecheck test report
 - single characters
 - check test single characters
 - report day period
 - secret level identifier identify:machine secret

1. itemsdirectory approx description
 1.1 check test background sceneanddirectoryof
 1.2 check test depend according(etc.protect identifier accurate/AuthorizationcertificateID)
 1.3 check testScope(IP /Systemclear single)
 1.4 check test time between
 1.5 check test

2. check testMethod
 2.1 check test route
 2.2 useuseTool
 2.3 check test policy strategy(Dictionarycome source/rate rate control make)

3. check testResulttotal
 3.1 Statisticsapprox
 - check testSystemtotal number
 - existinWeak CredentialsSystemnumber
 - Weak CredentialsDiscovertotal number
 - byRisk Levelpart deploy image
 - bySystemtype part deploy image

 3.2 riskStatisticstable
 | Risk Level | number quantity | share ratio |
 |---------|------|------|
 | Critical | | |
 | High | | |
 | in | | |

4. DetailedDiscover(byRisk Levelrank list)

 [ID] VULN-2025-001
 +----------------------------------------------+
 | Risk Level:Critical |
 | Systemname name:XXBastion Host |
 | access askAddress:https://10.x.x.x:443 |
 | Systemtype:Bastion Host () |
 | Weak CredentialsAccount:admin / admin123 |
 | AccountPermission:SystemAdministrator |
 | Discovertime between:2025-xx-xx xx:xx |
 | risk description: |
 | Bastion Hostuseuseout default auth interface command, attack attack persondirectly usableLogin |
 | manage manage backend console, ObtainAllaffected manageServerofaccess askPermission, |
 | CausingInternal NetworkComprehensive flaw. |
 | Impact Scope: |
 | PassBastion HostCanaccess ask XX platformInternal NetworkServer |
 | Remediation Recommendation: |
 | 1. standalone that isModifyasstrongPassword(unicode-226512characters, include case+number character+special)|
 | 2. enableusedual because Authentication(MFA) |
 | 3. limit make manage manage interface access ask source IP |
 | Validateintercept image:[attach intercept image] |
 +----------------------------------------------+

 (serious repeator moreformat mode list outAllDiscover)

5. integer body risk assess assess
 5.1 total bodySecurestate assess price
 5.2 primary need risk point return
 5.3 toward for ratioAnalyze(which typeSystemask problem mostSevere)

6. integer change create protocol
 6.1 fix repeatitems(24hoursinternal)
 - All"Critical"riskitemsstandalone that isModifyPassword
 - for external expose exposureofWeak Credentialsservice standalone that is judge network handle manage
 6.2 short period change advanceitems(1cycle internal)
 - part deploy system onePasswordpolicy strategy(most small long degree/repeat degree/expired time between)
 - Allmanage manage backend console enableuse MFA
 - clear manage default authAccount/Test Account
 6.3 long period create setitems(1-3)
 - create set system one identity copyAuthenticationPlatform(SSO + LDAP)
 - part deploy special permissionAccountmanage manageSystem(PAM)
 - create standalone set periodWeak Credentials check machine make
 - make set interface command manage manage make degree and injectSecurereference audit

7. participate reference identifier accurate
 - GB/T 22239-2019 informationSecuretechnique NetworkSecureetc.level protect protect basic need require
 - GB/T 25070-2019 informationSecuretechnique NetworkSecureetc.level protect protectSecureset plan technique need require
 - GB/T 39786-2021 informationSecuretechnique informationSystemPasswordApplicationbasic need require

Appendix
 A. Authorizationcertificate(Scanitem)
 B. check test resource assetCompleteclear single
 C. Toolversion versionandConfigurationParameter
 D. Passwordstrong degree assess assess identifier accurate
```

### 6.2 Passwordstrong degree assess assess identifier accurate(Appendix D participate reference)

| etc.level | identifier accurate | Example |
|------|------|------|
| extreme weak | Blank Password / andUsername related same / Top10 Weak Credentials | `(Empty)`/`admin`/`123456` |
| weak | number characteror character, long degree < 8 | `abc123`/`test`/`888888` |
| in | long degree unicode-2265 8 but modePredictable | `Admin@123`/`Password1!` |
| strong | long degree unicode-2265 12, include case + number character + Special Characters, noDictionary | `kT9#mP2x$vR5` |

### 6.3 combine scale map map

| etc.protect condition payment | need require | forshouldcheck testitems |
|---------|------|-----------|
| 8.1.4.1 identity copy appraise level (a) | shouldforLoginofUseradvancelinesidentity copy identifier identifyandappraise level | check testBlank Password/ name access ask |
| 8.1.4.1 identity copy appraise level (b) | identity copy identifier identifyshouldtool has one ness | check test sharedAccount |
| 8.1.4.1 identity copy appraise level (c) | shouldprovide provideLoginFailurehandle manage function can | ValidateAccount Lockoutpolicy strategywhethergenerate valid |
| 8.1.4.1 identity copy appraise level (d) | interface command repeat degree need require | Weak Credentials/default auth interface command check test audit coreitems |
| 8.1.4.1 identity copy appraise level (e) | shouldusetwo typeoror moreappraise level technique | check test keySystemwhether has MFA |

---

## 7. Toolpart deploy fast rate participate reference

### 7.1 Hydra

```bash
# macOS
brew install hydra

# Ubuntu/Debian
apt-get install -y hydra

# CentOS/RHEL
yum install -y hydra
```

### 7.2 Fscan(infer Internal Networkuseuse)

```bash
# Download
wget https://github.com/shadow1ng/fscan/releases/latest/download/fscan_amd64
chmod +x fscan_amd64

# Weak Credentialscheck test./fscan_amd64 -h 10.0.0.0/24 -pwdf weak_pass.txt -o result.txt
```

### 7.3 CrackMapExec / NetExec(domain environment environment)

```bash
#
pip3 install crackmapexec

# SMB Weak Credentialscheck test
crackmapexec smb 10.0.0.0/24 -u users.txt -p passwords.txt --continue-on-success

# RDP Weak Credentialscheck test
crackmapexec rdp 10.0.0.0/24 -u admin -p passwords.txt
```

### 7.4 DictionaryFileresult structure create protocol

```
dict/
+-- common_weak.txt # wilduse Top 1000 Weak Credentials
+-- ssh_users.txt # SSH common seenUsername (root, admin, ubuntu...)
+-- ssh_default.txt # SSH default auth interface command
+-- rdp_default.txt # RDP default auth interface command
+-- mysql_default.txt # MySQL default auth interface command
+-- mssql_default.txt # MSSQL default auth interface command
+-- oracle_default.txt # Oracle default auth interface command
+-- redis_default.txt # Redis default auth interface command
+-- network_device_default.txt # Networkset prepare default auth interface command
+-- web/
| +-- seeyon_default.txt # cause remote OA
| +-- weaver_default.txt # micro OA
| +-- tongda_default.txt # wild reach OA
| +-- coremail_default.txt # Coremail item
| +-- sangfor_default.txt # deep information server VPN
| +-- tomcat_default.txt # Tomcat
| +-- weblogic_default.txt # WebLogic
| +-- zabbix_default.txt # Zabbix
| +-- grafana_default.txt # Grafana
| +-- jumpserver_default.txt # JumpServer
+-- custom/
 +-- unit_related.txt # single characters related key interface command(need current scenario generate complete)
 +-- username_as_pwd.txt # Username=Passwordarray combine
```

---

## 8. Checklist(check testExecuteclear single)

| sequence number | Check Item | complete |
|------|--------|------|
| 1 | Obtaincertificate pageAuthorizationandConfirm IP Scope | [] |
| 2 | ConfirmeachSystemAccount Lockoutpolicy strategy | [] |
| 3 | Confirmcheck testTime Window | [] |
| 4 | part deploy check testToolandValidateCanuse | [] |
| 5 | integer manageTargetproduct forshouldofdefault auth interface commandDictionary | [] |
| 6 | generate complete single characters related keyWeak CredentialsDictionary | [] |
| 7 | PortScanandserviceIdentify | [] |
| 8 | Web Applicationspecified patternIdentify | [] |
| 9 | NetworkserviceWeak Credentialscheck test(SSH/RDP/DB/Redis etc.) | [] |
| 10 | Web manage manage backend console default auth interface command check test | [] |
| 11 | VPN GatewayWeak Credentialscheck test | [] |
| 12 | Bastion HostWeak Credentialscheck test | [] |
| 13 | Networkset prepare manage manage interfaceWeak Credentialscheck test | [] |
| 14 | Resultperson toolValidateandintercept image take cert | [] |
| 15 | compile write check test report | [] |
| 16 | report assess auditandtransaction pay | [] |
| 17 | Deleteversion check testDataandcredential according | [] |
