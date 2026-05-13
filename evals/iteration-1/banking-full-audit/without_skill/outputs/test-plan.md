# mobile machine banklines App business logic logicSecureassess assess report

## Documentinformation

| itemsdirectory | content |
|------|------|
| itemsdirectory name name | XXX mobile machine banklines App business logic logicSecureassess assess |
| version version number | v1.0 |
| test day period | 2026-XX-XX 2026-XX-XX |
| tester | |
| App version version | |
| testPlatform | Android / iOS |
| report secret level | machine secret |

---

## 1. assess assess approx description

### 1.1 assess assessScope

versiontimesassess assess cover cover mobile machine banklines App the followingaudit core business model block:

| model block | function canScope |
|------|----------|
| Transfer | linesinternalTransfer/crosslinesTransfer/BatchTransfer/expected constraintTransfer/collect payment person manage manage |
| Top-Up | feeTop-Up/flow quantityTop-Up/horizontal electronic fee/informationusecard payment |
| Withdrawal | banklinescardWithdrawal/fast ratetoaccount/ wildtoaccount/large amountWithdrawal |
| Wealth Product Purchase | manage finance product /risk assess assess/buy buy/ return/collect check query |
| Password Reset | LoginPassword Reset/transaction easyPassword Reset/mobile Password/specified pattern serious set |
| Real-Name Verification | Identity CardAuthentication/banklinescardBinding/person Identify/ body check test |

### 1.2 assess assessMethod

- test:model attack attack person, not depend relySource Code
- test:result combine packet captureAnalyzeInterfacelogic logic
- Tool:Burp Suite / mitmproxy / Frida / Objection / jadx

### 1.3 Risk Levelset define

| etc.level | set define | CVSS participate reference |
|------|------|-----------|
| Severe | directly usableforge complete resource funds loss lossorlarge scale modelDataDisclosure | 9.0-10.0 |
| High Risk | CanBypassaudit coreAuthentication/Authorizationmachine make | 7.0-8.9 |
| Medium Risk | CanObtainSensitive InformationorBypassNon-audit coreSecurecontrol make | 4.0-6.9 |
| Low Risk | Information DisclosureorMisconfiguration, exploitusecondition | 0.1-3.9 |
| information | Security Recommendations, not structure completeDirect | N/A |

---

## 2. wilduseSecurebase line test

### 2.1 wild informationSecure

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| COM-01 | HTTPS strong make useuse | packet captureCheckAllRequestwhether HTTPS | AllRequestuseuse TLS 1.2+ | | |
| COM-02 | cert certificateValidate(Certificate Pinning) | useuseself cert certificate code manage packet capture, Observewhetherreject reject continuous connect | App reject rejectNon-expected period cert certificate | | |
| COM-03 | cert certificate lock setBypass degree | Frida/Objection hook SSL Pinning | assess assessBypassrepeat degree | | |
| COM-04 | sensitive sensitiveDataclear text pass output | packet captureCheckPassword/Identity Cardnumber/banklinescard numberetc.whetheradd secret | sensitive sensitiveFieldadd secret pass output | | |
| COM-05 | RequestSignaturemachine make | tamper changeRequestParameter, ObserveServerwhetherreject reject | existinValidSignatureValidate | | |
| COM-06 | timestamp/Nonce defenseReplay | Replayhistory historyRequest, Observewhetherbe reject reject | RequestnotCanReplay | | |
| COM-07 | SSL/TLS version versionandPassword item | useuse testssl.sh or sslyze Scan | not support hold SSL3/TLS1.0/weakPassword item | | |

### 2.2 ClientSecure

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| CLI-01 | reverse engineering protect protect | jadx/apktool reverse engineering, CheckCodemix process degree | key logic logic topup part mix | | |
| CLI-02 | Root/bypass check test | in Root/bypass set prepare above operatelines App | App check testtoand limit make audit core function can | | |
| CLI-03 | debugging device check test | attach add Frida/lldb/gdb debugging | App check testtodebugging and refund out | | |
| CLI-04 | version DataStorage | Check SharedPreferences/Keychain/SQLite | no clear textStorageSensitive Information | | |
| CLI-05 | LogInformation Disclosure | logcat/Console ViewoperatelinestimeLog | not output outSensitive Information | | |
| CLI-06 | intercept /record defense protect | intransaction easy pageAttemptintercept | key page disable stop intercept | | |
| CLI-07 | key Secure | CheckPasswordoutput injectwhetheruseuseSecurekey | useuseself set defineSecurekey, Non-Systemkey | | |
| CLI-08 | twotimesbreak include check test | serious newSignature APK after operatelines | App check testtoSignaturenot one cause and reject reject operatelines | | |
| CLI-09 | dynamic state library protect protect | Check SO Filewhetheradd /doCompletenessValidate | audit core logic logic SO has protect protect | | |
| CLI-10 | WebView Secure | Check JavaScript Interfaceexpose exposure/file:// protocol protocol | noHigh Risk JS Bridge expose exposure | | |
| CLI-11 | templateSecure | repeat makeSensitive InformationafterCheckSystem template | not allow allow repeat makeorself dynamic clear remove | | |
| CLI-12 | backend console fast photo protect protect | will App switchtobackend console, Viewany service manage manage device expected | display ormodel image | | |

### 2.3 AuthenticationandSessionmanage manage

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| AUTH-01 | LoginBrute Force | continuous continue output inject errorPassword, Observelock set policy strategy | 5timeserror after lock setAccount, lock set time between recursive increase | | |
| AUTH-02 | CAPTCHASecure | Checkshort information/Image CAPTCHAofgenerate complete/Validate/Validity Period | CAPTCHA >= 6characters, 5minutesexpired, ServerValidate | | |
| AUTH-03 | Session manage manage | Analyze Token generate complete scale rule/Validity Period/continue period machine make | Token notPredictable, combine manageValidity Period, SecureStorage | | |
| AUTH-04 | SessionFixed | Loginfirst afterObserve Token whetherupdate change | Loginafter generate complete new Token | | |
| AUTH-05 | ConcurrencySessioncontrol make | many set prepare same timeLoginSameAccount | out oldSessionorprovide showUser | | |
| AUTH-06 | Token Disclosureexploituse | useuseDisclosureof Token inother set prepareCallInterface | has set prepareBindingor IP Validate | | |
| AUTH-07 | refund outLogin | refund out after useuseold Token Request | Token Immediately Invalidate | | |
| AUTH-08 | generate itemIdentifySecure | Checkspecified pattern/Face ID ofreal currentand level policy strategy | notCanBypass, level needPasswordValidate | | |

---

## 3. Transfermodel blockSecuretest

### 3.1 Business Logic Vulnerability

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| TRF-01 | Amount Tampering | InterceptTransferRequest, ModifyAmountParameter(such aschangeasNegative Number/0/super large number/small number precision degree attack attack 0.001->0.009) | ServerValidateAmountcombine method ness, reject reject abnormal common value | | |
| TRF-02 | collect paymentAccounttamper change | InterceptRequestModifycollect payment methodAccount/Name | ServerValidatecollect payment information one cause ness | | |
| TRF-03 | Transferlimit amountBypass | Modifysingle entry/day plan limit amountParameter;part many entry small amount scale | limit amountinServerstrong makeExecute, notCanClientcontrol make | | |
| TRF-04 | mobile continue fee tamper change | Modifymobile continue feeFieldas 0 orNegative Number | mobile continue feeServerCompute, not connect affectedClientpass value | | |
| TRF-05 | TransferTargetAccountTraversal | AttempttowardDifferentAccounttransfer small amount, ObserveReturninformation error abnormal | not expose exposureTargetAccountwhether existsoferror abnormal information | | |
| TRF-06 | transaction easyPasswordBypass | DeleteorModifytransaction easyPasswordParameter | Serverstrong makeValidatetransaction easyPassword | | |
| TRF-07 | SMS Verification CodeBypass | notSendCAPTCHAFieldorSendEmptyvalue/history historyCAPTCHA | Serverstrong makeValidatewhentimesValidCAPTCHA | | |
| TRF-08 | TransferOrderReplay | ReplaySuccessofTransferRequest | Idempotencyness set plan, not serious repeat deduct payment | | |
| TRF-09 | ConcurrencyTransfer(condition) | Sametime ConcurrencySubmitmany entryTransfer, total amount super outBalance | BalanceValidateAtomic, notCansuper amount transfer out | | |
| TRF-10 | expected constraintTransfertamper change | Modifyexpected constraint time betweenasthrough time between | ServerValidatetime between combine method ness | | |
| TRF-11 | Transferflow process skip step | skip throughConfirmStep, Direct Callmost finalSubmitInterface | ServerValidateCompleteflow processStatus | | |
| TRF-12 | cross type remit rate tamper change | Modifyremit rateParameter | remit rate byServerreal timeObtain, not connect affectedClientvalue | | |

### 3.2 bypass permission test

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| TRF-H01 | Horizontal Authorization Bypass - check query other personTransferRecord | ReplaceRequestinofUser ID/Account | only canViewversion personRecord | | |
| TRF-H02 | Horizontal Authorization Bypass - useuseother personAccountTransfer | Replacepay paymentAccountasother personAccount | ServerValidateAccountreturn attribute | | |
| TRF-V01 | Vertical Authorization Bypass - Regular UserCallBatchTransfer | Regular UserDirect Call businessBatchTransferInterface | PermissionValidatereject reject | | |

---

## 4. Top-Upmodel blockSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| RCH-01 | Top-UpAmount Tampering | ModifyTop-UpAmountasNegative Number/0/extreme large value | ServerValidateAmountScope | | |
| RCH-02 | Top-UpTargetnumber code tamper change | Modifymobile number/ fee account number | AmountandTargetnumber codeServerBindingValidate | | |
| RCH-03 | priority /discount deduct tamper change | Modifypriority Amountordiscount deduct ratiocases | priority byServerCompute, not connect affectedClientpass value | | |
| RCH-04 | serious repeatTop-Up(Replay) | ReplaySuccessTop-UpRequest | IdempotencyValidate, not serious repeat deduct payment | | |
| RCH-05 | ConcurrencyTop-Up(condition) | ConcurrencySubmitmany entryTop-UpRequest | Balancededuct reduceAtomic | | |
| RCH-06 | Top-Upchannel channel tamper change | ModifyPaymentchannel channel/banklinescard ID | ServerValidatechannel channelandUserBindingkey system | | |
| RCH-07 | Top-UpOrderStatustamper change | ModifyCallbackinofPaymentStatusField | Serveras banklines/Paymentchannel channel real actualCallbackasaccurate | | |
| RCH-08 | Top-Uppage amountandreal pay not one cause | select 100 yuanpage amount butModifyreal payas 1 yuan | ServerValidatepage amountandreal pay one cause ness | | |

---

## 5. Withdrawalmodel blockSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| WDR-01 | WithdrawalAmount Tampering | ModifyAmountasNegative Number/0/super outBalanceofvalue | ServerValidateAmountcombine method ness involvingBalancetopup | | |
| WDR-02 | Withdrawalbanklinescard tamper change | ReplaceWithdrawalTargetbanklinescardasother person card number | ServerValidatebanklinescard return attribute when firstUser | | |
| WDR-03 | Withdrawalmobile continue feeBypass | Modifymobile continue feeFieldas 0 | mobile continue feeServerCompute | | |
| WDR-04 | Withdrawallimit amountBypass | Modifysingle entry/day plan limit amountParameter | limit amountServerstrong makeExecute | | |
| WDR-05 | ConcurrencyWithdrawal(condition) | same time initiate initiate many entryWithdrawal, total amount superBalance | Balancededuct reduce principle sub operation, reject reject super amount | | |
| WDR-06 | WithdrawalOrderReplay | ReplaySuccessWithdrawalRequest | IdempotencyValidate, not serious repeat out payment | | |
| WDR-07 | Withdrawaltoaccount time between tamper change | Modifytoaccount type(wild change fast rate)but not change mobile continue fee | toaccount typeandfeeuseServerBinding | | |
| WDR-08 | WithdrawalCancelafter resource funds return refund | CancelWithdrawalafterCheckBalancewhethercorrect confirm return refund | resource funds correct confirm return, no over-refund under-refund | | |
| WDR-09 | large amountWithdrawalaudit auditBypass | large amountWithdrawalRequestinDelete/Modifyaudit audit identifier identify | Serverroot accordingAmountstrong make trigger initiate audit audit flow process | | |

---

## 6. Wealth Product Purchasemodel blockSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| FIN-01 | buy buyAmount Tampering | Modifybuy buyAmountLowfor initiate buyAmountorNon-recursive increase single characters | ServerValidateinitiate buyAmountandrecursive increase single characters | | |
| FIN-02 | product information tamper change | Modifyproduct ID buy buy already under architecture/not above line product | ServerValidateproductStatus | | |
| FIN-03 | collect rate tamper change | Modifyexpected period collect rateParameter | collect rate byServerCompute, not connect affectedClientvalue | | |
| FIN-04 | Risk LevelBypass | LowRisk LevelUserbuy buyHighrisk product(ModifyRisk LevelParameter) | ServerValidateUserreal actual risk assess assessetc.level | | |
| FIN-05 | buy buy amount degreeBypass | super limit amount buy buy;Modifylimit amountParameter | Serverstrong makeExecuteamount degree limit make | | |
| FIN-06 | Concurrencybuy buy(condition) | Concurrency buy limit amount product, super out product total amount degree | productBalancededuct reduceAtomic | | |
| FIN-07 | returnAmount Tampering | Modify return copy amount/Amountsuper out hold has quantity | ServerValidatereal actual hold has copy amount | | |
| FIN-08 | close period returnBypass | close period internalDirect Call returnInterface | ServerValidate close period limit make | | |
| FIN-09 | manage financeOrderReplay | Replaybuy buySuccessRequest | IdempotencyValidate, not serious repeat deduct payment | | |
| FIN-10 | collect check query bypass permission | ReplaceUser ID check query other person collect | onlyReturnwhen firstUserData | | |
| FIN-11 | singleTime Windowtamper change | super through single time between afterCall singleInterface | ServerValidate singleTime Window | | |
| FIN-12 | risk assess assess ask tamper change | DirectModifyrisk assess assessResultwhile not do ask | ServerRecordask flow processCompleteness | | |

---

## 7. Password Resetmodel blockSecuretest

### 7.1 LoginPassword Reset

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| PWD-01 | SMS Verification CodeBrute Force | Enumeration 4/6 charactersCAPTCHA | limit makeAttempttimesnumber(such as 5 timeslock set), CAPTCHAValidity Periodshort | | |
| PWD-02 | CAPTCHAreturn display | CheckSendCAPTCHAofResponseinwhetherinclude includeCAPTCHA | CAPTCHAnotinanyResponseinReturn | | |
| PWD-03 | CAPTCHAPredictableness | continuous continueObtainmanyCAPTCHAAnalyzescale law | CAPTCHA machine generate complete, no scale law | | |
| PWD-04 | CAPTCHAandmobile numberBinding | use A mobile numberofCAPTCHAValidate B mobile number | CAPTCHAandRequestmobile numberBinding | | |
| PWD-05 | serious set flow process skip step | skip through identity copyValidateStep, Direct CallSet New PasswordInterface | ServerValidateCompleteserious set flow process | | |
| PWD-06 | serious set Token Secure | Analyzeserious set link connect/Token ofPredictableness/Validity Period | Token onetimesness/shortValidity Period/notPredictable | | |
| PWD-07 | Passwordrepeat degreeValidate | set set weakPassword(number character/123456 etc.) | Serverstrong makePasswordrepeat degree | | |
| PWD-08 | oldPasswordInvalidate | serious setPasswordafter useuseoldPasswordLogin | oldPasswordImmediately Invalidate | | |
| PWD-09 | serious setRate Limit | short time between internal manytimesRequestSendCAPTCHA | limit makeSendfrequency rate(such as 60 between isolate) | | |
| PWD-10 | UserEnumeration | for existin/not existinofUserserious setPassword, for ratioResponseerror abnormal | system oneReturninformation, not expose exposureUserwhether exists | | |

### 7.2 transaction easyPassword Reset

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| TPW-01 | transaction easyPasswordandLoginPasswordindependent standalone ness | Checktwo typePasswordwhethercomplete all independent standalone | related independent standalone, notCanrelated same | | |
| TPW-02 | transaction easyPassword Resetneed many because Authentication | Observeserious set flow process | needLoginPassword + short information + identity copy information many seriousValidate | | |
| TPW-03 | transaction easyPassworderror lock set | continuous continue output inject error transaction easyPassword | limittimeslock set, need line under decode lock | | |
| TPW-04 | serious set after history history transaction easyPasswordInvalidate | useuseold transaction easyPasswordinitiate initiate transaction easy | oldPasswordImmediately Invalidate | | |

---

## 8. Real-Name Verificationmodel blockSecuretest

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| KYC-01 | Identity Cardinformation forgery | Submit falseIdentity Cardnumber code/Name | Callpermission DatasourceValidateName+Identity Cardnumber one cause ness | | |
| KYC-02 | Identity Cardphoto image forgery | useuse PS/AI generate completeofIdentity Cardimage image | OCR+defense check testIdentifyforgery cert item | | |
| KYC-03 | person IdentifyBypass - photo image attack attack | useuseTargetperson photo image for accurate Header | body check test reject reject photo image | | |
| KYC-04 | person IdentifyBypass - frequency attack attack | useuseTargetperson frequency release | body check test reject reject frequency return release | | |
| KYC-05 | person IdentifyBypass - 3D page tool | useuse 3D break page tool(such ascondition allow allow) | deep degree check test reject reject page tool | | |
| KYC-06 | person IdentifyBypass - inject inject attack attack | Hook related machine API, inject inject expected record make frequency flow | check test environment environmentCompleteness(Non- Header) | | |
| KYC-07 | AuthenticationResulttamper change | ModifyAuthenticationCallbackinofResultParameter | AuthenticationResultbyServerChannelConfirm, not information anyClient | | |
| KYC-08 | serious repeatAuthentication | Sameidentity copy informationBindingmanyAccount | limit make one person one accountordo risk control provide show | | |
| KYC-09 | AuthenticationInformation Disclosure | CheckAuthenticationflow processinIdentity Cardnumber/photo imageofStorageandpass output | add secret pass output/notinClienthold izeStorageclear text | | |
| KYC-10 | banklinescard four need ValidateBypass | tamper change banklinescard number/Name/Identity Card/mobile numberofany one need | four need one cause nessServerValidate | | |
| KYC-11 | Authenticationflow process skip step | skip through person IdentifyStepDirectSubmitAuthentication | ServerValidateflow processCompleteness | | |
| KYC-12 | OCR Resulttamper change | ModifyClient OCR IdentifyofIdentity Cardinformation | Serverserious new OCR orasServerResultasaccurate | | |

---

## 9. wildusebusiness logic logic test(cross model block)

### 9.1 InterfaceSecure

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| API-01 | Unauthorized Access | not with Token Direct Calleach businessInterface | Return 401, not expose exposure anyData | | |
| API-02 | InterfaceParameterinject inject | ineachParameterininject inject SQL/NoSQL/XSS/SSTI payload | Parameterize check query, output inject through filter, no inject inject | | |
| API-03 | BatchoperationInterfaceabuseuse | PassScriptBatchCallInterface | Rate Limit + linesasAnalyze + person machineValidate | | |
| API-04 | hidden hiddenInterfaceDiscover | reverse engineering App provide take notinFrontendexpose exposureof API Path | AllInterfaceaverage hasPermissionValidate | | |
| API-05 | Interfaceversion version level | will v2 Interface levelas v1(Cancan missing lessSecureValidate) | old versionInterfacealready under lineorsameetc.Securepolicy strategy | | |
| API-06 | errorInformation Disclosure | trigger initiate each type error, CheckResponseinofstack stack/SQL/Pathinformation | system one error format mode, not expose exposure internal part real current | | |
| API-07 | RequestParameter Pollution(HPP) | SameParameterpass recursive many value | Servercorrect confirm handle manage, not asset generate define | | |
| API-08 | Content-Type Bypass | ModifyRequest Content-Type(such as JSON change XML) | Serversevere formatValidate Content-Type | | |

### 9.2 business flow processSecure

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| BIZ-01 | flow processStatusmachineCompleteness | each business flow process skip step/ sequenceCall | Servermaintain protectStatusmachine, reject rejectNon-method skip transfer | | |
| BIZ-02 | Idempotencyness set plan | serious repeatSubmitSameentry transaction easy | SameRequestonly handle manage onetimes | | |
| BIZ-03 | Concurrencycondition | forBalanceoperationofConcurrencyRequest | Databaselevel level lock/principle sub operation protect cert one cause ness | | |
| BIZ-04 | negative value/boundary boundary value test | eachAmountFieldpass inject -1, 0, 0.001, MAX_INT, NaN | Serversevere formatValidate, reject rejectNon-method value | | |
| BIZ-05 | time /time between operation control | ModifyClienttime between, impact response limit time priority /lock set period | Serveruseuseself identity time between, not information anyClient | | |
| BIZ-06 | transaction easy flow horizontal numberPredictable | Analyzecontinuous continue transaction easyofflow horizontal number generate complete scale rule | flow horizontal number notPredictable/notCanTraversal | | |

### 9.3 bypass permission test matrix matrix

| ID | bypass permission type | Test Method | Expected Result | Actual Result | Risk Level |
|------|----------|----------|----------|----------|----------|
| IDOR-01 | Horizontal Authorization Bypass - Viewother personAccountinformation | Replace accountId/userId | reject reject access ask, onlyReturnself identityData | | |
| IDOR-02 | Horizontal Authorization Bypass - operation other personOrder | Replace orderId | ValidateOrderreturn attribute | | |
| IDOR-03 | Horizontal Authorization Bypass - Viewother person transaction easyRecord | Replace transactionId | ValidateRecordreturn attribute | | |
| IDOR-04 | Vertical Authorization Bypass - Regular UserCallmanage manageInterface | Call admin/internal PathInterface | Return 403 | | |
| IDOR-05 | Vertical Authorization Bypass - LowPermissionCallHighPermissionfunction can | not completeReal-Name VerificationofUserAttemptTransfer | strong make complete first set flow process | | |

---

## 10. risk controlandreverse test

| ID | Test Item | Test Method | Expected Result | Actual Result | Risk Level |
|------|--------|----------|----------|----------|----------|
| RISK-01 | abnormal Logincheck test | fromDifferent IP/ manage characters setLogin | trigger risk controlValidate(short information/person) | | |
| RISK-02 | set prepare specified pattern update change | update change set prepareorModifyset prepare specified pattern information | trigger initiate amount externalValidate | | |
| RISK-03 | large amount transaction easy risk control | initiate initiate super common scaleAmounttransaction easy | trigger initiate person tool audit audit/amount externalValidate | | |
| RISK-04 | Highfrequency transaction easy check test | short time between internal initiate initiate large quantity transaction easy | trigger initiateRate Limitor time result | | |
| RISK-05 | between transaction easy risk control | inabnormal common time (2-5 point)initiate initiate transaction easy | trigger initiate amount externalValidateorlimit make | | |
| RISK-06 | key connectAccountcheck test | manyAccountbetween frequency transfer | trigger initiate risk control scale rule | | |
| RISK-07 | model device/ machine check test | inmodel device/ machineinoperatelines App | check testtoand limit makeoramount externalValidate | | |
| RISK-08 | code manage/VPN check test | Passcode manage/VPN access ask | check testtoandRecordrisk controlLog | | |

---

## ten1. Discoverask problem remit total

### 11.1 ask problemStatistics

| Risk Level | number quantity |
|----------|------|
| Severe | |
| High Risk | |
| Medium Risk | |
| Low Risk | |
| information | |
| **combine plan** | |

### 11.2 ask problem detailed details

#### ask problem [ID]:[ask problem identifier problem]

| itemsdirectory | content |
|------|------|
| Risk Level | |
| attribute model block | |
| Test ItemID | |
| Impact Scope | |
| Reproduction Steps | |
| Request/Responseintercept image | |
| risk description | |
| Remediation Recommendation | |
| fix repeatPriority | |
| fix repeatValidateStatus | not fix repeat / already fix repeat pendingValidate / alreadyValidatePass |

(by model template one by one list outAllDiscoverofask problem)

---

## ten2. testToolclear single

| Tool | version version | Purpose |
|------|------|------|
| Burp Suite Professional | | flow quantityIntercept/tamper change/Replay |
| mitmproxy | | flow quantityAnalyze/self dynamic izeScript |
| Frida | | dynamic state Hook/BypassClientcheck test |
| Objection | | operatelinestimeAnalyze/SSL Pinning Bypass |
| jadx | | Android APK reverse engineering |
| apktool | | APK decode include/serious break include |
| adb | | Android debugging |
| ipatool / Clutch | | iOS Application |
| class-dump / Hopper | | iOS two advance makeAnalyze |
| sqlitebrowser | | version DatabaseAnalyze |
| Python / requests | | self dynamic ize testScript |
| testssl.sh / sslyze | | TLS ConfigurationScan |
| nmap | | Port/serviceDiscover |

---

## ten3. Remediation RecommendationPrioritymatrix matrix

| Priority | fix repeat time limit | forshouldrisk | Description |
|--------|----------|----------|------|
| P0 | 24 hoursinternal | Severe | directly usableforge complete resource funds loss loss, standalone that is fix repeat |
| P1 | 3 tool operation day | High Risk | audit coreAuthentication/AuthorizationBypass, fast fix repeat |
| P2 | 2 cycle internal | Medium Risk | Information Disclosure/Non-audit core logic logic missing flaw |
| P3 | under version version | Low Risk/information | SecureHardeningcreate protocol |

---

## ten4. SecureHardeningcreate protocol(wilduse)

### 14.1 Server

1. **output injectValidate**:AllBusiness Parameter(Amount/Account/product ID etc.)mustinServersevere formatValidate, not information anyClientany output inject
2. **Idempotencyset plan**:Allresource funds operationInterfacemustreal currentIdempotencyness, defense stopReplayforge complete serious repeat deduct payment/out payment
3. **Concurrencycontrol make**:resource funds operation useuseDatabaselineslock/optimistic lock/Distributed Lock, defense stop condition
4. **Statusmachine**:manyStepbusiness flow process maintain protectServerStatusmachine, reject reject skip step/ sequence operation
5. **PermissionValidate**:EachInterfaceindependent standaloneValidateUseridentity copyandresource source return attribute, not depend relyFrontendcontrol make
6. **Rate Limit**:forCAPTCHASend/LoginAttempt/transaction easy operation real part layerRate Limit
7. **Logaudit plan**:RecordAllsensitive sensitive operationofCompleteaudit planLog, include IP/set prepare/time between/operation detailed details

### 14.2 Client

1. **Codeprotect protect**:audit core logic logic useuse C/C++ compile write(SO/dylib), and do add andCompletenessValidate
2. **environment environment check test**:manyDimensioncheck test Root/bypass /model device/debugging device/Hook framework architecture
3. **SecureStorage**:Keyand Token useuse Android Keystore / iOS Keychain Storage
4. **wild informationSecure**:real cert certificate lock set(Certificate Pinning), useuseRequestSignature
5. **boundary page protect protect**:transaction easy page disable stop intercept, backend console switch change display

### 14.3 risk control body system

1. **set prepare specified pattern**:create standalone set prepare specified pattern body system, Identifyabnormal common set prepare/environment environment
2. **linesasAnalyze**:based onUserlinesasbase lineIdentifyabnormal common operation(time between/frequency rate/Amount/ manage characters set)
3. **part levelValidate**:root accordingRisk Leveldynamic state debug integerValidatestrong degree(short information->person ->person tool)
4. **real time monitor control**:large amount transaction easy/Highfrequency operation/abnormal Loginreal time report alert

---

## ten5. combine scale nessCheck

| ID | Check Item | for identifier scale scope | Result | Notes |
|------|--------|----------|------|------|
| CMP-01 | personFinancialinformation protect protect | JR/T 0171-2020"personFinancialinformation protect protect technique scale scope" | | |
| CMP-02 | move dynamicFinancialSecure | JR/T 0092-2019"move dynamicFinancialClientApplication itemSecuremanage manage scale scope" | | |
| CMP-03 | network above banklinesSecure | bank monitor initiate[2011]22number"electronic sub banklinesSecureassess assess specified cite" | | |
| CMP-04 | DataSecure | GB/T 35273-2020"Personal InformationSecurescale scope" | | |
| CMP-05 | PasswordApplication | GM/T 0028-2014"Passwordmodel blockSecuretechnique need require" | | |
| CMP-06 | App Secure | tool information part"App Personal Informationprotect protect manage manage linesscale set" | | |
| CMP-07 | reverse | "in person totalandnational reverse method"client account identity copyIdentifyneed require | | |

---

## Appendix A:Test CaseExecuteRecordtable

| usecasesID | model block | Test Item | Executeperson | Executeday period | Pass/Failure | Notes |
|----------|------|--------|--------|----------|-----------|------|
| | | | | | | |

## Appendix B:repeat testRecordtable

| ask problemID | ask problem identifier problem | principle initialetc.level | fix repeat method plan | repeat test day period | repeat testResult | repeat test person |
|----------|----------|----------|----------|----------|----------|--------|
| | | | | | | |

## Appendix C:Test Environmentinformation

| itemsdirectory | detailed details |
|------|------|
| test mobile machine type number(Android) | |
| Android version version | |
| test mobile machine type number(iOS) | |
| iOS version version | |
| App version version number | |
| testServerenvironment environment | generate asset / expected initiate deploy / test |
| Networkenvironment environment | |
| code manageToolinvolvingConfiguration | |

---

*report compile write complete day period:*
*audit audit person character:*
*itemsdirectory negative person character:*
