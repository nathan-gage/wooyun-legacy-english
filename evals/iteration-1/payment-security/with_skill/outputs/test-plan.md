# electronic commercePlatformPaymentandOrderflow processSecureTest Plan

> Based on the methodology from 22,132 real WooYun vulnerability cases | Financial Domain 2,919 Case + Logic Flow Domain 1,679 Case

---

## 1. Test Scopeandbusiness flow process map map

### 1.1 TargetSystem

| model block | audit core function can | involving resource funds flow |
|------|---------|-----------|
| Shopping Cart | commerce productAdd/Delete/Modifynumber quantity/price formatCompute | between connect(price format come source) |
| Online Payment | Alipay/WeChatPaymentInterfacefor connect/Callbackhandle manage | Direct |
| Order Management | OrderCreate/Statusflow transfer/check query/Cancel | Direct |
| Refund Flow | Refund please/audit audit/RefundExecute | Direct(toward resource funds flow) |

### 1.2 Order State Machinemap map

```
expected period flow process:
 Shopping Cart -> SubmitOrder(Pending Payment) -> Paymentin -> Paid -> handle managein -> already shipping -> already collect -> Completed
 down down
 alreadyCancel(notPaymentCancel) Refund please -> Refundaudit audit -> Refundin -> Refunded
```

**requiresValidateofNon-methodStatustransfer move(WooYun Order Tampering 1,227 Case, 74.2% High Risk):**

| Non-method transfer move | attack attack meaning image | Risk Level |
|---------|---------|---------|
| Pending Payment -> Paid | skip throughPaymentenvironment section | Severe |
| Pending Payment -> Completed | complete allBypassPaymentanditem flow | Severe |
| already shipping -> Refunded | collect goods afterRefund() | High |
| Completed -> Refundin | alreadyConfirmcollect goods after still trigger initiateRefund | High |
| alreadyCancel -> Paid | repeat alreadyCancelOrder | High |
| Refunded -> Refunded | Duplicate Refund | Severe |

### 1.3 participateandpersonandTrust Boundary

| Role | PermissionScope | Trust Boundaryrisk |
|------|---------|-------------|
| Anonymous User | commerce product/addShopping Cart | whether caninnotLoginStatusunderSubmitOrder/trigger initiatePayment? |
| Regular User | under single/Payment/Viewself ownofOrder | whether canView/Modifyother personOrder?(IDOR) |
| commerce account/ | manage manage commerce product/handle manageOrder/Confirmshipping | whether canModifyprice format?whether canselflinesaudit batchRefund? |
| Administrator | all global manage manage | manage manage backend consolewhether hasUnauthorized Access? |
| Payment Gateway(Alipay/WeChat) | Callbackwild notify/SignatureValidate | CallbackwhetherCanforgery?SignaturewhetherCanBypass? |

### 1.4 Test Accountaccurate prepare

```
mustaccurate prepare:
- Regular User A(primaryTest Account)
- Regular User B(useforHorizontal Authorization Bypasstest)
- commerce accountAccount(such assuitableuse)
- AdministratorAccount(useforVertical Authorization Bypasstest)
- RecordEachAccountof:session token / cookie / user_id / order_id version
```

### 1.5 testTool

| Tool | Purpose |
|------|------|
| Burp Suite Professional | HTTP Intercept/Replay/Turbo Intruder Racetest |
| mitmproxy | PaymentCallbackInterceptAnalyze |
| Python Script | ConcurrencyRequest/self dynamic izeEnumeration |
| Browseropen initiate personTool | Frontendlogic logicAnalyze/localStorage Check |

---

## 2. test model block one:Shopping CartSecure

> WooYun participate reference:Financial Domainprice format tamper change 70 Case(74.3% High Risk)+ Order Tampering 1,227 Case

### Test Point 2.1:Shopping Cartprice format tamper change

**false set:** Shopping Cartinofprice format/single price byClientpass recursive, ServernotfromDatabaseserious newObtainValidate.

**WooYun mode:** "innationalPing Ana locationValidatelogic logic ask problemCausingpercent ten-thousandSensitive Information Leak+manage manage commerce product price format" - ClientSubmitprice format beServerDirectinformation any.

**Test Steps:**

```
1. correct commonAddcommerce producttoShopping Cart, use Burp InterceptAddRequest
2. ObserveRequestParameterinwhetherinclude include price / unit_price / amount Field
3. such asinclude include, dependtimesModifyas:
 - [] price=0.01(most smallAmounttest)
 - [] price=0(zeroyuanbuy buy)
 - [] price=-1(Negative Number, CancanCausingRefundorBalanceincrease add)
 - [] price=0.001(small number precision degree test)
4. SubmitafterCheckShopping Cartpage displayofprice formatwhether istamper change afterofvalue
5. continue toresult algorithm page, Confirmresult algorithm total amountwhetherbased on tamper change afterofprice format
6. such asif result algorithm total amount correct common(fromServer take), Checkmost finalSubmitOrderofRequestinwhetherCanagaintimesModifyAmount
```

**Pass/Fail Criteria:** such asif any tamper change afterofprice format beServerconnect affected andusefor after continueCompute, ruleConfirmvulnerability existin.

### Test Point 2.2:number quantity tamper change

**false set:** Shopping Cartnumber quantityFieldnot doServerboundary boundaryValidate.

**Test Steps:**

```
1. InterceptModifyShopping Cartnumber quantityofRequest
2. dependtimesSubmitthe followingvalue:
 - [] quantity=0(zero number quantity, Observetotal pricewhether is 0)
 - [] quantity=-1(Negative Numberquantity, total pricewhetherchangeasNegative Number -> related when forRefund)
 - [] quantity=99999999(super large number quantity, integer number out test)
 - [] quantity=0.001(small number number quantity, ObserveServerhandle manage)
 - [] quantity="abc"(type mix, Observeerror handle manage)
3. Checkeach type details under:
 - Serverwhetherreject reject?
 - Shopping Carttotal priceComputewhetherabnormal common?
 - whether canadvance inject under single flow process?
```

### Test Point 2.3:commerce product ID Replace

**false set:** inShopping CartSubmitOrdertime, CanaswillHighprice commerce productof item_id ReplaceasLowprice commerce productof item_id, but protect retainHighprice commerce productofother information.

**WooYun mode:** Financial Domain "will item_id Modifyasrelated same number quantityofupdate product".

**Test Steps:**

```
1. willoneHighprice commerce product(such as ¥999)add injectShopping Cart
2. InterceptSubmitOrderRequest
3. will item_id / product_id / sku_id ReplaceasoneLowprice commerce product(such as ¥9.9)of ID
4. protect retain otherParameternot change(number quantity/collect goodsAddressetc.)
5. Observe:
 - [] OrderwhetherCreateSuccess?
 - [] OrderAmountis which commerce productofprice format?
 - [] shipping time initiateofis which commerce product?
```

### Test Point 2.4:Shopping Cartandresult algorithm price format one cause ness

**false set:** Shopping Cartpageofprice formatandreal actualSubmittoPayment GatewayofAmountbetween existinnot one cause window interface.

**Test Steps:**

```
1. Addcommerce producttoShopping Cart, RecordShopping Cartdisplay price format
2. advance inject result algorithm page, Recordresult algorithm display price format
3. InterceptSubmitOrderRequest, RecordRequestinofAmountParameter
4. for ratio threePhaseofAmountwhetherone cause
5. inresult algorithm page add after/SubmitOrderfirst, Pass oneRequestModifyShopping Cartinofcommerce product
6. SubmitOrder, Observemost finalAmountwhetherreverse mapModifyafterofShopping Cart
```

---

## 3. test model block two:Paymentflow processSecure

> WooYun participate reference:Payment Bypass 1,056 Case(68.7% High Risk), Amount Tampering 176 Case(83.0% High Risk)

### Test Point 3.1:Payment Amount Tampering(Client->Server)

**false set:** ClientSubmitofPaymentAmountbeServerDirectusefor generate completePayment GatewayRequest, notandOrderreal actualAmountValidate.

**WooYun mode:** "M1905Movie site value2588Packageonly costs5jiao" - ClientSubmitAmountbeDirectpass recursive toPayment Gateway.

**Test Steps:**

```
1. correct common under single(such astotal amount ¥299), advance injectPaymentpage
2. Intercept"initiate initiatePayment"ofRequest(wild commonas POST /api/pay ortype Endpoint)
3. ModifyRequestinofAmountParameter:
 - [] amount=0.01(most smallAmount)
 - [] amount=0(zeroyuanPayment)
 - [] amount=-1(Negative NumberAmount)
 - [] amount=1(Fixed 1 yuan)
4. Observe:
 - Alipay/WeChatPaymentpage displayofAmountwhether istamper change afterofvalue?
 - PaymentSuccessafter, OrderStatuswhetherchangeas"Paid"?
 - such asifPayment 0.01 yuanSuccessbutOrderis ¥299, SystemwhetherstillConfirmOrder?
```

**Severity:** Severe - Directfinancial loss.

### Test Point 3.2:Payment Callback Forgery

**false set:** PaymentCallback(notify_url)not severe formatValidateSignature, orSignatureValidatelogic logic existinmissing flaw.

**WooYun mode:** Financial Domain "inServerconnect collect firstModifyPayment GatewayResponse" + "forDifferentOrderReplaySuccessofPaymentCallback".

**Test Steps:**

```
1. complete onetimescorrect commonPayment, use Burp Payment GatewayCallbackRequest(Alipay/WeChatofabnormal step wild notify)
2. AnalyzeCallbackParameter:
 - whetherinclude includeSignatureField(sign)?
 - Signaturealgorithm method is?(MD5/RSA/HMAC-SHA256)
 - which someFieldparticipateandSignature?

3. SignatureBypasstest:
 - [] complete all sign Parameter, ObserveServerwhetherstill connect affected
 - [] will sign setasEmptycharacter symbol string
 - [] SubmitEmpty sign_type
 - [] ModifyAmountbut protect retain principleSignature, ObservewhetherValidateFailure

4. CallbackReplaytest:
 - [] willOrder A ofSuccessCallbackinof order_id changeasnotPaymentOrder B of order_id
 - [] protect retain principle initialSignaturenot change
 - [] ObserveOrder B whetherbe identifier recordasPaid

5. Callbackwild notify sourceValidate:
 - [] fromNon-Payment Gateway IP SendCallbackRequest, Observewhetherbe connect affected
 - [] CheckCallback URL whetherCanas bePublic InternetDirectaccess ask
```

**Severity:** Severe - Canno limit forgeryPaymentSuccess.

### Test Point 3.3:PaymentState-Machine Bypass

**false set:** Paymentflow processinofStepCanas be skip through, Directfrom"Pending Payment"skipto"Paid".

**WooYun mode:** Logic Flow Domain "buy buy flow process:Shopping Cart -> Address -> Payment -> Confirm, skip throughPaymentDirectConfirm"(1,391 Case, 65.3% High Risk).

**Test Steps:**

```
1. Create Order, ObtainOrdernumber(order_id)andPending PaymentStatus
2. not advancelinesPaymentoperation, DirectAttempt:
 - [] CallOrderConfirmInterface POST /api/order/confirm?order_id=xxx
 - [] CallshippingInterface(such ashas)
 - [] ModifyOrderStatusParameter:status=paid / status=2 / state=completed
 - [] mobile dynamic structure forgePaymentSuccessCallbackRequestSendto notify_url

3. manyStepBypasstest:
 - [] skip throughAddressfill inStep, DirectSubmitPayment
 - [] skip throughCouponValidateStep
 - [] inPaymentinModifyOrdercommerce product

4. Check:
 - Orderwhetherchangeas"Paid"Status?
 - commerce productInventorywhetherreduce less?
 - item flowwhetherCanas shipping?
```

### Test Point 3.4:Payment Gatewayswitch change attack attack

**false set:** Systemsupport holdAlipayandWeChattwo typePaymentmethod mode, switch changePaymentmethod mode timeCancanBypassAmountValidate.

**Test Steps:**

```
1. select AlipayPayment, Interceptgenerate completePaymentRequestofInterfaceCall
2. Modify payment_method / pay_type / channel ParameterasWeChatPayment
3. Observe:
 - [] Amountwhetherinswitch change through processinCanbeModify?
 - [] whetherCanas useuseTest Environment/ ofPaymentChannelParameter?
 - [] switch changetonot existinofPaymentChannel(such as pay_type=test)timeoflinesas?

4. testPaymentCredentialcrossGatewayuseuse:
 - [] willAlipayofSuccessCredentialuseforWeChatPaymentofConfirmflow process
```

### Test Point 3.5:Concurrent Payment / dual flower attack attack

**false set:** SameOrderCanbeConcurrent Paymentmanytimes, orSameCoupon/BalanceCaninRacewindow interface internal be manytimesuseuse.

**WooYun mode:** Logic Flow DomainRace Condition 266 Case(74.8% High Risk) - "from 100 ofBalanceinprovide take done 200".

**Test Steps:**

```
1. AccountBalanceRace:
 - Top-Up ¥100 toAccountBalance
 - useuse Burp Turbo Intruder or Python Scriptsame timeSend 10 "useuseBalancePayment ¥100 Order"ofRequest
 - [] Check:whether hasmanyOrderPaymentSuccess?BalancewhetherchangeasNegative Number?

2. CouponRace:
 - ObtainoneitemssingletimesuseuseCoupon
 - ConcurrencySubmit 10 useuseSameCouponofunder singleRequest
 - [] Check:Couponwhetherbe manytimesaudit?

3. InventoryRace:
 - forInventoryonly 1 itemofcommerce product
 - ConcurrencySubmit 10 buy buyRequest
 - [] Check:whetherCreatedone manyOrder?InventorywhetherchangeasNegative Number?

4. useuse Python ConcurrencyExample:
 import threading
 import requests

 def pay(session, order_id):
 resp = session.post('/api/pay', json={'order_id': order_id, 'method': 'balance'})
 print(resp.status_code, resp.json())

 threads = [threading.Thread(target=pay, args=(s, oid)) for _ in range(10)]
 for t in threads: t.start()
 for t in threads: t.join()
```

**Severity:** Severe - Directfinancial loss(dual flower/many flower).

### Test Point 3.6:Coupon/discount deduct abuseuse

**false set:** CouponValidateexistinlogic logic missing flaw, Canbe serious repeat useuse/cross product type useuseorBypasslimit make.

**WooYun mode:** Financial Domaindiscount deduct/CouponabuseuseCheckclear single(1,056 Case).

**Test Steps:**

```
1. serious repeat useusetest:
 - [] useuseCouponunder single -> CancelOrder -> Couponwhetherreturn -> againtimesuseuse
 - [] useusealready expiredCouponofValidRequestadvancelinesReplay
 - [] ConcurrencyuseuseSameCoupon(seen 3.5 Racetest)

2. discount deduct add test:
 - [] for already break discount commerce product useuse reduceCoupon
 - [] same timeSubmitmanyCouponcode
 - [] inRequestinModify discount Field(such as discount=100 -> all avoid)
 - [] Modify coupon_value Field

3. cross limit make useuse:
 - [] willlimit set product type A ofCouponusefor product type B ofcommerce product
 - [] not reachto" reduce" time useuse reduce coupon
 - [] newUsercouponusealreadyRegistrationAccountuseuse

4. CouponEnumeration:
 - [] AnalyzeCouponcode format mode(such as 8 characters number character), AttemptEnumerationValidcoupon code
 - [] testCouponcodewhether isorder sequence generate complete(Predictable)
```

---

## 4. test model block three:Order ManagementSecure

> WooYun participate reference:Order Tampering 1,227 Case(74.2% High Risk)+ bypass permission 1,705 Case(62.3% High Risk)

### Test Point 4.1:OrderAuthorization Bypass(IDOR)

**false set:** Ordercheck query/operation only depend rely order_id Parameter, notValidatewhen firstUserwhether isOrderAllperson.

**WooYun mode:** Authorization Domain "Hua.com horizontal authorization vulnerability(impact responseAlluseuseUser)" - AllUserDataCanPassTraversal ID access ask.

**Test Steps:**

```
1. User A Login, Create Order, Obtain order_id(such as 10001)
2. User B Login, Attemptthe followingoperation:
 - [] GET /api/order/detail?order_id=10001(View A ofOrderdetailed details)
 - [] POST /api/order/cancel?order_id=10001(Cancel A ofOrder)
 - [] POST /api/order/modify?order_id=10001(Modify A ofOrderAddress)
 - [] GET /api/order/logistics?order_id=10001(View A ofitem flow information)

3. ID Traversaltest:
 - [] recursive increase/recursive reduce order_id(10001 -> 10002 -> 10003...)
 - [] Record:whethercan access ask otherUserofOrder?
 - [] CheckOrderdetailed detailsinwhetherDisclosureUsermobile number/Addressetc.Personal Information

4. ID Encoding Bypass:
 - [] such asif order_id is add secret/Encodingof, Analyzeformat mode(Base64? MD5?)
 - [] Attempt order_id=0/order_id=-1/order_id=null
 - [] Parameter Pollution:order_id=10001&order_id=10002
```

**Severity:** High - Userhidden privateDisclosure, Cancan impact response all quantityUser.

### Test Point 4.2:OrderStatustamper change

**false set:** OrderStatusCanPassModifyRequestParameterbe strong make change updateasArbitraryStatus.

**Test Steps:**

```
1. CreateonePending PaymentOrder
2. InterceptAllandOrderStatusrelated keyofRequest
3. AttemptDirectModifyStatusParameter:
 - [] status=paid / status=2(skip throughPayment)
 - [] status=shipped(skip throughPayment+handle manage)
 - [] status=completed(Directcomplete)
 - [] status=refunded(DirectsetasRefunded -> trigger initiateRefund)

4. Pass API Direct CallStatuschange update:
 - [] POST /api/order/updateStatus {"order_id": "xxx", "status": "paid"}
 - [] PUT /api/order/xxx {"state": "completed"}

5. reverse towardStatuschange update:
 - [] Completed -> Pending Payment(serious new advance injectPaymentflow process, Cancan change price)
 - [] alreadyCancel -> Pending Payment(repeat Order)
```

### Test Point 4.3:OrderAmountModify

**false set:** OrderCreateafter, inPaymentfirstofwindow interface period internalCanModifyOrderAmount.

**WooYun mode:** Financial Domain "inPaymentafter but linesfirstModifyOrder".

**Test Steps:**

```
1. under single after, Interceptafter continueAllRequest
2. check whether hasModifyOrderofInterface(such as PUT /api/order/xxx)
3. AttemptModify:
 - [] total_amount / pay_amount Field
 - [] commerce product number quantity(reduce less number quantity but protect hold principle price not change -> reverse toward many collect)
 - [] inPaymentfirstModifycollect goodsAddress(testwhethersame timeCanModifyAmount)
 - [] Modifyoperate feeField:freight=0 or shipping_fee=-10

4. Time Windowtest:
 - [] initiate initiatePaymentbut not complete -> ModifyOrder -> completePayment
 - [] PaymentSuccessafter/commerce ConfirmfirstModifyOrder
```

### Test Point 4.4:OrderInformation Disclosure

**false set:** Order API Responseininclude include through manySensitive Information, super out when firstUser/page need.

**WooYun mode:** Information DisclosureDomain "API through degreeObtain" - API ResponseFieldnumber > UI CanseenFieldnumber(4,858 Case, 64.7% High Risk).

**Test Steps:**

```
1. correct commonRequestself ownofOrderdetailed details
2. for ratio API Responseandpage display:
 - [] whetherReturndoneCompletemobile number(Non-leak sensitive)?
 - [] whetherReturndoneCompletecollect goodsAddress?
 - [] whetherReturndonePaymenttransaction easy number/No. three method single number?
 - [] whetherReturndoneUser ID / commerce account internal part ID?
 - [] whetherReturndone otherUserofkey connect information?

3. BatchExporttest:
 - [] whether exists /api/order/export or /api/order/list?page_size=999999
 - [] Exportfunction canwhether hasPermissioncontrol make?
```

---

## 5. test model block four:Refund FlowSecure

> WooYun participate reference:Withdrawal 59 Case(83.1% High Risk)+ Balancetamper change 113 Case(77.9% High Risk)

### Test Point 5.1:RefundAmount Tampering

**false set:** RefundRequestinofAmountCanbeModifyassuper throughOrderreal actualPaymentAmount.

**WooYun mode:** Financial Domain "inClientRequestinModifyBalanceParameter" - no limit resource funds.

**Test Steps:**

```
1. correct common initiate initiateRefund please(such asOrderPayment ¥299)
2. InterceptRefundRequest
3. ModifyRefundAmount:
 - [] refund_amount=299.01(super outPaymentAmount)
 - [] refund_amount=2990(10 Amount)
 - [] refund_amount=999999(extreme end large amount)
 - [] refund_amount=-1(Negative NumberRefund = deduct payment?)
 - [] refund_amount=0(zeroyuanRefund, but protect retain refund goodsStatus)

4. part partRefundabuseuse:
 - [] please part partRefund ¥100 -> againtimes please ¥100 -> serious repeat vertical totalRefund > OrderAmount
 - [] Check:Systemwhether planRefundAmount?

5. RefundTargetAccount:
 - [] ModifyRefundTargetAccountParameter(such asifRequestininclude include)
 - [] CheckRefundwhethercan onlyrefund return principlePaymentchannel channel
```

**Severity:** Severe - Directfinancial loss.

### Test Point 5.2:RefundState-Machine Bypass

**false set:** Refund Flowofaudit auditStepCanas be skip through, Directtrigger initiateRefundExecute.

**WooYun mode:** Logic Flow Domain "Refund:Request -> audit audit -> batch accurate -> Payment, skip through audit auditDirecttrigger initiatePayment"(1,391 Case).

**Test Steps:**

```
1. initiate initiateRefund please, Obtain refund_id
2. notetc.pending audit audit, Direct Call:
 - [] POST /api/refund/approve?refund_id=xxx(selflinesbatch accurate)
 - [] POST /api/refund/execute?refund_id=xxx(DirectExecuteRefund)
 - [] ModifyRefundStatus:refund_status=approved / refund_status=completed

3. self I audit batch test:
 - [] Userself ownwhether canaudit batch self ownofRefund please?
 - [] commerce accountwhether caninno need toPlatformaudit auditofdetails underDirectRefund?

4. Check:
 - Refundresource fundswhetherreal actualtoaccount?
 - principleOrderStatuswhethercorrect confirmUpdate?
```

### Test Point 5.3:Duplicate Refund

**false set:** SameOrder/SameRefundRequestCanbe manytimesSubmitandExecute.

**WooYun mode:** Financial Domain "ReplaySuccessofTop-UpCallback" + Logic Flow DomainRace Condition.

**Test Steps:**

```
1. Idempotencyness test:
 - [] related sameRefundRequestSendtwotimes, whetherCreatedone two entryRefund?
 - [] RefundSuccessafter, againtimespoint attackRefundby /ResendRequest

2. Race Conditiontest:
 - [] useuse Burp Turbo Intruder ConcurrencySend 10 related sameRefundRequest
 - [] Check:RefundwhetherExecutedone manytimes?resource fundswhethermanytimesreturn?

3. RefundCallbackReplay:
 - [] Alipay/WeChatofRefundSuccessCallback
 - [] ReplaythisCallback, ObserveSystemwhetherserious repeat handle manage
 - [] ModifyCallbackinof refund_id asotherRefund please

4. Expected Result:
 - serious repeatRequestshouldReturn"already handle manage"whileNon-againtimesExecute
 - ConcurrencyRequestshouldonly has oneSuccess
```

**Severity:** Severe - no limit provide take resource funds.

### Test Point 5.4:notPaymentOrderRefund

**false set:** SystemnotCheckOrderwhetherreal actualPaymentSuccessthat is allow allow initiate initiateRefund.

**Test Steps:**

```
1. Create Orderbut notPayment(Statusas"Pending Payment")
2. Attemptfor thisOrderinitiate initiateRefund:
 - [] POST /api/refund/apply {"order_id": "notPaymentOrderID", "amount": 299}
 - [] ModifyRefundRequestinof order_id asnotPaymentOrder

3. alreadyCancelOrderRefund:
 - [] for alreadyCancelofOrderinitiate initiateRefund
 - [] forRefundedofOrderagaintimesinitiate initiateRefund

4. Check:
 - SystemwhetherValidateOrderofPaymentStatus?
 - Refundwhethercan onlybased onValidPaymentRecord?
```

### Test Point 5.5:Refundbypass permission

**false set:** User A Canas forUser B ofOrderinitiate initiateRefund please.

**Test Steps:**

```
1. User A Obtainself ownofonePaidOrder order_id
2. User B Login, Attempt:
 - [] POST /api/refund/apply {"order_id": "AofOrderID", "reason": "test"}
 - [] ModifyRefundInterfaceinof user_id Parameteras A of user_id

3. Refundaudit audit bypass permission:
 - [] Regular Userwhether canaccess askRefundaudit auditInterface?
 - [] whether canbatch accurate/reject reject other personofRefund please?
```

---

## 6. test model block:Payment Gatewaycollect completeSecure

> WooYun participate reference:Payment Bypass 1,056 Caseinlarge quantity involvingNo. three methodPaymentcollect complete missing flaw

### Test Point 6.1:Alipay/WeChatCallbackSignatureValidate

**Test Steps:**

```
1. SignatureCompleteness:
 - [] whetherValidatedoneAllkeyField(out_trade_no, total_amount, trade_status)?
 - [] Signaturealgorithm methodwhetherSecure(RSA2 > RSA > MD5)?
 - [] whetheruseusedoneAlipay/WeChatprovide provideof method SDK validate?

2. CallbacksourceValidate:
 - [] whetherValidatedoneCallbackRequestofcome source IP?
 - [] notify_url whetheronly connect affected HTTPS?
 - [] Callback URL whetherPredictable/CanEnumeration?

3. Business ParameterValidate:
 - [] Callbackinof total_amount whetherandOrderDatabaseinofAmountratio for?
 - [] Callbackinof seller_id / mch_id whetherandcommerce accountConfigurationratio for?
 - [] trade_status whetheronly handle manage TRADE_SUCCESS(Alipay)/ SUCCESS(WeChat)?

4. abnormal common handle manage:
 - [] Sendformat mode errorofCallback(missing lessField), ObserveServerlinesas
 - [] Send trade_status=TRADE_CLOSED ofCallback, Observewhethertrigger initiateRefund
```

### Test Point 6.2:PaymentCredentialrepeatuse

**Test Steps:**

```
1. complete one entry small amountPayment(such as ¥0.01, such asifSystemallow allow)
2. Obtainthis entryPaymentofSuccessCredential(trade_no / transaction_id)
3. AttemptwillthisCredentialkey connecttoone entry large amount notPaymentOrder
 - [] ModifyCallbackinof out_trade_no aslarge amountOrdernumber
 - [] Direct CallOrderConfirmInterface, pass inject already useuseof trade_no

4. crossOrderCallbackReplay:
 - [] useuseOrder A(¥10)ofSuccessCallbackParameter
 - [] onlyModify out_trade_no asOrder B(¥999)ofOrdernumber
 - [] ObserveOrder B whetherbe identifier recordasPaid
```

### Test Point 6.3:Paymentsuper time exploituse

**false set:** Paymentsuper time afterOrderCancel, butPayment Gatewayof CallbackstillCanbe handle manage.

**WooYun mode:** "114Ticketing site logic flaw used payment timeout to leak sensitive information for tens of thousands of users" - exploitusesuper time window interfaceofStatusnot one cause.

**Test Steps:**

```
1. Create Order, initiate initiatePaymentbut not complete
2. etc.pendingOrdersuper timeCancel(Recordsuper time time between)
3. insuper time after:
 - [] Attemptcomplete of first initiate initiateofPayment(such asifPaymentlink connect stillValid)
 - [] mobile dynamicSendPaymentSuccessCallback
 - [] Check:alreadyCancelOrderwhetherbe serious new?
 - [] resource fundswhetherbe deduct take butOrderalreadyCancel(Causingresource funds)?

4. key inject point:
 - OrderCancelandPaymentCallbackhandle manage betweenwhether haslock machine make?
 - whethercorrect confirm handle manage done"alreadyCancelOrdercollecttoPaymentSuccess"ofscenario scene?
```

---

## 7. test model block six:wilduseSecureCheck

### Test Point 7.1:InterfaceUnauthorized Access

**WooYun mode:** Unauthorized Access 2,102+1,891 Case - "58.2% ofUnauthorized Access = manage manage backend console complete all expose exposure".

**Test Steps:**

```
1. backend console manage manageInterfaceprobe test:
 - [] /admin/order/list - AdministratorOrderlist
 - [] /admin/refund/list - Refundaudit audit list
 - [] /admin/payment/config - PaymentConfiguration
 - [] /api/internal/order/* - internal partInterface

2. not with any Cookie/Token Directaccess ask above descriptionPath
3. such asReturn 302/401/403, AttemptBypass:
 - [] Add X-Forwarded-For: 127.0.0.1
 - [] Modify HTTP Method(GET -> POST -> PUT)
 - [] Pathcase change ize:/Admin/ /ADMIN/
 - [] URL Encoding Bypass:/%61dmin/
```

### Test Point 7.2:Sensitive InformationDisclosure

**Test Steps:**

```
1. PaymentConfiguration Disclosure:
 - [] CheckFrontend JS inwhetherhardEncodingdoneAlipay AppID / WeChat MchID
 - [] CheckwhetherDisclosuredonePaymentKey / API Secret
 - [] Check /api/docs or /swagger-ui.html whetherexpose exposure

2. OrderDataDisclosure:
 - [] API Responseinwhetherinclude includePaymentKey/Signature value
 - [] error informationwhetherexpose exposure doneDatabaseresult structure/table name
 - [] LogFilewhetherCanaccess ask(/logs/payment.log)

3. debugging information:
 - []?debug=true whetheropen enable debugging mode
 - [] generate asset environment environmentwhetheruseusedonePayment Configuration
```

### Test Point 7.3:many channel channel not one cause

**WooYun mode:** Logic Flow Domain "Web Validate, move dynamic API notValidate".

**Test Steps:**

```
1. part levelPass Web endandMobile Client(App/H5)Executerelated same operation:
 - [] under singlePayment - AmountValidatewhetherone cause?
 - [] Refund please - limit make conditionwhetherone cause?
 - [] ModifyOrder - PermissionValidatewhetherone cause?

2. API version version error abnormal:
 - [] /api/v1/order and /api/v2/order whether hasDifferentofValidatelogic logic?
 - [] old version version API whetherstillCanaccess ask and missing less new increaseofSecureValidate?
```

---

## 8. risk assess assess matrix matrix

| Test Point | Risk Level | WooYun Datasupport | Business Impact |
|--------|---------|----------------|---------|
| Payment Amount Tampering (3.1) | **Severe** | Amount Tampering 176 Case, 83.0% High Risk | Directfinancial loss |
| Payment Callback Forgery (3.2) | **Severe** | Payment Bypass 1,056 Case, 68.7% High Risk | no limit avoid fee buy buy |
| Duplicate Refund (5.3) | **Severe** | Withdrawal 59 Case, 83.1% High Risk | no limit resource funds provide take |
| RefundAmount Tampering (5.1) | **Severe** | Balancetamper change 113 Case, 77.9% High Risk | super amountRefund |
| Concurrent Paymentdual flower (3.5) | **Severe** | Race Condition 266 Case, 74.8% High Risk | Balancedual flower |
| OrderStatustamper change (4.2) | **High** | Order Tampering 1,227 Case, 74.2% High Risk | skip throughPayment |
| PaymentState-Machine Bypass (3.3) | **High** | Design Flaw 1,391 Case, 65.3% High Risk | avoid feeObtaincommerce product |
| RefundState-Machine Bypass (5.2) | **High** | logic logic vulnerability 266 Case, 74.8% High Risk | Bypassaudit auditRefund |
| Orderbypass permission (4.1) | **High** | bypass permission 1,705 Case, 62.3% High Risk | Userhidden privateDisclosure |
| Shopping Cartprice format tamper change (2.1) | **High** | price format tamper change 70 Case, 74.3% High Risk | Lowprice buy buy |
| Couponabuseuse (3.6) | **in** | Payment BypasssubCategory | priority loss loss |
| InterfaceUnauthorized Access (7.1) | **High** | Weak Credentials/Unauthorized 7,513 Case, 58.2% High Risk | manage manage backend console flaw |
| Information Disclosure (7.2) | **in** | Information Disclosure 4,858 Case, 64.7% High Risk | after continue attack attack |

---

## 9. testExecutePriority

root according WooYun Datainofhigh-risk percentagerank sequence, create protocol bythe followingPriorityExecutetest:

### P0 - must first test(Severe / Directfinancial loss)
1. Payment Callback ForgeryandSignatureValidate (3.2, 6.1)
2. Payment Amount Tampering (3.1)
3. RefundAmount TamperingandDuplicate Refund (5.1, 5.3)
4. Concurrencydual flower / Race Condition (3.5)

### P1 - HighPriority(High Risk / business logic logicBypass)
5. PaymentState-Machine Bypass (3.3)
6. OrderStatustamper change (4.2)
7. RefundState-Machine Bypass (5.2)
8. Shopping Cartprice format/number quantity tamper change (2.1, 2.2)
9. OrderAuthorization Bypass (4.1)

### P2 - identifier accuratePriority
10. Couponabuseuse (3.6)
11. PaymentCredentialrepeatuse (6.2)
12. Paymentsuper time exploituse (6.3)
13. commerce product ID Replace (2.3)
14. notPaymentOrderRefund (5.4)

### P3 - supplement topup test
15. Information Disclosure (7.2)
16. InterfaceUnauthorized Access (7.1)
17. many channel channel not one cause (7.3)
18. Refundbypass permission (5.5)
19. Payment Gatewayswitch change attack attack (3.4)

---

## 10. expected period transaction pay item

| transaction pay item | content |
|--------|------|
| vulnerability report | EachDiscoverofvulnerability byNo. fourPhasemodel template output out(Severity + WooYun mode + Business Impact + Reproduction Steps + supplement create protocol) |
| testEvidence | EachTest PointofRequest/Responseintercept image(Burp Suite Export) |
| risk matrix matrix | remit totalAllDiscover, bySeverity x Canexploituseness rank sequence |
| Remediation Recommendation | based on WooYun defense defense modeofServerfix repeat method plan(Non-Clientsupplement) |

---

## Appendix:WooYun keyStatisticsciteuse

| specified identifier | number value | come source |
|------|------|------|
| Financial DomaintotalCase | 2,919 | WooYun Database 2010-2016 |
| Payment BypassCase | 1,056(68.7% High Risk) | financial-domain.md |
| Order TamperingCase | 1,227(74.2% High Risk) | financial-domain.md |
| Amount TamperingCase | 176(83.0% High Risk) | financial-domain.md |
| Balancetamper changeCase | 113(77.9% High Risk) | financial-domain.md |
| WithdrawalvulnerabilityCase | 59(83.1% High Risk) | financial-domain.md |
| price format tamper changeCase | 70(74.3% High Risk) | financial-domain.md |
| Logic Flow DomaintotalCase | 1,679 | logic-flow-domain.md |
| State-Machine BypassCase | 1,391(65.3% High Risk) | logic-flow-domain.md |
| Race ConditionCase | 266(74.8% High Risk) | logic-flow-domain.md |
| Authorization BypassCase | 1,705(62.3% High Risk) | authorization-domain.md |
| Information DisclosureCase | 4,858(64.7% High Risk) | information-domain.md |
| all quantity vulnerabilityDatabase | 22,132 | SKILL.md |

---

> **audit core provide:** "ClientRequestinout currentofany finance service number value all is one pendingValidateoffalse set.price format/number quantity/discount deduct/Balance/mobile continue fee -- such asifClientSenddone, ClientCanasModify." - WooYun Financial Domain law
