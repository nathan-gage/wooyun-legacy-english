# H5 electronic commerce commerce SRC vulnerability plan

> Target:WeChatinternal H5 commerce | Time Window:2 days | already has resource asset:Regular UserAccount + 4 key API
> Methodcomment:WooYun Business Logic Vulnerability Methodology(22,132 Case)

---

## resource asset clear single

| resource asset | Description |
|------|------|
| `/api/user/info` | UserinformationInterface(Read/Cancan includeModify) |
| `/api/order/list` | OrderlistInterface(Read) |
| `/api/payment/create` | PaymentCreateInterface(write inject, Financialaudit core) |
| `/api/address/update` | AddressUpdateInterface(write inject) |
| Regular UserAccount | alreadyAuthenticationSession |
| WeChat H5 environment environment | WeChat OAuth + JS-SDK + internal WebView |

---

## Prioritytotal (by WooYun high-risk percentagerank sequence)

| Priority | test method toward | WooYun high-risk percentage | expected plan time | Target API |
|--------|---------|----------------|---------|---------|
| P0 | Payment Amount Tampering | 83.0% | 3h | `/api/payment/create` |
| P0 | Orderbypass permission (IDOR) | 74.2% + 62.3% | 3h | `/api/order/list` |
| P1 | Userinformation bypass permission | 62.3% | 2h | `/api/user/info` |
| P1 | Addressbypass permissionModify | 62.3% | 1.5h | `/api/address/update` |
| P1 | PaymentState-Machine Bypass | 68.7% | 2h | `/api/payment/create` |
| P2 | Race Condition (dual flower) | 74.8% | 2h | `/api/payment/create` |
| P2 | Information Disclosure | 64.7% | 1.5h | All API |
| P3 | WeChat OAuth Authenticationmissing flaw | 88.0% | 1h | Login/Authorizationflow process |
| P3 | hidden hiddenEndpointDiscover | 72.6% | 1h | JS source codeAnalyze |

---

## No. onedays:Highprice valueTarget(Financial + bypass permission)

### Phasezero: andaccurate prepare(1 hours)

#### 0.1 RegistrationNo. twoTest Account

at leastrequires 2 same levelAccount(Account A/Account B), useforHorizontal Authorization Bypasstest.

> **WooYun depend according:** 1,705 IDOR Casein, reject large many numberrequiresdualAccountfor ratio canDiscover.

#### 0.2 capture takeFrontend JS source code

```
Target:
- WeChat H5 page add ofAll JS File(webpack bundle)
- search keywords:/api//apiUrl/baseURL/admin/hidden/secret/token/key
- provide takeAll API Endpointlist(remote super already notifyof 4)
- check hardEncodingofKey/token
```

> **WooYun Case:** 4,858 Information DisclosureCaseinlarge quantity come selfFrontend JS expose exposureofinternal part API.

#### 0.3 Configurationpacket capture environment environment

```
Tool:Charles / Burp Suite(WeChat H5 need information any cert certificate)
Record:
- AllRequestofComplete Header(special level inject meaning Authorization/Cookie/X-Token etc.)
- Request/Responseinof ID Fieldformat mode(order sequence integer number vs UUID)
- ResponseinReturnofFieldnumber quantity(whetherthrough degreeReturn)
```

---

### P0-1:Payment Amount Tampering(3 hours)

**WooYun Statistics:** Amount Tampering 176 Case/83.0% High Risk + Payment Bypass 1,056 Case/68.7% High Risk

**WooYun Case References:**
- "M1905 Movie site value 2588 Packageonly costs 5 jiao" - ClientAmountCantamper change, 5000 price format error abnormal
- "Baidu can micro Cantamper change paymentAmount" - AmountParameternot doServerValidate
- " APP ArbitraryUserLoginCanimpact responseUserAccountBalance(sign Bypass)" - SignatureValidateCanBypass

#### Test Checklist

```
for /api/payment/create Request:

1. price format tamper change
 - [] InterceptPaymentRequest, Modify amount/price/total Fieldas 0.01
 - [] ModifyAmountas 0(zeroyuanbuy)
 - [] ModifyAmountasNegative Number(such as -100, Observewhethertrigger initiateRefundlogic logic)
 - [] ModifyAmountasextreme largeNegative Number(integer number out test)
 - [] part levelModify unit_price and total_price(such asif two person all existin)
 - [] Modifygoods single charactersField(such asif existin currency Parameter)

2. number quantity tamper change
 - [] number quantity changeas 0(avoid feeObtaincommerce product)
 - [] number quantity changeas -1(Negative Numberbuy buy = Cancan trigger initiateRefund)
 - [] number quantity changeassmall number(0.001)
 - [] number quantity changeasextreme large value(2147483647, test integer number out)
 - [] number quantityandprice format not one cause(number quantity=1 but total price=0.01)

3. priority /discount deduct tamper change
 - [] Add discount=100 or discount=99.99 Parameter
 - [] serious repeat useuseSameCouponcode
 - [] expiredCouponReplay
 - [] cross product type useuseCoupon
 - [] stack many type priority type(reduce + Coupon + part)

4. Signature/ValidateBypass
 - [] whether exists sign/signature Parameter?Analyzeother algorithm method
 - [] move remove sign Parameter, ObserveServerwhetherstill connect affected
 - [] ModifyAmountafter notUpdate sign, ObservewhetherValidate
 - [] Analyze sign algorithm method(common seen:MD5(key+params)), Attemptserious newCompute
```

#### keyObservepoint

```
PaymentCreateafter, Check:
- ServerReturnofOrderAmount vs ClientSubmitofAmount -> whetherasClientasaccurate?
- PaymentCallback(such asWeChatPayment notify_url)inofAmount vs OrderAmount -> whetherone cause nessValidate?
- PaymentSuccessafterOrderStatus -> LowpricePaymentwhether can completeOrder?
```

---

### P0-2:Orderbypass permission IDOR(3 hours)

**WooYun Statistics:** bypass permission 1,705 Case/62.3% High Risk + Order Tampering 1,227 Case/74.2% High Risk

**WooYun Case References:**
- "Beijing Hyundai platform allowed unauthorized traversal of millions of identity documents/vehicle registration documents" - order sequenceFile ID noAllpermissionValidate
- "Hua.com horizontal authorization vulnerability(impact responseAlluseuseUser)" - Horizontal Authorization BypassDisclosureAllUserData
- "China Eastern Airlines US site severe order information leak and authorization bypass" - OrderData + Privilege Escalation

#### Test Checklist

```
for /api/order/list andrelated keyEndpoint:

1. Horizontal Authorization Bypass(User A User B ofOrder)
 - [] Replace order_id asother value(+1/-1/ machine value)
 - [] Replace user_id asAccount B of ID
 - [] Parameter Pollution:order_id=self ownof&order_id=level personof
 - [] number array inject inject:order_id[]=self ownof&order_id[]=level personof
 - [] JSON Nested:{"order_id": "level personof", "user": {"id": "level personof"}}
 - [] Enumeration order_id Scope, CheckReturnDataAllpermission

2. Orderdetailed details bypass permission
 - [] Pass /api/order/detail?id=XXX Directaccess ask other personOrder
 - [] Ordernumberwhether isorder sequence integer number?(extreme easyEnumeration)
 - [] PassModifypart pageParameterbypass permission:page=1&size=99999(BatchDisclosure)

3. Orderoperation bypass permission
 - [] use A of token Cancel B ofOrder
 - [] use A of token Modify B ofOrderStatus
 - [] use A of token please B ofRefund
 - [] use A of token Confirmcollect goods B ofOrder

4. ID format modeAnalyze
 - [] Recordself ownof 3+ Order ID, Analyzescale law
 - [] such asif is order sequence ID -> DirectEnumeration(Severe)
 - [] such asif is timestamp + sequence number -> predictionScope small
 - [] such asif is UUID -> Attemptother inject interfaceObtainother person UUID
```

---

### P1-1:Userinformation bypass permission(2 hours)

**WooYun Statistics:** bypass permission 1,705 Case/62.3% High Risk + Information Disclosure 4,858 Case/64.7% High Risk

**WooYun Case References:**
- "TCL a systemMisconfiguration Leading To 600 ten-thousand clientName/mobile machine/ Disclosure" - API through degreeReturn
- "percent large vulnerability risk involving 2000W personDetailedinformation" - BatchUserInformation Disclosure
- "super level lesson process table some primary business logic logic missing flawCausingall bodyUserreal realNamemobile machineand QQ Disclosure" - Design Flaw

#### Test Checklist

```
for /api/user/info:

1. information through degreeReturn
 - [] for ratio API ResponseFieldnumber vs H5 page displayFieldnumber
 - [] whetherReturndone:Passwordhash hash/mobile machine all number/Identity Cardnumber/banklinescard number?
 - [] whetherReturndone internal partField:role/is_admin/permission/internal_id?
 - [] Responseinwhetherinclude include otherUserofkey connect information?

2. Horizontal Authorization BypassRead
 - [] Add/Modify user_id ParameterasotherUser ID
 - [] Modify URL Pathinof ID(such as /api/user/info/123 -> /api/user/info/124)
 - [] Pass Header inof X-User-Id orself set defineFieldReplace
 - [] EnumerationUser ID Scope(such asifasorder sequence ID, CanBatchDisclosure)

3. Vertical Authorization Bypass
 - [] inRequestinAdd role=admin or is_admin=1
 - [] access ask /api/admin/user/info etc.manage manageEndpoint
 - [] Modify HTTP Method(GET -> POST -> PUT -> DELETE)

4. UserinformationModifybypass permission
 - [] whether exists /api/user/update ortype Endpoint?
 - [] whether canModifyotherUserofmobile number/Email/ name?
 - [] whether canPassModifyEmail/mobile numberconnect manage otherAccount?
```

---

### P1-2:Addressbypass permissionModify(1.5 hours)

**WooYun Statistics:** Arbitrary Modification 159 Case/63.5% High Risk

#### Test Checklist

```
for /api/address/update:

1. Horizontal Authorization BypassModify
 - [] Replace address_id asother personAddress ID
 - [] Replace user_id asother personUser ID
 - [] useAccount A of token ModifyAccount B ofcollect goodsAddress
 - [] Modifyother person default authAddress -> after continueOrdershippingtoattack attack personAddress

2. BatchEnumeration
 - [] Enumeration address_id Obtainother personAddress(Name/electronic /DetailedAddress)
 - [] Pass /api/address/list whetherCanspecified set other user_id

3. Addressinject inject
 - [] AddressFieldwhether haslong degree limit make/through filter?(XSS Cancan ness)
 - [] AddressFieldwhetherusefor after continue flow process(such asinvoices/item flow identifier)-> Storagetype XSS

4. Business Impact
 - [] Modifyother person default authAddress -> include Intercept(real item loss loss)
 - [] Disclosureother personAddress -> Private Data(Name+electronic +)
```

---

## No. twodays:deep degree test(logic logic + Race + Information Disclosure + Authentication)

### P1-3:PaymentState-Machine Bypass(2 hours)

**WooYun Statistics:** Design Flaw 1,391 Case/65.3% High Risk + Payment Bypass 1,056 Case/68.7% High Risk

**WooYun Case References:**
- "114 Ticketing site logic flaw used payment timeout to leak sensitive information for tens of thousands of users" - Statusmachine missing flaw
- "Datebao official site business-logic vulnerability allowed buying insurance for free or at an extremely low price" - avoid fee buy buyBypass
- " sub a locationSeverelogic logic vulnerability" - electronic commerce logic logicBypass

#### Test Checklist

```
Paymentflow processStatusmachine:
 Shopping Cart -> SubmitOrder -> CreatePayment -> WeChatPayment -> PaymentCallback -> Ordercomplete

Attack Vector:

1. skip throughPaymentStep
 - [] SubmitOrderafter, Direct CallOrderConfirm/completeInterface
 - [] without going throughWeChatPayment, DirectforgeryPaymentSuccessCallback
 - [] AnalyzePaymentCallback URL(notify_url), Attemptprimary dynamicRequest

2. Payment Callback Forgery
 - [] onetimesreal realPaymentSuccessofCallbackData
 - [] userelated same result structureReplayto one notPaymentOrder
 - [] ModifyCallbackinof order_id specified towardHighprice valueOrder
 - [] Callbackvalidate whether exists?Signaturealgorithm methodwhetherCan decode?

3. OrderStatustamper change
 - [] DirectModifyOrderStatusParameter:status=paid / status=shipped
 - [] Paid -> Refund -> serious new useusecommerce product(Refundnot refund goods)
 - [] alreadyCancelofOrderwhether can repeat? repeat after price formatwhetherprotect hold?

4. PaymentafterModify
 - [] PaymentSuccessafterModifyOrderinofcommerce product/Address/number quantity
 - [] Lowprice commerce productPaymentSuccess -> ModifyasHighprice commerce product
```

---

### P2-1:Race Condition/dual flower(2 hours)

**WooYun Statistics:** logic logic vulnerability 266 Case/74.8% High Risk

**WooYun Case References:**
- BalanceRaceWithdrawal:from 100 BalanceinConcurrencyprovide take 200
- CouponRace:singletimesuseuseCouponbeConcurrencyuseusemanytimes

#### Test Checklist

```
useuse Burp Turbo Intruder orConcurrencyScript:

1. CouponRace
 - [] SameCoupon, Concurrency 10-20 useuseRequest
 - [] expected period:only 1 Success
 - [] vulnerability:manySuccess = no limit priority

2. InventoryRace
 - [] limit buy 1 item commerce product, Concurrency 10 under singleRequest
 - [] limit quantity commerce product, Concurrency buy
 - [] expected period:only allow allow buy buy limit buy number quantity
 - [] vulnerability:super out limit buy = Inventorycontrol makeInvalidate

3. Balance/ partRace
 - [] Balanceonly 1 timesmessage fee, Concurrency 5 timesPaymentRequest
 - [] part changeConcurrencyRequest
 - [] expected period:only 1 timesSuccess
 - [] vulnerability:manytimesSuccess = dual flower

4. to/domain takeRace
 - [] each day to ConcurrencyRequest
 - [] new person includeConcurrencydomain take
 - [] expected period:only 1 times
 - [] vulnerability:manytimesdomain take
```

---

### P2-2:Information Disclosure(1.5 hours)

**WooYun Statistics:** Information Disclosure 4,858 Case/64.7% High Risk(number quantity most manyofCategory)

**WooYun Case References:**
- "map client manyDatabaseServer flaw" - Source Code/Configuration Disclosure
- "Sunshine InsuranceSensitive InformationDisclosureCausingSuccessadvance injectInternal NetworkSystem" - Disclosurecredential according -> Internal Network toward

#### Test Checklist

```
1. API Responsethrough degreeReturn
 - [] All 4 API Responseinwhetherinclude super out UI showofField?
 - [] errorResponsewhetherDisclosurestack stack information/SQL /FilePath?
 - [] 404/500 ResponsewhetherDisclosureframework architecture version version(Spring Boot? Laravel?)

2. hidden hiddenEndpointprobe test
 - [] from JS source code provide takeof API list one by one test
 - [] /api/swagger-ui.html, /api/docs, /api-docs
 - [] /actuator, /actuator/env, /actuator/heapdump (Spring Boot)
 - [] /druid (Druid monitor control)
 - [] /.git/config, /.env, /config.json

3. WeChatspecial hasDisclosure
 - [] WeChat JS-SDK Signatureinof appId and appSecret
 - [] WeChat OAuth redirect_uri whetherValidatesevere format?
 - [] H5 page localStorage/sessionStorage inStoragedone?
 - [] WeChatpart link connectinwhether with sensitive sensitiveParameter?

4. ResponseHeaderAnalyze
 - [] Server / X-Powered-By -> framework architectureIdentify
 - [] Access-Control-Allow-Origin -> CORS Configurationwhether
 - [] Set-Cookie -> HttpOnly / Secure / SameSite identifier record
```

---

### P3-1:WeChat OAuth / Authenticationmissing flaw(1 hours)

**WooYun Statistics:** Password Reset 777 Case/88.0% High Risk(mostHighSevereness ratiocases)

#### Test Checklist

```
1. WeChat OAuth missing flaw
 - [] redirect_uri whetherCanbe tamper change?(open release serious set toward -> Token hold)
 - [] state Parameterwhether existsandValidate?(CSRF defense protect)
 - [] whetherCanuse code ReplayObtainotherUser token?
 - [] decode WeChatafter old token whetherInvalidate?

2. Token/Session Secure
 - [] Token whether hasexpired time between?
 - [] refund outLoginafter Token whetherImmediately Invalidate?
 - [] Token whetherBindingset prepare/IP?change set prepare/IP whetherstillValid?
 - [] Token format modeAnalyze(JWT? self set define?), whetherCanforgery?

3. SMS Verification Codemissing flaw(such asif existinmobile numberLogin)
 - [] CAPTCHAwhether hasrate rate limit make?
 - [] CAPTCHAlong degree(4 characters = 10000 typeCancan -> CanBrute Force)
 - [] CAPTCHAwhetherinResponseinReturn?
 - [] CAPTCHAwhetherCancrossUseruseuse?
 - [] CAPTCHAexpired time betweenwhethercombine manage?
```

---

### P3-2:hidden hiddenEndpointandMisconfiguration(1 hours)

**WooYun Statistics:** Misconfiguration 1,796 Case/72.6% High Risk

**WooYun Case References:**
- "Tongcheng Travel system misconfiguration allowed arbitrary file upload getshell/root Permission" - Misconfiguration -> RCE
- "cloud informationusesocial informationWeChatmanage managePlatform" - WeChatmanage managePlatformDefault Credentials

#### Test Checklist

```
1. manage manage backend console probe test
 - [] /admin, /manage, /backend, /console
 - [] /api/admin/*, /api/manage/*
 - [] from JS source codeinDiscoverofmanage manageEndpoint

2. debuggingEndpoint
 - [] /debug, /test, /api/test
 - []?debug=true,?test=1 Parameter
 - [] /phpinfo.php, /info.php

3. Default Credentials(such asifDiscovermanage manage backend console)
 - [] admin/admin, admin/123456, admin/admin123
 - [] test/test, demo/demo
 - [] company company name/company company name123

4. CORS Configuration
 - [] Origin: https://evil.com -> Check ACAO ResponseHeader
 - [] Origin: null -> whetherallow allow?
 - [] whether with Access-Control-Allow-Credentials: true?
 - [] CORS + withCredential = Cancross domain takeData
```

---

## time between part config table

### No. onedays(constraint 10 hoursValidtime between)

| time between | any service | Priority |
|--------|------|--------|
| 09:00-10:00 | accurate prepare:RegistrationAccountB/packet captureConfiguration/JSsource codeAnalyze | Phasezero |
| 10:00-13:00 | Payment Amount Tampering(AllsubTest Item) | P0 |
| 14:00-17:00 | Orderbypass permission IDOR(AllsubTest Item) | P0 |
| 17:00-19:00 | Userinformation bypass permission | P1 |
| 19:30-21:00 | Addressbypass permissionModify | P1 |

### No. twodays(constraint 10 hoursValidtime between)

| time between | any service | Priority |
|--------|------|--------|
| 09:00-11:00 | PaymentState-Machine Bypass | P1 |
| 11:00-13:00 | Race Condition/dual flower | P2 |
| 14:00-15:30 | Information Disclosure(API Response + hidden hiddenEndpoint) | P2 |
| 15:30-16:30 | WeChat OAuth / Authenticationmissing flaw | P3 |
| 16:30-17:30 | hidden hiddenEndpointandMisconfiguration | P3 |
| 17:30-19:00 | for alreadyDiscovervulnerability deep impact response + write report | report |
| 19:00-21:00 | machine dynamic time between:supplement topup testor large alreadyDiscovervulnerability | machine dynamic |

---

## vulnerability report model template

EachDiscoverbythe followingformat modeRecord:

```
## Discover:[identifier problem]
- Severity:Severe / High / in / Low
- Domain:Authentication / Authorization / Financial / information / logic logic / Configuration
- WooYun mode:[match configofhistory history mode name name]
- Business Impact:[Directloss lossAmount / impact responseUsernumber / DataDisclosureScope]
- Reproduction Steps:
 1. [precision confirmofRequest URL + Parameter]
 2. [ModifyofFieldandvalue]
 3. [Observetoofabnormal commonResponse]
- Request/ResponseEvidence:[intercept imageorprinciple initialData]
- Remediation Recommendation:[Serverfix repeat method plan, not isFrontendsupplement]
```

---

## maintainCheckclear single(defense stop layer test)

| flaw | correct confirm do method |
|------|---------|
| "change doneAmountas 0.01 noSuccess skip through" | has 16 typePayment Tamperingmode not test(Negative Number/ out/number quantity/discount deduct...) |
| "IDOR change done ID nouse skip through" | AttemptParameter Pollution/number array inject inject/JSON Nested/Encoding Bypass(WooYun Data:simple single change ID only share 30%) |
| "FrontendhasValidateSecure" | 68.7% ofPaymentvulnerability is becauseasValidateonlyinFrontend, Direct Burp Bypass |
| "only test done 4 already notify API" | JS source codeinone set has update manyEndpoint, hidden hidden manage manage API is most large interface |
| "Scandevice through done noDiscover" | version plan inAllVulnerability Typeall isScandevice no methodDiscoverofbusiness logic logic missing flaw |
| "WeChatenvironment environment limit make done attack attack page" | WeChatonly isFrontend, All API RequestCanasuse Burp/curl Directstructure forge |

---

## Toolclear single

| Tool | Purpose |
|------|------|
| Burp Suite | Request Interception/Modify/Replay |
| Burp Turbo Intruder | Race ConditionConcurrencytest |
| Charles Proxy | WeChat H5 packet capture(need information any cert certificate) |
| curl / httpie | Scriptize API test |
| Python Script | self dynamic ize ID Enumeration/ConcurrencyRequest |
| Browser DevTools | JS source codeAnalyze/localStorage Check |
| GitHack / git-dumper |.git Disclosureexploituse |

---

## WooYun Statisticsrate check

| Vulnerability Category | Case Count | high-risk percentage | version plan cover cover |
|---------|-------|---------|-----------|
| Password Reset | 777 | 88.0% | P3(WeChat OAuth scenario scene variant) |
| Amount Tampering | 176 | 83.0% | P0(Payment Amount Tampering) |
| Balancetamper change | 113 | 77.9% | P2(Race Condition) |
| logic logic vulnerability | 266 | 74.8% | P2(Race Condition) |
| Order Tampering | 1,227 | 74.2% | P0(Orderbypass permission) |
| Misconfiguration | 1,796 | 72.6% | P3(hidden hiddenEndpoint) |
| Payment Bypass | 1,056 | 68.7% | P1(State-Machine Bypass) |
| Design Flaw | 1,391 | 65.3% | P1(State-Machine Bypass) |
| Information Disclosure | 4,858 | 64.7% | P2(Information Disclosure) |
| bypass permission | 1,705 | 62.3% | P0+P1(Allbypass permission test) |

> version plan cover cover WooYun 22,132 Casein Top 10 High RiskCategoryofAlltestDimension.
