# Java Spring Boot Information DisclosureComprehensiveInvestigation ChecklistandTest Plan

> based on WooYun Methodcomment | Datacome source:22,132 real real vulnerabilityCase | Information DisclosureDomain:6,446 Case, 64.7% High Risk

---

## 1. background sceneandScope

**trigger initiate scenario scene:** itemsdirectory be report Spring Boot Actuator Endpointexpose exposure, domain need require above line firstComprehensiverank checkInformation Disclosurerisk.

**Methodcomment base foundation:** WooYun DatacollectinInformation Disclosure(4,858 + 1,588 Case)isAllattack attackof ize -- Disclosureofinformation can enable dynamicAccountconnect manage/Internal Network /precision accurate exploituseetc.after continue attack attack link.Actuator expose exposure only is one, mustSystemness rank check.

**WooYun Statisticsalert show:**
- Information DisclosureCasetotal number:6,446, Among them 64.7% asHigh Risk
- MisconfigurationCasetotal number:1,796, Among them 72.6% asHigh Risk
- Spring Boot Actuator No Authentication by Defaultofout current frequency rate:**Critical**

---

## 2. fourPhaseMethodcomment approx description

| Phase | key dynamic | identifier accurate |
|------|---------|---------|
| 1. map map | manageAllexpose exposure page:Endpoint/File/ResponseHeader/error page | Completeresource asset clear single already create standalone |
| 2. false set | based on WooYun mode completeInformation Disclosurefalse set | >=10 by impact response rank sequenceoffalse set |
| 3. test | one-by-oneitemsmobile dynamicValidate, RecordRequest/Response | Eachfalse set hasEvidencesupport holdorreverse |
| 4. report | Business Impactassess assess/Remediation Recommendation | EachDiscoverattach WooYun modeCategory |

---

## 3. Investigation Checklist(total 8 large type/42 Check Item)

### No. 1 type:Spring Boot Actuator Endpointexpose exposure [Severe]

**WooYun mode:** Misconfiguration / expose exposureofmanage manage boundary page(1,796 Case, 72.6% High Risk)
**WooYun Case References:** Spring Boot Actuator No Authentication by Default, out current frequency rate"Critical", and JBoss/Tomcat manage manageConsoleexpose exposure same type

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 1.1 | `/actuator` primaryEndpointwhetherCanUnauthorized Access | Severe | `curl -s https://target/actuator` |
| 1.2 | `/actuator/env` environment environment change quantityDisclosure | Severe | CheckResponsewhetherinclude includeDatabasePassword/API Key/Keyetc. |
| 1.3 | `/actuator/heapdump` stack internal exist transfer | Severe | Download heapdump, use `jhat` or Eclipse MAT Analyze, searchPassword/Key/Sessioncommand card |
| 1.4 | `/actuator/configprops` Configurationattributes | High | CheckDatasourcePassword/No. three method service credential according |
| 1.5 | `/actuator/mappings` route map map | High | expose exposureAll API Endpoint, include internal part/manage manageInterface |
| 1.6 | `/actuator/beans` Bean list | in | expose exposureApplicationarchitecture structure/array item list |
| 1.7 | `/actuator/trace` or `/actuator/httptrace` | Severe | expose exposure most Requesthistory history, Cancan include Cookie/Authorization Header |
| 1.8 | `/actuator/logfile` LogFile | High | LoginCancan includeUserData/SQL /abnormal common stack stack |
| 1.9 | `/actuator/shutdown` key closeEndpoint | Severe | POST Requestdirectly usablekey closeApplication(DoS) |
| 1.10 | `/actuator/jolokia` JMX expose exposure | Severe | CanPass JMX ExecuteArbitraryCode(RCE) |

**testScript:**
```bash
# Batchprobe test Actuator Endpoint
ENDPOINTS="actuator actuator/env actuator/heapdump actuator/configprops \
actuator/mappings actuator/beans actuator/httptrace actuator/logfile \
actuator/shutdown actuator/jolokia actuator/info actuator/health \
actuator/metrics actuator/conditions actuator/scheduledtasks \
actuator/threaddump actuator/caches actuator/flyway actuator/liquibase"

for ep in $ENDPOINTS; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "https://target/$ep")
 echo "$ep -> HTTP $STATUS"
done
```

**inject meaningPathvariant:** same time testthe followingPathprefix:
- `/actuator/xxx`(Spring Boot 2.x default auth)
- `/xxx`(Spring Boot 1.x default auth, such as `/env`/`/trace`/`/dump`)
- `/manage/xxx`(self set define management context-path)
- `/admin/actuator/xxx`(self set define prefix)

---

### No. 2 type:API Responsethrough degree expose exposure [High Risk]

**WooYun mode:** sensitive sensitiveDataDisclosure / API through degreeObtain(1,588 Case, 62.8% High Risk)
**WooYun Case References:**
- EmailDisclosureCausing 600+ personInformation Disclosure
- TCL a systemMisconfiguration Leading To 600 ten-thousand clientName/mobile machine/ Disclosure
- percent large vulnerability risk involving 2000W personDetailedinformation

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 2.1 | API ResponsewhetherReturndone UI not showofmany Field | High | for ratio API JSON ResponseFieldnumberandFrontendpage showFieldnumber |
| 2.2 | UserinformationInterfacewhetherReturnPasswordhash hash | Severe | Check `/api/user/info`/`/api/profile` etc.Response |
| 2.3 | listInterfacewhetherReturnCompletefor whileNon- need | High | Checkpart page list API whetherinclude includemobile number/Email/Identity Cardetc. |
| 2.4 | UsersearchInterfacewhetherCanTraversal | High | Attempt `/api/users?page=1&size=9999` orTraversal ID |
| 2.5 | Export/Downloadfunction canwhether hasPermissioncontrol make | Severe | test `/export`/`/download`/`/report` Endpoint |
| 2.6 | sequence list izeConfigurationwhetherrank remove done sensitive sensitiveField | High | Check Jackson `@JsonIgnore` whethercorrect confirm identifier inject |

**key specified identifier:** API ResponseFieldnumber > UI CanseenFieldnumber = existinthrough degree expose exposure

---

### No. 3 type:error informationandabnormal common handle manage [High Risk]

**WooYun mode:** Source Code/Configuration Disclosure - error information(4,858 Case)
**WooYun Case References:** map client manyDatabaseServerbecause error information expose exposure internal part architecture structure after flaw

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 3.1 | 500 errorwhetherReturnCompletestack stack | High | Send Requesttrigger initiate abnormal common, ObserveResponse Body |
| 3.2 | Databaseerrorwhetherexpose exposure SQL andtable result structure | High | SendNon-methodParameter(single cite number/super long character symbol string), Checkerror detailed details |
| 3.3 | 404 pagewhetherexpose exposure framework architectureandversion version information | in | access ask not existinofPath, Check Whitelabel Error Page |
| 3.4 | ParameterValidateerrorwhetherexpose exposure internal part type name | in | Sendtype not match configofParameter, Check `MethodArgumentNotValidException` detailed details |
| 3.5 | `spring.mvc.throw-exception-if-no-handler-found` Configuration | in | Checkwhetheropen enable, result combine all global abnormal common handle manage device |

**Test Method:**
```
# trigger initiate each type error
1. SendEmpty JSON bodytorequiresParameterof POST Interface
2. Sendsuper large number valuetonumber characterField(such as id=99999999999999999)
3. SendSpecial Characterstocharacter symbol stringField(such as name=<script>/name='OR 1=1)
4. Requestnot existinofEndpoint(such as /api/v99/nonexistent)
5. Senderrorof Content-Type(such as text/plain toperiod JSON ofInterface)
```

---

### No. 4 type:version version control makeandprepare copyFileDisclosure [Severe]

**WooYun mode:** Source Code/Configuration Disclosure - version version control makeDisclosure(4,858 Case, 64.7% High Risk)
**WooYun Case References:** new networkCommandExecuteCausing 45 ten-thousandUserInformation Disclosure(Source Code/Configurationtype)

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 4.1 | `/.git/config` Git repository libraryDisclosure | Severe | such asCanaccess ask, use GitHack/git-dumper Completesource code |
| 4.2 | `/.svn/entries` SVN repository libraryDisclosure | Severe | Check HTTP 200 Response |
| 4.3 | `/WEB-INF/web.xml` Java Configuration Disclosure | Severe | expose exposure Servlet map map/Filter link/Security Configuration |
| 4.4 | `/WEB-INF/classes/application.yml` | Severe | expose exposureDatabasecontinuous connect/Redis Passwordetc.AllConfiguration |
| 4.5 | prepare copyFileprobe test | High | Check `/backup.zip`/`/backup.sql`/`/[Domain Name].zip` etc. |
| 4.6 | `.bak`/`.old`/`.swp` File | High | Check `/application.yml.bak`/`/config.properties.old` |
| 4.7 | `/src/main/resources/application.yml` | High | Directaccess ask source codePath |

**Batchprobe testScript:**
```bash
PATHS=".git/config.git/HEAD.svn/entries.svn/wc.db \
WEB-INF/web.xml WEB-INF/classes/application.yml \
WEB-INF/classes/application.properties \
WEB-INF/classes/bootstrap.yml \
backup.zip backup.sql db.sql database.sql \
application.yml.bak application.properties.bak.env"

for p in $PATHS; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "https://target/$p")
 ["$STATUS"!= "404"] && echo "[!] $p -> HTTP $STATUS"
done
```

---

### No. 5 type:HTTP ResponseHeaderInformation Disclosure [Medium Risk]

**WooYun mode:** sensitive sensitiveDataDisclosure - keyDiscoverspecified identifier
**defense defense participate reference:** WooYun Methodcomment clear confirm need require"Delete Server/X-Powered-By/X-AspNet-Version"

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 5.1 | `Server` Headerexpose exposure Web Serverversion version | in | `curl -I https://target/` CheckResponseHeader |
| 5.2 | `X-Powered-By` expose exposure framework architecture information | in | same above |
| 5.3 | `X-Application-Context` expose exposure Spring Applicationinformation | in | Spring Boot 1.x default auth open enable |
| 5.4 | self set define errorHeaderexpose exposure internal part information | Low | CheckAllNon-identifier accurateResponseHeader |
| 5.5 | missing lessSecureResponseHeader | in | Check `X-Content-Type-Options`/`X-Frame-Options`/`Strict-Transport-Security`/`Content-Security-Policy` |
| 5.6 | `Cache-Control` MissingCausingsensitive sensitive page be exist | High | alreadyAuthenticationpagewhetherset set `no-store` |

---

### No. 6 type:Swagger/API Documentexpose exposure [High Risk]

**WooYun mode:** Source Code/Configuration Disclosure - debugging/testEndpoint

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 6.1 | `/swagger-ui.html` or `/swagger-ui/index.html` | High | expose exposureAll API set define/Parameter/model type |
| 6.2 | `/v2/api-docs` or `/v3/api-docs` | High | principle initial OpenAPI JSON/YAML |
| 6.3 | `/api-docs` | High | same above |
| 6.4 | `/doc.html`(Knife4j) | High | national assetitemsdirectoryHighfrequency useuseofincrease strong Swagger |
| 6.5 | `/druid/index.html`(Druid monitor control) | Severe | expose exposure SQL ExecuteLog/continuous connect Status/ check query |
| 6.6 | `/h2-console`(H2 DatabaseConsole) | Severe | directly usableExecute SQL, internal existDatabasecommonusefor open initiate |

**probe testScript:**
```bash
DOC_PATHS="swagger-ui.html swagger-ui/index.html v2/api-docs v3/api-docs \
api-docs doc.html druid/index.html druid/login.html h2-console \
graphql graphiql"

for p in $DOC_PATHS; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "https://target/$p")
 ["$STATUS"!= "404"] && echo "[!] $p -> HTTP $STATUS"
done
```

---

### No. 7 type:LoganddebuggingInformation Disclosure [High Risk]

**WooYun mode:** sensitive sensitiveDataDisclosure - LogFileCanaccess ask(1,588 Case)
**WooYun Case References:** Sunshine InsuranceSensitive InformationDisclosureCausingSuccessadvance injectInternal NetworkSystem(vertical many platform operations primary machine)

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 7.1 | `/logs/`/`/log/` directory recordwhetherCanaccess ask | Severe | Checkdirectory record listwhether enabled |
| 7.2 | `/access.log`/`/error.log` LogFileDirectCanDownload | High | Direct URL access ask |
| 7.3 | LoginwhetherRecorddone clear textPassword | Severe | Codeaudit plan:CheckLoginInterfaceLogwhetherRecord password Parameter |
| 7.4 | LoginwhetherRecorddoneCompleteRequest Body | High | Check `CommonsRequestLoggingFilter` Configuration |
| 7.5 | LoginwhetherRecorddoneUserSensitive Information(mobile machine/Identity Card) | High | Codeaudit plan:search `log.info`/`log.debug` in connectofUserData |
| 7.6 | generate asset environment environmentLoglevel levelwhether is DEBUG | High | Check `application.yml` in `logging.level` Configuration |

---

### No. 8 type:ClientandFrontendInformation Disclosure [Medium Risk]

**WooYun mode:** sensitive sensitiveDataDisclosure - ClientStorage / HTML/JS inject

| ID | Check Item | Risk Level | Test Method |
|------|--------|---------|---------|
| 8.1 | HTML inject inwhetherinclude include internal part information | Low | ViewpageSource Code, search `<!-- -->` |
| 8.2 | JavaScript inwhetherhardEncoding API Key/Key | Severe | search JS Fileinof `apiKey`/`secret`/`password`/`token` |
| 8.3 | Frontend JS whetherinclude includeComplete Source Map | High | Check `.map` FilewhetherCanaccess ask, Can principle source code |
| 8.4 | localStorage/sessionStorage whetherStorageSensitive Information | in | Browser DevTools Check |
| 8.5 | URL inwhetherpass recursive sensitive sensitiveParameter(GET Request) | High | CheckSessioncommand card/User ID whetherin URL Parameterin(Referer Disclosurerisk) |
| 8.6 | CORS Configurationwhether iswild config symbol `*` | High | Check `Access-Control-Allow-Origin` ResponseHeader |

---

## 4. Spring Boot specialitemsdeep degree rank check

### 4.1 ConfigurationFileSecureaudit plan

```yaml
# application.yml / application.properties inmustCheckofConfigurationitems

# 1. Actuator Secure
management:
 endpoints:
 web:
 exposure:
 include: health,info # only expose exposure must needEndpoint, rejectcannotis "*"
 endpoint:
 shutdown:
 enabled: false # disable stop remote process key close
 env:
 enabled: false # disable stop environment environment change quantity expose exposure
 heapdump:
 enabled: false # disable stop stack transfer
 server:
 port: -1 # most real:manage managePortnot for external, orBindingInternal NetworkAddress

# 2. error handle manage
server:
 error:
 include-stacktrace: never # reject notReturnstack stack
 include-message: never # notReturnprinciple initial error message
 include-binding-errors: never
 include-exception: false
 whitelabel:
 enabled: false # disableusedefault auth error page

# 3. Swagger(generate asset environment environment)
springfox:
 documentation:
 enabled: false # generate asset environment environment disableuse
springdoc:
 api-docs:
 enabled: false
 swagger-ui:
 enabled: false

# 4. H2 Console
spring:
 h2:
 console:
 enabled: false # generate asset environment environmentmustdisableuse

# 5. Druid monitor control
spring:
 datasource:
 druid:
 stat-view-servlet:
 enabled: false # orset set strongPassword + IP Whitelist
```

### 4.2 CodelevelCheckclear single

| Check Item | search mode | Description |
|--------|---------|------|
| all global abnormal common handle manage device | `@ControllerAdvice` / `@ExceptionHandler` | Confirmexistinand notReturnstack stack information |
| Jackson sequence list ize rank remove | `@JsonIgnore` / `@JsonProperty(access=WRITE_ONLY)` | Password/KeyFieldmustidentifier inject |
| Logleak sensitive | `log.info` / `log.debug` + UserData | Confirmsensitive sensitiveFieldalready leak sensitive |
| hardEncodingcredential according | `password =` / `secret =` / `apiKey =` | search source codeinofhardEncodingKey |
| Spring Security Configuration | `WebSecurityConfigurerAdapter` / `SecurityFilterChain` | Check Actuator Endpointwhether inject appraise permission |
| CORS Configuration | `@CrossOrigin` / `CorsConfiguration` | Checkwhetherlimit make done allow allowof Origin |
| FileUploadPath | `MultipartFile` + StoragePath | UploadFilewhetherin Web Canaccess ask directory record |

---

## 5. testExecutemethod plan

### 5.1 Test Environmentaccurate prepare

| itemsdirectory | need require |
|------|------|
| Test Account | at least 2 Regular User + 1 Administrator(usefor bypass permission for ratio) |
| Tool | Burp Suite / mitmproxy(Request Interception)/curl(Endpointprobe test)/Eclipse MAT(heapdump Analyze) |
| Network | fromexternal network test(model attack attack person)+ Internal Network (Checkinternal part expose exposure) |
| Code | source code access askPermission(config combine audit plan) |

### 5.2 testExecuteorder sequence

by WooYun high-risk percentagerank sequence, priority first test impact response most largeofCategory:

```
Phase 1 - fast rateScan(30 minutes)
+-- 1.1-1.10 Actuator EndpointBatchprobe test
+-- 4.1-4.7 version version control make/prepare copyFileprobe test
+-- 6.1-6.6 Swagger/Druid/H2 probe test
+-- output out:expose exposure page clear single

Phase 2 - deep degreeValidate(2-4 hours)
+-- forPhase 1 Discoverofexpose exposureEndpointone by one deep injectAnalyze
+-- 2.1-2.6 API ResponseFieldaudit plan(packet capture for ratio UI)
+-- 3.1-3.5 error handle manage test(structure forge Request)
+-- output out:Confirmofvulnerability list

Phase 3 - Codeaudit plan(2-4 hours)
+-- 7.1-7.6 LogConfigurationandcontent audit plan
+-- 4.2 CodelevelSecureCheck
+-- application.yml Security Configurationaudit plan
+-- output out:Codelayer page risk clear single

Phase 4 - Frontendand combine(1-2 hours)
+-- 8.1-8.6 FrontendInformation DisclosureCheck
+-- 5.1-5.6 ResponseHeaderSecureCheck
+-- crossCategorykey connectAnalyze
+-- output out:Completerank check report
```

### 5.3 false set dynamic test model template

forEachDiscoverofask problem, bythe followingresult structureRecord:

```
false set:[business flow process X] existin [Information Disclosuretype Y] risk
principle because:[ConcreteEvidence -- Canaccess askofEndpoint/Responseinofmany Field/errorinofstack stack]
WooYun mode:[match configof WooYun mode name name]
impact response:[Business Impact -- DataDisclosureScope/Cancanofattack attack link]
Test Steps:
 1. [ConcreteRequest]
 2. [expected period vs Actual Result]
Remediation Recommendation:[Serverend fix repeat, not isFrontend cover]
```

---

## 6. WooYun real realCasealert show

the followingCaseDescriptionInformation Disclosureofreal real after if, Eachall is WooYun personDiscoverofreal real vulnerability:

| Case | Disclosuretype | impact response scale model | lesson lesson |
|------|---------|---------|------|
| TCL a systemMisconfiguration Leading To 600 ten-thousand clientInformation Disclosure | Personal InformationDisclosure | 600 ten-thousand client accountName/mobile machine/ | Misconfiguration = large scale modelDataDisclosure |
| percent large vulnerability risk involving 2000W Personal Information | Personal InformationDisclosure | 2000 ten-thousand condition(Name/Identity Card/mobile machine/) | API not doPermissioncontrol makeandFieldthrough filter |
| map client manyDatabaseServer flaw | Source Code/Configuration Disclosure | many platformDatabaseServer | error information expose exposure architecture structure -> precision accurate attack attack |
| new networkCommandExecuteCausing 45 ten-thousandUserInformation Disclosure | Source Code/Configuration Disclosure | 45 ten-thousandUserRecord | ConfigurationFileDisclosure -> RCE -> Database |
| Sunshine InsuranceSensitive InformationDisclosureCausingadvance injectInternal Network | credential accordingDisclosure | many platform operations primary machine | Information Disclosure -> Internal Network attack attack |
| EmailDisclosure | Personal InformationDisclosure | 600+ User | API through degreeReturnField |
| pass ize collect itemSysteminternal partSensitive InformationDisclosure | internal partSystemexpose exposure | integer itemSystem | manage manage boundary page not doAccess Control |
| micro primary SQL inject inject impact response 860W person/46W generate | error information -> SQL inject inject | 860 ten-thousand person + 46 ten-thousand generate | error information expose exposureDatabaseresult structure -> inject inject |
| ChinaCache JBoss Misconfiguration Leading To Getshell | expose exposure manage manage boundary page | Server root Permission | manage manageConsoleDefault Credentials |
| DaoCloud Weak Credentials + Docker Remote API Unauthorized | Default Credentials | Container | Default Configuration = zero complete version inject |

**keyStatistics:**
- WooYun 6,446 Information DisclosureCasein, 64.7% be assessasHigh Risk
- Misconfiguration 1,796 Casein, 72.6% asHigh Risk
- Spring Boot Actuator Unauthorized Accessin WooYun out current frequency rateas"Critical"
- API through degree expose exposure isPersonal InformationDisclosureof need toward quantity

---

## 7. fix repeatPrioritymatrix matrix

| Priority | riskitems | fix repeat | SLA |
|--------|--------|---------|-----|
| P0 (standalone that is) | Actuator sensitive sensitiveEndpointexpose exposure | key closeoradd appraise permission, only protect retain `/health` and `/info` | above line firstmustcomplete |
| P0 (standalone that is) | heapdump/env Canaccess ask | `management.endpoint.*.enabled: false` | above line firstmustcomplete |
| P0 (standalone that is) | Swagger/Druid/H2 generate asset environment environment expose exposure | Pass Profile disableuseoradd appraise permission | above line firstmustcomplete |
| P0 (standalone that is) |.git/prepare copyFileCanaccess ask | Nginx/Gatewaylayer deny scale rule | above line firstmustcomplete |
| P1 (24h) | API ReturnPasswordhash hash/many Field | `@JsonIgnore` + DTO mode | 24 hoursinternal |
| P1 (24h) | generate asset environment environmentReturnstack stack | all global abnormal common handle manage device + `include-stacktrace: never` | 24 hoursinternal |
| P1 (24h) | LoginRecordclear textPassword | Logleak sensitive framework architecture(such as Logback MaskingPattern) | 24 hoursinternal |
| P2 (1cycle) | ResponseHeaderexpose exposure version version information | move remove `Server`/`X-Powered-By` Header | 1 cycle internal |
| P2 (1cycle) | CORS Configurationaswild config symbol | limit makeasConcreteDomain Name | 1 cycle internal |
| P2 (1cycle) | Frontend Source Map Canaccess ask | generate asset structure create disableuse source map orlimit make access ask | 1 cycle internal |
| P3 (hold continue) | SecureResponseHeaderMissing | Add CSP/HSTS/X-Content-Type-Options | hold continue priority ize |
| P3 (hold continue) | Loglevel level throughLow(DEBUG) | generate asset environment environment setas WARN/ERROR | hold continue priority ize |

---

## 8. hold continueProtection Recommendations

### architecture structure layer page
1. **Actuator EndpointBindingInternal NetworkPort:** `management.server.port=8081` + defense only allow allowInternal Networkaccess ask
2. **Spring Security Interceptmanage manageEndpoint:** All `/actuator/**` Pathneed requireAdministratorRole
3. **WAF scale rule:** stop external part access ask `/.git`/`/.svn`/`/.env`/`/backup*`/`/WEB-INF/*`
4. **CDN Configuration:** not exist alreadyAuthenticationofResponse(`Cache-Control: no-store`)
5. **reverse toward code manage layer through filter:** Nginx move remove `Server`/`X-Powered-By` etc.informationHeader

### monitor control layer page
1. **sensitive sensitivePathaccess ask report alert:** external part IP access ask `/actuator`/`/.git`/`/.env`/`/admin` time trigger initiate report alert
2. **BatchDataaccess ask report alert:** large type API ResponseorHighfrequencyDataRequesttime report alert
3. **500 error rate monitor control:** abnormal common increaseCancan meaning attack attack personinadvancelines
4. **credential accordingDisclosureScan:** set periodin GitHub/GitLab/Pastebin above searchitemsdirectory keywords

### open initiate scale scope
1. **DTO mode strong make:** All API Interfaceuseuse DTO Return, disable stopDirectReturn Entity
2. **all global abnormal common handle manage device:** `@ControllerAdvice` system one handle manage, generate asset environment environment onlyReturnerror code
3. **Profile isolation:** Swagger/Druid/H2 onlyin `dev`/`test` Profile under enableuse
4. **Codeaudit check Checklist:** PR audit check timemustCheckInformation Disclosureitems(Log/ResponseField/error handle manage)

---

> version method plan based on WooYun Business Logic Vulnerability Methodology v2.0, Datacome sourceas WooYun vulnerabilityDatabase(2010-2016)22,132 real realCaseinofInformation DisclosureDomain 6,446 CaseinvolvingMisconfigurationDomain 1,796 Case.
