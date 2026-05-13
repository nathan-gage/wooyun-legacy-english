# mobile machine banklines App business logic logicSecureassess assess report

> Methodcomment:WooYun Business Logic Vulnerability Methodology v2.0
> Database foundation:22,132 real real vulnerabilityCase - 6 Domain - 33 type vulnerability
> TargetSystem:mobile machine banklines App(Transfer/Top-Up/Withdrawal/Wealth Product Purchase/Password Reset/Real-Name Verification)
> assess assess day period:____________day
> assess assess person:________________
> version version:v1.0

---

## directory record

- [No. one part part:business flow process map map](#No. one part part business flow process map map)
- [No. two part part:Securefalse set matrix matrix](#No. two part partSecurefalse set matrix matrix)
- [No. three part part:partDomainTest Case](#No. three part part partDomainTest Case)
 - [Domainone:AuthenticationSecure(8,846 Case Basis)](#DomainoneAuthenticationSecure)
 - [Domaintwo:AuthorizationSecure(6,838 Case Basis)](#DomaintwoAuthorizationSecure)
 - [Domainthree:FinancialSecure(2,919 Case Basis)](#DomainthreeFinancialSecure)
 - [Domainfour:Information Disclosure(6,446 Case Basis)](#DomainfourInformation Disclosure)
 - [Domain:logic logic flowSecure(1,679 Case Basis)](#Domain logic logic flowSecure)
 - [Domainsix:ConfigurationSecure(1,796 Case Basis)](#DomainsixConfigurationSecure)
- [No. four part part:DiscoverRecordmodel template](#No. four part partDiscoverRecordmodel template)
- [No. part part:risk assess level identifier accurate](#No. part part risk assess level identifier accurate)
- [No. six part part:assess assess total result](#No. six part part assess assess total result)
- [Appendix](#Appendix)

---

## No. one part part:business flow process map map

### 1.1 business approx description

| itemsdirectory | content |
|------|------|
| Applicationtype | mobile machine banklines App |
| primary need participateandperson | Anonymous User/alreadyRegistrationUser/banklinesclient account(already card)/VIP client account/client account through manage/Administrator |
| collect inject mode | mobile continue fee/manage finance funds/exploit error collect inject |
| sensitive sensitiveData | banklinescard number/Identity Cardnumber/mobile number/transaction easyPassword/Balance/transaction easy flow horizontal |
| combine scale need require | "commerce business banklinesInternet banklinesmanage manage lines method""banklinesbusinessFinancialmachine structure informationSecurespecified cite" |

### 1.2 audit core business flow process map map

#### flow process 1:Transfer

```
initiate initiateTransfer -> output inject collect payment information -> output injectAmount -> output inject transaction easyPassword/CAPTCHA -> Confirm -> handle manage -> complete
 | | | | |
 v v v v v
 identity copyValidate collect payment personValidate AmountValidate twotimesAuthentication Serverhandle manage
(Session) (card number/account name) (limit amount/Balance) (short information/person) (audit coreSystem)
```

Statustransfer move: -> pendingConfirm -> pending handle manage -> handle managein -> Success/Failure

#### flow process 2:Top-Up

```
select Top-Upmethod mode -> output injectAmount -> select Paymentchannel channel -> PaymentValidate -> CallbackConfirm -> BalanceUpdate
```

Statustransfer move:Pending Payment -> Paymentin -> PaymentSuccess -> inject account complete / PaymentFailure

#### flow process 3:Withdrawal

```
initiate initiateWithdrawal -> select banklinescard -> output injectAmount -> transaction easyPasswordValidate -> risk control audit audit -> break payment -> complete
```

Statustransfer move:pending audit audit -> audit auditPass -> break paymentin -> alreadytoaccount / audit audit reject reject

#### flow process 4:Wealth Product Purchase

```
 product -> Viewdetailed details -> output inject buy buyAmount -> risk assess assessConfirm -> transaction easyPassword -> deduct payment -> hold repositoryUpdate
```

Statustransfer move:select buy -> pendingConfirm -> pending deduct payment -> deduct paymentSuccess -> hold repositoryin

#### flow process 5:Password Reset

```
select serious set method mode -> identity copyValidate(mobile number+SMS Verification Code/person Identify) -> Set New Password -> complete
 | | |
 v v v
 Accountset characters Validateidentity copy PasswordUpdate
(mobile number/Identity Card) (short information/person /Secureask problem) (strong degreeValidate)
```

Statustransfer move:Request -> Validatein -> alreadyValidate -> PasswordalreadyUpdate

#### flow process 6:Real-Name Verification(KYC)

```
fill inPersonal Information -> Uploadcert item photo -> OCR Identify -> person body check test -> company connect network audit check -> Bindingbanklinescard -> four need Validate
```

Statustransfer move:notAuthentication -> informationSubmit -> audit auditin -> alreadyAuthentication / AuthenticationFailure

### 1.3 Trust BoundaryIdentify

| Trust Boundary | risk point | key inject degree |
|---------|-------|-------|
| Client vs Server | Amount/number quantity/Statusetc.ParameterwhetheronlyinClientValidate | Critical |
| Regular User vs Administrator | manage manageInterfacewhetherdo donePermissionisolation | High |
| User A vs User B | whetherCanas operation other personAccount/Order/resource asset | Critical |
| App vs audit coreSystem | inbetween layerwhether hasindependent standaloneofSecureValidate | High |
| correct mode environment environment vs Test Environment | Test Interface/Accountwhether retainingenerate asset environment environment | High |

### 1.4 Test Accountaccurate prepare

| Accounttype | Purpose | number quantity |
|---------|------|------|
| Regular User A | Horizontal Authorization Bypasstest(initiate initiate method) | 1 |
| Regular User B | Horizontal Authorization Bypasstest(Targetmethod) | 1 |
| VIP User | Permissionerror abnormal test | 1 |
| not real nameUser | Real-Name Verificationflow process test | 1 |
| AdministratorAccount | Vertical Authorization Bypasstest participate photo | 1 |

---

## No. two part part:Securefalse set matrix matrix

based on WooYun 22,132 CaseofStatisticsscale law, for mobile machine banklines App completethe followingSecurefalse set.byhigh-risk percentage sequence rank list.

| ID | false set | WooYun mode | high-risk percentage | impact response | Priority |
|------|------|------------|---------|------|-------|
| H-01 | Password Resetflow process existinStepskip throughorCAPTCHADisclosure | Password Reset(777cases, 88.0%High Risk) | 88.0% | ArbitraryUserAccountconnect manage | P0 |
| H-02 | Transfer/WithdrawalAmountParameterCaninClienttamper changeasnegative value | Amount Tampering(176cases, 83.0%High Risk) | 83.0% | Directresource funds | P0 |
| H-03 | WithdrawalInterfaceexistinConcurrencyRace ConditionCausingdual flower | Withdrawal(59cases, 83.1%High Risk) | 83.1% | super amountWithdrawal | P0 |
| H-04 | BalanceParameterfromClientpass recursive andServernot serious newCompute | Balancetamper change(113cases, 77.9%High Risk) | 77.9% | no limit resource funds | P0 |
| H-05 | Transfer/Top-Upflow processCanskip throughPaymentValidateStep | Order Tampering(1,227cases, 74.2%High Risk) | 74.2% | notPaymentcomplete transaction easy | P0 |
| H-06 | User A CanPasstamper change ID View/operationUser B oftransaction easy | bypass permission(1,705cases, 62.3%High Risk) | 62.3% | other person resource asset be operation control | P0 |
| H-07 | Top-UpCallbackInterfacemissing SignatureValidateCanbe forgery | Payment Bypass(1,056cases, 68.7%High Risk) | 68.7% | falseTop-Uptoaccount | P0 |
| H-08 | SMS Verification Codeno rate rate limit make/no expired/CancrossUseruseuse | CAPTCHA Bypass(384cases, 44%High Risk) | 44.0% | Validatebody systemInvalidate | P1 |
| H-09 | App InterfaceReturndone super out UI showofsensitive sensitiveField | Information Disclosure(4,858cases, 64.7%High Risk) | 64.7% | Private DataBatchDisclosure | P1 |
| H-10 | Real-Name Verificationflow processCanbeBypassorStatusCanbe tamper change | Design Flaw(1,391cases, 65.3%High Risk) | 65.3% | not real nameUser Allfunction can | P1 |
| H-11 | manage manage backend console/debuggingInterfaceexpose exposureinPublic Internetno need toAuthentication | Misconfiguration(1,796cases, 72.6%High Risk) | 72.6% | Systemcomplete all flaw | P1 |
| H-12 | Wealth Product PurchaseCanBypassrisk assess assessortamper change product ID buy buy not match configofproduct | logic logic vulnerability(266cases, 74.8%High Risk) | 74.8% | monitor manage risk + resource funds risk | P1 |

---

## No. three part part:partDomainTest Case

---

### Domainone:AuthenticationSecure

> WooYun Database foundation:8,846 Case, cover cover weakCredential/Password Reset/LoginBypass/CAPTCHA Bypass
> audit core principle rule:identity copyAuthenticationis one condition link, each one environment allmust

#### 1.1 LoginAuthenticationtest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| AUTH-01 | Weak Credentials/default authPassword | useuse admin/admin/admin/123456/test/test etc.common seenCredentialAttemptLogin | reject rejectLogin | | |
| AUTH-02 | Brute Forcedefense protect | continuous continue output inject errorPassword 10+ times, Observewhether hasAccountlock set/IP disable/CAPTCHAtrigger initiate | 5 timesFailureafter trigger initiate protect protect machine make | | |
| AUTH-03 | CAPTCHAValidness | ObtainImage CAPTCHAafter, useSameCAPTCHAvalue manytimesSubmitLoginRequest | CAPTCHAsingletimesValid, useuseafterInvalidate | | |
| AUTH-04 | CAPTCHA Bypass-move removeParameter | InterceptLoginRequest, move removeCAPTCHAField, ObservewhetherstillCanLogin | Serverreject reject noCAPTCHAofRequest | | |
| AUTH-05 | CAPTCHA Bypass-Emptyvalue | willCAPTCHAParametersetasEmptycharacter symbol string | Serverreject reject | | |
| AUTH-06 | AccountEnumeration | part level output inject existinandnot existinofUsername, for ratioResponseerror abnormal(content/time between/Statuscode) | system oneoferror provide show, no method part | | |
| AUTH-07 | LoginInterfacerate rate limit make | useuse Burp Intruder fast rateSend 100 timesLoginRequest | trigger initiate rate rate limit make/IP disable | | |
| AUTH-08 | many because AuthenticationBypass | completePasswordValidateafter, not complete short information/person ValidateDirectaccess ask function canInterface | function canInterfacereject reject not complete MFA ofRequest | | |
| AUTH-09 | SessionFixed | LoginfirstRecord Session ID/Token, LoginafterCheckwhetherUpdate | Loginafter generate complete all newof Session/Token | | |
| AUTH-10 | ConcurrencyLogincontrol make | SameAccountintwo platform set prepare same timeLogin | root according policy strategy: out first oneorreject reject after one | | |
| AUTH-11 | Token Validity Period | provide take JWT/Token, etc.pending super time after useuse | expired Token be reject reject | | |
| AUTH-12 | Token forgery | Analyze JWT result structure, AttemptModify payload(user_id etc.)after useuse | SignatureValidateFailure, Requestbe reject reject | | |

**WooYun participate referenceCase:**
- special item flowa systembackend consoleLoginBypass/SQLinject inject(ten-thousandUser/operate single/banklinescard/Identity Cardphoto image)
- search APPa siteLoginBypass+SQLinject injectrootPermission
- card cart network some serious needSystemSuccessBypassCAPTCHAlimit make

#### 1.2 Password Resettest

> WooYun Statistics:777 Case, 88.0% High Risk -- integerDatacollectinSevereness mostHighofVulnerability Category

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| RST-01 | serious set command cardDisclosure | InterceptPassword ResetofAll HTTP Response, Check token/CAPTCHAwhetherout currentinResponse Bodyin | Token notinanyResponseinexpose exposure | | |
| RST-02 | serious set command cardPredictableness | continuous continueRequestmanytimesPassword Reset, Analyze token valueandgenerate complete scale law | Token asHigh machine value(>=32character section), no method prediction | | |
| RST-03 | Stepskip through-Directset setPassword | skip through short informationValidateStep, DirectRequest"Set New Password"Interface(Modify step ParameterorDirect CallInterface) | ServerValidatefirst setStepcompleteStatus, reject rejectRequest | | |
| RST-04 | Useridentifier identifyReplace | inserious set flow processin, will user_id/mobile numberReplaceasTargetUser B ofidentifier identify | ServerBindingwhen firstValidateSessionandUseridentifier identify, reject rejectReplace | | |
| RST-05 | SMS Verification CodeBrute Force | 4-6 charactersSMS Verification Code, use Burp Intruder TraversalAllCancan value | CAPTCHAerrortimesnumber limit make(such as 5 timesafterInvalidate) | | |
| RST-06 | SMS Verification Codenot expired | ObtainCAPTCHAafteretc.pending 10 minutes, useuseoldCAPTCHA | CAPTCHAhasValidity Period(create protocol <=5 minutes) | | |
| RST-07 | SMS Verification CodecrossUseruseuse | use A mobile machine collecttoofCAPTCHA serious set B ofPassword | CAPTCHAandmobile number/UserBinding, reject reject crossUseruseuse | | |
| RST-08 | Responsetamper change | InterceptServer"CAPTCHAerror"ofResponse, tamper changeas"ValidatePass", ObserveClientwhetherreleaselines | Client+Serverdual seriousValidate, tamper changeResponsenot impact responseServerStatus | | |
| RST-09 | Host Headerinject inject | inPassword ResetRequestinModify Host Headerasattack attack personDomain Name, Checkserious set link connectwhetheruseusethisDomain Name | serious set link connectinofDomain NamehardEncoding, not affected Host Headerimpact response | | |
| RST-10 | serious set command card serious repeat useuse | Successserious setPasswordafter, againtimesuseuseSamecommand card/CAPTCHA | command card singletimesValid, useuseafterImmediately Invalidate | | |
| RST-11 | andlinesserious setRace | forSameAccountsame time initiate initiate many serious setRequest | Systemcorrect confirm handle manageConcurrency, after continueRequestuse first sequence command cardInvalidate | | |

**WooYun participate referenceCase:**
- TCLsystem one identity copyAuthenticationPlatformvulnerability, AllUserAccountPasswordCanserious set -- cross N+ businessSystemCompleteAccountconnect manage
- FMcompany PlatformArbitrary User Password Reset
- above Empty toolPersonal InformationDisclosure/Password Reset(Bypassshort informationValidate)

#### 1.3 SMS Verification CodeSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| SMS-01 | SMS Bombing | forSamemobile numbercontinuous continueRequestSendCAPTCHA 20 times | SendRate Limit(such as 60 1 times, eachdays 10 times) | | |
| SMS-02 | Arbitrarymobile numberSend | ModifyRequestinofmobile numberasArbitrarynumber code | mobile numberandwhen firstUser/SessionBindingValidate | | |
| SMS-03 | national actual number codeBypass | mobile numberfirst add +86/0086 oruseusenational actual number code format mode | system one format mode ize handle manage, not impact responseSecureValidate | | |
| SMS-04 | CAPTCHAlong degree | ObserveCAPTCHAcharacters number | >= 6 characters number character | | |
| SMS-05 | CAPTCHArepeat degree | manytimesObtainCAPTCHA, Analyzewhether is order sequence/ number character/Predictable | machine generate complete, no scale law | | |

---

### Domaintwo:AuthorizationSecure

> WooYun Database foundation:6,838 Case, cover coverHorizontal Authorization Bypass(IDOR)/Vertical Authorization Bypass/Unauthorized Access
> audit core principle rule:identity copyAuthenticationreturn " is?", Authorizationreturn " can do?" -- large many numberApplicationinNo. two ask problem above table current

#### 2.1 Horizontal Authorization Bypass(IDOR)test

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| IDOR-01 | Viewother person transaction easyRecord | use A of Token access ask B oftransaction easy listInterface(Replace user_id/account_id) | Return 403 oronlyReturn A ofData | | |
| IDOR-02 | Viewother personTransferdetailed details | Replace transfer_id/order_id as B ofTransferOrder ID | Return 403 | | |
| IDOR-03 | Viewother person banklinescard information | Replace card_id as B ofbanklinescard ID | Return 403 | | |
| IDOR-04 | Viewother person manage finance hold repository | Replace portfolio_id or user_id View B ofmanage finance hold repository | Return 403 | | |
| IDOR-05 | Modifyother person collect payment person list | use A of Token for B ofcommonusecollect payment person advancelinesincrease/delete/change | Return 403 | | |
| IDOR-06 | ID Enumeration | Observe user_id/order_id whether isorder sequence integer number, Traversal ID Scope | useuse UUID v4 notPredictableidentifier identify symbol | | |
| IDOR-07 | Parameter PollutionBypass | Send?user_id=A&user_id=B, ObserveServertake which value | takeNo. one valueorreject reject serious repeatParameter | | |
| IDOR-08 | Encoding Bypass | will ID advancelines Base64/Hex EncodingafterReplace | Serverdecode code after still doAllpermissionValidate | | |
| IDOR-09 | JSON Nestedinject inject | in JSON Request BodyinNested user for Modify ID, such as `{"user":{"id":"BofID"}}` | ServerignoreClientprovide provideofUseridentifier identify | | |
| IDOR-10 | BatchExportbypass permission | CallExport/DownloadInterfacetime, Modify select conditionObtainAllUserData | ExportScopelimit set for when firstUser | | |

**IDOR Highlevel technique(WooYun Statistics:simple single ID Replaceonly shareCaseof 30%):**

```
- Direct ID Replace:123 -> 124
- Negative Number/zero ID:id=0, id=-1
- number array inject inject:uid[]=123(BypasstypeCheck)
- JSON Nested:{"user": {"id": 456}}
- Parameter Pollution:?uid=123&uid=456
- Encoding Bypass:Base64(456)/Hex(456)
- PathTraversal:/users/../users/456
```

#### 2.2 Vertical Authorization Bypasstest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| PRIV-01 | Regular Useraccess ask manage manageInterface | useRegular User Token Request /admin/* or /api/admin/* Interface | Return 403 | | |
| PRIV-02 | tamper changeRoleParameter | RegistrationorModifyPersonal Informationtime, Add role=admin/is_admin=true Parameter | ServerignoreClientprovide provideofRoleParameter | | |
| PRIV-03 | HTTP Methodtamper change | for manage manageInterfaceuseuseDifferent HTTP Method(GET->POST/POST->PUT) | AllMethodaverage needPermissionValidate | | |
| PRIV-04 | FrontendrouteBypass | Directaccess ask App inAdministrator can toofpage route | BackendInterfacestill doPermissionValidate | | |
| PRIV-05 | function canPermissiondetail degree | wild client accountwhetherCanCallclient account through manage special attributeInterface(such asaudit batch/debug amount) | Return 403 | | |

#### 2.3 Unauthorized Accesstest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| UNAUTH-01 | no Token access ask sensitive sensitiveInterface | move removeRequestinof Authorization Header/Cookie, access askAllbusinessInterface | Return 401 | | |
| UNAUTH-02 | manage manage backend console expose exposure | Scan /admin//console//manage//api-docs etc.Path | notCanaccess askorrequiresAuthentication | | |
| UNAUTH-03 | API DocumentDisclosure | access ask /swagger-ui.html//api-docs//openapi.json | generate asset environment environment not expose exposure API Document | | |
| UNAUTH-04 | debuggingEndpoint | access ask /actuator//debug//trace//heapdump//env | notCanaccess ask | | |
| UNAUTH-05 | internal partInterfaceprotect protect | PassAdd X-Forwarded-For: 127.0.0.1 AttemptBypass IP limit make | not affected Headerimpact response | | |

**WooYun participate referenceCase:**
- Beijing Hyundai platform allowed unauthorized traversal of millions of identity documents/vehicle registration documents -- order sequenceFile ID noOwnership Check
- finance networkPermissionBypassLoginotherUserAccount
- innationalFinancialAuthenticationincorea systemUnauthorized Access(involvingInternal Networkinformation)

---

### Domainthree:FinancialSecure

> WooYun Database foundation:2,919 Case, 68-83% High Risk -- andfunds Directrelated keyoflogic logic initial final is mostHighPriority
> audit core law:ClientRequestinout currentofany finance service number value all is one pendingValidateoffalse set

#### 3.1 TransferSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| TRF-01 | TransferAmount Tampering-Zero Value | InterceptTransferRequest, will amount changeas 0 | Serverreject reject 0 yuanTransfer | | |
| TRF-02 | TransferAmount Tampering-negative value | will amount changeas -1000(CancanCausingcollect payment person reverse toward deduct payment) | Serverreject reject negative value | | |
| TRF-03 | TransferAmount Tampering-most small value | will amount changeas 0.001(small number precision degree attack attack) | has mostLowTransferAmountlimit make | | |
| TRF-04 | TransferAmount Tampering-super large value | will amount changeas 999999999999(integer number out) | has mostHighlimit amount andServerValidateBalance | | |
| TRF-05 | TransferAmount Tampering- plan number method | will amount setas 1e10 | Servercorrect confirm decode orreject reject | | |
| TRF-06 | transfer outAccounttamper change | will from_account Replaceasother personAccount | ServerValidate from_account attribute for when firstUser | | |
| TRF-07 | Transfermobile continue fee tamper change | such asifRequestininclude include fee Parameter, Modifyas 0 | mobile continue fee byServerCompute, not connect affectedClientvalue | | |
| TRF-08 | Transferlimit amountBypass | Modifysingle entry/day plan limit amountParameter(Clientpass recursive) | limit amountinServerValidate, notCantamper change | | |
| TRF-09 | Race Condition-dual flower | Balance 100 yuan, same time initiate initiate two entry 100 yuanTransfer(Burp Turbo Intruder Concurrency) | only one entrySuccess, Balancecorrect confirm | | |
| TRF-10 | transaction easyPasswordBrute Force | continuous continue output inject error transaction easyPassword | transaction easyPassworderrortimesnumber limit make(such as 5 timeslock set) | | |
| TRF-11 | transaction easyPasswordBypass | move removeRequestinof trade_password/pay_password Parameter | Serverneed requiremustprovide provide transaction easyPassword | | |
| TRF-12 | TransferOrderReplay | ReplaySuccessofTransferRequest | IdempotencynessValidate, reject reject serious repeat transaction easy | | |

#### 3.2 Top-UpSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| RCH-01 | Top-UpAmount Tampering | inTop-UpRequestinModify amount | AmountbyServerandPayment Gatewaydual towardConfirm | | |
| RCH-02 | Payment Callback Forgery | model Payment GatewayCallbackInterface, Send falseofPaymentSuccesswild notify | CallbackValidateSignature, forgeryRequestbe reject | | |
| RCH-03 | CallbackReplayattack attack | Replayreal realofTop-UpSuccessCallback | IdempotencyValidate, Same order_id not serious repeat inject account | | |
| RCH-04 | CallbackAmountnot one cause | real actualPayment 1 yuanbutCallbackwild notifyAmountas 1000 yuan | Serveraudit forOrderAmountandCallbackAmountone cause | | |
| RCH-05 | CallbackOrdernumberReplace | use 1 yuanofPaymentSuccessCallbackmatch config 1000 yuanofTop-UpOrder | OrdernumberandPaymentflow horizontal number one for oneBinding | | |
| RCH-06 | testPaymentchannel channel | Checkwhether retainTest EnvironmentofPayment GatewayConfiguration | generate asset environment environment no testPaymentChannel | | |
| RCH-07 | Top-UpStatustamper change | ModifyClientTop-UpStatusfrom pending changeas success | Top-UpStatusbyServerroot accordingPaymentCallbackUpdate | | |

#### 3.3 WithdrawalSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| WDR-01 | WithdrawalAmount-negative value | willWithdrawal amount changeas -500(Cancan changeasTop-Up) | Serverreject reject negative value | | |
| WDR-02 | WithdrawalAmount-superBalance | Balance 100, Withdrawal 200 | ServerValidateBalancetopup ness | | |
| WDR-03 | WithdrawalTargetAccounttamper change | ModifyWithdrawaltoaccount banklinescardasother person card number | toaccount cardmustis when firstUseralreadyBindingofcard | | |
| WDR-04 | Race Condition-ConcurrencyWithdrawal | Balance 1000, same time initiate initiate 5 entry 1000 yuanWithdrawal(ConcurrencyRequest) | only 1 entrySuccess, Balancecorrect confirm deduct reduce | | |
| WDR-05 | small number precision degree attack attack | Withdrawal 0.001 yuan x 10000 times(exploituse inject cumulative error abnormal) | has mostLowWithdrawalAmountlimit make | | |
| WDR-06 | Withdrawalmobile continue feeBypass | Modify fee=0 ormove remove mobile continue feeParameter | mobile continue fee byServerCompute | | |
| WDR-07 | Withdrawalaudit auditBypass | Direct Callbreak paymentInterface, skip through audit auditStep | mustthrough through audit audit flow process | | |
| WDR-08 | WithdrawalOrderStatustamper change | willWithdrawalOrderStatusfrom pending tamper changeas approved | StatusbyServercontrol make | | |

#### 3.4 Wealth Product PurchaseSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| FIN-01 | product ID Replace | will product_id ReplaceasHighcollect /limit buy/Non-company open product | ServerValidateproductCanbuy buy nessandUserresource format | | |
| FIN-02 | buy buyAmount Tampering | Modifybuy buyAmountLowfor initiate buyAmount | has mostLowbuy buyAmountValidate | | |
| FIN-03 | Risk LevelBypass | LowRisk LevelUserbuy buyHighrisk product(Modify risk_level Parameter) | ServerValidateUserrisk assess assessResult | | |
| FIN-04 | risk assess assess skip through | not complete risk assess assess ask Direct Callbuy buyInterface | mustfirst complete risk assess assess | | |
| FIN-05 | exploit rate/collect rate tamper change | such asifRequestininclude include rate/yield Parameter, ModifyasHighvalue | collect rate byServerby productConfigurationCompute | | |
| FIN-06 | return other person manage finance | use A of Token return B ofmanage finance product(Replace holding_id) | AllpermissionValidate, only allow allow operation self ownofhold repository | | |
| FIN-07 | super amount buy buy | buy buyAmountsuper through product Balancedegree | ServerValidateproduct Canbuy amount degree | | |
| FIN-08 | Race Condition-limit buy product | Concurrencybuy buySamelimit buy product | not super, correct confirm control make amount degree | | |

**WooYun participate referenceCase:**
- M1905Movie site value2588Packageonly costs5jiao -- Passself audit batch real current 5000 price format error abnormal
- inprinciple banklines2handle vulnerabilityCangetshellimpact response finance pay wild/AlipayPayment
- banklinesvertical banklinesArbitrarycardBalance
- APPArbitraryUserLoginCanimpact responseUserAccountBalance(signBypass)
- innational wild plan feeSystemGetShell+Cangenerate completeTop-Upcard -- ArbitraryTop-Upcard generate complete

---

### Domainfour:Information Disclosure

> WooYun Database foundation:6,446 Case(shareAllDiscoverof 29%), Information DisclosureisAllother attack attackof ize
> audit core principle rule:Applicationexpose exposureofany super outUserneed requireofinformation all is vulnerability

#### 4.1 API ResponseDataDisclosure

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| INFO-01 | API through degreeReturn | for ratio API ResponseinofFieldand UI showofField(Userdetailed details/transaction detailsetc.) | ResponseField = UI requiresField, no many Sensitive Information | | |
| INFO-02 | banklinescard numberDisclosure | CheckeachInterfaceReturnofcard numberwhetherleak sensitive(shouldonly display after 4 characters) | card number leak sensitive show **** **** **** 1234 | | |
| INFO-03 | Identity CardnumberDisclosure | CheckeachInterfaceReturnofIdentity Cardnumberwhetherleak sensitive | Identity Cardnumber leak sensitive 110***********1234 | | |
| INFO-04 | mobile numberDisclosure | CheckeachInterfaceReturnofmobile numberwhetherleak sensitive | mobile numberleak sensitive 138****1234 | | |
| INFO-05 | transaction easyPasswordhash hashDisclosure | CheckUserinformationInterfacewhetherReturnPasswordrelated keyField | notReturnanyPasswordrelated keyField | | |
| INFO-06 | other personInformation Disclosure | Transfertime output inject collect payment card number, CheckReturnofaccount name informationDetailedprocess degree | onlyReturnleak sensitiveofaccount name(such as *) | | |
| INFO-07 | error information through degree expose exposure | SubmitNon-methodParametertrigger initiateServererror, CheckwhetherReturnstack stack /SQL /internal partPath | Returnsystem oneoferror information, no technique detail section | | |
| INFO-08 | ClientStorageCheck | Check App version Storage(SharedPreferences/Keychain/SQLite)inwhetherexist has clear text sensitive sensitiveData | sensitive sensitiveDataadd secretStorageornot version Storage | | |

#### 4.2 sensitive sensitivePathandConfigurationFileDisclosure

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| LEAK-01 | version version control makeFile | access ask /.git/config//.svn/entries | Return 404, notCanaccess ask | | |
| LEAK-02 | prepare copyFile | access ask /backup.zip//db.sql//*.bak | Return 404 | | |
| LEAK-03 | environment environmentConfigurationFile | access ask /.env//config.yml//application.properties | Return 404 | | |
| LEAK-04 | LogFile | access ask /logs///log///access.log | Return 404 | | |
| LEAK-05 | API Document | access ask /swagger-ui.html//api-docs//redoc | generate asset environment environment not expose exposure | | |
| LEAK-06 | monitor control page template | access ask /grafana//prometheus//kibana | requiresAuthenticationornotCanfromPublic Internetaccess ask | | |
| LEAK-07 | debuggingEndpoint | access ask /actuator/env//actuator/heapdump//debug/pprof | notCanaccess ask | | |
| LEAK-08 | test page | access ask /test//demo//phpinfo.php | generate asset environment environment no test page | | |

#### 4.3 wild informationSecure

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| COMM-01 | HTTPS strong make | check whether there is HTTP Portopen release, HTTP Requestwhether 301 to HTTPS | all strong make HTTPS | | |
| COMM-02 | SSL cert certificate | Checkcert certificateValidness/expired time between/cert certificate link | Validand not expired | | |
| COMM-03 | SSL Pinning | Attemptuse mitmproxy/Burp code manage packet capture | App enableuse SSL Pinning(needBypass can packet capture) | | |
| COMM-04 | ResponseHeaderSecure | Check Server/X-Powered-By etc.Headerwhetherexpose exposure technique stack | no technique stack version versionInformation Disclosure | | |
| COMM-05 | sensitive sensitiveDataclear text pass output | CheckPassword/card numberetc.whetherinRequest Bodyinclear text pass output | sensitive sensitiveFieldadd secret pass output | | |

**WooYun participate referenceCase:**
- TCLa systemMisconfiguration Leading To600ten-thousand clientName/mobile machine/ Disclosure
- percent large vulnerability risk involving2000WpersonDetailedinformation(Name/Identity Card/mobile number/)
- Sunshine InsuranceSensitive InformationDisclosureCausingSuccessadvance injectInternal NetworkSystem

---

### Domain:logic logic flowSecure

> WooYun Database foundation:1,679 Case, cover coverState-Machine Bypass/Race Condition/Business Rule Bypass
> audit core principle rule:EachmanyStepbusiness flow process all is oneStatusmachine, such asif can skip throughPrerequisitestoreach someStatus, ruleStatusmachine be

#### 5.1 State-Machine Bypasstest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| FLOW-01 | TransferStepskip through | notSend"output inject transaction easyPassword"ofRequest, Direct Call"ConfirmTransfer"Interface | mustcomplete transaction easyPasswordValidate | | |
| FLOW-02 | Top-UpStepskip through | without going throughPayment Gateway, Direct CallTop-UpcompleteCallback | CallbackrequiresValidofPayment GatewaySignature | | |
| FLOW-03 | Real-Name VerificationStepskip through | not complete body check test, Direct Call"Authenticationcomplete"Interface | mustcompleteAllAuthenticationStep | | |
| FLOW-04 | Wealth Product PurchaseStepskip through | not complete risk assess assess, Direct Callbuy buyInterface | mustfirstPassrisk assess assess | | |
| FLOW-05 | reverse towardStatustransfer move | CompletedofTransferAttemptchange return"Pending Payment"Status | not allow allow reverse towardStatustransfer move | | |
| FLOW-06 | no validStatustransfer move | AttemptwillOrderfrom"pending audit audit"Directchangeas"Completed" | only allow allow combine methodofStatustransfer movePath | | |
| FLOW-07 | StatusParameterClienttamper change | ModifyRequestinof status/step/stage Parameter | StatusbyServermaintain protect, not connect affectedClientStatusParameter | | |

#### 5.2 Race Conditiontest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| RACE-01 | Balancedual flower-Transfer | Balance X, use Turbo Intruder ConcurrencySend N entry X yuanTransfer | only 1 entrySuccess | | |
| RACE-02 | Balancedual flower-Withdrawal | Balance X, ConcurrencySend N entry X yuanWithdrawal | only 1 entrySuccess | | |
| RACE-03 | Coupon/ includeRace | singletimesuseuseofCoupon/ include, ConcurrencySend N timesuseuseRequest | only message 1 times | | |
| RACE-04 | to/ partRace | each day to, ConcurrencySend N timesto | only 1 times | | |
| RACE-05 | limit buy productRace | limit buy 1 copyofmanage finance product, Concurrencybuy buy N times | onlySuccess 1 times | | |
| RACE-06 | new person includeRace | newUsertimesLogin include, Concurrencydomain take N times | only domain take 1 times | | |

**Race Conditiontest technique need point:**

```
Toolselect:
- Burp Suite Turbo Intruder(infer, support hold HTTP/2 singletimescontinuous connect manyRequest)
- Python threading/asyncio Script
- curl backend consoleConcurrency (&)

Concurrencynumber:5-20 same timeRequest
keyValidate:Checkmost finalBalance/Statuswhetherandexpected period one cause
vulnerability determine set:manyRequestSuccess = existinRace Condition
```

#### 5.3 Business Rule Bypasstest

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| BIZ-01 | not real nameUserTransfer | not completeReal-Name VerificationofUserAttemptCallTransferInterface | be reject reject, provide show need first real name | | |
| BIZ-02 | not cardUserWithdrawal | Not BoundbanklinescardofUserAttemptWithdrawal | be reject reject | | |
| BIZ-03 | Transferto self own | collect payment person setasself ownofAccount | root according business scale rule allow alloworreject reject(needValidateno abnormal common) | | |
| BIZ-04 | infer / please self infer | self ownof please code to self own useuse | be reject reject | | |
| BIZ-05 | dynamic single | PassBatchRegistration/Logindomain take new person | has set prepare specified pattern/IP/mobile numberetc.Dimensionofrisk control | | |
| BIZ-06 | many channel channel not one cause | Sameoperation part levelPass App/H5/Web endExecute, for ratioValidateerror abnormal | each channel channelSecureValidateone cause | | |
| BIZ-07 | Time Windowexploituse | inSystemmaintain protect/day switchTime WindowExecuteTransfer | correct confirm reject rejectorrank handle manage | | |
| BIZ-08 | type mix | AmountFieldSendcharacter symbol string "0"/deploy value false/Emptyfor {} | Serverdo typeValidate | | |

#### 5.4 Real-Name Verification(KYC)logic logic test

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| KYC-01 | AuthenticationStatustamper change | Modifyversion exist/RequestinofAuthenticationStatusas"alreadyAuthentication" | Serverindependent standaloneValidateAuthenticationStatus | | |
| KYC-02 | other person cert itemAuthentication | use B ofIdentity Cardinformationas A completeReal-Name Verification | Name+Identity Card+mobile number+banklinescard four need one cause nessValidate | | |
| KYC-03 | body check testBypass | useusephoto image/ frequency replace code real person advancelines body check test | body check test reject reject state image image/expected record frequency | | |
| KYC-04 | OCR Resulttamper change | Intercept OCR IdentifyResultofRequest, Modifyidentity copy information | OCR ResultinServerandcompany Systemaudit validate | | |
| KYC-05 | AuthenticationinformationModify | alreadyAuthenticationUserAttemptModifyreal name information | requiresupdate severe formatofValidateflow processornot allow allowModify | | |
| KYC-06 | serious repeatAuthentication | Sameidentity copy informationAuthenticationmanyAccount | root according business scale rule limit make | | |

**WooYun participate referenceCase:**
- percent combine network someAPPDesign Flawimpact response100W+ submobile number -- Design FlawCausingBatchInformation Disclosure
- 114Ticketing site logic flaw used payment timeout to leak sensitive information for tens of thousands of users
- Datebao official site business-logic vulnerability allowed buying insurance for free or at an extremely low price

---

### Domainsix:ConfigurationSecure

> WooYun Database foundation:1,796 Case, 72.6% High Risk -- most tool powerofinject come selfDefault Configuration
> audit core principle rule:EachserviceofDefault Configurationall isas exploit whileNon-Secureset planof

#### 6.1 ServerConfigurationCheck

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| CONF-01 | Default Credentials-inbetween item | test Tomcat Manager (tomcat/tomcat)/Jenkins(No Authentication)/JBoss (admin/admin) etc. | noDefault CredentialsCanuse | | |
| CONF-02 | Default Credentials-Database | test Redis(No Authentication)/MongoDB(No Authentication)/MySQL (root/Empty) etc.Port | Databasenot expose exposureinPublic InternetorrequiresstrongAuthentication | | |
| CONF-03 | Default Credentials-monitor controlTool | test Grafana (admin/admin)/Zabbix (Admin/zabbix)/Nacos (nacos/nacos) | noDefault CredentialsCanuse | | |
| CONF-04 | Spring Boot Actuator | access ask /actuator/env//actuator/heapdump//actuator/configprops | notCanaccess askorrequiresAuthentication | | |
| CONF-05 | Druid monitor control | access ask /druid/index.html | notCanaccess askorrequiresAuthentication | | |
| CONF-06 | directory record list | access ask no index Fileofdirectory record | directory record list already disableuse | | |
| CONF-07 | HTTP Method | OPTIONS RequestCheckallow allowof HTTP Method | only allow allow must needofMethod, disableuse PUT/DELETE/TRACE | | |
| CONF-08 | CORS Configuration | Check Access-Control-Allow-Origin Header | notaswild config symbol *, limit setCaninformationDomain Name | | |
| CONF-09 | SecureResponseHeader | Check X-Frame-Options/X-Content-Type-Options/CSP/HSTS Header | AllSecureHeaderalready correct confirm set set | | |
| CONF-10 | FileUploadlimit make | AttemptUpload.jsp/.php/.aspx etc.CanExecuteFile | Whitelistlimit makeFiletype | | |
| CONF-11 | open release serious set toward | Modify redirect_url/return_url/callback_url asexternal partDomain Name | serious set towardTargetWhitelistValidate | | |
| CONF-12 | SSRF check test | in Webhook URL/HeaderURL etc.Parameterinoutput injectInternal Network IP (127.0.0.1, 10.0.0.0/8) | Server stop forInternal NetworkAddressofRequest | | |

#### 6.2 Mobile ClientSecurity Configuration

| ID | Test Item | Test Method | Expected Result | Actual Result | Status |
|------|-------|---------|---------|---------|------|
| MOB-01 | App Hardening/mix | reverse engineering APK/IPA, CheckCodewhethermix | Codealready mix, key logic logic notdirectly usableRead | | |
| MOB-02 | Root/bypass check test | in Root/bypass set prepare above operatelines App | App check testto Root/bypass and limit make function canorreject reject operatelines | | |
| MOB-03 | debugging mode | Check APK of android:debuggable attributes | setas false | | |
| MOB-04 | Logoutput out | operatelines logcat/Console, check whether there isSensitive Informationoutput out | noSensitive InformationinLoginoutput out | | |
| MOB-05 | templateSecure | repeat make banklinescard number/PasswordafterCheck template | sensitive sensitiveFielddisable stop repeat makeorself dynamic clear remove | | |
| MOB-06 | intercept image protect protect | inPasswordoutput inject/Balance show page intercept image | sensitive sensitive page disable stop intercept image | | |
| MOB-07 | key Secure | Passwordoutput inject time useuseofkey type | useuseSecurekey (self set define key, defense record /record) | | |
| MOB-08 | version Dataadd secret | Check SQLite/SharedPreferences/Keychain inofData | sensitive sensitiveDataadd secretStorage | | |
| MOB-09 | NetworkSecurity Configuration | Check network_security_config.xml (Android) / ATS (iOS) | disable stop clear text HTTP, Configuration SSL Pinning | | |

**WooYun participate referenceCase:**
- cloud informationusesocial informationWeChatmanage managePlatform -- banklinesPlatformDefault Credentials
- DaoCloudWeak Credentials+docker remote APIUnauthorized Access
- Tongcheng Travel system misconfiguration allowed arbitrary file uploadgetshell

---

## No. four part part:DiscoverRecordmodel template

eachDiscoverone vulnerability, useusethe followingmodel templateRecord:

```
## Discover #[ID]:[vulnerability identifier problem]

### basic information
- **Severity:** [Severe / High / in / Low / information]
- **Domain:** [Authentication / Authorization / Financial / Information Disclosure / logic logic flow / Configuration]
- **WooYun mode:** [match configofhistory history mode name name involvingCase Count/high-risk percentage]
- **CVSS assess part:** [0.0 - 10.0]
- **impact response function can:** [Transfer / Top-Up / Withdrawal / manage finance / Password Reset / Real-Name Verification / other]
- **forshouldTest ID:** [such as TRF-09, RACE-01]

### Business Impact
[Concrete description for banklinesbusinessofimpact response -- resource funds loss lossAmount/affected impact responseUserScope/combine scale risketc.]

### Reproduction Steps
1. [precision confirmofOperation Steps]
2. [include includeRequest/Responseintercept imageortext]
3. [...]

### Requestdetailed details
```
[HTTP Requestprinciple text]
```

### Responsedetailed details
```
[HTTP Responseprinciple text]
```

### intercept image/Evidence
[intercept imagePathor description]

### supplement create protocol
**Serverfix repeat(must):**
- [ConcreteofCode/architecture structureRemediation Recommendation]

**architecture structure layerHardening(create protocol):**
- [architecture structure level levelofchange advance create protocol]

**monitor control increase strong(create protocol):**
- [requiresincrease addofmonitor control specified identifier]

### participate reference
- WooYun type Case:[Casename name involving impact response]
- fix repeat participate reference:[linesbusiness most real]
```

---

## No. part part:risk assess level identifier accurate

### 5.1 Severityset define(Financiallinesbusiness specialuse)

| level level | set define | type scenario scene | CVSS Scope |
|------|------|---------|----------|
| **Severe** | directly usableCausingresource funds loss lossorlarge scale modelDataDisclosure, no need toUsertransaction | ArbitraryUserTransfer/Balancetamper change/Concurrencydual flower/Payment Callback Forgery/ArbitraryPassword Reset | 9.0 - 10.0 |
| **High** | CanCausingsingle oneUserAccountconnect manageorsensitive sensitiveDataBatchDisclosure | bypass permissionViewtransaction easyRecord/IDOR TraversalUserData/WithdrawalBypassaudit audit/manage manage backend console expose exposure | 7.0 - 8.9 |
| **in** | Canimpact responseUserhidden privateorbusiness flow processCompleteness, need one set condition | SMS Bombing/CAPTCHACanserioususe/through degree informationReturn/weakPasswordpolicy strategy | 4.0 - 6.9 |
| **Low** | Information DisclosureorMisconfiguration, notDirectimpact response businessSecure | technique stack version version expose exposure/MissingSecureResponseHeader/Detailederror information | 0.1 - 3.9 |
| **information** | Canprovide change advance but noDirectSecurerisk | not enableuse HSTS/Cookie missing less SameSite attributes | 0.0 |

### 5.2 WooYun DataValidate -- high-risk percentagepart deploy

| Domain | WooYun Case Count | high-risk percentage | banklines App forshouldfunction can |
|------|-------------|---------|-----------------|
| Password Reset | 777 | **88.0%** | Password Reset/transaction easyPassword Reset |
| Withdrawal | 59 | **83.1%** | Withdrawaltobanklinescard |
| Amount Tampering | 176 | **83.0%** | TransferAmount/Top-UpAmount |
| Balancetamper change | 113 | **77.9%** | AccountBalance/manage finance hold repository |
| logic logic vulnerability | 266 | **74.8%** | Race Condition/Flow Bypass |
| Order Tampering | 1,227 | **74.2%** | transaction easyOrderStatus |
| Misconfiguration | 1,796 | **72.6%** | ServerConfiguration/inbetween item |
| Payment Bypass | 1,056 | **68.7%** | Top-UpCallback/PaymentValidate |
| Information Disclosure | 4,858 | **64.7%** | API DataDisclosure/Configuration Disclosure |
| bypass permission | 1,705 | **62.3%** | IDOR/Vertical Authorization Bypass |
| Weak Credentials | 7,513 | **58.2%** | manage manage backend console/service array item |

---

## No. six part part:assess assess total result

### 6.1 DiscoverStatistics

| Severity | number quantity | percent part ratio |
|---------|------|-------|
| Severe | | |
| High | | |
| in | | |
| Low | | |
| information | | |
| **combine plan** | | **100%** |

### 6.2 byDomainpart deploy

| Domain | Severe | High | in | Low | information | combine plan |
|------|------|---|---|---|------|------|
| AuthenticationSecure | | | | | | |
| AuthorizationSecure | | | | | | |
| FinancialSecure | | | | | | |
| Information Disclosure | | | | | | |
| logic logic flowSecure | | | | | | |
| ConfigurationSecure | | | | | | |
| **combine plan** | | | | | | |

### 6.3 by function can part deploy

| function can | Severe | High | in | Low | information | combine plan |
|------|------|---|---|---|------|------|
| Transfer | | | | | | |
| Top-Up | | | | | | |
| Withdrawal | | | | | | |
| Wealth Product Purchase | | | | | | |
| Password Reset | | | | | | |
| Real-Name Verification | | | | | | |
| wilduse/base foundation set | | | | | | |
| **combine plan** | | | | | | |

### 6.4 integer body risk assess price

**Risk Level:** [Critical / High / in / Low]

**audit coreDiscover need:**

1. ________________
2. ________________
3. ________________

**priority firstRemediation Recommendation(by process degree rank sequence):**

| Priority | DiscoverID | Vulnerability Description | create protocol fix repeat period limit |
|-------|---------|---------|------------|
| P0 | | | 24 hoursinternal |
| P1 High | | | 7 daysinternal |
| P2 in | | | 30 daysinternal |
| P3 Low | | | under one version version |

### 6.5 combine scale map map

| Discover | related key method scale/identifier accurate | combine scale risk |
|------|-------------|---------|
| | "NetworkSecuremethod"No. two ten one condition | |
| | "Personal Informationprotect protect method" | |
| | "commerce business banklinesInternet banklinesmanage manage lines method" | |
| | PCI DSS | |
| | etc.protect 2.0 three level | |

---

## Appendix

### Appendix A:testToolclear single

| Tool | Purpose | Notes |
|------|------|------|
| Burp Suite Professional | HTTP Request Interception/Modify/Replay | audit coreTool |
| Burp Turbo Intruder | Race ConditionConcurrencytest | Financial Domainmust prepare |
| mitmproxy | Mobile Client HTTPS flow quantityIntercept | config combine SSL Pinning Bypass |
| Frida | App operatelinestime Hook(Bypass Root check test/SSL Pinning) | Mobile Clienttest must prepare |
| objection | based on Frida ofMobile ClientSecuretest framework architecture | |
| JADX / Hopper | APK/IPA reverse engineeringAnalyze | |
| Python + aiohttp/threading | self set defineRace ConditiontestScript | |
| Nmap | PortScan, Discoverexpose exposureofmanage managePort | |
| curl | fast rate API test | |
| jq | JSON ResponseAnalyze | |

### Appendix B:Test Environmentinformation

| itemsdirectory | content |
|------|------|
| App version version | |
| operationSystem | Android ____ / iOS ____ |
| test set prepare | |
| code manageTool | |
| testNetwork | |
| ServerDomain Name/IP | |
| API base foundationPath | |

### Appendix C:WooYun Methodcomment audit core principle rule return

**requiresavoidof maintain flaw (come self 22,132 Caseoflesson lesson):**

| flaw | current real |
|------|------|
| "ScandeviceCanas cover cover business logic logic" | Scandevice toofis special, not is logic logic vulnerability.no hasScandevice canDiscover"OrderStatusCanas skip throughPayment". |
| "I test done primary flow process, isSecureof" | 22,132 Casecert clear:logic logic vulnerability existinfor boundary boundary details. |
| "only need change price formatas 0.01" | that only is one test.WooYun Datadisplay 17+ typePaymentAttack Pattern. |
| "IDOR simple single, only need change ID" | IDOR hasEncoding Bypass/Parameter Pollution/JSON Nested.simple single change ID only shareCaseof 30%. |
| "FrontendValidatedone, no ask problem" | 68.7% ofPaymentvulnerability existinis becauseasValidateonlyinClient. |
| "Administratorpage templaterequiresDifferentofCredential" | 58.2% ofUnauthorized Access = complete all no has identity copyValidateofmanage manage backend console. |

**fourPhaseMethodCheck:**

- [] No. onePhase(map map):Allbusiness flow process/Statusmachine/Trust BoundaryalreadyCompleteRecord
- [] No. twoPhase(false set):>= 12 by impact response rank sequenceofSecurefalse set already complete
- [] No. threePhase(test):Eachfalse set hasEvidencesupport holdorreverse, Test CasealreadyExecute
- [] No. fourPhase(report):AllDiscoveralready by model templateRecord, includeBusiness ImpactandRemediation Recommendation

---

*report based on WooYun Business Logic Vulnerability Methodology v2.0, Datasource:WooYun vulnerabilityDatabase(20167)22,132 real realCase*

*assess assess person character:________________ day period:________________*

*audit audit person character:________________ day period:________________*
