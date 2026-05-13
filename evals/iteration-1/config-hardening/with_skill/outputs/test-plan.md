# Tomcat + MySQL + Redis + Nginx ConfigurationSecureCheckclear single

> Based on 22,132 real WooYun vulnerability cases(2010-2016) - Configuration Domain 1,796 Case - 72.6% High Risk
>
> suitableusescenario scene:Alibaba Cloud ECS above operations transaction connectMissingofitemsdirectory, one-by-oneitemsrank checkDefault Configurationrisk

---

## useuseDescription

- **Checkmethod mode**:SSH Login ECS after, bySectionorder sequence one-by-oneitemsExecuteCommand, for photo"Expected Result"determine judgewhethercombine scale
- **Priorityidentifier record**:`[Severe]` `[High Risk]` `[Medium Risk]` `[Low Risk]` -- priority first fix repeatSevereandHigh Riskitems
- **WooYun citeuse**:EachSectionidentifier inject key connectof WooYun CasemodeandStatisticsData

---

## 1. Tomcat ConfigurationSecureCheck

> **WooYun Data**:Tomcat Manager Default Credentialsout current frequency rate"Critical", isConfiguration DomainmostHighfrequencyofattack attack inject interface of one.
> ** typeCase**:ChinaCache a system JBoss Misconfiguration Leading To Getshell(same type Java inbetween item manage manage backend console ask problem)

### 1.1 Default Credentialsandmanage manage backend console `[Severe]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 1 | Tomcat Manager whetherCanaccess ask | `curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/manager/html` | Return 404 orcontinuous connect reject reject(Non- 401/200) |
| 2 | Host Manager whetherCanaccess ask | `curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/host-manager/html` | Return 404 orcontinuous connect reject reject |
| 3 | tomcat-users.xml whether existsdefault authAccount | `cat $CATALINA_HOME/conf/tomcat-users.xml \| grep -i 'username='` | not existin tomcat/tomcat/admin/admin etc.Default Credentials |
| 4 | Manager ApplicationwhetheralreadyDelete | `ls $CATALINA_HOME/webapps/ \| grep -E 'manager\|host-manager'` | generate asset environment environment not existinthis two directory record |
| 5 | default authExampleApplicationwhetheralreadyDelete | `ls $CATALINA_HOME/webapps/ \| grep -E 'docs\|examples\|ROOT'` | not existin docs/examples directory record;ROOT only include businessCode |

### 1.2 Information Disclosuredefense protect `[High Risk]`

> **WooYun Data**:Information Disclosuredomain 4,858 Casein 64.7% High Risk.error page expose exposureServerversion versionandstack stack is precision accurate exploituseoffirst provide.

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 6 | Server Headerwhetherexpose exposure version version | `curl -sI http://localhost:8080/ \| grep -i server` | not display "Apache-Coyote" or Tomcat version version number |
| 7 | server.xml whetherkey close version versionDisclosure | `grep -i 'server=' $CATALINA_HOME/conf/server.xml` | Connector inConfiguration `server="Server"` orself set define value |
| 8 | self set define error page | `grep '<error-page>' $CATALINA_HOME/conf/web.xml` | Configurationdone 404/500 etc.error codeofself set define page |
| 9 | directory record listwhetherkey close | `grep '<param-name>listings</param-name>' -A1 $CATALINA_HOME/conf/web.xml` | `<param-value>false</param-value>` |
| 10 | TRACE Methodwhether disabled | `curl -sI -X TRACE http://localhost:8080/` | Return 405 Method Not Allowed |

### 1.3 continuous connect deviceandprotocol protocolSecure `[High Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 11 | AJP continuous connect devicewhetherexpose exposure(Ghostcat CVE-2020-1938) | `grep 'Connector.*8009' $CATALINA_HOME/conf/server.xml` | already inject orConfigurationdone `secretRequired="true"` + `secret="..."` |
| 12 | Shutdown PortwhetherModifydefault auth value | `grep '<Server port=' $CATALINA_HOME/conf/server.xml` | PortNon- 8005, orCommandcharacter symbol stringNon- "SHUTDOWN" |
| 13 | Tomcat whetheras root operatelines | `ps aux \| grep tomcat \| grep -v grep \| awk '{print $1}'` | operatelinesUserasspecialuseNon- root Account(such as tomcat) |
| 14 | self dynamic part deploywhetherkey close | `grep 'autoDeploy' $CATALINA_HOME/conf/server.xml` | `autoDeploy="false"` and `deployOnStartup="false"` |

### 1.4 Session Secure `[Medium Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 15 | Cookie HttpOnly identifier record | `grep 'useHttpOnly' $CATALINA_HOME/conf/context.xml` | `useHttpOnly="true"` |
| 16 | Session super time time between | `grep '<session-timeout>' $CATALINA_HOME/conf/web.xml` | not super through 30 minutes |

---

## 2. MySQL ConfigurationSecureCheck

> **WooYun Data**:phpMyAdmin root/Blank Passwordout current frequency rate"Critical";MySQL 3306 PortnoPasswordexpose exposure isDatabasemanage manage type most common seen ask problem.
> ** typeCase**:micro primary SQL inject inject impact response 860W+ person/46W+ generate -- DatabaseSecureis most after defense line.

### 2.1 AuthenticationandPermission `[Severe]`

> **WooYun Data**:weakCredentialdomain 7,513 Case, 58.2% High Risk.admin/admin/root/Empty is WooYun all libraryinout current frequency rate mostHighofDefault Credentialsmode.

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 17 | root whether hasPassword | `mysql -u root --password='' -e "SELECT 1" 2>&1` | continuous connectFailure(Access denied) |
| 18 | whether existsBlank PasswordAccount | `mysql -u root -p -e "SELECT User,Host FROM mysql.user WHERE authentication_string='' OR authentication_string IS NULL;"` | ResultasEmpty |
| 19 | whether exists nameAccount | `mysql -u root -p -e "SELECT User,Host FROM mysql.user WHERE User='';"` | ResultasEmpty |
| 20 | test DatabasewhetherDelete | `mysql -u root -p -e "SHOW DATABASES LIKE 'test';"` | ResultasEmpty |
| 21 | root whetherlimit make version Login | `mysql -u root -p -e "SELECT User,Host FROM mysql.user WHERE User='root';"` | Host list only include localhost / 127.0.0.1, not include % |
| 22 | businessAccountPermissionmost small ize | `mysql -u root -p -e "SHOW GRANTS FOR 'app_user'@'%';"` | only has SELECT/INSERT/UPDATE/DELETE etc.must needPermission, no GRANT/SUPER/FILE |

### 2.2 Networkexpose exposure `[Severe]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 23 | monitor Addresswhetherlimit make | `grep 'bind-address' /etc/my.cnf /etc/mysql/my.cnf 2>/dev/null` | `bind-address = 127.0.0.1`(Non- 0.0.0.0) |
| 24 | 3306 whetherfor external open release | `ss -tlnp \| grep 3306` | only monitor 127.0.0.1:3306 |
| 25 | Alibaba CloudSecurearraywhetherreleaselines 3306 | LoginAlibaba CloudConsole -> ECS -> Securearray scale rule | inject method toward not existin 3306 of 0.0.0.0/0 scale rule |

### 2.3 Security Configuration `[High Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 26 | whether disabled LOCAL INFILE | `mysql -u root -p -e "SHOW VARIABLES LIKE 'local_infile';"` | `OFF` |
| 27 | whether disabledsymbol number link connect | `mysql -u root -p -e "SHOW VARIABLES LIKE 'have_symlink';"` | `DISABLED` |
| 28 | errorLogwhetheropen enable | `mysql -u root -p -e "SHOW VARIABLES LIKE 'log_error';"` | ConfigurationdoneLogFilePath |
| 29 | check queryLogwhetheropen enable | `mysql -u root -p -e "SHOW VARIABLES LIKE 'slow_query_log';"` | `ON` |
| 30 | MySQL whetheras root operatelines | `ps aux \| grep mysqld \| grep -v grep \| awk '{print $1}'` | operatelinesUseras mysql, Non- root |

### 2.4 Dataprotect protect `[Medium Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 31 | whether enabled SSL continuous connect | `mysql -u root -p -e "SHOW VARIABLES LIKE '%ssl%';"` | `have_ssl = YES` |
| 32 | two advance makeLogwhetheropen enable(prepare) | `mysql -u root -p -e "SHOW VARIABLES LIKE 'log_bin';"` | `ON` |

---

## 3. Redis ConfigurationSecureCheck

> **WooYun Data**:Redis No Authentication by Default, out current frequency rate"Critical".6379 PortUnauthorized AccessisConfiguration Domaininsingle one service impact response most largeofVulnerability Category.
> ** typeCase**:DaoCloud Weak Credentials + Docker Remote API Unauthorized Access -- Redis Unauthorizedcommonandother service array combine complete exploituselink.
> **Attack Pattern**:Unauthorized Redis -> write SSH company / write Crontab / write Webshell -> Server flaw

### 3.1 AuthenticationandAccess Control `[Severe]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 33 | whetherset set donePassword | `grep '^requirepass' /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | existin `requirepass <strongPassword>`(Non-Empty/Non- foobared) |
| 34 | noPasswordwhether cancontinuous connect | `redis-cli -h 127.0.0.1 ping` | Return `NOAUTH Authentication required.` |
| 35 | monitor Addresswhetherlimit make | `grep '^bind' /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | `bind 127.0.0.1`(Non- 0.0.0.0 orinject Status) |
| 36 | 6379 whetherfor external open release | `ss -tlnp \| grep 6379` | only monitor 127.0.0.1:6379 |
| 37 | Alibaba CloudSecurearraywhetherreleaselines 6379 | LoginAlibaba CloudConsole -> ECS -> Securearray scale rule | inject method toward not existin 6379 of 0.0.0.0/0 scale rule |
| 38 | protected-mode whetheropen enable | `grep '^protected-mode' /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | `protected-mode yes` |

### 3.2 risk Commandlimit make `[High Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 39 | whether disabled/serious fatal name risk Command | `grep -E 'rename-command' /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | FLUSHALL/FLUSHDB/CONFIG/KEYS/DEBUG/EVAL already rename as machine character symbol stringorEmptystring |
| 40 | whether disabled Lua Script | business notrequirestime, Check rename-command EVAL | EVAL already be rename ordisableuse |

### 3.3 operatelinesSecure `[High Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 41 | Redis whetheras root operatelines | `ps aux \| grep redis-server \| grep -v grep \| awk '{print $1}'` | operatelinesUseras redis, Non- root |
| 42 | Datadirectory recordPermission | `ls -la /var/lib/redis/` | attribute primaryas redis User, Permission 750 orupdate severe |
| 43 | ConfigurationFilePermission | `ls -la /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | Permission 640 orupdate severe, attribute primary root:redis |
| 44 | whether enabledhold ize | `grep -E '^(save\|appendonly)' /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | at leastConfigurationdone RDB (save) or AOF (appendonly yes) |

---

## 4. Nginx ConfigurationSecureCheck

> **WooYun Data**:Misconfigurationservice typein, directory record list enableuse/DetailederrorInformation Disclosure/allow allow PUT/DELETE MethodisHighimpact response mode.
> ** typeCase**:Tongcheng Travel system misconfiguration allowed arbitrary file upload getshell/root Permission

### 4.1 Information Disclosuredefense protect `[High Risk]`

> **WooYun Data**:404 ResponseHeaderexpose exposureServerversion version number isInformation Disclosuredomaininofcommon seenDiscoverspecified identifier, asafter continue precision accurate exploituseprovide provide version version information.

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 45 | whetherhidden hidden version version number | `grep 'server_tokens' /etc/nginx/nginx.conf` | `server_tokens off;` |
| 46 | Server Headerwhetherexpose exposure version version | `curl -sI http://localhost/ \| grep -i server` | not display Nginx version version number |
| 47 | whether disabled autoindex | `grep -r 'autoindex' /etc/nginx/` | not existin `autoindex on`;oronlyInternal Networkdirectory record open enable |
| 48 | self set define error page | `grep 'error_page' /etc/nginx/nginx.conf /etc/nginx/conf.d/*.conf 2>/dev/null` | Configurationdone 403/404/500/502 etc.self set define error page |
| 49 | whetherexpose exposure X-Powered-By | `curl -sI http://localhost/ \| grep -i x-powered-by` | not existinthisResponseHeader(Pass proxy_hide_header move remove) |

### 4.2 Access Control `[Severe]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 50 | Tomcat Manager whetherPass Nginx expose exposure | `grep -r 'manager\|host-manager' /etc/nginx/conf.d/ /etc/nginx/sites-enabled/ 2>/dev/null` | not existinreverse codeto /manager/ ofscale rule;orConfigurationdone IP Whitelist |
| 51 | sensitive sensitivePathwhetherlimit make access ask | `grep -rE '(\.git\|\.svn\|\.env\|\.bak\|WEB-INF)' /etc/nginx/conf.d/ 2>/dev/null` | Configurationdone `deny all` scale rule stop access ask.git/.svn/.env etc. |
| 52 | phpMyAdmin etc.manage manage boundary page | `grep -rE '(phpmyadmin\|pma\|adminer)' /etc/nginx/conf.d/ 2>/dev/null` | not existin, orConfigurationdone IP Whitelist + Authentication |
| 53 | default auth pointwhetherclear manage | `ls /etc/nginx/sites-enabled/ 2>/dev/null` | not existin default pointConfiguration |
| 54 | not must needof HTTP Method | `curl -sI -X OPTIONS http://localhost/ \| grep -i allow` | only allow allow GET/HEAD/POST;not allow allow PUT/DELETE/TRACE |

### 4.3 SecureHeaderpart `[Medium Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 55 | X-Frame-Options | `curl -sI http://localhost/ \| grep -i x-frame-options` | `DENY` or `SAMEORIGIN` |
| 56 | X-Content-Type-Options | `curl -sI http://localhost/ \| grep -i x-content-type-options` | `nosniff` |
| 57 | X-XSS-Protection | `curl -sI http://localhost/ \| grep -i x-xss-protection` | `1; mode=block` |
| 58 | Content-Security-Policy | `curl -sI http://localhost/ \| grep -i content-security-policy` | existin CSP policy strategy |
| 59 | Strict-Transport-Security(HTTPS time) | `curl -sI https://Domain Name/ \| grep -i strict-transport-security` | `max-age=31536000; includeSubDomains` |

### 4.4 SSL/TLS Configuration(such asalready enableuse HTTPS)`[High Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 60 | TLS protocol protocol version version | `grep 'ssl_protocols' /etc/nginx/nginx.conf /etc/nginx/conf.d/*.conf 2>/dev/null` | only `TLSv1.2 TLSv1.3`;not include SSLv3/TLSv1/TLSv1.1 |
| 61 | add secret itemConfiguration | `grep 'ssl_ciphers' /etc/nginx/nginx.conf /etc/nginx/conf.d/*.conf 2>/dev/null` | useusestrong add secret item, no RC4/DES/3DES/MD5 |
| 62 | whetherstrong make HTTPS skip transfer | `grep -E 'return 301.*https\|rewrite.*https' /etc/nginx/conf.d/*.conf 2>/dev/null` | HTTP 80 Port 301 skip transferto HTTPS |
| 63 | cert certificateValidity Period | `echo \| openssl s_client -connect localhost:443 2>/dev/null \| openssl x509 -noout -dates` | not expired, andtoperiod day > 30 days |

### 4.5 reverse toward code manageSecure `[Medium Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 64 | whethertransfer initiate real real IP | `grep -r 'X-Real-IP\|X-Forwarded-For' /etc/nginx/conf.d/` | Configurationdone `proxy_set_header X-Real-IP $remote_addr` |
| 65 | Request Bodylarge small limit make | `grep 'client_max_body_size' /etc/nginx/nginx.conf /etc/nginx/conf.d/*.conf 2>/dev/null` | set set done combine manage above limit(such as 10m), Non-default auth 1m orno limit make |
| 66 | super time set set | `grep -E 'proxy_connect_timeout\|proxy_read_timeout' /etc/nginx/conf.d/*.conf 2>/dev/null` | Configurationdone combine manage super time(such as 60s), defense stop rate attack attack |

---

## 5. operationSystemand ECS Securebase line

> **WooYun Data**:cloudMisconfigurationis WooYun time code afterofnew High Riskmode.Securearray 0.0.0.0/0 releaselinesmanage managePortetc.same for no defense.

### 5.1 SSH Secure `[Severe]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 67 | whether disabled root SSH Login | `grep '^PermitRootLogin' /etc/ssh/sshd_config` | `PermitRootLogin no` |
| 68 | whether disabledPasswordLogin | `grep '^PasswordAuthentication' /etc/ssh/sshd_config` | `PasswordAuthentication no`(useuseKeyAuthentication) |
| 69 | SSH PortwhetherModify | `grep '^Port' /etc/ssh/sshd_config` | Non-default auth 22 Port |
| 70 | LoginFailurelimit make | `grep '^MaxAuthTries' /etc/ssh/sshd_config` | `MaxAuthTries 3`(oralready part deploy fail2ban) |

### 5.2 Alibaba CloudSecurearray `[Severe]`

| # | Check Item | Check Method | Expected Result |
|---|--------|---------|---------|
| 71 | inject method towardwhether has 0.0.0.0/0 all releaselinesscale rule | Alibaba CloudConsole -> Securearray scale rule | not existinallow allowAllPortof 0.0.0.0/0 scale rule |
| 72 | manage managePortwhetherlimit make come source IP | Check 22/8080/3306/6379 ofSecurearray scale rule | only allow allow company IP / Bastion Host IP access ask |
| 73 | out method towardwhetherlimit make | Checkout method toward scale rule | Non-all releaselines;limit maketomust needofTargetandPort |

### 5.3 SystemHardening `[High Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 74 | Systemwhether hasnot fix supplement vulnerability | `yum check-update 2>/dev/null \|\| apt list --upgradable 2>/dev/null` | no serious largeSecureUpdatepending |
| 75 | whether existsnot must needof SUID File | `find / -perm -4000 -type f 2>/dev/null` | onlySystemidentifier accurate SUID File, no self set defineorabnormal commonitems |
| 76 | set time any servicewhetherabnormal common | `crontab -l; ls /etc/cron.d/; cat /etc/crontab` | noCanof Script/reverse shell etc.abnormal common any service |
| 77 | whether hasabnormal common monitor Port | `ss -tlnp` | only has business must needofPortinmonitor, no not notify service |
| 78 | defense whether enabled | `iptables -L -n \|\| firewall-cmd --list-all 2>/dev/null` | existinclear confirmofinject scale rule, Non-all releaselines |

---

## 6. Applicationlayer wilduseCheck

> **WooYun Data**:Information Disclosuredomain 6,446 Case + Misconfigurationdomain 1,796 Casetotal same specified toward -- version version control makeFileDisclosure/prepare copyFileexpose exposure/debuggingEndpointnot key is operations transaction connectMissingof type special.

### 6.1 sensitive sensitiveFileandInformation Disclosure `[High Risk]`

> **WooYun mode**:Source Code/Configuration Disclosure 4,858 Case, 64.7% High Risk./.git/config Disclosure -> Completesource code -> credential according provide take is WooYun inHighfrequency exploituselink.

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 79 |.git directory recordwhetherCanaccess ask | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/.git/config` | Return 403 or 404 |
| 80 |.svn directory recordwhetherCanaccess ask | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/.svn/entries` | Return 403 or 404 |
| 81 | prepare copyFilewhetherCanaccess ask | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/backup.zip` | Return 403 or 404 |
| 82 |.env FilewhetherCanaccess ask | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/.env` | Return 403 or 404 |
| 83 | WEB-INF whetherCanaccess ask | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/WEB-INF/web.xml` | Return 403 or 404 |
| 84 | phpinfo whether retain | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/phpinfo.php` | Return 404 |
| 85 | Swagger/API Documentwhetherexpose exposure | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/swagger-ui.html` | Return 404 orrequiresAuthentication |
| 86 | Druid monitor controlwhetherexpose exposure | `curl -s -o /dev/null -w "%{http_code}" http://Domain Name/druid/index.html` | Return 404 orrequiresAuthentication |

### 6.2 No. three method array itemCheck `[High Risk]`

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 87 | Tomcat version versionwhether hasalready notify CVE | `$CATALINA_HOME/bin/version.sh 2>/dev/null` | version versionasmost new set versionorno serious large CVE |
| 88 | MySQL version version | `mysql --version` | no already notify not fix supplementofserious large CVE |
| 89 | Redis version version | `redis-server --version` | no already notify not fix supplementofserious large CVE |
| 90 | Nginx version version | `nginx -v 2>&1` | no already notify not fix supplementofserious large CVE |
| 91 | Java/JDK version version | `java -version 2>&1` | Non- EOL version version, already fix supplement already notify vulnerability |

---

## 7. Logandmonitor control

> **WooYun defense defense mode**:Configuration move check test/new service check test/expose exposure service set periodScanis defense defenseMisconfigurationofthree major monitor control support.

| # | Check Item | Check Command | Expected Result |
|---|--------|---------|---------|
| 92 | Tomcat access askLogwhetheropen enable | `grep 'AccessLogValve' $CATALINA_HOME/conf/server.xml` | Valve not be inject, Logcorrect common write inject |
| 93 | Nginx access askLogwhetheropen enable | `grep 'access_log' /etc/nginx/nginx.conf` | Non- `access_log off`, LogPathexistin |
| 94 | MySQL check queryLog | `mysql -u root -p -e "SHOW VARIABLES LIKE 'slow_query_log';"` | `ON` |
| 95 | Logwhether hasrotate transfer | `ls /etc/logrotate.d/ \| grep -E 'nginx\|tomcat\|mysql'` | existinforshouldof logrotate Configuration |
| 96 | whether hasLoginFailurereport alert | `grep -c 'Failed password' /var/log/secure /var/log/auth.log 2>/dev/null` | has monitor control machine make(fail2ban / Alibaba Cloud etc.) |

---

## Statistics need

| Dimension | number quantity |
|------|------|
| totalCheck Item | 96 items |
| Severe | 22 items(#1-5, 17-21, 33-38, 50, 67-68, 71-72) |
| High Risk | 42 items |
| Medium Risk | 20 items |
| Low Risk | 12 items |

## WooYun Caseciteusesearch cite

| WooYun Case | key connectCheck Item | Attack Pattern |
|-------------|-----------|---------|
| ChinaCache a system JBoss Misconfiguration Leading To Getshell | #1-5 | Default Credentials -> manage manage backend console -> part deploy WebShell |
| DaoCloud Weak Credentials + Docker Remote API Unauthorized Access | #33-38 | Redis/Docker Unauthorized -> Container |
| Tongcheng Travel system misconfiguration allowed arbitrary file upload getshell/root Permission | #47, 54, 91 | Misconfiguration -> FileUpload -> RCE |
| micro primary SQL inject inject impact response 860W+ person/46W+ generate | #17-22, 23-25 | Databaseexpose exposure -> DataDisclosure |
| TCL a systemMisconfiguration Leading To 600 ten-thousand clientInformation Disclosure | #79-86 | Information Disclosure -> large scale modelDataexternal |
| repeat protect informationa systemMisconfiguration GetShell impact response large quantity protect single information | #45-49, 87-91 | serviceMisconfiguration -> RCE -> DataDisclosure |
| Sunshine InsuranceSensitive InformationDisclosureCausingSuccessadvance injectInternal NetworkSystem | #79-86, 67-70 | credential accordingDisclosure -> Internal Network toward move dynamic |

## WooYun keyStatistics

- **Misconfigurationdomain**:1,796 Case, 72.6% High Risk -- Default Configuration = vulnerability
- **weakCredentialdomain**:7,513 Case, 58.2% High Risk -- WooYun all library 34% ofvulnerability source for default auth/weakPassword
- **Information Disclosuredomain**:4,858 Case, 64.7% High Risk -- Disclosureofinformation isAllother attack attackof ize
- **Default Credentialsfrequency rate**:Tomcat Manager (Critical)/Redis No Authentication (Critical)/phpMyAdmin root/Empty (Critical)
- **audit core lesson lesson**:WooYun 22,132 real realCasereverse repeat cert clear -- most tool powerofinject come self notModifyofDefault Configuration, whileNon-zero day vulnerability

---

> generate complete depend according:WooYun Business Logic Vulnerability Methodology v2.0 - Configuration Domain 1,796 Case + Information Disclosuredomain 6,446 Case + Authenticationdomain 8,846 Case
