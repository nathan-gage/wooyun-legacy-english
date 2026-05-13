# Multi-Tenant SaaS PlatformAuthorization BypassTest Plan

## 1. Test ScopeandTarget

### 1.1 Test Objective

ValidateMulti-Tenant SaaS Platforminthe followingthreeDimensionofAccess Controlwhether all:

| Dimension | model type | audit core ask problem |
|------|---------|---------|
| Horizontal Authorization Bypass (IDOR) | samePermissionUser A access askUser B ofresource source | resource source identifier identify symbolwhetherbe correct confirm appraise permission? |
| Vertical Authorization Bypass | LowPermissionUserExecuteHighPermissionoperation | RolePermissionboundary boundarywhethersevere format? |
| Unauthorized Access | notLogin/noCredentialUseraccess ask affected protect protect resource source | Authenticationmachine makewhetherall cover cover? |

### 1.2 Test Scope

- All REST API Endpoint(CRUD operation)
- Cross-TenantDataisolation
- File/Object Storageaccess ask
- BatchoperationInterface
- Export/report tableInterface
- WebSocket continuous connect(such ashas)
- GraphQL check query(such ashas)

### 1.3 Prerequisites

accurate preparethe followingTest Account(most less):

| AccountID | Role | Tenant | Purpose |
|---------|------|------|------|
| A1 | Super Administrator | Tenant A | Vertical Authorization Bypassbase accurate |
| A2 | wildAdministrator | Tenant A | Vertical Authorization Bypasstest |
| A3 | Regular User | Tenant A | Horizontal Authorization Bypass + Vertical Authorization Bypass |
| A4 | only readUser | Tenant A | Vertical Authorization Bypasstest |
| B1 | wildAdministrator | Tenant B | Cross-Tenantbypass permission |
| B2 | Regular User | Tenant B | Cross-TenantHorizontal Authorization Bypass |
| -- | (noCredential) | -- | Unauthorized Accesstest |

---

## 2. Horizontal Authorization Bypass (IDOR) test

### 2.1 test principle manage

IDOR (Insecure Direct Object Reference) ofaudit core is:attack attack personPasstamper changeRequestinofresource source identifier identify symbol(ID/UUID/Filenameetc.), access ask not attribute for self ownofresource source.

### 2.2 Test Casematrix matrix

#### TC-IDOR-001: based onPathParameterof IDOR

**Target**: All `/{resource}/{id}` modeofEndpoint

```
Step:
1. useAccount A3 Createresource source, Recordresource source ID(false setas res_123)
2. useAccount B2 of Token SendRequest:
 GET /api/v1/orders/res_123
 Authorization: Bearer <B2_token>
3. ValidateResponse

expected period: 403 Forbidden or 404 Not Found
Failure Indicators: 200 OK andReturndone A3 ofData
```

**cover coverEndpointclear single**(one by one test):

```
GET /api/v1/users/{userId}
GET /api/v1/users/{userId}/profile
PUT /api/v1/users/{userId}
DELETE /api/v1/users/{userId}
GET /api/v1/orders/{orderId}
PUT /api/v1/orders/{orderId}
GET /api/v1/invoices/{invoiceId}
GET /api/v1/projects/{projectId}
GET /api/v1/documents/{docId}
GET /api/v1/reports/{reportId}
GET /api/v1/organizations/{orgId}/members...(root according real actual API supplement topup)
```

#### TC-IDOR-002: based on check queryParameterof IDOR

```
Step:
1. use A3 of Token Send:
 GET /api/v1/messages?user_id=<B2_user_id>
2. use A3 of Token Send:
 GET /api/v1/audit-logs?tenant_id=<tenant_B_id>

expected period: ReturnEmptycollector 403, notReturn B2 ofData
Failure Indicators: Returndone otherUser/TenantofData
```

#### TC-IDOR-003: based onRequest BodyParameterof IDOR

```
Step:
1. use A3 of Token Send:
 PUT /api/v1/profile
 {
 "user_id": "<B2_user_id>",
 "email": "attacker@evil.com"
 }
2. Check B2 of profile whetherbeModify

expected period: Serverignore user_id ParameterorReturn 403
Failure Indicators: B2 of email beModify
```

#### TC-IDOR-004: based onFile/for citeuseof IDOR

```
Step:
1. use A3 UploadFile, ObtainFile URL/Key:
 POST /api/v1/files/upload -> Return file_key: "abc123.pdf"
2. use B2 of Token access ask:
 GET /api/v1/files/abc123.pdf
3. AttemptDirectaccess askStorage URL(such as S3 pre-signed URL Disclosure)

expected period: 403 or 404
Failure Indicators: B2 canDownload A3 ofFile
```

#### TC-IDOR-005: Batchoperationinof IDOR

```
Step:
1. use A3 of Token SendBatchoperation:
 POST /api/v1/orders/batch-delete
 {
 "ids": ["own_order_1", "B2_order_1", "B2_order_2"]
 }

expected period: onlyDelete own_order_1, other Returnerrororbe ignore
Failure Indicators: B2 ofOrderbeDelete
```

#### TC-IDOR-006: ID Predictableness test

```
Step:
1. continuous continueCreate 3 resource source, Record ID
2. Analyze ID mode:
 - self increase integer number (1001, 1002, 1003) -> Highrisk
 - short sequence list UUID -> inrisk
 - UUIDv4 -> Lowrisk(but still need appraise permission)
3. such asif ID Predictable, AttemptEnumeration:
 for id in range(1000, 1010):
 GET /api/v1/resources/{id}

expected period: that is use ID Canguessing, appraise permission should stop access ask
Failure Indicators: canPassEnumerationObtainother personData
```

#### TC-IDOR-007: Cross-Tenant IDOR(Multi-Tenantaudit core)

```
Step:
1. use A3 of Token, ReplaceRequestinAllTenantidentifier identify:
 GET /api/v1/tenants/<tenant_B_id>/users
 GET /api/v1/tenants/<tenant_B_id>/settings
 GET /api/v1/tenants/<tenant_B_id>/billing
2. Checkwhether existshidden includeofTenantabove under text(Header/Cookie/Token inof tenant_id):
 - Modify X-Tenant-ID header
 - Modify JWT inof tenant claim(such asif JWT not add secret onlySignature, should notgenerate valid)

expected period: AllCross-TenantRequestReturn 403
Failure Indicators: ReturndoneTenant B ofanyData
```

#### TC-IDOR-008: key connect resource sourceofbetween connect IDOR

```
Step:
1. A3 Createoneitemsdirectory proj_A
2. B2 Createoneitemsdirectory proj_B, other under has any service task_B1
3. use A3 of Token:
 GET /api/v1/projects/proj_B/tasks/task_B1
 POST /api/v1/projects/proj_A/tasks
 {
 "parent_project": "proj_B" // Attemptcrossitemsdirectory key connect
 }

expected period: reject reject crossitemsdirectory/Cross-Tenantofkey connect operation
```

### 2.3 IDOR test self dynamic izeScriptmodel template

```python
#!/usr/bin/env python3
"""IDOR self dynamic ize testScriptmodel template"""

import requests
import json
from dataclasses import dataclass

@dataclass
class TestAccount:
 name: str
 token: str
 tenant_id: str
 user_id: str

# === Configuration ===
BASE_URL = "https://api.your-saas.com"

VICTIM = TestAccount(name="victim_A3",
 token="Bearer eyJ...",
 tenant_id="tenant_a_id",
 user_id="user_a3_id")

ATTACKER = TestAccount(name="attacker_B2",
 token="Bearer eyJ...",
 tenant_id="tenant_b_id",
 user_id="user_b2_id")

# === IDOR Endpointlist ===
IDOR_ENDPOINTS = [{"method": "GET", "path": "/api/v1/users/{user_id}"},
 {"method": "GET", "path": "/api/v1/users/{user_id}/profile"},
 {"method": "PUT", "path": "/api/v1/users/{user_id}", "body": {"name": "hacked"}},
 {"method": "DELETE", "path": "/api/v1/users/{user_id}"},
 {"method": "GET", "path": "/api/v1/orders/{order_id}"},
 {"method": "GET", "path": "/api/v1/tenants/{tenant_id}/settings"},
 #... AddAllEndpoint]

def test_idor(endpoint, victim: TestAccount, attacker: TestAccount):
 """use attacker of token access ask victim ofresource source"""
 path = endpoint["path"].format(user_id=victim.user_id,
 tenant_id=victim.tenant_id,
 order_id="victim_order_id", # Replaceasreal actual ID)
 url = f"{BASE_URL}{path}"
 headers = {"Authorization": attacker.token, "Content-Type": "application/json"}

 method = endpoint["method"]
 body = endpoint.get("body")

 resp = getattr(requests, method.lower())(url, headers=headers, json=body)

 status = "PASS" if resp.status_code in (403, 404, 401) else "FAIL"
 print(f"[{status}] {method} {path} -> {resp.status_code}")

 if status == "FAIL":
 print(f"!!! bypass permissionSuccess, Response: {resp.text[:200]}")

 return status

# === Execute ===
if __name__ == "__main__":
 results = {"PASS": 0, "FAIL": 0}
 for ep in IDOR_ENDPOINTS:
 result = test_idor(ep, VICTIM, ATTACKER)
 results[result] += 1

 print(f"\n=== Resultremit total ===")
 print(f"Pass: {results['PASS']}, Failure: {results['FAIL']}")
```

---

## 3. Vertical Authorization Bypass(Privilege Escalation)test

### 3.1 test principle manage

LowPermissionRoleAttemptExecuteHighPermissionRole can advancelinesofoperation.key inject point:Role /API EndpointPermissionValidate/function can levelAccess Control.

### 3.2 Permissionmatrix matrix(test first first create standalone)

firstConfirmSystemofPermissionmodel type, create standalonesuch asunder matrix matrix:

| API Endpoint | Super Administrator | Administrator | Regular User | only readUser | notLogin |
|---------|:---------:|:-----:|:------:|:------:|:-----:|
| GET /api/v1/users | Y | Y | N | N | N |
| POST /api/v1/users | Y | Y | N | N | N |
| DELETE /api/v1/users/{id} | Y | N | N | N | N |
| GET /api/v1/settings | Y | Y | Y | Y | N |
| PUT /api/v1/settings | Y | Y | N | N | N |
| GET /api/v1/admin/dashboard | Y | N | N | N | N |
| POST /api/v1/roles | Y | N | N | N | N |
| GET /api/v1/billing | Y | Y | N | N | N |
| POST /api/v1/export/all-data | Y | N | N | N | N |
| DELETE /api/v1/tenants/{id} | Y | N | N | N | N |

### 3.3 Test Case

#### TC-VERT-001: Regular Useraccess askAdministratorEndpoint

```
Step:
1. use A3(Regular User)of Token one by oneRequestAdministratorEndpoint:
 GET /api/v1/admin/dashboard
 GET /api/v1/admin/users
 POST /api/v1/admin/users
 DELETE /api/v1/admin/users/{userId}
 PUT /api/v1/admin/settings
 GET /api/v1/admin/audit-logs
 POST /api/v1/admin/export

expected period: AllReturn 403 Forbidden
Failure Indicators: any oneReturn 200/201
```

#### TC-VERT-002: only readUserExecutewrite operation

```
Step:
1. use A4(only readUser)of Token:
 POST /api/v1/orders {"item": "test"}
 PUT /api/v1/orders/{id} {"status": "cancelled"}
 DELETE /api/v1/orders/{id}
 POST /api/v1/documents {"title": "test"}
 PUT /api/v1/profile {"name": "hacked"}

expected period: AllReturn 403
Failure Indicators: write operationSuccessExecute
```

#### TC-VERT-003: self I provide permission -- Roletamper change

```
Step:
1. use A3 of Token Modifyself ownofRole:
 PUT /api/v1/users/A3_id
 {
 "role": "admin"
 }
2. use A3 of Token to self ownAddPermission:
 POST /api/v1/users/A3_id/roles
 {
 "roles": ["admin", "super_admin"]
 }
3. use A3 of Token CreateHighPermission API Key:
 POST /api/v1/api-keys
 {
 "permissions": ["*"],
 "role": "admin"
 }

expected period: Allbe reject reject(403)
Failure Indicators: RoleorPermissionbeModify
```

#### TC-VERT-004: Administratorbypass permissionasSuper Administrator

```
Step:
1. use A2(wildAdministrator)of Token:
 DELETE /api/v1/tenants/tenant_a_id (DeleteTenant)
 PUT /api/v1/system/config (ModifySystemConfiguration)
 GET /api/v1/system/all-tenants (ViewAllTenant)
 POST /api/v1/super-admin/impersonate (model otherUser)
 PUT /api/v1/users/A1_id/role (ModifySuper Administrator)

expected period: AllReturn 403
Failure Indicators: any operationSuccess
```

#### TC-VERT-005: HTTP Methodcover coverBypass

```
Step:
1. for only allow allow GET ofEndpointAttemptotherMethod:
 PUT /api/v1/readonly-resource/{id}
 DELETE /api/v1/readonly-resource/{id}
 PATCH /api/v1/readonly-resource/{id}

2. AttemptMethodcover cover:
 POST /api/v1/admin/users
 X-HTTP-Method-Override: DELETE

 POST /api/v1/admin/users
 X-HTTP-Method: PUT

 GET /api/v1/admin/users?_method=DELETE

expected period: Non-AuthorizationMethodReturn 405 or 403
Failure Indicators: PassMethodcover coverSuccessExecutedoneUnauthorizedoperation
```

#### TC-VERT-006: ParameterlevelPermissionBypass

```
Step:
1. Regular UserModifyRequest Bodyinofhidden hidden/AdministratorField:
 POST /api/v1/orders
 {
 "item": "product_1",
 "price": 0.01, // Attempttamper change price format
 "discount": 99, // Attemptset set discount deduct
 "is_admin_order": true, // AttemptAdministratoridentifier record
 "bypass_approval": true // AttemptBypassaudit batch
 }

2. UserRegistrationtime inject injectRole:
 POST /api/v1/register
 {
 "email": "new@test.com",
 "password": "pass123",
 "role": "admin", // inject injectRole
 "tenant_id": "target_tenant" // inject injectTenant
 }

expected period: Serverignore this someFieldorclear confirm reject reject
Failure Indicators: Non-AuthorizationFieldbe connect affected and generate valid
```

#### TC-VERT-007: JWT/Token tamper change

```
Step:
1. decode code when first JWT(base64), Modify payload:
 - Modify "role": "user" -> "role": "admin"
 - Modify "tenant_id": "a" -> "tenant_id": "b"
 - Modify "user_id" asotherUser
 - notModifySignature, DirectSend

2. Attempt None algorithm method attack attack:
 - will JWT header of alg changeas "none"
 - move removeSignaturepart part

3. AttemptweakKeySignature:
 - usecommon seen weakKey("secret", "123456", "password")serious newSignature

4. Attemptexpired Token:
 - useusealready expiredof Token access ask

expected period: AllReturn 401 Unauthorized
Failure Indicators: tamper change afterof Token be connect affected
```

#### TC-VERT-008: Multi-TenantRoleisolation

```
Step:
1. B1 isTenant B ofAdministrator
2. use B1 of Token Attemptmanage manageTenant A ofresource source:
 GET /api/v1/tenants/tenant_a/users
 POST /api/v1/tenants/tenant_a/users
 PUT /api/v1/tenants/tenant_a/settings
 DELETE /api/v1/tenants/tenant_a/projects/{id}

expected period: B1 ofAdministratorPermissiononlyinTenant B internalValid, forTenant A Return 403
Failure Indicators: B1 can manage manageTenant A
```

### 3.4 Vertical Authorization Bypassself dynamic izeScriptmodel template

```python
#!/usr/bin/env python3
"""Vertical Authorization Bypassself dynamic ize test"""

import requests

BASE_URL = "https://api.your-saas.com"

TOKENS = {
 "super_admin": "Bearer eyJ...",
 "admin": "Bearer eyJ...",
 "user": "Bearer eyJ...",
 "readonly": "Bearer eyJ...",
}

# Permissionmatrix matrix: (method, path, allowed_roles)
PERMISSION_MATRIX = [("GET", "/api/v1/admin/dashboard", ["super_admin"]),
 ("GET", "/api/v1/admin/users", ["super_admin", "admin"]),
 ("POST", "/api/v1/admin/users", ["super_admin", "admin"]),
 ("DELETE", "/api/v1/admin/users/test_id", ["super_admin"]),
 ("PUT", "/api/v1/settings", ["super_admin", "admin"]),
 ("GET", "/api/v1/orders", ["super_admin", "admin", "user"]),
 ("POST", "/api/v1/orders", ["super_admin", "admin", "user"]),
 ("GET", "/api/v1/reports/export", ["super_admin", "admin"]),
 ("DELETE", "/api/v1/tenants/test_tenant", ["super_admin"]),
 ("POST", "/api/v1/roles", ["super_admin"]),
 #... supplement topupAllEndpoint]

def test_vertical_escalation():
 results = {"PASS": 0, "FAIL": 0}

 for method, path, allowed_roles in PERMISSION_MATRIX:
 for role, token in TOKENS.items():
 url = f"{BASE_URL}{path}"
 headers = {"Authorization": token}
 resp = getattr(requests, method.lower())(url, headers=headers)

 if role in allowed_roles:
 expected = "ALLOWED"
 passed = resp.status_code in (200, 201, 204)
 else:
 expected = "DENIED"
 passed = resp.status_code in (401, 403, 404)

 status = "PASS" if passed else "FAIL"
 results[status] += 1

 if not passed:
 print(f"[FAIL] {role:12s} {method:6s} {path:40s} "
 f"-> {resp.status_code} (expected {expected})")

 print(f"\n=== Result === PASS: {results['PASS']}, FAIL: {results['FAIL']}")

if __name__ == "__main__":
 test_vertical_escalation()
```

---

## 4. Unauthorized Accesstest

### 4.1 test principle manage

ValidateAllrequiresAuthenticationofEndpointinmissing lessValidCredentialtimewhethercorrect confirm reject reject access ask.

### 4.2 Test Case

#### TC-UNAUTH-001: no Token access ask

```
Step:
1. forAll API EndpointSendRequest, not with Authorization header:
 GET /api/v1/users
 GET /api/v1/orders
 GET /api/v1/admin/dashboard
 POST /api/v1/orders {"item": "test"}
 PUT /api/v1/profile {"name": "test"}

expected period: AllReturn 401 Unauthorized
Failure Indicators: anyEndpointReturn 200/201 and include includeBusiness Data
```

** avoidWhitelist**(this someEndpointshouldthis allow allow name access ask):

```
POST /api/v1/auth/login
POST /api/v1/auth/register
POST /api/v1/auth/forgot-password
GET /api/v1/health
GET /api/v1/public/*
```

#### TC-UNAUTH-002: no valid Token access ask

```
Step:
1. useuseeach type no valid Token:
 Authorization: Bearer invalid_token_string
 Authorization: Bearer eyJhbGciOiJIUzI1NiJ9.eyJ0ZXN0IjoidGVzdCJ9.invalid
 Authorization: Bearer null
 Authorization: Bearer undefined
 Authorization: Bearer ""
 Authorization: Basic dGVzdDp0ZXN0 (errorofAuthenticationtype)
 Authorization: bearer <valid_token> (small write bearer)

expected period: AllReturn 401
Failure Indicators: anyRequestbe connect affected
```

#### TC-UNAUTH-003: expired/ Token

```
Step:
1. ObtainValid Token
2. Call outInterface:
 POST /api/v1/auth/logout
3. usealready outof Token continue access ask:
 GET /api/v1/users/me
4. usealready expiredof Token(mobile dynamicModify exp oretc.pending expired)access ask

expected period: Return 401
Failure Indicators: already out/expiredof Token still Valid
```

#### TC-UNAUTH-004: API EndpointDiscover

```
Step:
1. Attemptcommon seenofnot protect protectEndpoint:
 GET /api/v1/swagger.json
 GET /api/v1/openapi.json
 GET /api/docs
 GET /api/v1/graphql (GraphQL introspection)
 GET /api/v1/debug
 GET /api/v1/metrics
 GET /api/v1/actuator
 GET /api/v1/actuator/env
 GET /api/v1/internal/*
 GET /.env
 GET /config
 GET /api/v1/test

expected period: generate asset environment environment under debugging/DocumentEndpointshouldbe disableuseorrequiresAuthentication
Failure Indicators: exposed internal API result structure/environment environment change quantityordebugging information
```

#### TC-UNAUTH-005: CORS Configurationtest

```
Step:
1. Sendexpected checkRequest:
 OPTIONS /api/v1/users
 Origin: https://evil-site.com

2. CheckResponseHeader:
 Access-Control-Allow-Origin: * -> Highrisk
 Access-Control-Allow-Origin: https://evil.com -> Highrisk
 Access-Control-Allow-Credentials: true -> and * array combine isSeverevulnerability

expected period: CORS only allow allow already notifyofFrontendDomain Name
Failure Indicators: allow allowArbitrary Origin and with Credentials
```

#### TC-UNAUTH-006: AuthenticationBypasstechnical

```
Step:
1. PathTraversalBypass:
 GET /api/v1/public/../admin/dashboard
 GET /api/v1/./admin/users
 GET /api//v1//admin//users
 GET /api/v1/admin/users/..;/public (Tomcat special has)

2. caseBypass:
 GET /api/v1/ADMIN/dashboard
 GET /api/v1/Admin/Users

3. URL Encoding Bypass:
 GET /api/v1/%61dmin/dashboard (a -> %61)
 GET /api/v1/admin%2Fusers (/ -> %2F)
 GET /api/v1/admin/dashboard%00 (null byte)

4. HTTP version version level:
 Send HTTP/1.0 Request(some someinbetween itemCancan notCheckAuthentication)

5. Request private:
 Transfer-Encoding: chunked + Content-Length not one cause

expected period: Allbe correct confirm reject reject
Failure Indicators: PassEncoding/Pathtechnical BypassdoneAuthenticationCheck
```

#### TC-UNAUTH-007: state resource sourceandUploadFile

```
Step:
1. Passalready notifyorguessingofPathDirectaccess ask:
 GET /uploads/user_avatar_A3.jpg
 GET /static/exports/report_20240101.pdf
 GET /api/v1/files/download?path=../../etc/passwd

expected period: private hasFilerequiresAuthentication, PathTraversalbe stop
Failure Indicators: Canas nameDownloadUserUploadofprivate hasFile
```

### 4.3 Unauthorized Accessself dynamic izeScriptmodel template

```python
#!/usr/bin/env python3
"""Unauthorized AccessScandevice"""

import requests

BASE_URL = "https://api.your-saas.com"

# requiresAuthenticationofEndpoint(from API Document/routeScaninObtain)
PROTECTED_ENDPOINTS = [("GET", "/api/v1/users"),
 ("GET", "/api/v1/users/me"),
 ("GET", "/api/v1/orders"),
 ("POST", "/api/v1/orders"),
 ("GET", "/api/v1/admin/dashboard"),
 ("GET", "/api/v1/settings"),
 ("GET", "/api/v1/billing"),
 ("GET", "/api/v1/reports"),
 #... AllEndpoint]

# notrequiresAuthenticationofEndpoint(WhitelistValidate)
PUBLIC_ENDPOINTS = [("POST", "/api/v1/auth/login"),
 ("POST", "/api/v1/auth/register"),
 ("GET", "/api/v1/health"),]

# sensitive sensitiveEndpoint(should notexpose exposure)
SENSITIVE_ENDPOINTS = [("GET", "/api/docs"),
 ("GET", "/api/v1/swagger.json"),
 ("GET", "/api/v1/openapi.json"),
 ("GET", "/debug"),
 ("GET", "/metrics"),
 ("GET", "/api/v1/actuator"),
 ("GET", "/api/v1/actuator/env"),
 ("GET", "/.env"),
 ("GET", "/api/v1/graphql"), # introspection]

INVALID_TOKENS = [None, # no header
 "invalid_token", # machine character symbol string
 "null", # null character symbol string
 "", # Emptycharacter symbol string
 "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJ0ZXN0IjoidGVzdCJ9.", # alg:none]

def test_no_auth():
 """testNo Authenticationaccess ask affected protect protectEndpoint"""
 print("=== test 1: no Token access ask affected protect protectEndpoint ===")
 fails = 0
 for method, path in PROTECTED_ENDPOINTS:
 url = f"{BASE_URL}{path}"
 resp = getattr(requests, method.lower())(url)
 if resp.status_code not in (401, 403):
 print(f"[FAIL] {method} {path} -> {resp.status_code}")
 fails += 1
 print(f"Failure: {fails}/{len(PROTECTED_ENDPOINTS)}\n")

def test_invalid_tokens():
 """test no valid Token"""
 print("=== test 2: no valid Token ===")
 fails = 0
 test_path = "/api/v1/users/me" # useone code table nessEndpoint
 for token in INVALID_TOKENS:
 headers = {}
 if token is not None:
 headers["Authorization"] = f"Bearer {token}"
 resp = requests.get(f"{BASE_URL}{test_path}", headers=headers)
 if resp.status_code not in (401, 403):
 print(f"[FAIL] Token='{token}' -> {resp.status_code}")
 fails += 1
 print(f"Failure: {fails}/{len(INVALID_TOKENS)}\n")

def test_sensitive_exposure():
 """test sensitive sensitiveEndpointexpose exposure"""
 print("=== test 3: sensitive sensitiveEndpointexpose exposure ===")
 for method, path in SENSITIVE_ENDPOINTS:
 url = f"{BASE_URL}{path}"
 resp = getattr(requests, method.lower())(url)
 if resp.status_code == 200:
 print(f"[WARN] {path} Cancompany open access ask! Content-Type: {resp.headers.get('Content-Type')}")

if __name__ == "__main__":
 test_no_auth()
 test_invalid_tokens()
 test_sensitive_exposure()
```

---

## 5. Multi-Tenantspecialitemstest

### 5.1 TenantisolationValidate

#### TC-TENANT-001: Databaselayer isolation

```
Step:
1. Tenant A Create 100 conditionRecord
2. Tenant B check query list:
 GET /api/v1/orders?page=1&size=1000
3. CheckReturnDatainwhetherinclude includeTenant A ofRecord

expected period: Tenant B ofcheck query reject notReturnTenant A ofData
Failure Indicators: listinout current done otherTenantofData
```

#### TC-TENANT-002: search/through filter device isolation

```
Step:
1. Tenant A Createidentifier problemas "IDOR_TEST_MARKER" ofresource source
2. Tenant B search:
 GET /api/v1/search?q=IDOR_TEST_MARKER
 GET /api/v1/orders?filter=title:IDOR_TEST_MARKER

expected period: Tenant B search nottothis resource source
Failure Indicators: searchResultDisclosuredoneCross-TenantData
```

#### TC-TENANT-003: combine/StatisticsDataisolation

```
Step:
1. useTenant B of Token access askStatisticsInterface:
 GET /api/v1/dashboard/stats
 GET /api/v1/analytics/overview
2. CheckReturnofnumber characterwhetheronly reverse mapTenant B ofData
 (CanPassalready notifyDataquantityValidate)

expected period: StatisticsDataonly include include when firstTenantofData
Failure Indicators: Statisticsnumber character include include done otherTenantofData
```

#### TC-TENANT-004: Tenantabove under text switch change

```
Step:
1. Usersame time attribute for manyTenanttime:
 GET /api/v1/orders
 X-Tenant-ID: tenant_a

 GET /api/v1/orders
 X-Tenant-ID: tenant_b

2. Attemptswitch changetonot attribute for self ownofTenant:
 GET /api/v1/orders
 X-Tenant-ID: tenant_c (Usernot attribute for Tenant)

expected period: can onlyaccess ask self own attributeTenantofData
Failure Indicators: can switch changetoArbitraryTenant
```

---

## 6. testExecuteflow process

### 6.1 Endpointcollect collect

inbefore formal testing, firstCompletecollect collectAll API Endpoint:

```bash
# Method 1: from OpenAPI/Swagger Documentprovide take
curl -s https://api.your-saas.com/api/docs/swagger.json | \
 jq -r '.paths | to_entries[] |.key as $path |.value | to_entries[] | "\(.key | ascii_upcase) \($path)"'

# Method 2: fromFrontend JS inprovide take
# DownloadFrontendbreak includeFile, grep API Path
curl -s https://app.your-saas.com/main.js | grep -oP '/api/v[0-9]+/[a-zA-Z0-9/_-]+' | sort -u

# Method 3: fromServerCodeprovide take (such ashasCodeaccess ask permission)
grep -rn '@(Get|Post|Put|Delete|Patch)Mapping\|@RequestMapping\|router\.\(get\|post\|put\|delete\)' src/ --include="*.java" --include="*.ts" --include="*.py"

# Method 4: flow quantity packet capture
# use mitmproxy/Burp Suite code manage correct common useuseApplication, collect collectAll API Call
```

### 6.2 Executeorder sequence

```
Phase 1: (Day 1)
+-- collect collectAll API Endpoint
+-- create standalonePermissionmatrix matrix
+-- accurate prepareTest Account
+-- ConfigurationTest Environment

Phase 2: Unauthorized Access (Day 2)
+-- TC-UNAUTH-001 ~ 007
+-- identifier recordAllnotrequiresAuthenticationthat isCanaccess askofEndpoint
+-- ValidateWhitelistEndpointofcombine manage ness

Phase 3: Horizontal Authorization Bypass IDOR (Day 3-4)
+-- TC-IDOR-001 ~ 008
+-- sameTenantinternalUserbetweenof IDOR
+-- Cross-Tenant IDOR
+-- Batchoperation IDOR

Phase 4: Vertical Authorization Bypass (Day 5-6)
+-- TC-VERT-001 ~ 008
+-- Permissionmatrix matrix all quantityValidate
+-- Token tamper change test
+-- Parameterinject inject test

Phase 5: Multi-Tenantspecialitems (Day 7)
+-- TC-TENANT-001 ~ 004
+-- DataisolationValidate
+-- search/ combineDisclosure

Phase 6: reportandrepeat test (Day 8)
+-- remit totalAllDiscover
+-- assess assessRisk Level
+-- fix repeat after repeat test
```

---

## 7. report model template

### 7.1 vulnerability report format mode

EachDiscoverofvulnerability bythe followingformat modeRecord:

```
### [CRITICAL/HIGH/MEDIUM/LOW] vulnerability identifier problem

**Vulnerability Type**: Horizontal Authorization Bypass / Vertical Authorization Bypass / Unauthorized Access
**impact responseEndpoint**: `GET /api/v1/orders/{orderId}`
**CVSS assess part**: 8.6 (High)

** description**:
User A CanasPassModify URL inof orderId Parameteraccess askUser B ofOrderData,
ServernotValidateRequestpersonwhether isresource sourceAllperson.

**Reproduction Steps**:
1. useUser A of Token SendRequest
2. will orderId ReplaceasUser B ofOrder ID
3. ObserveReturndoneUser B ofOrderdetailed details

**Request**:
GET /api/v1/orders/order_B_12345
Authorization: Bearer <user_A_token>

**Response**:
HTTP/1.1 200 OK
{
 "order_id": "order_B_12345",
 "user_id": "user_B",
 "items": [...]
}

**Impact Scope**:
- anyAuthenticationUserCanReadArbitraryUserofOrderData
- involving PII(Personal Information)Disclosure
- impact responseAllTenant

**Remediation Recommendation**:
1. inDataaccess ask layerAddAllpersonValidate: `WHERE order_id =? AND user_id =?`
2. useusenotPredictableof UUID replace code self increase ID(manipulate deep defense defense, Non-primary need fix repeat)
3. AddRequestLogaudit plan

**fix repeatPriority**: P0 - standalone that is fix repeat
```

### 7.2 risk assess level identifier accurate

| etc.level | set define | Example |
|------|------|------|
| CRITICAL | large scale modelDataDisclosure/Cross-TenantComprehensive | crossTenant Administratorconnect manage/BatchDataExportno appraise permission |
| HIGH | single one sensitive sensitive resource sourceAuthorization Bypass | IDOR Readother personOrder/vertical vertical provide permission Administrator |
| MEDIUM | has limitInformation Disclosureoraffected limit write operation | only read IDOR(Non-sensitive sensitiveData)/part part manage manage function can expose exposure |
| LOW | information collect collect type/manage comment risk | API Documentexpose exposure/errorInformation Disclosureinternal partPath |

---

## 8. commonuseToolclear single

| Tool | Purpose | type |
|------|------|------|
| Burp Suite Pro | mobile dynamic test + self dynamicScan | code manage/Scandevice |
| OWASP ZAP | self dynamic izeSecureScan | open sourceScandevice |
| Postman/Insomnia | API Requeststructure forge | API Client |
| jwt.io / jwt_tool | JWT Analyzeandtamper change | JWT Tool |
| ffuf / dirsearch | EndpointDiscoverandmodel test | directory recordBrute Force |
| mitmproxy | flow quantityInterceptandModify | code manage |
| Autorize (Burp item) | self dynamic ize bypass permission check test | Burp item |
| AuthMatrix (Burp item) | Permissionmatrix matrix self dynamicValidate | Burp item |
| Python requests | self set define testScript | Script |
| nuclei | based on model templateofvulnerabilityScan | Scandevice |

### Burp Suite Autorize item useuseMethod

```
1. Autorize item
2. ConfigurationLowPermissionUserof Cookie/Token
3. asHighPermissionUsercorrect common Application
4. Autorize self dynamicuseLowPermission Token ReplayEachRequest
5. for ratioResponseerror abnormal, identifier record inbypass permission point
```

---

## 9. Checkclear single (Checklist)

### Horizontal Authorization Bypass (IDOR)

- [] All CRUD EndpointofPathParameter ID already test
- [] Allcheck queryParameterinof ID/citeusealready test
- [] Request Bodyinof ID Fieldalready test(Mass Assignment)
- [] FileUpload/DownloadEndpointalready test
- [] BatchoperationInterfacealready test
- [] ID Predictableness already assess assess
- [] Cross-Tenantresource source citeusealready test
- [] key connect resource sourceofbetween connect citeusealready test
- [] GraphQL check queryinof ID Parameteralready test(such assuitableuse)
- [] WebSocket messageinof ID already test(such assuitableuse)

### Vertical Authorization Bypass

- [] Permissionmatrix matrix already create standalone and all quantityValidate
- [] EachRoleforEachEndpointofaccess ask alreadyValidate
- [] self I provide permission(Modify role Field)already test
- [] HTTP Methodcover cover already test
- [] AdministratorEndpointforRegular Userofdefense protect already test
- [] only readUserofwrite operation already test
- [] JWT/Token tamper change already test
- [] ParameterlevelPermissionBypassalready test(hidden hiddenFieldinject inject)
- [] Cross-TenantRoleisolation already test

### Unauthorized Access

- [] AllEndpointno Token access ask already test
- [] no valid/expired/ Token already test
- [] company openEndpointWhitelistalready audit check
- [] sensitive sensitiveEndpointexpose exposure alreadyCheck(swagger, debug, metrics)
- [] CORS ConfigurationalreadyValidate
- [] PathTraversal/Encoding Bypassalready test
- [] state resource source/UploadFileofAccess Controlalready test
- [] Authenticationtype mix already test(Bearer vs Basic)

### Multi-Tenant

- [] list check queryofTenantisolation alreadyValidate
- [] search function canofTenantisolation alreadyValidate
- [] combine/StatisticsDataofTenantisolation alreadyValidate
- [] Tenantswitch change function canofSecureness alreadyValidate
- [] shared resource sourceofAccess ControlalreadyValidate

---

## 10. Remediation Recommendationtotal rule

### architecture structure layer page

1. **system one appraise permissioninbetween item**: All API Requestmustthrough through system oneofAuthenticationandAuthorizationinbetween item, not allow allowEndpointselflinesreal current appraise permission
2. **resource source return attributeValidate**: Dataaccess ask layer strong makeBindingwhen firstUser/Tenant, SQL check query self dynamic attach add `tenant_id =?` condition
3. **most smallPermissionprinciple rule**: default auth reject reject, display modeAuthorization.newEndpointnotConfigurationPermissiontimeshoulddefault auth 403
4. **notPredictableidentifier identify symbol**: useuse UUIDv4 operationasresource source ID(manipulate deep defense defense, Non-replace code appraise permission)

### Codelayer page

```python
# reversecases - only credential ID check query, no return attributeValidate
@app.get("/api/v1/orders/{order_id}")
def get_order(order_id: str):
 return db.query("SELECT * FROM orders WHERE id =?", order_id)

# correctcases - strong makeValidateresource source return attribute
@app.get("/api/v1/orders/{order_id}")
@require_auth
def get_order(order_id: str, current_user: User):
 order = db.query("SELECT * FROM orders WHERE id =? AND tenant_id =?",
 order_id, current_user.tenant_id)
 if not order:
 raise HTTPException(404)
 if order.user_id!= current_user.id and not current_user.has_role("admin"):
 raise HTTPException(403)
 return order
```

### test layer page

1. **CI/CD collect complete**: willPermissionmatrix matrix test collect completeto CI flow horizontal line, eachtimespart deploy self dynamicValidate
2. **return return test**: Eachbypass permission vulnerability fix repeat after, willotherTest Caseadd inject return return test item
3. **set period audit plan**: each degreeExecuteonetimesCompleteofAuthorization Bypasstest
