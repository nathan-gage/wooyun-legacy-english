# Multi-Tenant SaaS PlatformAuthorization BypassCompleteTest Plan

> Based on the methodology from 22,132 real WooYun vulnerability cases | cover coverHorizontal Authorization Bypass(IDOR)/Vertical Authorization Bypass(Privilege Escalation)/Unauthorized Accessthree majorDimension

---

## 1. test background sceneandScope

### 1.1 TargetSystemprofile

| Dimension | description |
|------|------|
| Systemtype | Multi-Tenant SaaS Platform(REST API) |
| Client | Web Frontend + Mobile Client |
| participateandRole | Anonymous User/Regular User/Tenant Administrator/Super Administrator/API Client |
| Core Assets | TenantDataisolation/UserPersonal Information/Business Data/API Credential |
| Trust Boundary | Tenantbetween isolation/RolebetweenPermissionboundary boundary/Authentication/notAuthenticationboundary boundary |

### 1.2 WooYun Datasupport

Authorization Domainin WooYun Datacollectintotal **6,838 Case**, is second onlytimesforAuthentication(8,846)andInformation Disclosure(6,446)ofNo. three majorVulnerability Category.Among them:

| subCategory | Case Count | high-risk percentage | versionTest PlanforshouldSection |
|--------|--------|----------|-------------------|
| Horizontal Authorization Bypass/IDOR | 1,935 | 62.3% | Chapter 3 |
| Vertical Authorization Bypass/Privilege Escalation | 341 | High | Chapter 4 |
| Unauthorized Access/MissingAuthentication | 3,993 | 58.2%+ | Chapter 5 |
| ArbitraryX(Arbitrary Account/Modify/Delete/View/operation) | 529 | 51-86% | Chapter 6 |

**keyStatistics:** 58.2% ofUnauthorized AccessDiscover = manage manage backend console complete all expose exposureinInternet above, no any identity copyAuthentication.

---

## 2. Pre-Test Preparation

### 2.1 Accountmatrix matrix(strong make need require)

```
mostLowneed require:
 TenantA:
 - Regular User A1(Record session token/user_id/tenant_id)
 - Regular User A2(sameTenant, DifferentUser -- useforHorizontal Authorization Bypass)
 - Tenant Administrator A-admin
 TenantB:
 - Regular User B1(Cross-Tenanttest)
 - Tenant Administrator B-admin
 Platform:
 - Super Administrator Super-admin
 - noAccount/Anonymous State(useforUnauthorized Accesstest)
```

### 2.2 Tool Preparation

| Tool | Purpose |
|------|------|
| Burp Suite / mitmproxy | Request InterceptionandModify |
| Postman / curl | API mobile dynamicCall |
| Burp Turbo Intruder | Batch ID Enumeration |
| Browseropen initiate personTool | JavaScript source codeAnalyze/localStorage Check |
| jq | JSON ResponseAnalyze |

### 2.3 Information-Gathering Checklist

inbefore formal testing, completethe following check:

```
[] collect collectAll API Endpoint(Swagger/OpenAPI Document/Frontend JS source code/Mobile Clientreverse engineering)
[] RecordEachEndpointof HTTP Method/Parameter/Responseresult structure
[] IdentifyAllresource source identifier identify symbol(user_id, tenant_id, order_id, file_id, doc_id etc.)
[] Analyze ID format mode(order sequence integer number vs UUID vs Base64 Encoding vs self set define format mode)
[] map mapRolePermissionmatrix matrix(which someRolecan access ask which someEndpoint)
[] Check API Documentwhetherexposed internal/manage manageEndpoint
[] from robots.txt/sitemap.xml collect collect hidden hiddenPath
```

---

## 3. Horizontal Authorization Bypass(IDOR)Test Plan

> WooYun Case References:"Beijing Hyundai platform allowed unauthorized traversal of all user-uploaded documents(percent ten-thousandidentity documents/vehicle registration documents/invoices/driver licenses)" -- order sequenceFile ID and noOwnership Check.

### 3.1 test principle manage

IDOR(Insecure Direct Object Reference)ofessence:ServernotValidate"Requestpersonwhether haspermission access ask this resource source".inMulti-Tenantscenario scene under, existintwo layerHorizontal Authorization Bypass:

1. **sameTenantinternalUserbetween bypass permission**:User A1 access ask sameTenantUser A2 ofprivate hasData
2. **Cross-Tenantbypass permission**:Tenant A ofUseraccess askTenant B ofData(**Multi-Tenant SaaS most cause fatalofvulnerability**)

### 3.2 Systematictest protocol protocol

#### Step 1:IdentifyAllresource source identifier identify symbol

forEach API Endpoint, identifier record resource source identifier identify symbol out currentofcharacters set:

| identifier identify symbol characters set | Example | Risk Level |
|-----------|------|---------|
| URL Path | `/api/v1/users/{user_id}/orders` | High |
| check queryParameter | `/api/v1/orders?user_id=123&tenant_id=456` | High |
| POST/PUT Request Body | `{"user_id": 123, "action": "view"}` | High |
| HTTP Header | `X-User-Id: 123` / `X-Tenant-Id: 456` | High |
| Cookie | `user_session=base64(user_id=123)` | in |

**keyParameterclear single:** `user_id`, `uid`, `id`, `order_id`, `file_id`, `account_id`, `tenant_id`, `org_id`, `workspace_id`, `doc_id`, `msg_id`, `invoice_id`, `project_id`

#### Step 2:CRUD all cover cover test

forEachinclude include resource source identifier identify symbolofEndpoint, asUser A1 ofidentity copyLogin, ReplaceasUser A2/B1 ofidentifier identify symbol:

```
forEachEndpoint + eachitems CRUD operation:

[C] Create:
 - [] A1 whether canas A2 Createresource source?(POST /api/users/A2_id/orders)
 - [] TenantAUserwhether caninTenantBunderCreateresource source?(body in tenant_id Replace)

[R] Read(most common seenof IDOR):
 - [] A1 whether canView A2 ofOrder/Personal Information/File?
 - [] A1 whether canViewTenantBofData?
 - [] API ResponsewhetherReturndone super out UI displayScopeofField?(API through degreeObtain)

[U] Update:
 - [] A1 whether canModify A2 ofperson resource /set set?
 - [] A1 whether canModifyTenantBofConfiguration?

[D] Delete:
 - [] A1 whether canDelete A2 ofresource source?
 - [] A1 whether canDeleteTenantBofresource source?
```

#### Step 3:identifier identify symbol manipulation techniques

> WooYun lesson lesson:"IDOR hasEncoding Bypass/Parameter Pollution/JSON Nested.simple single change ID only shareCaseof 30%."

| technique | Test Method | Example |
|------|---------|------|
| Direct ID Replace | `id=123` -> `id=124` | most basic, but stillValid |
| ID Enumeration/Traversal | from 1 to N Traversal | order sequence integer number ID when extremelyHigh Risk |
| Parameter Pollution(HPP) | `?uid=123&uid=456` | ServerCancan take most after one value |
| number array inject inject | `uid[]=123` or `uid=123,456` | BypasstypeCheck |
| JSON Nested | `{"user": {"id": 456}}` | Bypasstop layerParameterthrough filter |
| Base64 Encoding | `id=base64(456)` | ReplaceEncodingafterof ID |
| ten six advance makeEncoding | `id=0x1c8` | ReplaceasTarget ID of hex |
| Negative Number/Zero Value | `id=0`/`id=-1` | CancanReturndefault auth/AllData |
| UUID prediction | Analyze UUID version version(v1 include timestamp, Predictable) | UUID v1 Canreverse infer |
| hash hash collision collision | such asif ID is short hash hash(such as MD5 first 8 characters) | collision collision approx rateAnalyze |
| wild config symbol | `id=*` or `id=all` | some some real current ReturnAll |

#### Step 4:Multi-Tenantisolation specialitems

```
Cross-Tenant IDOR test matrix matrix:

[] ReplaceRequestinof tenant_id/org_id/workspace_id
[] useTenantAof token access askTenantBof API Path(/api/tenants/B_id/...)
[] shared resource source test:File/report/dashboardwhether hasTenantlevel levelofAccess Control
[] search/listInterfacewhetherDisclosureotherTenantofData
[] Exportfunction canwhethercanExportotherTenantofData
[] wild notify/messageSystemwhetherCross-TenantCanseen
[] Webhook Configurationwhethercan connect collect otherTenantofevent
```

### 3.3 Highfrequency vulnerabilityEndpoint(priority first test)

root according WooYun Data, the followingEndpoint IDOR Discoverrate mostHigh:

| Priority | Endpointtype | test serious point |
|--------|---------|---------|
| P0 | UserPersonal Information API | GET /api/users/{id} - Replace id |
| P0 | Order/transaction details | GET /api/orders/{id} - Replace order_id |
| P0 | FileDownload/View | GET /api/files/{id} - order sequenceFile ID |
| P0 | Tenantmanage manage API | GET /api/tenants/{id}/settings |
| P1 | message/wild notify | GET /api/messages/{id} |
| P1 | invoices/account single | GET /api/invoices/{id} |
| P1 | report/Export | GET /api/reports/{id}/download |
| P2 | assess comment/feedback | GET /api/comments/{id} |
| P2 | Log/audit planRecord | GET /api/audit-logs?user_id={id} |

### 3.4 WooYun Real Case References

| Case | Vulnerability Pattern | impact response scale model |
|------|---------|---------|
| Beijing Hyundai platform allowed unauthorized traversal of millions of identity documents/vehicle registration documents | order sequenceFile ID + noOwnership Check | number percent ten-thousandidentity documents |
| Hua.com horizontal authorization vulnerability(impact responseAlluseuseUser) | Horizontal Authorization Bypass - Replace user_id | AllUserDataCanaccess ask |
| EMS site horizontal authorization vulnerability involving large volumes of user information | Horizontal Authorization Bypass - ID Traversal | large quantityUserPersonal Information |
| China Eastern Airlines US site severe order information leak and authorization bypass | Order ID Traversal + PermissionBypass | OrderDataDisclosure |

---

## 4. Vertical Authorization Bypass(Privilege Escalation)Test Plan

> WooYun Data:255+86 Privilege EscalationCase."Arbitrary Accountaccess ask"subCategory 86.4% High Risk, isAllAuthorizationvulnerabilityMedium Risk most largeof.

### 4.1 test principle manage

Vertical Authorization Bypass = LowPermissionUserExecutedoneHighPermissionoperation.inMulti-Tenant SaaS in, existinthree layerVertical Authorization Bypassrisk:

```
attack attackPath:
 Regular User -> Tenant Administrator(TenantlevelPrivilege Escalation)
 Tenant Administrator -> Super Administrator(PlatformlevelPrivilege Escalation)
 Anonymous User -> any alreadyAuthenticationRole(AuthenticationBypassthat isPrivilege Escalation)
```

### 4.2 Systematictest protocol protocol

#### Step 1:map mapPermissionlayer levelandmanage manageEndpoint

```
1. IdentifyAllPermissionlevel level:
 [] name(notAuthentication)
 [] alreadyRegistrationRegular User
 [] paidUser/VIP
 [] Tenant Administrator
 [] Platformoperations
 [] Super Administrator

2. collect collect manage manageEndpoint(many sourceDiscover):
 [] Directguessing:/admin/*, /api/admin/*, /manage/*, /internal/*
 [] JavaScript source codeAnalyze:search "admin", "manage", "internal", "role" keywords
 [] API Document/Swagger:check identifier recordas admin or internal ofEndpoint
 [] robots.txt / sitemap.xml:View Disallow ofPath
 [] FrontendrouteConfiguration(React Router/Vue Router)inofhidden hidden route
 [] Mobile Clientreverse engineering:hardEncodingofmanage manage API
 [] error pageDisclosureofinternal partPath
```

#### Step 2:LowPermissionaccess askHighPermissionEndpoint

useRegular Userof Token/Session DirectRequestmanage manageEndpoint:

```
forEachmanage manageEndpoint:

[] Directaccess ask:useRegular User Token RequestAdministrator API
 GET /api/admin/users (Authorization: Bearer <user_token>)
 GET /api/admin/tenants (Authorization: Bearer <user_token>)
 POST /api/admin/settings (Authorization: Bearer <user_token>)

[] HTTP Methodswitch change:
 principle initial:GET /api/admin/users -> 403
 Attempt:POST /api/admin/users ->?
 Attempt:PUT /api/admin/users ->?
 Attempt:PATCH /api/admin/users ->?
 Attempt:DELETE /api/admin/users ->?

[] Pathcase/Encodingvariant(Bypassroute levelPermissionCheck):
 /api/admin/users
 /api/Admin/users
 /api/ADMIN/users
 /api/%61dmin/users
 /api/admin/./users
 /api/;/admin/users
 /api/admin;/users
 /api/..;/admin/users
```

#### Step 3:ParameterlevelPrivilege Escalation

```
Registration/Updateperson resource timeofRoletamper change:

[] Registrationtime inject injectRoleParameter:
 POST /api/register
 {"username":"evil", "password":"xxx", "role":"admin"}
 {"username":"evil", "password":"xxx", "is_admin":true}
 {"username":"evil", "password":"xxx", "level":9}
 {"username":"evil", "password":"xxx", "type":"superadmin"}
 {"username":"evil", "password":"xxx", "permissions":["admin","write","delete"]}

[] Updateperson resource time provide escalatePermission:
 PUT /api/users/me
 {"name":"normal_user", "role":"admin"}

[] Passhidden hiddenParameterprovide escalate:
 incorrect commonRequestinAdd:group_id, role_id, privilege, admin, is_staff, is_superuser

[] Batch value(Mass Assignment):
 SendCompleteofUserfor (include includeRoleField), ObserveServerwhetherthrough filter
```

#### Step 4:Tenant Administratorbypass permissiontoPlatformmanage manage

```
[] Tenant Administratorwhether canaccess ask /api/platform/* Endpoint
[] Tenant Administratorwhether canView/ModifyotherTenantofinformation
[] Tenant Administratorwhether canCreateSuper AdministratorAccount
[] Tenant Administratorwhether canModifyPlatformlevelConfiguration(plan fee/Package/all global set set)
[] Tenant Administratorof JWT/Token inwhetherinclude includeCantamper changeofRoleField
```

### 4.3 JWT/Token Privilege Escalationspecialitems

```
such asifSystemuseuse JWT:

[] decode code JWT payload, Checkwhetherinclude include role/permissions Field
[] Modify role Fieldafter serious newSignature(Attempt none algorithm method/EmptyKey)
[] Modify tenant_id Field
[] Modify user_id Field(JWT layer pageof IDOR)
[] Check JWT whetheruseuseweakKeySignature(common seen weakKeyDictionaryBrute Force)
[] CheckServerwhetherValidate JWT Signature(tamper change payload but protect retain principleSignature)
[] Check JWT expired time betweenwhetherbeServerstrong makeValidate
```

### 4.4 WooYun "ArbitraryX" attack attackCategoryspecialitems

> WooYun Data:529 Case, 51-86% High Risk.and IDOR Different, "ArbitraryX"is key forExecute"should notthis hasofoperation".

| subCategory | Case Count | high-risk percentage | SaaS scenario sceneTest Point |
|--------|--------|----------|----------------|
| **Arbitrary Accountaccess ask** | 220 | **86.4%** | no need toCredentialasArbitraryUseridentity copyLogin/operation.test:whether canPass API Directas otherUseridentity copyExecuteoperation, without going through correct commonAuthenticationflow process |
| **Arbitrary Modification** | 159 | 63.5% | ModifyArbitraryRecord.test:whether canModifyotherTenantofConfiguration/Userresource /Business Data |
| **ArbitraryUserRegistration** | 24 | **75.0%** | BypassRegistrationcontrol make.test:key closeRegistrationtime still canRegistration;whether canRegistrationasAdministratorRole;whether canBypass please code/Domain Namelimit make |
| **Arbitrary Viewing** | 45 | 55.6% | super bypass IDOR ofBatchDataView.test:Administrator image/BatchExport/not through filteroflistInterface |
| **Arbitrary Deletion** | 41 | 51.2% | DeleteArbitraryRecord.test:whether canDeleteotherTenantofUser/Data/Configuration |
| **Arbitrary Operation** | 40 | **72.5%** | Executespecial permission operation.test:whether canasRegular Useridentity copyExecuteaudit batch/initiate deploy/Executeetc.manage manage operation;whether canself I audit batch |

**ArbitraryX test protocol protocol:**

```
forEachwrite inject/Delete/manage manage operation:

1. IdentifyPermissionmodel type
 - shouldthis be allow allowExecute operation?
 - PermissionCheckinUserlevel level/Rolelevel level is for level level?

2. testPermissionBypass
 [] as no special permissionUseridentity copyExecuteoperation
 [] forNon-when firstUser hasoffor Executeoperation
 [] Batchoperation:Pass API EnumerationModify/DeleteAll
 [] asRegular Useridentity copyExecuteonly limitAdministratorofoperation(audit batch/initiate deploy/useAccount)
 [] self I audit batch:CreateRequest + audit batch self ownofRequest

3. testRegistrationcontrol make
 [] whenRegistration"key close"or"only please"timewhether canRegistration
 [] whether canasAdministrator/provide escalateofRoleRegistration
 [] whether canBypassEmailDomain Namelimit make(SaaS common seen:only allow allow @company.com)
 [] whether canBypassRegistrationofmobile machine/EmailValidate
```

### 4.5 WooYun Real Case References

| Case | Vulnerability Pattern | impact response |
|------|---------|------|
| finance networkPermissionBypassLoginotherUserAccount | Vertical Authorization Bypass - Accountconnect manage | ArbitraryUserAccountconnect manage |
| expose risk a siteSQLinject inject/59itemstable/Permissioncontrol makeDatabase | Vertical Authorization Bypass - inject inject provide permission | CompleteDatabaseaccess ask |
| China Eastern Airlines US site severe order information leak and authorization bypass | Vertical Authorization Bypass - RoleBypass | OrderData + Privilege Escalation |

---

## 5. Unauthorized AccessTest Plan

> WooYun Data:2,102+1,891 Case.58.2% ofDiscover = manage manage backend console complete all expose exposureinInternet, no anyAuthentication.

### 5.1 test principle manage

Unauthorized Access = Endpointcomplete all notCheckidentity copyAuthentication, name that isCanaccess ask.this is most base foundation is most risk ofvulnerability -- notrequiresanyAccount.

### 5.2 EndpointDiscovermatrix matrix

| DiscoverMethod | Operation Steps | Target |
|---------|---------|------|
| Direct URL guessing | one by one access ask common seen manage managePath | `/admin`, `/console`, `/debug`, `/status`, `/api/docs`, `/internal` |
| robots.txt | `GET /robots.txt` View Disallow Path | be"disable stop"but not doAuthenticationofPath |
| sitemap.xml | `GET /sitemap.xml` Enumeration URL | meaning external expose exposureofmanage manage URL |
| JavaScript source code | searchFrontend JS inof API Endpoint | hardEncodingofinternal part API Address |
| API DocumentDisclosure | Check `/swagger-ui.html`, `/api-docs`, `/openapi.json`, `/redoc` | Complete API clear single |
| error page | trigger initiate 404/500 errorViewstack stack | expose exposureofinternal partPath |
| HTTP OPTIONS | for eachEndpointSend OPTIONS Request | expose exposure allow allowofMethodandEndpoint |
| PathTraversal | `/..;/admin`, `/%2e%2e/admin` | BypassPathlevelAuthentication |

### 5.3 Systematictest protocol protocol

```
forEachDiscoverofEndpoint, bythe followingStepone by one test:

Step 1:complete all name access ask
 [] not with any Authorization Headerand Cookie Direct GET Request
 [] such asifReturn 200 -> Recordas[Severe]Unauthorized Access
 [] such asifReturnData -> assess assessDatasensitive sensitive ness

Step 2:Bypassserious set toward
 [] such asif 302 serious set towardtoLoginpage -> CheckResponse Bodywhetherstill includeData
 [] use curl -L vs not, for ratioResponse
 [] Add X-Forwarded-For: 127.0.0.1(Internal Networkcome source)
 [] Add X-Original-URL / X-Rewrite-URL Header

Step 3:Bypass 403
 [] replace code HTTP Method:GET -> POST -> PUT -> DELETE -> PATCH -> HEAD
 [] Pathscale scope ize:/admin/ vs /admin vs /Admin vs /ADMIN
 [] URL Encoding:/%61dmin (a->%61)
 [] dual seriousEncoding:/%2561dmin
 [] Path bypass:/accessible/../admin
 [] part number inject inject:/admin;.css(some someinbetween item ignore part number after content)
 [] changelinesinject inject:/admin%0a
 [] Addafter:/admin.json, /admin.html, /admin/

Step 4:API version versionBypass
 [] /api/v1/admin/users -> 403
 [] /api/v2/admin/users ->?(new version versionCancan not addPermission)
 [] /api/internal/admin/users ->?
 [] /api/admin/users.json ->?
```

### 5.4 Multi-Tenant SaaS special hasofUnauthorized Accesspoint

```
High RiskUnauthorizedEndpointclear single:

[] TenantRegistration/CreateEndpoint - whetherallow allowArbitraryCreateTenant
[] API DocumentEndpoint - /swagger, /api-docs whetherexpose exposureAll API
[] CheckEndpoint - /health, /status whetherDisclosureinternal part information
[] specified identifier/monitor controlEndpoint - /metrics, /actuator whetherexpose exposure
[] GraphQL Playground - /graphql whetheropen enable introspection
[] WebSocket Endpoint - ws:// continuous connectwhetherrequiresAuthentication
[] FileUpload/Download - /uploads/*, /files/* whetherrequiresAuthentication
[] Webhook Callback - /webhooks/* whetherValidatecome source
[] Password ResetEndpoint - whetherexpose exposureUserEnumerationinformation
[] Usersearch/list - whetherallow allow name searchUser
[] company open API(Public API) - whetherthrough degree expose exposure internal partData
[] debuggingEndpoint - /debug, /trace, /console
```

### 5.5 Spring Boot Actuator / framework architecture special setEndpoint

> WooYun Data:Misconfiguration 1,796 Case, 72.6% High Risk.Spring Boot Actuator No Authentication by DefaultisCriticalfrequencyDiscover.

```
[] /actuator
[] /actuator/env - DisclosureAllenvironment environment change quantity(includeKey)
[] /actuator/heapdump - Disclosureinternal exist(include Token/Password)
[] /actuator/mappings - DisclosureAll API route
[] /actuator/beans - Disclosure Spring Bean information
[] /actuator/configprops - DisclosureConfigurationattributes
[] /actuator/trace - Disclosuremost Request(include Header)
[] /druid/index.html - Druid monitor control()
[] /swagger-ui.html - API Document
[] /graphql - GraphQL Playground
```

### 5.6 WooYun Real Case References

| Case | Vulnerability Pattern | impact response |
|------|---------|------|
| Sina many handlezookeepernotConfigurationPermissioncontrol make involvingSensitive Information | internal part service expose exposure | Internal NetworkInformation Disclosure |
| innationalFinancialAuthenticationincorea systemUnauthorized Access(involvingInternal Networkinformation) | manage manage backend consoleNo Authentication | Internal Network |
| lesson a locationUnauthorized AccessCanimpact response large quantity generate information | MissingAuthentication | large quantity generatePersonal Information |

---

## 6. crossDomainarray combine test

### 6.1 Authentication + Authorizationarray combine attack attack

> WooYun Case References:"TCLsystem oneAuthenticationPlatformCanserious setAllUserPassword" -- cross N+ businessSystemofCompleteAccountconnect manage.

```
Password Resetinofbypass permission(777Case, 88.0%High Risk):

[] asUserARequestPassword Reset -> will user_id/email ReplaceasUserB
[] Password Resetcommand cardwhetherin API ResponseinReturn(whileNon-onlySendtoEmail/mobile machine)
[] serious set command cardwhetherPredictable(based on timestamp/order sequence number character)
[] whether canskip throughValidateStep, DirectRequest"Set New Password"Endpoint
[] Host Headerinject inject:in Host Headerininject inject attack attack person domain as take serious set link connect
[] SMS Verification CodewhethercrossUsershared(A ofCAPTCHAusefor B ofserious set)
```

### 6.2 Information Disclosure -> bypass permission link

> WooYun Data:Information Disclosure 4,858 Case, 64.7% High Risk.Disclosureofinformation is bypass permission attack attackof ize.

```
[] API through degreeObtain:API Responseinwhetherinclude includeshould notReturnofField
 (such as:GET /api/users/me Returndone role/tenant_id/internal_id)
[] errorInformation Disclosure:errorResponsewhetherexpose exposure otherUserof ID orinternal part result structure
[] listInterfaceDisclosure:/api/users whetherReturnAllUser(include otherTenant)
[] searchInterfaceDisclosure:search function canwhethercan searchtootherTenantofData
[] LogInterfaceDisclosure:/api/logs whetherexpose exposure otherUserofoperation
```

### 6.3 Statusmachine + bypass permission array combine

> WooYun Data:Design Flaw 1,391 Case, 65.3% High Risk.

```
[] OrderStatusbypass permissionModify:whether canwillother personOrderfrom"Pending Payment"changeas"Paid"
[] audit batch flow process bypass permission:whether canaudit batch self ownCreateofRequest(can part separateMissing)
[] Refundbypass permission:whether canasother personOrderinitiate initiateRefund
[] Rolechange update bypass permission:whether canPass API DirectModifyself ownorother personofRole
```

### 6.4 Race Condition + bypass permission

> WooYun Data:Race Condition 266 Case, 74.8% High Risk.

```
[] PermissionCheckof TOCTOU:ConcurrencyRequestwhethercaninPermissionchange updateofbetween bypass permission
 scenario scene:Administrator UserPermissionofsame time, UserConcurrencyinitiate initiate operation
[] RegistrationRace:ConcurrencyRegistrationwhethercanBypass please code/name amount limit make
[] Rolechange updateRace:ConcurrencyModifyRolewhetherCausingPermissionnot one cause
```

---

## 7. testExecutematrix matrix

### 7.1 Priorityrank sequence(by WooYun high-risk percentagerank sequence)

| Priority | Test Item | high-risk percentage | expected assess time | Prerequisites |
|--------|--------|----------|---------|---------|
| **P0** | Arbitrary Accountaccess ask | 86.4% | 2h | 2+ Test Account |
| **P0** | Password Resetbypass permission | 88.0% | 2h | Password Resetfunction can |
| **P0** | ArbitraryUserRegistration | 75.0% | 1h | Registrationfunction can |
| **P0** | Cross-Tenant IDOR | 62.3% | 4h | 2 TenantAccount |
| **P1** | manage manageEndpointUnauthorized Access | 58.2% | 3h | Endpointclear single |
| **P1** | Arbitrary Operation(audit batch/initiate deploy) | 72.5% | 2h | business flow process map map |
| **P1** | Arbitrary Modification | 63.5% | 2h | write inject API clear single |
| **P1** | vertical verticalPrivilege Escalation | High | 3h | manage manageEndpointclear single |
| **P2** | sameTenantinternal IDOR | 62.3% | 3h | sameTenant 2 Account |
| **P2** | Arbitrary Deletion | 51.2% | 1h | Delete API clear single |
| **P2** | Arbitrary Viewing/BatchExport | 55.6% | 2h | Exportfunction can |
| **P2** | JWT/Token Privilege Escalation | High | 2h | JWT useusescenario scene |
| **P3** | Race Conditionbypass permission | 74.8% | 2h | ConcurrencytestTool |
| **P3** | Statusmachine bypass permission | 65.3% | 2h | Statusflow map map |

### 7.2 testRecordmodel template

EachTest Caseuseusethe followingformat modeRecord:

```
## TC-[ID]: [Test Casename name]

- Category: [Horizontal Authorization Bypass | Vertical Authorization Bypass | Unauthorized Access | ArbitraryX]
- Priority: [P0 | P1 | P2 | P3]
- Endpoint: [HTTP_METHOD] [URL]
- Prerequisites: [requiresofAccount/Permission/Status]

### Test Steps
1. as [RoleA] identity copyLogin, Obtain Token
2. SendRequest:
 ```
 curl -X GET https://api.example.com/endpoint \
 -H "Authorization: Bearer <token_A>" \
 -H "Content-Type: application/json"
 ```
3. will [Parameter] Replaceas [Targetvalue]
4. ObserveResponse

### Expected Result
- shouldReturn 403 Forbidden or 404 Not Found

### Actual Result
- [] Pass(correct confirm reject reject)
- [] Failure(bypass permissionSuccess) - RecordDetailedResponse

### Evidence
- Requestintercept image/cURL Command
- Responsecontent(leak sensitive)
```

---

## 8. vulnerability assess level identifier accurate

### 8.1 Severeness assess level

| level level | set define | Example |
|------|------|------|
| **Severe** | Cross-TenantDataDisclosure/tamper change;Arbitrary Accountconnect manage;manage manage backend console complete all expose exposure | Replace tenant_id Canaccess askAllTenantData |
| **High** | sameTenantinternal IDOR DisclosureSensitive Information;Regular Userprovide permission Administrator | Traversal user_id ObtainAllUserPersonal Information |
| **in** | has limitScopeofbypass permission(such asonly canViewcannotModify);Non-sensitive sensitiveDataDisclosure | canViewotherUserofcompany open information |
| **Low** | need special first provide condition;impact response extreme has limit | can tootherUserof name |

### 8.2 Multi-Tenantscenario sceneofspecial assess level scale rule

```
Cross-Tenantbypass permission -> self dynamic provide escalate oneetc.level
 - sameTenant IDOR Read = High Risk
 - Cross-Tenant IDOR Read = Severe
 - Cross-Tenant IDOR write inject/Delete = Severe(Cancan impact responseAllclient account)
```

---

## 9. Discoverreport model template

```
## Discover:[identifier problem]

- Severity:[Severe/High/in/Low]
- Domain:Authorization
- WooYun mode:[Discovermatch configofhistory history mode name name]
- Vulnerability Type:[Horizontal Authorization Bypass | Vertical Authorization Bypass | Unauthorized Access | ArbitraryX]
- Impact Scope:[affected impact responseofTenantnumber/Usernumber/Dataquantity]
- Business Impact:[finance service loss loss / DataDisclosure / combine scale risk / client account information any]

### Reproduction Steps
1. asUser A (tenant_id=100, user_id=1001) identity copyLogin
2. Sendthe followingRequest:
 ```
 GET /api/v1/users/1002/profile
 Authorization: Bearer <user_A_token>
 ```
3. will user_id from 1001 Replaceas 1002
4. ServerReturn 200, Response Bodyinclude includeUser 1002 ofCompletePersonal Information

### impact responseAnalyze
- attack attack personCanPassEnumeration user_id ObtainPlatformAllUserofPersonal Information
- Cross-Tenantscenario scene under, Canaccess askAllTenantofUserData
- reverse GDPR/protect method combine scale need require

### supplement create protocol(Serverend fix repeat, Non-Client)
1. inDataaccess ask layer strong makeOwnership Check:`resource.owner_id == current_user.id`
2. in ORM check queryinstrong make tenant_id through filter:`Model.where(tenant_id: current_tenant.id)`
3. useuse UUID v4 replace code order sequence integer number ID
4. real API GatewaylayerofcollectinmodeAuthorizationCheck
5. AddcrossUseraccess ask mode monitor control report alert
```

---

## 10. Defense Recommendationstotal result

> based on WooYun 6,838 AuthorizationvulnerabilityCaseoffix repeatDataprovide.

### 10.1 Codelayer page

| | Description | forshouldvulnerability |
|------|------|---------|
| **default auth reject reject** | company openEndpointWhitelistmake, other one switch needAuthentication | Unauthorized Access |
| **AllpermissionValidate** | Eachcheck queryValidate `resource.owner_id == current_user.id` | IDOR |
| **ORM level through filter** | `Model.where(user_id: current_user.id, tenant_id: current_tenant.id)` | IDOR + Multi-Tenantisolation |
| **notPredictable ID** | UUID v4 replace code order sequence integer number | IDOR Enumeration |
| **RBAC/ABAC** | based onRoleorattributesofAccess Controlframework architecture | Vertical Authorization Bypass |
| ** can part separate** | Createpersoncannotaudit batch self ownofRequest | Arbitrary Operation |
| **Batch value defense protect** | Whitelistallow allowUpdateofField, reject reject role/permission etc. | Parameterlevel provide permission |

### 10.2 architecture structure layer page

| | Description |
|------|------|
| **API GatewaycollectinAuthorization** | inGatewaylayer system oneExecuteAuthenticationandbase foundationAuthorizationCheck |
| **Multi-TenantDatabaseisolation** | Allcheck query strong make tenant_id through filter, oruseuseindependent standalone schema/Database |
| **zero information any architecture structure** | EachRequestValidateidentity copyandPermission, no commentNetworkcome source |
| **URL mode protect protect** | framework architecture level routeAuthorization(Spring Security/Django Permissions) |
| **most small ize API Response** | onlyReturnClientrequiresofField, notReturnCompleteDatabasefor |

### 10.3 monitor controlandreport alert

| monitor controlitems | trigger initiate condition |
|--------|---------|
| crossUseraccess ask mode | singleUseraccess ask large quantity otherUserofresource source |
| manage manageEndpointabnormal common access ask | Non-Administrator IP/Token access ask /admin/* |
| ID Enumerationcheck test | singleSessioninitiate out order sequence ID Request |
| Permissionchange update audit plan | AllRole/PermissionModifyRecordand report alert |
| Batchoperation abnormal common | singleUsershort time between internalModify/Deletelarge quantityRecord |
| Cross-Tenantaccess ask | anyRequestof tenant_id and Token inofnot match config |

---

## Appendix A:WooYun vulnerabilityStatisticsremit total

| Domain | Casetotal number | high-risk percentage | version plan cover cover degree |
|------|---------|---------|------------|
| AuthenticationBypass | 8,846 | 58-88% | part part(Password Resetrelated key) |
| **AuthorizationBypass(version plan audit core)** | **6,838** | **51-86%** | **Completecover cover** |
| Information Disclosure | 6,446 | 64.7% | part part(API through degreeObtain) |
| Financialtamper change | 2,919 | 68-83% | between connect(Statusbypass permission) |
| logic logic missing flaw | 1,679 | 65-75% | part part(Statusmachine bypass permission) |
| Misconfiguration | 1,796 | 72.6% | part part(UnauthorizedEndpoint) |

## Appendix B:Multi-Tenant SaaS bypass permission test Checklist(Canbreak version)

```
=== Horizontal Authorization Bypass (IDOR) ===
[] All GET Endpoint:Replace URL/Parameterinofresource source ID
[] All POST/PUT Endpoint:ReplaceRequest Bodyinofresource source ID
[] All DELETE Endpoint:ReplaceTargetresource source ID
[] ID operation manipulate:order sequenceReplace/Parameter Pollution/number array inject inject/JSON Nested/Encoding Bypass
[] Cross-Tenant:Replace tenant_id/org_id access ask otherTenantData
[] list/searchInterface:whetherDisclosureotherTenantData
[] FileDownload:whether hasOwnership Check
[] Exportfunction can:whetherlimit makeaswhen firstTenantData

=== Vertical Authorization Bypass ===
[] manage manageEndpoint:useRegular User Token access askAll /admin/* Endpoint
[] Parameterprovide permission:Registration/Updatetime inject inject role/is_admin Parameter
[] HTTP Methodswitch change:GET->POST->PUT->DELETE->PATCH
[] PathBypass:case/Encoding/part number inject inject/Path bypass
[] JWT tamper change:Modify role/permissions/tenant_id Field
[] Tenant Administrator -> Platformmanage manage:access askPlatformlevelEndpoint

=== Unauthorized Access ===
[] manage manage backend console:no Token access ask /admin, /console, /manage
[] API Document:/swagger, /api-docs, /openapi.json
[] monitor controlEndpoint:/actuator/*, /metrics, /health, /debug
[] Databasemanage manage:/phpmyadmin, /druid
[] framework architectureEndpoint:Spring Actuator, Django Debug Toolbar
[] 403 Bypass:Methodswitch change/Pathvariant/Encoding Bypass
[] serious set towardBypass:X-Forwarded-For, X-Original-URL

=== ArbitraryX ===
[] Arbitrary Accountaccess ask:no need toCredentialas other person identity copy operation
[] Arbitrary Modification:Modifyother person/otherTenantofConfigurationandData
[] ArbitraryRegistration:BypassRegistrationlimit make/ please code/Domain Namelimit make
[] Arbitrary Viewing:BatchExport/Administrator image
[] Arbitrary Deletion:Deleteother person resource source
[] Arbitrary Operation:Regular UserExecuteaudit batch/initiate deployetc.manage manage operation
```

---

*versionTest PlanBased on the methodology from 22,132 real WooYun vulnerability casescompile write, cover coverAuthorization Domain 6,838 CaseofCompleteAttack PatternCategory.AllTest Itemaveragedirectly usableuseforMulti-Tenant SaaS PlatformofSecureassess assess.*
