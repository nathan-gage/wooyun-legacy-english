# Tomcat + MySQL + Redis + Nginx ConfigurationSecureCheckclear single

> suitableusescenario scene:connect mobile noDocumentofitemsdirectory, Alibaba Cloud ECS part deploy, one-by-oneitemsrank checkDefault Configurationrisk.
> Checkmethod mode:eachitemsto out**Check Command**and**expected periodSecureStatus**, not symbol combine rule need integer change.

---

## 1. operationSystemand ECS base foundation

### 1.1 SSH Secure

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 1 | disable stop root DirectLogin | `grep "^PermitRootLogin" /etc/ssh/sshd_config` | `PermitRootLogin no` |
| 2 | disable stopPasswordLogin, only allow allowKey | `grep "^PasswordAuthentication" /etc/ssh/sshd_config` | `PasswordAuthentication no` |
| 3 | SSH PortwhetherchangeasNon- 22 | `grep "^Port" /etc/ssh/sshd_config` | Non- 22 Port(such as 2222) |
| 4 | Empty super time judge open | `grep "ClientAliveInterval" /etc/ssh/sshd_config` | set set combine manage value(such as 300) |
| 5 | most largeAuthenticationAttempttimesnumber | `grep "MaxAuthTries" /etc/ssh/sshd_config` | `MaxAuthTries 3` |

### 1.2 SystemUserandPermission

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 6 | each servicewhetheras independent standaloneNon- root Useroperatelines | `ps aux \| grep -E "(java\|mysql\|redis\|nginx)" \| awk '{print $1}'` | part levelas tomcat/mysql/redis/nginx etc.Non- root User |
| 7 | whether existsBlank PasswordAccount | `awk -F: '($2 == "") {print $1}' /etc/shadow` | no output out |
| 8 | sudo Permissionwhethercollect | `cat /etc/sudoers.d/*; grep -v "^#" /etc/sudoers \| grep -v "^$"` | only must needUserhas sudo, and limit makeConcreteCommand |

### 1.3 defense andSecurearray

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 9 | iptables/firewalld whether enabled | `systemctl status firewalld; iptables -L -n` | defense handle for active Status, has scale rule |
| 10 | Alibaba CloudSecurearray scale rule | Alibaba CloudConsole > ECS > Securearray > Viewscale rule | only open release 80/443/SSH Port, come source IP limit make |
| 11 | MySQL Port(3306)whetherfor external expose exposure | `iptables -L -n \| grep 3306; ss -tlnp \| grep 3306` | 3306 only monitor 127.0.0.1, Securearray not open release |
| 12 | Redis Port(6379)whetherfor external expose exposure | `ss -tlnp \| grep 6379` | 6379 only monitor 127.0.0.1, Securearray not open release |
| 13 | Tomcat manage managePort(8080/8443)whetherfor external expose exposure | `ss -tlnp \| grep -E "8080\|8443"` | only monitor 127.0.0.1(by Nginx reverse code), Securearray not open release |

### 1.4 SystemUpdateandinternal audit

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 14 | Systemwhether hasnot fix repeatofSecuresupplement | `yum check-update --security` or `apt list --upgradable` | noHigh RiskSecureUpdatepending |
| 15 | internal audit version versionwhetherthrough old | `uname -r` | no already notifyHigh Riskvulnerabilityofinternal audit version version |

---

## 2. Nginx Security Configuration

### 2.1 Information Disclosure

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 16 | hidden hidden Nginx version version number | `grep "server_tokens" /etc/nginx/nginx.conf` | `server_tokens off;` |
| 17 | ResponseHeaderinwhetherDisclosureversion version | `curl -sI http://localhost \| grep Server` | `Server: nginx`(no version version number) |
| 18 | move remove X-Powered-By etc.many Header | `curl -sI http://localhost \| grep -iE "x-powered-by\|x-aspnet"` | no output out |

### 2.2 HTTPS andcert certificate

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 19 | whether enabled HTTPS | `grep -r "ssl_certificate" /etc/nginx/` | existin SSL cert certificateConfiguration |
| 20 | whetherstrong make HTTP skip transfer HTTPS | `grep -rA3 "listen 80" /etc/nginx/conf.d/` | include `return 301 https://` |
| 21 | SSL protocol protocol version version | `grep "ssl_protocols" /etc/nginx/nginx.conf` | `TLSv1.2 TLSv1.3`(disableuse TLSv1.0/1.1) |
| 22 | SSL add secret item | `grep "ssl_ciphers" /etc/nginx/nginx.conf` | useusestrong add secret item, disableuse RC4/DES/3DES/MD5 |
| 23 | HSTS Header | `grep "Strict-Transport-Security" /etc/nginx/` -r` | `max-age=31536000; includeSubDomains` |
| 24 | cert certificatewhetherthat iswillexpired | `echo \| openssl s_client -connect localhost:443 2>/dev/null \| openssl x509 -noout -dates` | Validity Period > 30 days |

### 2.3 SecureHeader

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 25 | X-Frame-Options | `curl -sI https://localhost \| grep -i x-frame` | `DENY` or `SAMEORIGIN` |
| 26 | X-Content-Type-Options | `curl -sI https://localhost \| grep -i x-content-type` | `nosniff` |
| 27 | X-XSS-Protection | `curl -sI https://localhost \| grep -i x-xss` | `1; mode=block` |
| 28 | Content-Security-Policy | `curl -sI https://localhost \| grep -i content-security` | existincombine manage CSP policy strategy |
| 29 | Referrer-Policy | `curl -sI https://localhost \| grep -i referrer` | `strict-origin-when-cross-origin` orupdate severe format |

### 2.4 Access ControlandRate Limiting

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 30 | disable stop directory record list | `grep "autoindex" /etc/nginx/ -r` | `autoindex off;` orno specified command(default auth off) |
| 31 | sensitive sensitivePathAccess Control | `grep -rE "location.*(admin\|manager\|status\|\.git\|\.env\|\.svn)" /etc/nginx/` | sensitive sensitivePathhas `deny all` or IP Whitelist |
| 32 | Request Bodylarge small limit make | `grep "client_max_body_size" /etc/nginx/nginx.conf` | set set combine manage value(such as 10m), Non-default auth 1m Non-no limit make |
| 33 | continuous connect number/Requestrate rate limit make | `grep -rE "limit_req_zone\|limit_conn_zone" /etc/nginx/` | existinRate LimitingConfiguration |
| 34 | reverse toward code manage super time set set | `grep -rE "proxy_connect_timeout\|proxy_read_timeout" /etc/nginx/` | set set combine manage super time(such as 60s), avoid default auth no limitetc.pending |

### 2.5 Log

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 35 | access askLogwhetheropen enable | `grep "access_log" /etc/nginx/nginx.conf` | `access_log` specified towardValidPath, Non- off |
| 36 | errorLogwhetheropen enable | `grep "error_log" /etc/nginx/nginx.conf` | `error_log` specified towardValidPath, level levelas warn or error |
| 37 | LogFilePermission | `ls -la /var/log/nginx/` | Permission 640 orupdate severe format, attribute primaryas nginx/root |

---

## 3. Tomcat Security Configuration

### 3.1 default auth credential accordingandmanage manage page

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 38 | whether existsdefault auth manage manageUser | `cat $CATALINA_HOME/conf/tomcat-users.xml \| grep -v "<!--"` | no default authUser(admin/tomcat/manager), orFileasEmptyinject |
| 39 | Manager App whetherCanaccess ask | `curl -s http://localhost:8080/manager/html -o /dev/null -w "%{http_code}"` | 404 or 403(shouldDeleteorlimit make access ask) |
| 40 | Host Manager whetherCanaccess ask | `curl -s http://localhost:8080/host-manager/html -o /dev/null -w "%{http_code}"` | 404 or 403 |
| 41 | default authExampleApplicationwhetherDelete | `ls $CATALINA_HOME/webapps/ \| grep -E "examples\|docs\|ROOT"` | no examples/docs directory record;ROOT asbusinessApplicationoralreadyDelete |

### 3.2 Information Disclosure

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 42 | hidden hidden Tomcat version version number | `grep "server=" $CATALINA_HOME/conf/server.xml` | Connector ininclude `server=""`(self set define valueorEmpty) |
| 43 | self set define error page | `grep "<error-page>" $CATALINA_HOME/conf/web.xml` | set define done 404/500 etc.error page, not expose exposure stack stack |
| 44 | disable stop directory record list | `grep "listings" $CATALINA_HOME/conf/web.xml` | `<param-value>false</param-value>` |
| 45 | X-Powered-By Header | `grep "xpoweredBy" $CATALINA_HOME/conf/server.xml` | `xpoweredBy="false"` orno attributes(default auth false) |

### 3.3 continuous connect deviceSecure

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 46 | AJP continuous connect devicewhether disabledorsetKey | `grep -i "AJP" $CATALINA_HOME/conf/server.xml \| grep -v "<!--"` | AJP continuous connect device already inject /Delete, orset set done `secret`/`requiredSecret` |
| 47 | Shutdown Port | `grep "shutdown=" $CATALINA_HOME/conf/server.xml` | Portchangeas -1(disableuse), orchangeasNon-default auth 8005 and shutdown character symbol string already update change |
| 48 | Connector BindingAddress | `grep "address=" $CATALINA_HOME/conf/server.xml` | 8080 Binding `127.0.0.1`(Nginx reverse code scenario scene) |
| 49 | maxPostSize limit make | `grep "maxPostSize" $CATALINA_HOME/conf/server.xml` | set set combine manage value(such as 2097152 = 2MB) |

### 3.4 Sessionand Cookie

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 50 | Cookie HttpOnly | `grep "httpOnly" $CATALINA_HOME/conf/context.xml` | `useHttpOnly="true"` |
| 51 | Cookie Secure identifier | `grep -i "secure" $CATALINA_HOME/conf/web.xml` | `<secure>true</secure>`(HTTPS scenario scene) |
| 52 | Session super time | `grep "session-timeout" $CATALINA_HOME/conf/web.xml` | combine manage value(such as 30 minutes), Non-default auth no limit |
| 53 | JSESSIONID not out currentin URL | `grep "tracking-mode" $CATALINA_HOME/conf/web.xml` | `<tracking-mode>COOKIE</tracking-mode>` |

### 3.5 JVM andoperatelinesSecure

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 54 | Tomcat operatelinesUser | `ps aux \| grep java \| grep -v grep \| awk '{print $1}'` | Non- root User |
| 55 | CATALINA_HOME directory recordPermission | `ls -la $CATALINA_HOME/` | conf/ directory recordPermission 700, attribute primaryas tomcat User |
| 56 | Logdirectory recordPermission | `ls -la $CATALINA_HOME/logs/` | Permission 750 orupdate severe format |
| 57 | JMX remote processwhetheropen release | `ps aux \| grep java \| grep -o "jmxremote[^]*"` | not enableuseremote process JMX, orset set doneAuthenticationand SSL |
| 58 | Debug modewhetherkey close | `ps aux \| grep java \| grep "agentlib:jdwp"` | no output out(generate asset not open debug Port) |

### 3.6 Tomcat version version

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 59 | Tomcat version versionwhetherthrough old | `$CATALINA_HOME/bin/version.sh 2>/dev/null \|\| java -cp $CATALINA_HOME/lib/catalina.jar org.apache.catalina.util.ServerInfo` | when first large version versionofmost newSecuresupplement version version |

---

## 4. MySQL Security Configuration

### 4.1 AuthenticationandUser

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 60 | root whether hasPassword | `mysql -u root -e "SELECT 1" 2>&1` | report error `Access denied`(hasPasswordprotect protect) |
| 61 | whether existsAnonymous User | `mysql -e "SELECT user,host FROM mysql.user WHERE user=''"` | noResult |
| 62 | whether existsBlank PasswordUser | `mysql -e "SELECT user,host FROM mysql.user WHERE authentication_string='' OR authentication_string IS NULL"` | noResult |
| 63 | root whetherlimit make remote processLogin | `mysql -e "SELECT user,host FROM mysql.user WHERE user='root'"` | host onlyas localhost/127.0.0.1 |
| 64 | whetherDelete test Database | `mysql -e "SHOW DATABASES LIKE 'test'"` | noResult |
| 65 | businessAccountPermissionmost small ize | `mysql -e "SHOW GRANTS FOR 'appuser'@'localhost'"` | only business needofmost smallPermission, no GRANT OPTION |
| 66 | whetheroperatelinesthrough mysql_secure_installation | combineCheckabove description 60-64 | AllPass |

### 4.2 Networkandmonitor

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 67 | BindingAddress | `grep "bind-address" /etc/my.cnf /etc/mysql/my.cnf /etc/mysql/mysql.conf.d/mysqld.cnf 2>/dev/null` | `bind-address = 127.0.0.1` |
| 68 | skip-networking(such asnotrequiresremote process) | `grep "skip-networking" /etc/my.cnf /etc/mysql/my.cnf 2>/dev/null` | such asif only version machineApplicationaccess ask, create protocol enableuse |
| 69 | Portwhether isdefault auth 3306 | `grep "port" /etc/my.cnf \| head -1` | create protocol update changeasNon-default authPort(manipulate deep defense defense) |

### 4.3 FileandPermission

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 70 | local-infile whether disabled | `mysql -e "SHOW VARIABLES LIKE 'local_infile'"` | `OFF` |
| 71 | symbolic-links whether disabled | `mysql -e "SHOW VARIABLES LIKE 'symbolic_links'"` or `grep "symbolic-links" /etc/my.cnf` | `skip-symbolic-links` orvalueas `OFF` |
| 72 | secure_file_priv whetherset set | `mysql -e "SHOW VARIABLES LIKE 'secure_file_priv'"` | set setasspecial set directory recordor NULL(disable stop LOAD DATA OUTFILE) |
| 73 | Datadirectory recordPermission | `ls -la /var/lib/mysql/` | attribute primary mysql:mysql, Permission 750 |
| 74 | ConfigurationFilePermission | `ls -la /etc/my.cnf /etc/mysql/my.cnf 2>/dev/null` | Permission 640 orupdate severe format |

### 4.4 Logandaudit plan

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 75 | errorLogwhetheropen enable | `mysql -e "SHOW VARIABLES LIKE 'log_error'"` | hasValidPath |
| 76 | check queryLog | `mysql -e "SHOW VARIABLES LIKE 'slow_query_log'"` | `ON`(generate asset environment environment create protocol open enable) |
| 77 | wildusecheck queryLog(generate asset key close) | `mysql -e "SHOW VARIABLES LIKE 'general_log'"` | `OFF`(generate asset not open, ness can impact response large andCancanRecordsensitive sensitiveData) |
| 78 | two advance makeLog | `mysql -e "SHOW VARIABLES LIKE 'log_bin'"` | `ON`(usefor repeatandaudit plan) |

### 4.5 other

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 79 | MySQL version version | `mysql --version` | no already notifyHigh Risk CVE ofversion version |
| 80 | Passwordpolicy strategy(5.7+) | `mysql -e "SHOW VARIABLES LIKE 'validate_password%'"` | enableusePasswordValidate item, policy strategy MEDIUM oror more |

---

## 5. Redis Security Configuration

### 5.1 Authenticationandaccess ask

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 81 | whetherset set donePassword | `grep "^requirepass" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | `requirepass <strongPassword>`(Non-Empty/Non- foobared) |
| 82 | BindingAddress | `grep "^bind" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | `bind 127.0.0.1`(notBinding 0.0.0.0) |
| 83 | protected-mode | `grep "^protected-mode" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | `protected-mode yes` |
| 84 | whetheras root operatelines | `ps aux \| grep redis-server \| grep -v grep \| awk '{print $1}'` | Non- root(such as redis User) |

### 5.2 risk Command

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 85 | disableuse/serious fatal name risk Command | `grep -E "^rename-command" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | at leastserious fatal namethe followingCommand:`FLUSHALL`/`FLUSHDB`/`CONFIG`/`KEYS`/`DEBUG`/`EVAL` |
| 86 | CONFIG CommandwhetherCanremote processExecute | `redis-cli -a <password> CONFIG GET dir 2>/dev/null` | be reject rejectoralready serious fatal name |

### 5.3 hold izeandFile

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 87 | RDB/AOF Filedirectory recordPermission | `ls -la $(grep "^dir" /etc/redis/redis.conf \| awk '{print $2}')` | attribute primary redis, Permission 750 |
| 88 | LogFile | `grep "^logfile" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | specified towardValidPath, Non-Empty |

### 5.4 version versionandNetwork

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 89 | Redis version version | `redis-server --version` | >= 6.0(support hold ACL), no already notifyHigh Risk CVE |
| 90 | most large internal exist limit make | `grep "^maxmemory" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | set set done above limit(defense stop OOM) |
| 91 | super time judge openEmpty continuous connect | `grep "^timeout" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null` | set set combine manage value(such as 300) |

---

## 6. ApplicationlayerSecure(wilduseCheck)

### 6.1 Sensitive Information

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 92 | ConfigurationFileinwhether hasclear textPassword | `grep -rn -iE "(password\|passwd\|secret\|api.key)\s*=" /path/to/app/conf/ \| head -20` | Passworduseuseadd secretStorageorenvironment environment change quantity inject inject, Non-clear text |
| 93 | Databasecontinuous connect stringwhetheradd secret | CheckApplicationof `application.properties` / `server.xml` of DataSource | useuse Jasypt add secretorenvironment environment change quantity |
| 94 |.git directory recordwhetherexpose exposurein Web root directory record | `ls -la /path/to/webroot/.git 2>/dev/null` | not existin, or Nginx alreadyIntercept |
| 95 | prepare copyFilewhetherexpose exposure | `find /path/to/webroot -name "*.bak" -o -name "*.sql" -o -name "*.tar.gz" -o -name "*.zip" 2>/dev/null` | no prepare copyFilein Web Canaccess ask directory record |

### 6.2 LogSecure

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 96 | LoginwhetherRecordSensitive Information | `grep -rn -iE "(password\|token\|secret\|credit.card)" /path/to/app/logs/ \| head -10` | noSensitive Informationoutput outtoLog |
| 97 | Logwhether hasrotate transfer machine make | `ls /etc/logrotate.d/ \| grep -iE "nginx\|tomcat\|mysql\|redis"` | existinforshouldof logrotate Configuration |

---

## 7. set time any serviceandafter rank check

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 98 | Can crontab | `for u in $(cut -f1 -d: /etc/passwd); do echo "==$u=="; crontab -u $u -l 2>/dev/null; done` | noCanofDownload/reverse shell any service |
| 99 | Can open machine enable dynamicitems | `systemctl list-unit-files --state=enabled` | no not auth identifyofservice |
| 100 | CanNetworkcontinuous connect | `ss -tlnp; ss -tnp \| grep ESTABLISHED` | no continuous connecttoCan external part IP/Port(such as IRC 6667/reverse shell) |
| 101 | abnormal common SUID File | `find / -perm -4000 -type f 2>/dev/null` | onlySystemidentifier accurate SUID File(passwd, sudo, ping etc.) |
| 102 | /tmp directory recordCanFile | `ls -la /tmp/ /var/tmp/ /dev/shm/` | noCanScriptortwo advance makeFile |
| 103 | authorized_keys whetherbe tamper change | `find /root /home -name "authorized_keys" -exec md5sum {} \;` | only include include already notifyofcompany |

---

## 8. prepare copyand repeat

| # | Check Item | Check Command | SecureStatus |
|---|--------|----------|----------|
| 104 | MySQL whether hasset period prepare copy | `crontab -l \| grep -i "mysqldump\|xtrabackup"` | existinset period prepare copy plan |
| 105 | prepare copyFilewhetheradd secretStorage | `file /path/to/backup/*.sql*` | useuse gpg add secretorStorageinadd secret |
| 106 | prepare copywhether hasabnormal version | check whether there is OSS/S3 same stepScript | at leastone copy abnormal prepare copy |
| 107 | ECS fast photo policy strategy | Alibaba CloudConsole > ECS > fast photo policy strategy | open enable self dynamic fast photo, protect retain >= 7 days |

---

## 9. Alibaba Cloudspecial setCheck

| # | Check Item | Checkmethod mode | SecureStatus |
|---|--------|----------|----------|
| 108 | RAM subAccountPermission | Alibaba CloudConsole > RAM > User | follow most smallPermissionprinciple rule, no allPermissionsubAccount |
| 109 | AccessKey DisclosureCheck | `grep -rn "LTAI" /path/to/app/ 2>/dev/null` | Code/Configurationinno hardEncoding AK |
| 110 | /cloudSecureincore | Alibaba CloudConsole > cloudSecureincore | already and no not handle manage report alert |
| 111 | ECS realcasesyuanDataaccess ask limit make | `curl -s --connect-timeout 2 http://100.100.100.200/latest/meta-data/` | Applicationinternal partshould notcan meaning access ask(defense SSRF) |

---

## CheckPrioritycreate protocol

**P0 - standalone that is fix repeat(CanbeDirectexploituse):**
- Redis noPassword + Binding 0.0.0.0(#81, #82) - directly usablewrite crontab reverse shell
- MySQL root noPasswordorallow allow remote processLogin(#60, #63, #67)
- Tomcat Manager useusedefault auth credential accordingCanaccess ask(#38, #39)
- AJP continuous connect device open release(Ghostcat vulnerability)(#46)
- SSH root PasswordLogin(#1, #2)

**P1 - fast fix repeat(large attack attack page):**
- service as root operatelines(#6, #54, #84)
- Securearray through degree open release(#10, #11, #12, #13)
- sensitive sensitivePath/default authApplicationnot move remove(#31, #41)
-.git / prepare copyFileexpose exposure(#94, #95)
- CodeinhardEncoding AK(#109)

**P2 - plan fix repeat(manipulate deep defense defense):**
- HTTPS ConfigurationHardening(#19-#24)
- SecureResponseHeader(#25-#29)
- version versionInformation Disclosure(#16, #42)
- Logandaudit plan complete (#75-#78, #96-#97)
- prepare copy policy strategy(#104-#107)

---

## fast rate one keyScanScript

willthe followingScriptprotect existas `quick-check.sh`, in ECS above as root Execute, fast rateObtainkey risk point:

```bash
#!/bin/bash
echo "====== fast rateSecureCheck ======"

echo -e "\n[1] SSH Configuration"
grep -E "^(PermitRootLogin|PasswordAuthentication|Port)" /etc/ssh/sshd_config 2>/dev/null

echo -e "\n[2] service operatelinesUser"
ps aux | grep -E "(java|mysql|redis|nginx)" | grep -v grep | awk '{print $1, $11}' | sort -u

echo -e "\n[3] monitor Port"
ss -tlnp | grep -E "(3306|6379|8080|8443|8005|22)"

echo -e "\n[4] Redis Password"
grep "^requirepass" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null || echo "alert report: not to requirepass Configuration!"

echo -e "\n[5] Redis BindingAddress"
grep "^bind" /etc/redis/redis.conf /etc/redis.conf 2>/dev/null

echo -e "\n[6] MySQL BindingAddress"
grep "bind-address" /etc/my.cnf /etc/mysql/my.cnf /etc/mysql/mysql.conf.d/mysqld.cnf 2>/dev/null

echo -e "\n[7] Tomcat AJP"
grep -i "AJP" $CATALINA_HOME/conf/server.xml 2>/dev/null | grep -v "<!--"

echo -e "\n[8] Tomcat Manager User"
grep -v "<!--" $CATALINA_HOME/conf/tomcat-users.xml 2>/dev/null | grep -i "user "

echo -e "\n[9] Nginx server_tokens"
grep "server_tokens" /etc/nginx/nginx.conf 2>/dev/null

echo -e "\n[10] Can crontab"
for u in $(cut -f1 -d: /etc/passwd); do crontab -u $u -l 2>/dev/null | grep -v "^#" | grep -v "^$"; done

echo -e "\n[11] SUID File"
find / -perm -4000 -type f 2>/dev/null | grep -v -E "/(sudo|passwd|ping|mount|umount|su|chfn|chsh|newgrp|gpasswd|pkexec)"

echo -e "\n[12] Securearray(needinAlibaba CloudConsoleConfirm)"
echo "please mobile dynamicCheckSecurearray scale rule:only open release 80/443/SSH"

echo -e "\n====== Checkcomplete ======"
```

---

> **useusecreate protocol**:one-by-one sectionCheck, priority first handle manage P0 level ask problem.each fix repeat oneitems, inforshouldlinesidentifier inject `[already fix repeat] + day period`, operationasinteger changeRecordretain.
