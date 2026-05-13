# Java Spring Boot Information DisclosureComprehensiveInvestigation ChecklistandTest Plan

## 1. rank checkScopetotal

| risk domain | Risk Level | rank check serious point |
|--------|---------|---------|
| Actuator Endpointexpose exposure | High Risk | Check/environment environment change quantity/Configurationattributes/stack transfer |
| error handle manageandabnormal common information | High Risk | stack stack /SQL error/framework architecture version version number |
| ConfigurationFileandsensitive sensitiveData | High Risk | DatabasePassword/API Key/KeyhardEncoding |
| HTTP ResponseHeader | Medium Risk | Server Header/X-Powered-By/framework architecture specified pattern |
| API ResponseData | High Risk | through degreeReturnField/UserPrivate Data |
| state resource sourceanddirectory recordTraversal | Medium Risk |.git directory record/prepare copyFile/source codeDisclosure |
| Logoutput out | Medium Risk | sensitive sensitiveDatawrite injectLog/LogFilefor externalCanaccess ask |
| Swagger/OpenAPI Document | Medium Risk | InterfaceDocumentexpose exposure/debuggingEndpoint |
| Spring DevTools | High Risk | remote process debugging/self dynamic serious Endpoint |
| Databaseandinbetween itemConsole | High Risk | H2 Console/Druid Monitor/Redis Unauthorized |

---

## 2. one-by-oneitemsInvestigation ChecklistandTest Plan

### 2.1 Spring Boot Actuator Endpointexpose exposure

**background scene**:this is abovetimesbe reportofVulnerability Type, is Spring Boot mostHighfrequencyofInformation Disclosureask problem.

#### Investigation Checklist

- [] Check `application.yml` / `application.properties` in `management.endpoints.web.exposure.include` Configuration
- [] Check `management.server.port` whetherandprimaryServerinterface part separate
- [] Check `management.endpoints.web.base-path` whetherModifydone default authPath `/actuator`
- [] CheckeachEndpointwhetherConfigurationdone independent standaloneofSecureAuthentication
- [] Checkself set define Actuator Endpointwhether exists

#### High RiskEndpointclear single

| Endpoint | Disclosurecontent | Risk Level |
|------|---------|---------|
| `/actuator/env` | environment environment change quantity/Databasecontinuous connect string/API Key | High Risk |
| `/actuator/configprops` | AllConfigurationattributes involving value | High Risk |
| `/actuator/heapdump` | JVM stack transfer (Canprovide takePassword/Key/Session) | High Risk |
| `/actuator/threaddump` | line process information/internal part type name | Medium Risk |
| `/actuator/mappings` | All URL map map involving control make deviceMethod | Medium Risk |
| `/actuator/beans` | All Spring Bean involving depend rely key system | Medium Risk |
| `/actuator/conditions` | self dynamicConfigurationcondition assess assessResult | Low Risk |
| `/actuator/health` | Database/Redis/MQ etc.array item continuous connectStatusinvolving version version | Medium Risk |
| `/actuator/info` | Applicationinformation(Git commit/structure create version version) | Low Risk |
| `/actuator/metrics` | JVM internal exist/CPU/Requestplan numberetc.operatelinesspecified identifier | Low Risk |
| `/actuator/loggers` | Loglevel levelConfiguration(POST Candynamic stateModify) | Medium Risk |
| `/actuator/scheduledtasks` | set time any service list | Low Risk |
| `/actuator/httptrace` / `/actuator/httpexchanges` | most HTTP Requestinclude Header(Cancan include Token) | High Risk |
| `/actuator/shutdown` | key closeApplication(default auth key close, but needConfirm) | High Risk |
| `/actuator/jolokia` | JMX MBean operation(Can RCE) | High Risk |
| `/actuator/prometheus` | Prometheus specified identifierData | Low Risk |

#### Test Plan

```bash
# 1. base foundation probe test - Checkdefault authPath
BASE_URL="http://target:8080"
ENDPOINTS=("/actuator"
 "/actuator/env"
 "/actuator/configprops"
 "/actuator/heapdump"
 "/actuator/threaddump"
 "/actuator/mappings"
 "/actuator/beans"
 "/actuator/conditions"
 "/actuator/health"
 "/actuator/info"
 "/actuator/metrics"
 "/actuator/loggers"
 "/actuator/scheduledtasks"
 "/actuator/httptrace"
 "/actuator/httpexchanges"
 "/actuator/shutdown"
 "/actuator/jolokia"
 "/actuator/prometheus"
 "/actuator/caches"
 "/actuator/flyway"
 "/actuator/liquibase"
 "/actuator/sessions"
 "/actuator/startup"
 "/actuator/quartz"
 "/actuator/integrationgraph"
 "/actuator/sbom")

for ep in "${ENDPOINTS[@]}"; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}${ep}")
 echo "[${STATUS}] ${ep}"
done

# 2. variantPathprobe test(BypassPaththrough filter)
VARIANTS=("/actuator"
 "/Actuator"
 "/ACTUATOR"
 "/%61ctuator" # URL Encoding
 "/actuator/"
 "/actuator;.js" # Tomcat PathParameterBypass
 "/actuator%00" # Emptycharacter section intercept judge
 "//actuator"
 "/./actuator"
 "/manage" # old version Spring Boot 1.x Path
 "/admin"
 "/monitor")

for v in "${VARIANTS[@]}"; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}${v}/env")
 echo "[${STATUS}] ${v}/env"
done

# 3. self set define manage managePortprobe test
for PORT in 8081 8443 9090 9091 8180 18080; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" --connect-timeout 3 "http://target:${PORT}/actuator")
 echo "[${STATUS}] Port ${PORT} /actuator"
done

# 4. heapdump Analyze(such asCanDownload)
curl -s -o heapdump "${BASE_URL}/actuator/heapdump"
# useuse Eclipse MAT or jhat Analyze
# oruseuse JDumpSpider self dynamic provide takeSensitive Information:
# java -jar JDumpSpider.jar heapdump
```

#### SecureHardeningcreate protocol

```yaml
# application.yml infer Configuration
management:
 endpoints:
 web:
 exposure:
 include: health,info # only expose exposure must needEndpoint
 # include: "*" # reject for disable stop
 endpoint:
 health:
 show-details: never # not display array item detailed details
 env:
 enabled: false
 heapdump:
 enabled: false
 threaddump:
 enabled: false
 configprops:
 enabled: false
 mappings:
 enabled: false
 beans:
 enabled: false
 shutdown:
 enabled: false
 server:
 port: 19090 # manage managePortandprimary service part separate, onlyInternal NetworkCanaccess ask
```

---

### 2.2 error handle manageandabnormal commonInformation Disclosure

#### Investigation Checklist

- [] Checkwhether existsall global abnormal common handle manage device(`@ControllerAdvice` / `@RestControllerAdvice`)
- [] Check `server.error.include-stacktrace` Configurationvalue
- [] Check `server.error.include-message` Configurationvalue
- [] Check `server.error.include-binding-errors` Configurationvalue
- [] Check `server.error.include-exception` Configurationvalue
- [] Check Whitelabel Error Page whether disabled
- [] Checkself set define ErrorController ofreal current
- [] Check SQL abnormal commonwhetherbeDirectReturntoFrontend
- [] Check MyBatis / Hibernate errorwhetherDisclosuretable name/Fieldname

#### Test Plan

```bash
# 1. trigger initiate 404 - Checkdefault auth error page
curl -v "${BASE_URL}/nonexistent_path_xyz"

# 2. trigger initiate 500 - Parametertype error
curl -v "${BASE_URL}/api/users/abc" # expected period int pass string
curl -v "${BASE_URL}/api/users/-1" # boundary boundary value
curl -v "${BASE_URL}/api/users/99999999999" # super large number

# 3. trigger initiate SQL error
curl -v "${BASE_URL}/api/users?id=1'" # SQL inject inject probe test
curl -v "${BASE_URL}/api/search?q=test' OR '1'='1"

# 4. trigger initiateParameterValidateerror
curl -X POST "${BASE_URL}/api/users" \
 -H "Content-Type: application/json" \
 -d '{"email": "not-an-email", "age": -1}'

# 5. trigger initiateRequest Bodyformat mode error
curl -X POST "${BASE_URL}/api/users" \
 -H "Content-Type: application/json" \
 -d '{"malformed json'

# 6. trigger initiate 405 Method Not Allowed
curl -X DELETE "${BASE_URL}/api/users"

# 7. Content-Type not match config
curl -X POST "${BASE_URL}/api/users" \
 -H "Content-Type: application/xml" \
 -d '<test>123</test>'
```

**Pass/Fail Criteria**:Responseinshould notinclude includethe followingany content:
- Java include name(`com.xxx.xxx`/`org.springframework`)
- stack stack (`at java.lang.`/`.java:123`)
- SQL ortable name
- framework architecture version version number
- Serverinternal partPath(`/home/app/`/`/opt/xxx/`)
- abnormal common type name(`NullPointerException`/`SQLException`)

#### SecureHardeningcreate protocol

```yaml
# application.yml
server:
 error:
 include-stacktrace: never
 include-message: never
 include-binding-errors: never
 include-exception: false
 whitelabel:
 enabled: false
```

```java
// all global abnormal common handle manage device
@RestControllerAdvice
public class GlobalExceptionHandler {

 @ExceptionHandler(Exception.class)
 public ResponseEntity<ErrorResponse> handleException(Exception e) {
 log.error("Internal error", e); // LogRecordCompleteinformation
 return ResponseEntity.status(500).body(new ErrorResponse("INTERNAL_ERROR", "Serverinternal part error")); // leak sensitiveReturn
 }

 @ExceptionHandler(MethodArgumentNotValidException.class)
 public ResponseEntity<ErrorResponse> handleValidation(MethodArgumentNotValidException e) {
 return ResponseEntity.status(400).body(new ErrorResponse("VALIDATION_ERROR", "ParameterValidateFailure"));
 }
}
```

---

### 2.3 ConfigurationFileandsensitive sensitiveDataDisclosure

#### Investigation Checklist

- [] `application.yml` / `application.properties` inwhetherhardEncodingDatabasePassword
- [] whetheruseusedoneConfigurationadd secret(Jasypt / Spring Cloud Config add secret)
- [] `bootstrap.yml` whetherinclude includeSensitive Information
- [] many environment environmentConfigurationFile(`application-dev.yml`/`application-prod.yml`)whetherall do done leak sensitive
- [] whether exists `.env` Filebe break includetomake productin
- [] Git repository library history historyinwhether hasSensitive Information(that is use when first alreadyDelete)
- [] `pom.xml` / `build.gradle` inwhether hasprivate has repository library credential according
- [] Docker Imageinwhetherinclude includeConfigurationFileclear text
- [] Kubernetes ConfigMap / Secret whethercorrect confirm useuse

#### Test Plan

```bash
# 1. Coderepository librarySensitive InformationScan(useuse trufflehog or gitleaks)
gitleaks detect --source=. --report-format=json --report-path=gitleaks-report.json

# 2. keywords search
grep -rn "password\s*=" src/ --include="*.yml" --include="*.yaml" --include="*.properties" --include="*.xml"
grep -rn "secret\s*=" src/ --include="*.yml" --include="*.yaml" --include="*.properties"
grep -rn "api[_-]key\s*=" src/ --include="*.yml" --include="*.yaml" --include="*.properties"
grep -rn "jdbc:" src/ --include="*.yml" --include="*.yaml" --include="*.properties" --include="*.xml"
grep -rn "aws_access_key\|aws_secret" src/
grep -rn "BEGIN RSA PRIVATE KEY\|BEGIN PRIVATE KEY" src/

# 3. break include asset itemCheck(decode JAR/WAR)
jar -tf target/app.jar | grep -E "(\.yml|\.yaml|\.properties|\.xml|\.env|\.key|\.pem)"
# decode afterCheckConfigurationFilecontent
jar -xf target/app.jar BOOT-INF/classes/application.yml
cat BOOT-INF/classes/application.yml | grep -i "password\|secret\|key\|token"

# 4. Docker ImagelayerAnalyze
docker history --no-trunc app:latest
docker save app:latest | tar -xf - -C /tmp/image-layers/
# one-by-one layercheck whether there issensitive sensitiveFile
find /tmp/image-layers/ -name "*.yml" -o -name "*.properties" -o -name "*.env" | xargs grep -l "password"
```

---

### 2.4 HTTP ResponseHeaderInformation Disclosure

#### Investigation Checklist

- [] `Server` ResponseHeaderwhetherexpose exposureServertypeandversion version(such as `Apache-Coyote/1.1`)
- [] `X-Powered-By` Headerwhetherexpose exposure framework architecture information
- [] `X-Application-Context` Headerwhetherexpose exposureApplicationnameand Profile
- [] whethermissing lessSecureResponseHeader(`X-Content-Type-Options`/`X-Frame-Options`/`Strict-Transport-Security`)
- [] CORS Configurationwhetherthrough for (`Access-Control-Allow-Origin: *`)
- [] `Set-Cookie` whethermissing less `HttpOnly`/`Secure`/`SameSite` identifier

#### Test Plan

```bash
# 1. CheckAllResponseHeader
curl -sI "${BASE_URL}/api/health" | head -30

# 2. Checksensitive sensitiveHeader
curl -sI "${BASE_URL}/" | grep -iE "^(server|x-powered-by|x-application-context|x-aspnet)"

# 3. CORS Check
curl -sI -H "Origin: https://evil.com" "${BASE_URL}/api/users" | grep -i "access-control"

# 4. Cookie Secureidentifier Check
curl -sI "${BASE_URL}/login" | grep -i "set-cookie"
# Confirminclude include: HttpOnly; Secure; SameSite=Lax (or Strict)

# 5. SecureHeaderCheck
curl -sI "${BASE_URL}/" | grep -iE "^(x-content-type|x-frame|strict-transport|content-security-policy|x-xss)"
```

#### SecureHardeningcreate protocol

```yaml
# application.yml - hidden hidden Server Header
server:
 server-header: "" # clearEmpty Server Header
```

```java
// Spring Security Configuration
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
 http.headers(headers -> headers.frameOptions(f -> f.deny()).xssProtection(x -> x.disable()) // current codeBrowseralready internal set.contentTypeOptions(Customizer.withDefaults()).httpStrictTransportSecurity(h -> h.includeSubDomains(true).maxAgeInSeconds(31536000)));
 return http.build();
}
```

---

### 2.5 API ResponseDatathrough degree expose exposure

#### Investigation Checklist

- [] Userrelated keyInterfacewhetherReturndonePasswordhash hash/ value
- [] listInterfacewhetherReturndone not must needofsensitive sensitiveField(mobile number/Identity Card/banklinescard)
- [] whetheruseusedone `@JsonIgnore` / DTO mode control make output outField
- [] part pageInterfacewhetherallow allow onetimesness check queryAllData(such as `pageSize=999999`)
- [] Interfacewhether existsHorizontal Authorization Bypass(Passchange ID access ask other personData)
- [] EnumerationInterfacewhetherCanTraversal(such asrecursive increase ID TraversalAllUser)
- [] GraphQL Interfacewhetherallow allow internal (Introspection)

#### Test Plan

```bash
# 1. CheckUserInterfaceReturnField
curl -s "${BASE_URL}/api/users/1" | python3 -m json.tool
# Checkwhetherinclude include: password, salt, idCard, bankCard, phone etc.sensitive sensitiveField

# 2. ChecklistInterface
curl -s "${BASE_URL}/api/users?page=1&size=10" | python3 -m json.tool
# ConfirmReturnFieldandsingle check query one cause, not many outField

# 3. large page test
curl -s "${BASE_URL}/api/users?page=1&size=999999" | wc -c
# shouldhas page large small above limit

# 4. Horizontal Authorization Bypasstest(use A User Token access ask B UserData)
curl -s -H "Authorization: Bearer ${TOKEN_A}" "${BASE_URL}/api/users/2"

# 5. ID EnumerationTraversal
for i in $(seq 1 20); do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}/api/users/${i}")
 echo "[${STATUS}] user/${i}"
done

# 6. GraphQL internal Check
curl -X POST "${BASE_URL}/graphql" \
 -H "Content-Type: application/json" \
 -d '{"query":"{ __schema { types { name fields { name } } } }"}'
```

---

### 2.6 state resource sourceanddirectory recordTraversal

#### Investigation Checklist

- [] `.git` directory recordwhetherCanPass Web access ask
- [] whether existsprepare copyFile(`.bak`/`.swp`/`.old`/`~`)
- [] whether existssource codeFiledirectly usableaccess ask(`.java`/`.class`)
- [] whether enableddone directory record list function can
- [] `robots.txt` whetherexpose exposure done sensitive sensitivePath
- [] `sitemap.xml` whetherinclude include manage manage backend consolePath
- [] `crossdomain.xml` / `clientaccesspolicy.xml` whether existsandConfigurationthrough

#### Test Plan

```bash
# 1. sensitive sensitiveFileprobe test
SENSITIVE_FILES=("/.git/HEAD"
 "/.git/config"
 "/.gitignore"
 "/.env"
 "/.env.local"
 "/.env.production"
 "/WEB-INF/web.xml"
 "/WEB-INF/classes/application.yml"
 "/WEB-INF/classes/application.properties"
 "/robots.txt"
 "/sitemap.xml"
 "/crossdomain.xml"
 "/swagger-ui.html"
 "/swagger-ui/index.html"
 "/v2/api-docs"
 "/v3/api-docs"
 "/druid/index.html"
 "/h2-console"
 "/favicon.ico"
 "/backup.sql"
 "/dump.sql"
 "/application.yml"
 "/application.properties"
 "/.DS_Store"
 "/Thumbs.db")

for f in "${SENSITIVE_FILES[@]}"; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}${f}")
 if ["$STATUS"!= "404"] && ["$STATUS"!= "403"]; then
 echo "[FOUND ${STATUS}] ${f}"
 fi
done

# 2. directory recordTraversaltest
curl -s "${BASE_URL}/static/"
curl -s "${BASE_URL}/resources/"
curl -s "${BASE_URL}/public/"
curl -s "${BASE_URL}/uploads/"

# 3. Path bypass test
curl -s "${BASE_URL}/static/../../etc/passwd"
curl -s "${BASE_URL}/static/..%2F..%2Fetc%2Fpasswd"
curl -s "${BASE_URL}/static/....//....//etc/passwd"
```

---

### 2.7 LogInformation Disclosure

#### Investigation Checklist

- [] Loginwhetherbreak doneUserPassword/Token/Session ID
- [] Loginwhetherbreak doneCompleteofRequest/Response Body(include sensitive sensitiveData)
- [] LogFilewhetherCanPass Web access ask(such as `/logs/`/`/log/`)
- [] Loglevel levelingenerate asset environment environmentwhetherset setas `INFO` oror more(should notas `DEBUG`/`TRACE`)
- [] whetheruseusedoneLogleak sensitive array item
- [] Logwhetheroutput outto stdout after be collect collectSystemexpose exposure

#### Test Plan

```bash
# 1. LogFileprobe test
LOG_PATHS=("/logs/"
 "/log/"
 "/logs/spring.log"
 "/logs/app.log"
 "/logs/error.log"
 "/log/spring.log"
 "/output.log"
 "/nohup.out")

for p in "${LOG_PATHS[@]}"; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}${p}")
 if ["$STATUS" == "200"]; then
 echo "[EXPOSED] ${p}"
 fi
done

# 2. Codeaudit plan - searchLoginofSensitive Informationoutput out
grep -rn "log\.\(info\|debug\|warn\|error\)" src/ --include="*.java" | \
 grep -iE "(password|token|secret|credential|session|cookie|authorization)"

# 3. Checkgenerate asset environment environmentLoglevel levelConfiguration
grep -rn "logging.level" src/ --include="*.yml" --include="*.properties"
```

---

### 2.8 Swagger / OpenAPI Documentexpose exposure

#### Investigation Checklist

- [] Swagger UI whetheringenerate asset environment environmentCanaccess ask
- [] OpenAPI JSON/YAML Endpointwhetherexpose exposure
- [] Knife4j(increase strong Swagger)whetheringenerate asset environment environmentCanaccess ask
- [] whetherPass Profile control make Swagger onlyinopen initiate environment environment enableuse

#### Test Plan

```bash
# Swagger / OpenAPI Endpointprobe test
SWAGGER_PATHS=("/swagger-ui.html"
 "/swagger-ui/"
 "/swagger-ui/index.html"
 "/swagger-resources"
 "/swagger-resources/configuration/ui"
 "/v2/api-docs"
 "/v3/api-docs"
 "/v3/api-docs.yaml"
 "/doc.html" # Knife4j
 "/webjars/springfox-swagger-ui/"
 "/api-docs"
 "/api/swagger.json"
 "/api/v1/swagger.json")

for p in "${SWAGGER_PATHS[@]}"; do
 STATUS=$(curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}${p}")
 if ["$STATUS" == "200"]; then
 echo "[EXPOSED] ${p}"
 fi
done
```

#### SecureHardeningcreate protocol

```java
// Pass Profile control make, only dev/test environment environment enableuse
@Configuration
@Profile({"dev", "test"})
public class SwaggerConfig {
 // Swagger Configuration
}
```

```yaml
# application-prod.yml - generate asset environment environment key close
springdoc:
 api-docs:
 enabled: false
 swagger-ui:
 enabled: false
```

---

### 2.9 Spring DevTools Disclosure

#### Investigation Checklist

- [] `spring-boot-devtools` depend relywhetheringenerate asset includein(shouldas `optional` + `provided` scope)
- [] remote process debuggingPortwhetherexpose exposure(`spring.devtools.remote.secret`)
- [] LiveReload Port(35729)whetheropen release
- [] remote process serious enableEndpoint `/.~~spring-boot!~/restart` whetherCanaccess ask

#### Test Plan

```bash
# 1. Check DevTools remote processEndpoint
curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}/.~~spring-boot!~/restart"

# 2. Check LiveReload Port
curl -s -o /dev/null -w "%{http_code}" --connect-timeout 3 "http://target:35729/"

# 3. Codeaudit plan - pom.xml Check
grep -A5 "spring-boot-devtools" pom.xml
# Confirm scope as runtime + optional=true
```

---

### 2.10 Databaseandinbetween itemConsole

#### Investigation Checklist

- [] H2 Console whetheringenerate asset environment environment enableuse(`spring.h2.console.enabled`)
- [] Druid monitor control pagewhetherCanUnauthorized Access(`/druid/index.html`)
- [] Redis whetherset set donePasswordand not expose exposureinPublic Internet
- [] RabbitMQ / Kafka manage manage boundary pagewhether hasAuthentication
- [] Elasticsearch `_cat`/`_cluster` Endpointwhetherexpose exposure
- [] Nacos / Apollo / Spring Cloud Config Consolewhether hasAuthentication

#### Test Plan

```bash
# 1. H2 Console
curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}/h2-console"
curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}/h2-console/"

# 2. Druid Monitor
curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}/druid/index.html"
curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}/druid/login.html"
curl -s -o /dev/null -w "%{http_code}" "${BASE_URL}/druid/api.html"
# default authUsername/PasswordAttempt:admin/admin, druid/druid

# 3. Registrationincore / Configurationincore
curl -s -o /dev/null -w "%{http_code}" "http://target:8848/nacos/"
curl -s -o /dev/null -w "%{http_code}" "http://target:8070/" # Apollo
curl -s "http://target:8848/nacos/v1/cs/configs?dataId=&group=&tenant=&pageNo=1&pageSize=100"

# 4. Elasticsearch
curl -s "http://target:9200/"
curl -s "http://target:9200/_cat/indices"
curl -s "http://target:9200/_cluster/health"
```

---

### 2.11 Spring Security Configurationmissing flaw

#### Investigation Checklist

- [] whether existsAuthenticationBypassPath(`permitAll()` ConfigurationofPathwhethercombine manage)
- [] Session whetheruseuseSecurity Configuration(super time/Fixedattack attack defense protect)
- [] CSRF protect protectwhethercombine manage enableuse/key close
- [] Passwordwhetheruseuse BCrypt etc.Securealgorithm method(whileNon- MD5/SHA1)
- [] Token(JWT)whetherexpose exposure done not must needof Claim(UserRole/Permissionlist)
- [] JWT Secret whetherhardEncodinginCodein

#### Test Plan

```bash
# 1. JWT Token decode codeCheck(notrequiresKey can read payload)
# Obtainone token after
echo "$JWT_TOKEN" | cut -d. -f2 | base64 -d 2>/dev/null | python3 -m json.tool
# Check payload inwhetherinclude includeSensitive Information

# 2. Codeaudit plan - search hardEncodingKey
grep -rn "jwt\.\(secret\|key\)" src/ --include="*.yml" --include="*.properties" --include="*.java"
grep -rn "SecretKeySpec\|signing[Kk]ey\|\.signWith" src/ --include="*.java"

# 3. Check permitAll Path
grep -rn "permitAll\|anonymous" src/ --include="*.java"
```

---

### 2.12 depend rely array item version versionDisclosure

#### Investigation Checklist

- [] whetheruseusedone already notify hasInformation Disclosurevulnerabilityof Spring Boot version version
- [] Jackson/Fastjson etc.sequence list ize library version versionwhetherSecure
- [] No. three method depend relywhether hasalready notify CVE

#### Test Plan

```bash
# 1. depend rely vulnerabilityScan
mvn org.owasp:dependency-check-maven:check
# or./gradlew dependencyCheckAnalyze

# 2. Spring Boot version versionConfirm
grep "spring-boot" pom.xml | head -5
# for photo already notify vulnerability list:https://spring.io/security

# 3. Responseinframework architecture specified patternIdentify
curl -sI "${BASE_URL}/" | grep -iE "server|x-powered|x-application"
curl -s "${BASE_URL}/error" | grep -i "whitelabel\|spring\|tomcat"
```

---

## 3. self dynamic izeScanToolinfer

| Tool | Purpose | Command/link connect |
|------|------|----------|
| **nuclei** | Actuator + wildusevulnerability model templateScan | `nuclei -u http://target -t spring/` |
| **SpringBoot-Scan** | Spring Boot specialitemsScan | GitHub: AabyssZG/SpringBoot-Scan |
| **gitleaks** | Git repository librarySensitive InformationDisclosure | `gitleaks detect --source.` |
| **trufflehog** | Git history history credential according search | `trufflehog git file://.` |
| **OWASP ZAP** | Web Secure combineScan | includeInformation Disclosurecheck test scale rule |
| **dependency-check** | depend rely CVE check test | Maven/Gradle item |
| **JDumpSpider** | heapdump self dynamic provide takeSensitive Information | GitHub: whwlsfb/JDumpSpider |
| **pspy** | advance process monitor control(Checkenable dynamicParameterwhetherincludePassword) | GitHub: DominicBreuker/pspy |

---

## 4. rank checkExecuteplan

### No. onePhase:HighPriority(standalone that isExecute, 1-2 days)

| sequence number | any service | Risk Level | negative |
|------|------|---------|------|
| 1 | Actuator Endpointall quantityScan + | High Risk | Secure/operations |
| 2 | error pageInformation DisclosureCheck + all global abnormal common handle manage device audit check | High Risk | open initiate |
| 3 | ConfigurationFileSensitive InformationScan(include Git history history) | High Risk | Secure |
| 4 | Swagger / H2 Console / Druid generate asset environment environment key closeConfirm | High Risk | operations |
| 5 | DevTools depend relyCheck | High Risk | open initiate |

### No. twoPhase:inPriority(3-5 daysinternal)

| sequence number | any service | Risk Level | negative |
|------|------|---------|------|
| 6 | HTTP ResponseHeaderSecureaudit plan | Medium Risk | open initiate |
| 7 | API ResponseFieldthrough degree expose exposureCheck | Medium Risk | open initiate |
| 8 | LogSensitive Informationaudit plan | Medium Risk | open initiate |
| 9 | state resource sourceandsensitive sensitiveFilePathScan | Medium Risk | Secure/operations |
| 10 | JWT Token Payload audit check | Medium Risk | open initiate |

### No. threePhase:hold continue change advance(1-2 cycle)

| sequence number | any service | Risk Level | negative |
|------|------|---------|------|
| 11 | depend rely array item CVE Scan | Medium Risk | open initiate |
| 12 | Docker ImageSecureaudit plan | Medium Risk | operations |
| 13 | CI/CD flow horizontal line collect completeSecureScan | Low Risk | DevOps |
| 14 | create standaloneSecurebase lineandset period check machine make | Low Risk | Secure |

---

## 5. validate collect identifier accurate

Allrank checkitemsPassafter, should the followingcondition:

1. **Actuator**:only `/actuator/health`(`show-details: never`)and `/actuator/info`(noSensitive Information)for external open release
2. **errorResponse**:Allabnormal commonReturnsystem one format mode, not include stack stack/SQL/type name/Path
3. **ConfigurationFile**:zero hardEncodingPassword/Key, AllPassenvironment environment change quantityoradd secretConfigurationinject inject
4. **ResponseHeader**:no Server version version/no X-Powered-By/include includeAllSecureHeader
5. **API Response**:useuse DTO mode, sensitive sensitiveField(mobile number/Identity Cardetc.)leak sensitiveReturn
6. **Document/Console**:Swagger/H2 Console/Druid Monitor generate asset environment environment complete all key close
7. **Log**:notRecordPassword/Token/Completebanklinescard numberetc.sensitive sensitiveData
8. **depend rely**:noHigh Risk CVE not fix repeat, DevTools notingenerate asset structure createin
9. **Git repository library**:no history historySensitive InformationDisclosure(alreadyPass BFG / filter-branch clear manage)
10. **self dynamic ize**:CI/CD collect complete done gitleaks + dependency-check, increase quantity check test
