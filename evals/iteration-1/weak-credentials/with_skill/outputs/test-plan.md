# admin internal part manage manageSystemWeak Credentialsanddefault auth interface command specialitemscheck test method plan

> Based on 22,132 real WooYun vulnerability cases | Authentication Domain 8,846 cases | ConfigurationDomain 1,796 cases

---

## 1. itemsdirectory background sceneandcheck testScope

### 1.1 background scene

admin internal part manage manageSystem(OA/ item/VPN/Bastion Host/Databasemanage manageetc.)byDifferent commerceinDifferent code part deploy, existinthe followingSystemness risk:

- commerce transaction pay time useuseDefault Credentials, operations person notModify
- history history retainSystemmissing Passwordpolicy strategy strong makeExecute
- manySystemindependent standaloneAuthentication, missing system one identity copy manage manage
- operations person as exploit set setWeak Credentials

### 1.2 WooYun Datasupport

| specified identifier | Data |
|------|------|
| Weak Credentials/default auth interface commandCasetotal number | **7,513 cases**(share WooYun AllCaseof **34%**) |
| Weak CredentialsCaseinhigh-risk percentage | **58.2%** |
| Misconfiguration(includeDefault Credentials)Case | **1,796 cases**, high-risk percentage **72.6%** |
| Authentication DomaintotalCase | **8,846 cases**(shareAllDiscoverof 40%) |

**audit core result comment:** WooYun Datacollectinsuper through three part of oneofvulnerability return because for weakPasswordordefault authPassword.this not is boundary ask problem, while is most ofSecurerisk.

### 1.3 check testScope

| SystemCategory | typeTarget | Risk Level |
|---------|---------|---------|
| OA System | cause remote OA/ micro OA/wild reach OA/ten-thousand account OA/ OA | High |
| itemSystem | Coremail/Exchange/Zimbra/Postfix+Roundcube | High |
| VPN Gateway | deep information server VPN/Array VPN/Pulse Secure/OpenVPN | Severe |
| Bastion Host | Bastion Host/JumpServer/linescloud manage | Severe |
| Databasemanage manage | phpMyAdmin/Navicat Web/DBeaver/Databasevertical continuous | Severe |
| operations monitor control | Zabbix/Grafana/Nagios/Prometheus | High |
| inbetween item manage manage | Tomcat Manager/WebLogic Console/JBoss | High |
| Networkset prepare | route device/transaction change machine/defense Web manage manage boundary page | High |

---

## 2. default auth interface commandDictionarycome sourceandstructure create

### 2.1 WooYun HighfrequencyDefault CredentialsDatabase

the followingDataDirectcome self WooYun 1,796 MisconfigurationCaseofStatisticsAnalyze:

| service/System | Default Credentials | WooYun out current frequency rate |
|-----------|---------|--------------|
| Tomcat Manager | tomcat/tomcat, admin/admin | Critical |
| JBoss Console | admin/admin, jboss/jboss | Critical |
| WebLogic | weblogic/weblogic1 | High |
| Jenkins | (No Authentication by Default) | Critical |
| Zabbix | Admin/zabbix | High |
| phpMyAdmin | root/(Blank Password) | Critical |
| MongoDB | (No Authentication by Default) | High |
| Redis | (No Authentication by Default) | Critical |
| Elasticsearch | (No Authentication by Default) | High |
| Docker Remote API | (No Authentication by Default) | High |
| Grafana | admin/admin | High |
| RabbitMQ | guest/guest | High |
| ActiveMQ | admin/admin | High |
| Nacos | nacos/nacos | High |
| Spring Boot Actuator | (No Authentication by Default) | Critical |
| Hadoop YARN | (No Authentication by Default) | High |

### 2.2 admin / business scenario scene specialuseDictionarystructure create policy strategy

root according WooYun Authentication DomainMethodcomment, Dictionarystructure create need cover cover fourPhase:

#### Phase 1: commerceDefault Credentials

```
# OA System
system/system, admin/admin, audit/audit
cause remote: seeyon/seeyon1, A8/seeyon123456, yyoa/seeyon
 micro: sysadmin/1, admin/weaver@2001
wild reach: admin/(Blank Password), admin/td3200

# itemSystem
Coremail: admin/coremail, admin/admin
Exchange: administrator/P@ssw0rd
Zimbra: admin/zimbra

# VPN
deep information server: admin/admin, dlanrecover/(Blank Password)
Array: admin/admin, array/admin

# Bastion Host: admin/admin, shterm/shterm
JumpServer: admin/admin, admin/ChangeMe

# Databasemanage manageTool
phpMyAdmin: root/(Blank Password), root/root, root/123456

# Networkset prepare
H3C: admin/admin, admin/h3capadmin
as: admin/Admin@123, admin/admin: admin/admin, admin/ruijie: cisco/cisco, admin/admin
```

#### Phase 2:social tool process Password(admin scenario scene special ize)

```
# array related key
[single characters simple name]@123, [single characters simple name]123, [single characters simple name]2024, [single characters simple name]2025
[]@123, []2024
gov123, gov@123, gov123456

# operations
P@ssw0rd, p@ssword, Passw0rd!, Admin@123, Admin123!
qwer1234, 1qaz2wsx, 1qaz@WSX,!QAZ2wsx
root123, root@123, test123, test@123

# mobile numbermode(innationalSystemextremeascommon seen)
1[3-9]xxxxxxxxx(11charactersmobile numberDirectoperationasPassword)
```

#### Phase 3:innational Top 100 Weak Credentials

```
123456, a123456, 123456789, password, 12345678
111111, 123123, abc123, 1234567, 000000
a123456789, 1234567890, woaini1314, qq123456, abc123456
iloveyou, 123321, qwerty, 147258369, 123456a
a12345678, 987654321, zxcvbnm, asd123456, aa123456
q123456, 1q2w3e4r, 123456abc, abcd1234, 110110
woaini, 11111111, 5201314, aini1314, wang1234...
```

#### Phase 4:linesbusiness special set default authPassword

```
# admin servicelinesbusiness
zwfw@123(admin service service), egov123, digital@gov
oa123456, oa@123, mail@123

# linesbusiness(such asinvolving System)
his@123, pacs@123, lis@123

# lesson linesbusiness(such asinvolving lesson globalSystem)
edu@123, school@123
```

### 2.3 Dictionarycome source remit total

| come source | Description | Obtainmethod mode |
|------|------|---------|
| WooYun vulnerability libraryStatistics | 7,513 Weak CredentialsCaseprovide ofHighfrequencyPassword | version method plan already internal set |
| SecLists (Daniel Miessler) | all most allofSecuretestDictionarycollect combine | `github.com/danielmiessler/SecLists/Passwords/` |
| Weak Credentialsreal validate (weakpass.com) | many national Weak Credentialslibrary, includeintext special ize | weakpass.com |
| DefaultCreds-cheat-sheet | commerceDefault Credentialsrate check table | `github.com/ihebski/DefaultCreds-cheat-sheet` |
| CISA Known Default Credentials | national CISA maintain protectofalready notifyDefault Credentialslist | cisa.gov |
| commerce methodDocument | EachTargetSystemof mobile /operations mobile | one by one check |
| Changeme | Default Credentialsself dynamic check testToolinternal set library | `github.com/ztgrace/changeme` |
| national internalSecuresocial | first notify/supplementdays/CNVD history history vulnerabilityinofdefault auth interface command | mobile dynamic integer manage |

---

## 3. check testToolmatrix matrix

### 3.1 audit coreTool

| Tool | Purpose | suitableusescenario scene | Notes |
|------|------|---------|------|
| **Hydra** | many protocol protocolinline interface commandBrute Force | SSH/FTP/RDP/HTTP-Form/SMTP/POP3/IMAP/MySQL/MSSQL/VNC | support hold 50+ protocol protocol, admin scenario scene select |
| **Medusa** | andlinesinline interface commandBrute Force | and Hydra type, set ness update good | model block ize set plan, suitable combine long time between operatelines |
| **Ncrack** | HighrateNetworkAuthentication decode | SSH/RDP/FTP/Telnet/HTTP(S) | Nmap out product, and Nmap connect dynamic good |
| **Burp Suite** | Web table single interface commandBrute Force | OA/ item Webmail/manage manage backend console | Intruder model block, handle manage CSRF Token/CAPTCHAscenario scene |
| **super levelWeak Credentialscheck testTool** | Windows image izeWeak Credentialscheck test | combine scenario scene, operation simple single | national assetTool, support hold many protocol protocol, boundary page good |
| **fscan** | Internal Network combineScan+Weak Credentialscheck test | Internal Networkfast rateScan | national assetTool, one keyScancommon seen serviceWeak Credentials |
| **Nmap NSE Scripts** | serviceDiscover+default auth interface command check test | largeScoperesource assetIdentify | `--script=default-credentials,brute` |

### 3.2 specialitemsTool

| Tool | specialitemsPurpose |
|------|---------|
| **SNETCracker** | super levelWeak CredentialsCheckTool, support hold SSH/RDP/MySQL/MSSQL/FTP etc. |
| **DefaultCreds-cheat-sheet + changeme** | self dynamic match config service specified pattern andAttemptDefault Credentials |
| **CrackMapExec (NetExec)** | Windows domain environment environment SMB/WinRM/LDAP/MSSQL Weak Credentials |
| **Patator** | model block izeBrute Forceframework architecture, support hold self set define protocol protocolandrepeat Authenticationflow process |
| **John the Ripper / Hashcat** | separate linePasswordhash hash decode(ObtaintoDatabase/ConfigurationFileafter) |
| **RouterSploit** | route device/IoT set prepare default auth interface command check test |
| **ssh-audit** | SSH serviceConfigurationaudit plan(include weakPasswordpolicy strategyCheck) |

### 3.3 Tool

| Tool | Purpose |
|------|------|
| **Nmap** | resource assetDiscover/PortScan/service specified patternIdentify |
| **Masscan** | large scale modelPortfast rateScan |
| **EHole (hole)** | resource asset specified patternIdentify, fast rate set characters OA/VPN/Bastion Host |
| **Goby** | resource asset test +vulnerabilityScan+Weak Credentialscheck test one body ize |

---

## 4. check test flow process

### 4.1 fourPhasecheck test flow process

```
Phase 1:resource asset test andserviceIdentify
 |
 +-- Nmap/Masscan allPortScan -> IdentifyAllopen release service
 +-- EHole/Goby specified patternIdentify -> set characters OA/VPN/Bastion Host/Databasemanage manageetc.System
 +-- mobile dynamicConfirmmanage manage boundary page URL andLogininject interface
 +-- output out:"resource asset clear singleandservice list"
 |
Phase 2:Default Credentialscheck test(zero risk, priority firstExecute)
 |
 +-- by WooYun HighfrequencyDefault Credentialslist one by oneAttempt
 +-- CheckNo Authenticationexpose exposureofmanage manage boundary page(Jenkins/Redis/MongoDB/ES/Spring Actuator etc.)
 +-- CheckBlank Password/ name access ask
 +-- output out:"Default CredentialsDiscoverclear single"
 |
Phase 3:Weak CredentialsBrute Force(needAuthorization, control make frequency rate)
 |
 +-- structure create for nessDictionary(array name/Domain Name/operations)
 +-- Web System:Burp Suite Intruder(handle manageCAPTCHA/CSRF)
 +-- Networkservice:Hydra/Medusa(SSH/RDP/FTP/Database)
 +-- domain environment environment:CrackMapExec(SMB/LDAP)
 +-- severe format control make:line process number unicode-2264 5, Requestbetween isolate unicode-2265 1s, avoid lock setAccount
 +-- output out:"Weak CredentialsDiscoverclear single"
 |
Phase 4:Passwordpolicy strategy audit plan
 |
 +-- CheckeachSystemPasswordrepeat degree policy strategyConfiguration
 +-- CheckAccountlock set policy strategy
 +-- CheckPasswordValidity Periodpolicy strategy
 +-- Checkdefault authPasswordstrong makeModifymachine make
 +-- output out:"Passwordpolicy strategy audit plan report"
```

### 4.2 WooYun Case References:CAPTCHA/defenseBrute ForceBypass

inPhase 3 in, toCAPTCHAorAccountlock set machine make, participate reference WooYun 384 CAPTCHA BypassCase:

| Bypasstechnique | Test Method | Successrate |
|---------|---------|--------|
| move removeCAPTCHAParameter | fromRequestinDelete captcha/verifycode Field | High |
| CAPTCHAserioususe | SameSessioninmanytimesSubmitSameCAPTCHAvalue | Critical |
| IP rotate changeBypasslock set | Modify X-Forwarded-For / X-Real-IP Header | Medium |
| ClientCAPTCHAValidate | CAPTCHAonlyin JavaScript inValidate, BackendnotValidate | High |
| SMS Verification Codeno expired | oldCAPTCHAlong time betweenValid, CanBrute Force | Medium |

---

## 5. self dynamic izeScript route

### 5.1 total body architecture structure

```
weak-cred-scanner/
+-- config/
| +-- targets.yaml # Targetresource asset clear single
| +-- credentials/
| | +-- default_creds.yaml # by serviceCategoryofDefault Credentials
| | +-- weak_passwords.txt # wilduseWeak CredentialsDictionary
| | +-- gov_passwords.txt # admin scenario scene special izeDictionary
| | +-- custom_passwords.txt # itemsdirectory set makeDictionary
| +-- settings.yaml # all globalConfiguration(line process/between isolate/super time)
+-- scanners/
| +-- web_form_scanner.py # Web table singleLogincheck test
| +-- service_scanner.py # NetworkserviceWeak Credentialscheck test(Call Hydra)
| +-- db_scanner.py # Databasedefault auth interface command check test
| +-- noauth_scanner.py # No Authenticationservice check test
| +-- device_scanner.py # Networkset prepare default auth interface command check test
+-- utils/
| +-- fingerprint.py # service specified patternIdentify
| +-- dict_generator.py # dynamic stateDictionarygenerate complete device
| +-- rate_limiter.py # Requestfrequency rate control make
| +-- reporter.py # report generate complete device
+-- reports/
| +-- (self dynamic generate complete)
+-- main.py # primary inject interface
```

### 5.2 audit core model block Code

#### primary debug degree device

```python
# main.py - primary debug degree logic logic
def main():
 # 1. add Targetresource asset
 targets = load_targets("config/targets.yaml")

 # 2. service specified patternIdentify(Call Nmap)
 for target in targets:
 target.services = fingerprint(target.ip, target.ports)

 # 3. by service type part check test device
 findings = []
 for target in targets:
 for service in target.services:
 # Phase 2:Default Credentials(priority first)
 creds = get_default_creds(service.name, service.version)
 result = try_default_creds(target, service, creds)
 if result.success:
 findings.append(result)
 continue # alreadyDiscoverdefault auth interface command, no need to continueBrute Force

 # No Authenticationcheck test
 if service.name in NO_AUTH_SERVICES:
 result = check_no_auth(target, service)
 if result.success:
 findings.append(result)
 continue

 # Phase 3:Weak Credentialscheck test(affected control)
 passwords = generate_dict(target, service)
 result = brute_force(target, service, passwords,
 threads=3, delay=1.0, max_attempts=50)
 findings.extend(result)

 # 4. generate complete report
 generate_report(findings, template="gov_audit")
```

#### dynamic stateDictionarygenerate complete device

```python
# utils/dict_generator.py
def generate_dict(target, service):
 """root accordingTargetinformation dynamic state generate complete for nessDictionary"""
 passwords = set()

 # base foundationWeak Credentials
 passwords.update(load_file("config/credentials/weak_passwords.txt"))

 # commerceDefault Credentials
 vendor_creds = VENDOR_DEFAULT_CREDS.get(service.fingerprint, [])
 passwords.update(vendor_creds)

 # social tool process Password(based onTargetarray information)
 org_name = target.organization # such as "some some create global"
 pinyin = to_pinyin(org_name) # zjj, zhujj, zhujjj
 for suffix in ["123", "@123", "2024", "2025", "!@#", "888"]:
 passwords.add(f"{pinyin}{suffix}")

 # Domain Name generate
 if target.domain:
 base = target.domain.split(".")[0]
 for suffix in ["123", "@123", "Admin", "admin"]:
 passwords.add(f"{base}{suffix}")

 # mobile numbermode(onlyusefor already notifyUsername scenario scene)
 # not generate complete, butinDictionaryininclude include common seenmobile numberprefix mode

 return list(passwords)
```

#### Web table single check test device

```python
# scanners/web_form_scanner.py
def scan_web_form(target_url, usernames, passwords):
 """
 handle manage Web Logintable singleofWeak Credentialscheck test
 - self dynamicIdentifyLogintable singleField
 - handle manage CSRF Token
 - handle manageCAPTCHA(AttemptBypass)
 - based onResponseerror abnormal determine judgeSuccess/Failure
 """
 session = requests.Session()

 # 1. ObtainLoginpage, provide take table single result structure
 form = parse_login_form(session.get(target_url))

 # 2. check testCAPTCHA
 if form.has_captcha:
 # AttemptBypass:move removeCAPTCHAParameter
 bypass_result = try_without_captcha(session, form, "admin", "admin")
 if bypass_result.captcha_required:
 # AttemptBypass:serioususeCAPTCHA
 bypass_result = try_reuse_captcha(session, form, "admin", "admin")
 if bypass_result.captcha_required:
 log.warning(f"[{target_url}] CAPTCHAno methodBypass, need mobile dynamic test")
 return []

 # 3. base line:RecordFailureLoginofResponsespecial
 baseline = login_attempt(session, form, "nonexist_user_xyzzy", "wrong_pass")

 # 4. TraversalCredentialarray combine
 findings = []
 for username in usernames:
 for password in passwords:
 resp = login_attempt(session, form, username, password)
 if is_success(resp, baseline):
 findings.append(Finding(target=target_url, username=username,
 password=password, severity="CRITICAL"))
 break # thisUseralreadyDiscoverWeak Credentials, skiptounder one
 rate_limit_wait() # frequency rate control make

 return findings
```

#### No Authenticationservice check test device

```python
# scanners/noauth_scanner.py
# based on WooYun Configuration DomainData:this some serviceNo Authentication by Default, out current frequency rateCritical

NO_AUTH_CHECKS = {
 "redis": {"port": 6379, "probe": "INFO\r\n", "match": "redis_version"},
 "mongodb": {"port": 27017, "probe": None, "method": "pymongo_connect"},
 "elasticsearch": {"port": 9200, "probe": "GET /", "match": '"cluster_name"'},
 "jenkins": {"port": 8080, "probe": "GET /", "match": "Dashboard [Jenkins]"},
 "docker_api": {"port": 2375, "probe": "GET /version", "match": '"ApiVersion"'},
 "spring_actuator": {"port": 8080, "probe": "GET /actuator", "match": '"_links"'},
 "hadoop_yarn": {"port": 8088, "probe": "GET /ws/v1/cluster", "match": '"clusterInfo"'},
}

def check_no_auth(target, service):
 """check test servicewhether existsUnauthorized Access"""
 check = NO_AUTH_CHECKS.get(service.name)
 if not check:
 return None

 try:
 response = probe_service(target.ip, check["port"], check["probe"])
 if check["match"] in response:
 return Finding(target=f"{target.ip}:{check['port']}",
 service=service.name,
 issue="Unauthorized Access(no need toanyCredential)",
 severity="CRITICAL",
 wooyun_ref="Configuration Domain - No Authentication by Defaultservice")
 except Exception:
 pass
 return None
```

### 5.3 Securecontrol make need point

```yaml
# config/settings.yaml
safety:
 max_threads: 3 # singleTargetmost largeConcurrencyline process
 request_delay_ms: 1000 # Requestbetween isolate()
 max_attempts_per_user: 50 # singleUsermost largeAttempttimesnumber(defense lock set)
 lockout_detection: true # check testtolock set standalone that is stop
 lockout_indicators: # lock set special keywords
 - "Accountalready lock set"
 - "account locked"
 - "too many attempts"
 - "please after again test"
 whitelist_hours: "09:00-17:00" # onlyintool operation time between check test
 notification_on_critical: true # DiscoverSevereask problem standalone that is wild notify
```

---

## 6. WooYun typeCase References

### 6.1 admin / event business single charactersWeak CredentialsCase

the followingCasecome self WooYun Database, showWeak Credentialsinreal real attack attackinofSevereafter if:

| Case | Vulnerability Type | impact response | lesson lesson |
|------|---------|------|------|
| cloud informationusesocial informationWeChatmanage managePlatform | Default Credentials | banklinesPlatformbe complete all control make | FinancialSystemuseusedefault auth interface command |
| Emptyaccurate prepare network | Default Credentials | EmptySecureSystem flaw | key base foundation set default auth interface command |
| ChinaCache a system JBoss Misconfiguration Leading To Getshell | Default Credentials+expose exposure manage manage boundary page | JBoss manage manageConsolebe exploituse, ServerPermission | inbetween item default auth interface command |
| DaoCloud Weak Credentials+Docker Remote API Unauthorized | Weak Credentials+No Authentication | Container, primary machine be control | operationsToolWeak Credentialslink mode exploituse |
| special item flowa systembackend consoleLoginBypass | Weak Credentials+SQLinject inject | 1000ten-thousand+User/banklinescard/Identity Cardphoto imageDisclosure | Weak Credentialsoperationas interface advance one step |
| repeat protect informationa systemMisconfiguration GetShell | Misconfiguration+Default Credentials | large quantity protect protect singleInformation Disclosure(Name/Identity Card/Address) | protect linesbusinessDefault Configuration |
| Tongcheng Travel system misconfiguration allowed arbitrary file upload getshell | Misconfiguration | PassFileUpload root Permission | manage manage backend consoleWeak Credentialsadvance inject afterUpload WebShell |

### 6.2 keyStatistics

- **WooYun Weak Credentials Top 3 affected linesbusiness:** admin /event business single characters/lesson /
- **default auth interface command exist rate:** in WooYun Configuration Domain 1,796 Casein, super through 60% ofSystemuseuse commerce out Default Credentials
- **attack attack link release large validshould:** Weak Credentialsversion identity risk Cancanas"High", but operationasattack attack link inject interface(Weak Credentials -> backend console -> Upload WebShell -> ServerPermission -> Internal Network), most final risk wild commonas"Severe"
- **WooYun law:** "inany other identity copyAuthenticationtest of first, first testDefault Credentials.WooYun AllCasein 34% attribute for weakPassword/default authPassword."

---

## 7. check test report model template

### 7.1 page

```
unicode-2554==============================================================unicode-2557
| |
| XX XX global internal part manage manageSystem |
| Weak Credentialsanddefault auth interface command specialitemsSecurecheck test report |
| |
| itemsdirectoryID:XXXX-XXXX-XXX |
| check test single characters:XXXXXXXXXX |
| report day period:2026 XX XX day |
| secret level identifier identify:[machine secret] |
| |
unicode-255A==============================================================unicode-255D
```

### 7.2 report correct text result structure

```
1. approx description
 1.1 itemsdirectory background scene
 1.2 check testScope
 1.3 check test depend according(GB/T 22239 etc.protect/GB/T 28448 test assess need require)
 1.4 check test time betweenandmethod mode
 1.5 check test

2. check testMethod
 2.1 resource assetIdentifyMethod
 2.2 default auth interface command check testMethod
 2.3 Weak Credentialscheck testMethod
 2.4 Passwordpolicy strategy audit planMethod
 2.5 ToolandDictionaryDescription

3. check testResultremit total
 3.1 Statisticsapprox (image/ image)
 - DiscoverWeak Credentials/default auth interface command total number
 - bySystemtype part deploy
 - bySevereness part deploy
 - by interface command type part deploy(default auth interface command / Weak Credentials / Emptyinterface command / No Authentication)
 3.2 Risk Levelpart deploy table

4. DetailedDiscover
 [EachDiscoveruseusethe followingmodel template]

 +--------------------------------------------------------+
 | DiscoverID:WC-001 |
 | Severity:[Severe]/[High]/[in]/[Low] |
 | Systemname name:XX OA System |
 | SystemAddress:http://10.x.x.x:8080 |
 | Discovertype:default auth interface command / Weak Credentials / Emptyinterface command / Unauthorized Access |
 | involvingAccount:admin |
 | interface command content:admin123(leak sensitive handle manage:adm***23) |
 | Business Impact:AdministratorPermission, Canaccess askAll XX condition company text/XX Userinformation |
 | WooYun history history mode:Configuration Domain-Default Credentials(WooYun out current frequency rate:Critical) |
 | Reproduction Steps: |
 | 1. access ask http://10.x.x.x:8080/login |
 | 2. output injectUsername admin, Password admin123 |
 | 3. SuccessLoginmanage manage backend console |
 | Evidenceintercept image:[attach imageID] |
 | Remediation Recommendation: |
 | - standalone that isModifyasstrongPassword(unicode-226512characters, include case+number character+Special Characters) |
 | - enableusetimesLoginstrong make change secret |
 | - ConfigurationAccountlock set policy strategy(5timesFailureafter lock set15minutes) |
 | - part deploy many because Authentication(MFA) |
 +--------------------------------------------------------+

5. Passwordpolicy strategy audit planResult
 5.1 eachSystemPasswordpolicy strategyConfigurationfor ratio table
 5.2 andetc.protect 2.0 need requireoferror Analyze

6. riskAnalyze
 6.1 Weak Credentialsoperationasattack attack link inject interfaceofrisk(participate reference WooYun Case)
 6.2 Internal Network toward move dynamic risk
 6.3 DataDisclosurerisk assess assess

7. integer change create protocol
 7.1 (24hoursinternal)
 - standalone that isModifyAllalreadyDiscoverofdefault auth interface commandandWeak Credentials
 - key closeorlimit makeNo Authenticationexpose exposureofmanage manage boundary page
 7.2 short period (1cycle internal)
 - allSystemstrong makePasswordrepeat degree policy strategy
 - ConfigurationAccountlock setandLoginFailurereport alert
 - manage manage boundary page limit makeasInternal Network/VPN access ask
 7.3 inperiod (1 internal)
 - part deploy system one identity copyAuthentication(SSO)
 - keySystemenableusemany because Authentication
 - create standalone set periodWeak CredentialsScanmachine make
 7.4 long period (hold continue)
 - Passwordpolicy strategy injectSecurebase line
 - newSystemabove line first strong make default auth interface command check test
 - set periodSecuremeaning identify lesson

8. Appendix
 8.1 check testToolclear single
 8.2 check testDictionaryDescription
 8.3 Evidenceintercept image(leak sensitive)
 8.4 etc.protect 2.0 identity copy appraise level related key condition payment for photo
```

### 7.3 Severeness set level identifier accurate

| level level | set define | Weak Credentialsscenario sceneExample |
|------|------|-------------|
| **Severe** | directly usableCausingaudit coreSystem flaworlarge scale modelDataDisclosure | Bastion Host/VPN/domain control default auth interface command/Database root Blank Password |
| **High** | CanObtainsensitive sensitiveDataorserious needSystemmanage managePermission | OA AdministratorWeak Credentials/ itemSystemdefault auth interface command |
| **in** | CanObtainpart partSystemfunction canorNon-sensitive sensitiveData | monitor controlSystemWeak Credentials/Regular UserWeak Credentials |
| **Low** | impact response has limit, but reverseSecuremost real | Test EnvironmentWeak Credentials/Non-generate assetSystemdefault auth interface command |

---

## 8. combine scale for photo

### 8.1 etc.protect 2.0(GB/T 22239-2019)identity copy appraise level need require

| etc.protect condition payment | need require | check test key connect |
|---------|------|---------|
| 8.1.4.1 a) | forLoginofUseradvancelinesidentity copy identifier identifyandappraise level | check testNo Authenticationexpose exposureofmanage manage boundary page |
| 8.1.4.1 b) | identity copy identifier identify tool has one ness | check test sharedAccount/wilduseAccount |
| 8.1.4.1 c) | tool hasLoginFailurehandle manage function can | check testAccountlock set policy strategywhethergenerate valid |
| 8.1.4.1 d) | remote process manage manage time defense | check test clear text pass outputCredentialofSystem |
| 8.1.4.1 e) | interface command repeat degree need require | check testPasswordpolicy strategyConfiguration |
| 8.1.4.1 f) | initial interface command/default auth interface command strong makeModify | check test default auth interface command exist details |

---

## 9. inject meaning eventitems

### 9.1 method law combine scale

- **musthold has method deployofcertificate pageAuthorizationcertificate**, clear confirm check testScope/time between/method mode
- check test through processinDiscoverofAllCredentialinformation need severe format protect secret
- reportininterface command contentmustleak sensitive handle manage
- check test complete afterDeleteversion StorageofAllCredentialinformation

### 9.2 Securecontrol make

- inNon-businessHigh period(such as betweenorcycle)ExecuteBrute Forcetype check test
- severe format control makeConcurrencynumberandRequestfrequency rate, avoid trigger initiateAccountlock set
- real time monitor controlTargetSystemoperatelinesStatus, Discoverabnormal common standalone that is stop
- and method operations protect hold real time wildChannel
- forBastion Host/Databaseetc.keySystemusemobile dynamic one by oneAttemptmethod mode, disable stop self dynamic izeBatchBrute Force

### 9.3 WooYun Methodcomment provide

> "inany other identity copyAuthenticationtest of first, first testDefault Credentials."
> -- WooYun Authentication Domain law

Executeorder sequence law:**Default Credentials -> Emptyinterface command -> No Authenticationservice -> Weak CredentialsBrute Force**.this order sequence based on WooYun 7,513 Weak CredentialsCaseofStatisticsscale law:large part partSysteminNo. one step be attack, no need toadvance injectBrute ForcePhase.

---

*version method plan based on WooYun vulnerabilityDatabase(2010-2016)22,132 real realCase, Among themAuthentication Domain 8,846 cases/ConfigurationDomain 1,796 cases.Methodcomment version version v2.0.*
