# H5 commerce SRC vulnerability plan (2days)

## Targetapprox

- **Target**: electronic commercePlatform H5 commerce (WeChatinternal page)
- **already has resource source**: Regular UserAccount/packet capture environment environment
- **already notify API**:
 - `GET /api/user/info` - Userinformation check query
 - `GET /api/order/list` - Orderlist
 - `POST /api/payment/create` - CreatePayment
 - `POST /api/address/update` - AddressUpdate

---

## Day 1: High Riskvulnerability priority first (constraint 10h)

### P0 - bypass permission vulnerability(IDOR)[expected plan 3-4h]

> **Reason**: electronic commerce scenario scene under bypass permission is mostHighfrequency/mostHigh RiskofVulnerability Type, SRC wild common assessasHigh Risk/Severe.

#### /api/user/info - Horizontal Authorization BypassRead

1. capture take correct commonRequest, IdentifyUseridentifier identifyParameter(`userId`/`uid`/`id`/or JWT inof sub Field)
2. ReplaceasotherUser ID(Traversal/+1/-1/already notifyNo. twoAccount ID), ObservewhetherReturnother person information
3. key injectReturnField:mobile number/real realName/Identity Cardnumber/Email - any oneDisclosurethat isCanreport

#### /api/order/list - Horizontal Authorization BypassReadOrder

1. same aboveMethodReplaceUseridentifier identify, AttemptReadother personOrder
2. such asif has `orderId` Parameter, AttemptTraversalOrdernumberViewother personOrderdetailed details
3. Checkwhether exists `/api/order/detail?orderId=xxx` type Endpoint

#### /api/address/update - bypass permissionModifyother personAddress

1. capture takeUpdateAddressRequest, to `addressId` ortype identifier identify
2. Replaceasother personAddress ID, AttemptModify(useno Datatest, Confirmafter standalone that is repeat)
3. same timeCheckwhether exists `/api/address/list`/`/api/address/delete` bypass permission

#### /api/payment/create - bypass permissionPayment / Order Tampering

1. CreatePaymenttime, Replace `orderId` asother personOrder, Observewhethercan code payor holdPaymentflow process
2. this isSeverityvulnerability, test, pointtoasstop

### P1 - Paymentlogic logic vulnerability [expected plan 3-4h]

> **Reason**: electronic commerce audit core business, Directforge complete resource funds loss loss, wild common assessasSevere.

#### Amount Tampering

1. `/api/payment/create` RequestintoAmountField(`amount`/`totalPrice`/`price`)
2. AttemptModifyas 0.01/0/Negative Number(-1)/super large number
3. ObserveBackendwhetherserious newValidateAmount(for ratioOrderreal actualAmount)

#### number quantity/commerce product tamper change

1. under single flow processinModifycommerce product number quantityas 0 orNegative Number, Observetotal priceCompute
2. Replacecommerce product ID asLowprice commerce product, protect holdHighprice commerce productofOrderabove under text
3. CheckCoupon/discount deductwhetherCan add(serious repeat useuseSameCoupon ID)

#### PaymentStatusforgery

1. AnalyzePaymentCallbackInterface(wild commonas `/api/payment/callback` or `/api/payment/notify`)
2. AttemptDirectstructure forgePaymentSuccessofCallbackRequest
3. CheckSignatureValidatewhether exists(MissingSignatureValidate = Severevulnerability)

#### Race Condition(Race Condition)

1. SameCoupon/Balance, Concurrencyinitiate initiate many entryPaymentRequest(10-20 Concurrency)
2. Tool: `turbo intruder` or Python `asyncio` + `aiohttp` Concurrency
3. Observewhetherout currentBalancemany deduct/Couponmanyuse

### P2 - Information Disclosure [expected plan 2h]

> **Reason**: fast rate out complete if, operationasprotect asset out.

#### API Responsethrough degree expose exposure

1. one-by-oneCheckalready notify API ofResponse JSON, whetherinclude includeshould notReturnofField
2. serious point key inject: `idCard`/`phone`(Completemobile number vs leak sensitive)/`password`/`salt`/`token`/`openid`/internal part ID
3. ChecklistInterfacewhetherReturnall quantityData(no part page above limit -> library risk)

#### errorInformation Disclosure

1. forEach API Send Parameter(Emptyvalue/super long character symbol string/SQL Special Characters `'`)
2. ObserveerrorResponsewhetherexpose exposure: stack stack information/Databasetype/internal partPath/No. three method SDK version version

#### WeChatrelated keyDisclosure

1. Checkpage source code/JS inwhetherhardEncoding `appId`/`appSecret`(Severe)
2. Check JSSDK ConfigurationInterfacewhetherDisclosureSensitive Information
3. Check `openid` whetherinFrontendclear text pass recursive andCanbeReplace(result combine bypass permission)

---

## Day 2: inHigh Riskvulnerability + deep degree exploituse(constraint 10h)

### P3 - InterfaceDiscoverandUnauthorized Access [expected plan 2-3h]

> **Reason**: large attack attack page, Discoverhidden hiddenofHigh RiskEndpoint.

#### InterfaceEnumeration

1. **JS FileAnalyze**: DownloadAll JS File(webpack break include), search `/api/` Path
 ```
 keywords: /api/, axios, fetch, request, baseURL, endpoint
 ```
2. **Source Map**: Checkwhether exists `.js.map` File(common seen), principleCompleteFrontendsource code
3. **common seenPathBrute Force**:
 - `/api/admin/*` - backend consoleInterface
 - `/api/user/delete`/`/api/user/update` - CRUD supplement all
 - `/api/coupon/*`/`/api/refund/*`/`/api/logistics/*`
 - `/swagger-ui.html`/`/api-docs`/`/doc.html` - API Document
 - `/actuator`/`/env`/`/heapdump` - Spring Boot Endpoint

#### Unauthorized Access

1. forDiscoverofAllInterface, move remove Cookie/Token afterReplay
2. check whether there isInterfaceno need toAuthenticationthat isCanaccess ask
3. special level key inject manage manage typeInterface(Usermanage manage/Order Management/commerce product manage manage)

### P4 - inject inject type vulnerability [expected plan 2-3h]

#### SQL inject inject

1. forAllParameterAttemptbase foundation payload: `'`/`' OR '1'='1`/`1 AND 1=1`
2. serious pointTarget:
 - `/api/order/list` ofrank sequence/search/ selectParameter
 - `/api/user/info` ofcheck queryParameter
3. time between inject check test: `1' AND SLEEP(5)--`, ObserveResponse
4. Tool: sqlmap Validate(`--level 3 --risk 2`, not need `--dump`)

#### XSS(Storagetype priority first)

1. AddressField(`/api/address/update`)write inject XSS payload:
 ```
 collect goods person: <img src=x onerror=alert(1)>
 DetailedAddress: "><script>alert(document.domain)</script>
 ```
2. such asif commerce has assess comment/assess price function can, same inject inject
3. Checkwhetherinmanage manage backend console trigger initiate(Blind XSS -> use XSS Hunter orself createCallback)
4. WeChatenvironment environment special reference: `javascript:` protocol protocol/`<a href>` skip transfer

#### SSRF

1. such asif hasHeaderUpload/image image URL Importfunction can, Attempt `http://127.0.0.1`/`http://169.254.169.254`
2. CheckPaymentCallback URL whetherCancontrol(`notifyUrl` Parameter)

### P5 - Business Logic Vulnerability [expected plan 2-3h]

#### short information/CAPTCHArelated key

1. SMS Bombing: Registration/Login/ returnPasswordofSendCAPTCHAInterface, whether hasRate Limit
2. CAPTCHA Bypass: ten-thousand canCAPTCHA(`0000`/`1234`/`8888`)/Returnincludeinwhetherinclude includeCAPTCHA
3. CAPTCHArepeatuse: SameCAPTCHAwhetherCanmanytimesuseuse

#### Userbody system

1. ArbitraryPassword Reset: Modifymobile numberParameter -> useself ownofCAPTCHA -> serious set other personPassword
2. AccountEnumeration: Registration/LoginInterfacewhether part"Usernot existin"and"Passworderror"
3. LoginBrute Force: whether hasImage CAPTCHA/Account Lockoutmachine make

#### Coupon/ part

1. Coupon ID CanTraversal -> domain take other person special attributeCoupon
2. part changeNegative Numbercommerce product -> part increase add
3. already useuseCouponPassModifyStatusserious new useuse

### P6 - FileUpload / other [expected plan 1-2h]

1. such asif hasHeader/assess price image imageUploadfunction can:
 - Bypassafter: `.php`/`.jsp`/`.phtml`/dual after `1.php.jpg`
 - Content-Type Bypass: `image/jpeg` + real actual PHP content
 - CheckUploadPathwhetherdirectly usableaccess askExecute
2. CORS Configuration: Check `Access-Control-Allow-Origin` whether is `*` orCancontrol
3. JSONP hold: check whether there is callback ParameterCaninject inject

---

## Toolclear single

| Tool | Purpose |
|------|------|
| Burp Suite Pro | audit core packet capture/Replay/Brute Force |
| sqlmap | SQL inject injectValidate |
| Turbo Intruder | ConcurrencyRacetest |
| ffuf / dirsearch | PathBrute Force |
| LinkFinder / JSFinder | JS inprovide take API Endpoint |
| WeChatopen initiate personTool | debuggingWeChat H5 environment environment |
| Xray (be dynamicScan) | in Burp under, self dynamic check test common vulnerabilities |

## WeChat H5 special inject meaning eventitems

1. **packet captureConfiguration**: WeChatinternal setBrowserSystemcode manage, but need inject meaning cert certificate information any ask problem(Android 7+ need root orusemodel device)
2. **appraise permission method mode**: large approx rate based onWeChat OAuth -> `openid` operationasidentity copy identifier identify, serious point key inject `openid` whetherCanforgery/Replace
3. **JSSDK**: Check `wx.config` inofSignaturewhetherCanbeReplayorforgery
4. **small process sequence key connect**: check whether there isforshouldsmall process sequence, small process sequenceand H5 Cancan totaluseBackend API but appraise permission policy strategyDifferent

## time between part config total

| time | content | expected period asset out |
|------|------|----------|
| Day1 above | P0 bypass permission test | 1-3 High Risk/Severe |
| Day1 under | P1 Paymentlogic logic | 1-2 Severe |
| Day1 above | P2 Information Disclosure | 2-3 Medium Risk |
| Day2 above | P3 InterfaceDiscover + Unauthorized | large attack attack page, 1-2 inHigh Risk |
| Day2 under | P4 inject inject type | 1-2 High Risk(such asexistin) |
| Day2 above | P5-P6 business logic logic + | 2-3 Medium Risk, integer manage report |

## report write need point

- Eachvulnerability single independentSubmit, not need combine and
- include include: vulnerability identifier problem/risk etc.level/Reproduction Steps(intercept image+Requestinclude)/Impact Scope/Remediation Recommendation
- bypass permission type write clear impact responseUsernumber quantity level assess algorithm
- Paymenttype write clear resource funds loss lossofmanage comment above limit
- firstSubmitHigh Risk/Severe, again supplement topupinLow Risk(avoid serious repeatandcollision hole)
