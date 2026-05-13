# social transactionPlatformPassword Resetfunction can - allAttack VectorandTest Plan

> Methodcomment base foundation:WooYun Business Logic Vulnerability Methodology(22,132 real realCase)
> Domain:identity copyAuthentication - Password Reset(777 Case, 88.0% High Risk, WooYun allDatacollectinSevereness rank nameNo. one)

---

## 1. business flow process map map

### 1.1 Password ResetthreeChannelStatusmachine

```
UserRequestserious set
 +- ChannelA:mobile machineSMS Verification Code
 | -> output injectmobile number -> SendCAPTCHA -> output injectCAPTCHA -> ValidatePass -> Set New Password -> complete
 |
 +- ChannelB:Emaillink connect serious set
 | -> output injectEmail -> Sendserious set link connect -> point attack link connect -> Validatecommand card -> Set New Password -> complete
 |
 +- ChannelC:Secureask problem serious set
 -> output injectAccount -> showSecureask problem -> return ask problem -> ValidatePass -> Set New Password -> complete
```

### 1.2 keyTrust Boundary

| boundary boundary | risk point |
|------|--------|
| Client vs Server | Validatelogic logicwhetheronlyinFrontend?ResponsewhetherCantamper change? |
| UserA vs UserB | serious set flow processinofidentity copy identifier identifywhetherandValidateCredentialBinding? |
| StepbetweenStatus | eachStepbetweenwhether existsServerStatusValidate?whether canskip step? |
| Channelbetween isolation | three type serious set method mode betweenwhethersharedStatus?whether canmixuse? |

---

## 2. Attack Vectorall scene image

based on WooYun 777 Password ResetCaseprovide ofAttack Patternmatrix matrix, by three serious setChannelone by one open.

---

### ChannelA:mobile machineSMS Verification Codeserious set

#### A1 - CAPTCHABrute Force

**WooYun mode:** SMS Verification Codeno rate rate limit make(CAPTCHA Bypasssub domain, 384 CaseinHighfrequency out current)

**Attack Principle:** 4-6 characters number characterCAPTCHA, totalEmptybetween only 10,000-1,000,000. no rate rate limit makeorlock set machine make, CaninnumberminutesinternalExhaustive Guessing.

**Test Steps:**
1. asself ownofmobile numberRequestoneCAPTCHA
2. useuse Burp Intruder forCAPTCHAValidateInterfaceinitiate initiateBrute Force:
 - 4 charactersCAPTCHA:Payload Scope `0000-9999`
 - 6 charactersCAPTCHA:Payload Scope `000000-999999`
3. ObserveServerResponse:
 - whether existsrate rate limit make?(Observewhetherout current 429/403 Statuscode)
 - manytimeserror afterAccount/IP whetherbe lock set?
 - CAPTCHAwhetherin N timeserror afterInvalidate?
4. no limit make -> forTargetAccountmobile numberRequestCAPTCHAafterDirectBrute Force

**WooYun Case References:**
- card cart network some serious needSystemset plan logic logic missing flawSuccessBypassCAPTCHAlimit make - Brute Force mobile
- networkfromCAPTCHA BypassagaintoArbitrary DataExport

---

#### A2 - CAPTCHAserioususe/not expired

**WooYun mode:** SMS Verification Codeno expired machine make(CAPTCHA Bypassmatrix matrix)

**Attack Principle:** CAPTCHASendafter, oldCAPTCHAnotInvalidate;orCAPTCHAValidity PeriodToo Long(>30minutes), to attack attack person topup ofBrute Forcewindow interface.

**Test Steps:**
1. asself ownAccountRequestCAPTCHA, Recordas Code1
2. againtimesRequestCAPTCHA, Recordas Code2
3. useuse Code1(oldCAPTCHA)SubmitValidate -> whetherstill Valid?
4. etc.pending 5 minutes/15 minutes/30 minutesafter part leveluse Code2 Submit -> confirm set expired time between
5. such asif oldCAPTCHAnotInvalidate -> attack attack personCanasinArbitraryTime Windowinternal useuseintercept ofCAPTCHA

---

#### A3 - CAPTCHAcrossUsershared

**WooYun mode:** CAPTCHAserioususe - inDifferentUserbetween useuserelated sameofSMS Verification Code(WooYun Prevalence:Medium)

**Attack Principle:** CAPTCHANot Boundtospecial setmobile number/UserSession, attack attack personuseself ownmobile numberObtainCAPTCHAafter, willotheruseforTargetUserofserious set flow process.

**Test Steps:**
1. accurate prepareAccount A(attack attack person)andAccount B(Target)
2. asAccount A ofmobile numberRequestserious setCAPTCHA, Recordas CodeA
3. asAccount B ofmobile numberRequestserious setCAPTCHA
4. inAccount B ofValidateStepinSubmit CodeA -> whetherValidatePass?
5. variant test:inValidateRequestinwillmobile numberfrom B Replaceas A, but protect hold otherSessionParameternot change

---

#### A4 - mobile numberParametertamper change(UserIDoperation manipulate)

**WooYun mode:** User ID operation manipulate - inserious setRequestinupdate change user_id/email/phone(WooYun Prevalence:Critical)

**Attack Principle:** ValidateStepPassafter, Set New PasswordtimeServerdepend relyClientpass comeofmobile number/UserID, whileNon-ServerSessioninBindingofidentity copy identifier identify.

**Test Steps:**
1. useattack attack personmobile number completeCAPTCHAValidateStep
2. inmost after"Set New Password"ofRequestin, Interceptflow quantity(Burp Suite)
3. willRequestinofmobile number/user_id/account ParameterReplaceasTargetUserofidentifier identify
4. SubmitRequest -> ObserveTargetUserofPasswordwhetherbeModify
5. serious point key injectofParametername:`phone`, `mobile`, `user_id`, `uid`, `account`, `username`, `cellphone`

**WooYun Case References:**
- TCLsystem one identity copyAuthenticationPlatformvulnerability, AllUserAccountPasswordCanserious set - PassReplaceUseridentifier identify real currentArbitrary Accountserious set
- FMcompany PlatformArbitrary User Password Reset

---

#### A5 - SMS Verification CodeinResponseinDisclosure

**WooYun mode:** command cardin URL/ResponseinDisclosure(WooYun Prevalence:Critical)

**Attack Principle:** open initiate personasdone debugging method, willCAPTCHADirectReturnin HTTP Response Body/ResponseHeaderor Cookie in.

**Test Steps:**
1. RequestSendSMS Verification Code, InterceptCompleteof HTTP Response
2. CheckResponse Body JSON inwhetherinclude includeCAPTCHAField(such as `code`, `smsCode`, `verifyCode`, `captcha`)
3. CheckResponseHeaderinofself set defineHeader(such as `X-Verify-Code`, `X-SMS-Code`)
4. Check Set-Cookie inwhetherinclude includeCAPTCHA
5. CheckFrontend JavaScript source codeinwhether hasCAPTCHAlogic logicDisclosure
6. such asif is APP -> CheckReturnof JSON Completeresult structure(APP common ratio Web manyReturnField)

---

#### A6 - SMS Verification CodePredictable

**WooYun mode:** Predictablecommand card(WooYun Prevalence:High)

**Test Steps:**
1. continuous continueasSamemobile numberRequest 10+ timesCAPTCHA
2. AnalyzeCAPTCHAmode:
 - whether is order sequence recursive increase?
 - whetherbased on timestamp?
 - whether hasFixedprefix/after?
 - valueAnalyze:whether existsPredictableofgenerate complete algorithm method?
3. such asifPredictable -> directly usableComputeoutTargetUserofCAPTCHA

---

#### A7 - SMS Bombing / CAPTCHASendnoRate Limit

**Attack Principle:** CAPTCHASendInterfacenoRate Limit, Canbe abuseuseadvancelinesSMS Bombing, orasBrute Forcecreate forge large quantityValidCAPTCHA.

**Test Steps:**
1. forSendCAPTCHAInterfacecontinuous continueRequest 10 times, Observewhether hasRate Limit
2. testBypassmethod mode:
 - AddEmptyformat/prefix:`+8613800138000` vs `13800138000` vs ` 13800138000`
 - Addnational actual number variant:`0086-138...`, `86138...`
 - Modify `X-Forwarded-For` HeaderBypass IP limit make
3. assess assesswhetherCanexploituse vulnerabilityasBrute Forcemake forge manyValidCAPTCHAwindow interface

---

### ChannelB:Emaillink connect serious set

#### B1 - serious set command cardinResponseinDisclosure

**WooYun mode:** command cardin URL/ResponseinDisclosure(WooYun Prevalence:Critical)

**Test Steps:**
1. RequestEmailserious set, Intercept HTTP Response
2. CheckResponse BodyinwhetherDirectinclude include serious set link connectorcommand card
3. CheckResponseHeaderinwhether hasDisclosure(`Location`, `X-Reset-Token` etc.self set defineHeader)
4. Checkpage source codeinhidden hiddenof `<input type="hidden">` whetherinclude include command card
5. such asif command cardinResponsein -> no need toaccess askEmailthat isdirectly usableserious setArbitraryUserPassword

---

#### B2 - serious set command cardPredictable/Low

**WooYun mode:** Predictablecommand card(WooYun Prevalence:High)

**Attack Principle:** command card based onPredictableofbecause sub generate complete(timestamp/UserID/MD5(email)/order sequence number characteretc.).

**Test Steps:**
1. asSameEmailcontinuous continueRequest 5 timesserious set, collect collect 5 command card
2. asDifferentEmaileachRequest 1 timesserious set, collect collect N command card
3. Analyzecommand card result structure:
 - long degreewhetherone cause?character symbol collect is?
 - whether is Base64 Encoding?decode code afterwhetherCanread?
 - whetherinclude include timestamp complete part?(for ratioRequesttime betweenandcommand card value)
 - whether is MD5/SHA1(email + salt)?(Attemptalready notify information array combine)
 - continuous continue command card betweenoferror valuewhetherFixed?
4. common seen weak command card mode:
 - `MD5(email)` -> directly usableCompute
 - `Base64(user_id + timestamp)` -> Predictable
 - `sequential_number` -> CanTraversal
 - `timestamp` -> precision confirmtoCanBrute Force
5. such asifPredictable -> asTargetEmailgenerate complete forshouldcommand cardDirectserious set

---

#### B3 - serious set command card not expired / Canserioususe

**Test Steps:**
1. Requestserious set link connect, Recordcommand cardas Token1
2. useuse Token1 Successserious setPassword
3. againtimesuseuse Token1 -> whetherstillCanserious set?(singletimesuseuseCheck)
4. Requestnew command card Token2, not useuse, etc.pending 1 hours/24 hoursafter useuse -> whetherexpired?
5. Request Token2 after againRequest Token3 -> Token2 whetherInvalidate?(new command cardwhetheroperation old command card)

---

#### B4 - Host Headerinject inject take command card

**WooYun mode:** Host Headerinject inject - in Host Headerininject inject attack attack person domain asObtainserious set link connect(WooYun Prevalence:Medium)

**Attack Principle:** Applicationroot according HTTP Host Headergenerate complete serious set link connect.attack attack person tamper change Host Headerasself own control makeofDomain Name, affected person collecttoofserious set link connect specified toward attack attack personServer, point attack after command card be take.

**Test Steps:**
1. RequestPassword Reset, InterceptRequest
2. will Host HeaderModifyasattack attack person control makeofDomain Name:`Host: evil.com`
3. CheckTargetEmailcollecttoofserious set link connect -> Domain Namewhetherchangeas `evil.com`?
4. variant test:
 - `Host: evil.com` - DirectReplace
 - `X-Forwarded-Host: evil.com` - transfer initiateHeaderinject inject
 - `Host: target.com\r\nHost: evil.com` - dual Host Header
 - `Host: target.com@evil.com` - @ symbol number mix
 - `Host: target.com.evil.com` - sub domain mix
5. such asif link connect be tamper change -> affected person point attack after command card beSendtoattack attack personServer

---

#### B5 - Referer Disclosurecommand card

**Test Steps:**
1. useuseserious set link connect access askSet New Passwordpage
2. inthis page above point attack any external part link connect(social transaction body image identifier/help link connectetc.)
3. Checkexternal partRequestof Referer Header -> whetherinclude includeCompleteofserious set command card URL
4. such asif page add external part resource source(JS/CSS/image image CDN) -> Checkthis someRequestof Referer
5. such asifDisclosure -> No. three methodCanPass Referer Obtainserious set command card

---

#### B6 - EmailParametertamper change

**WooYun mode:** User ID operation manipulate(WooYun Prevalence:Critical)

**Test Steps:**
1. Requestserious set timeInterceptRequest, testthe followingParametertamper change:
 - Replace `email` asTargetEmailbut protect holdSessionnot change
 - AddNo. twoEmailParameter:`email=victim@x.com&email=attacker@x.com`
 - useusenumber array:`email[]=victim@x.com&email[]=attacker@x.com`
 - useuse JSON:`{"email":"victim@x.com","cc":"attacker@x.com"}`
 - number part isolate:`email=victim@x.com,attacker@x.com`
 - useusepart number:`email=victim@x.com;attacker@x.com`
2. Observeserious set itemSendtowhichEmail -> whetherCanaswillcommand cardSendtoattack attack personEmail
3. inSet New PasswordStepin, ReplaceEmail/user_id asTargetAccount

**WooYun Case References:**
- M1905electronic impact network some serious need pointArbitraryPassword Reset(already inject methodAccount) - PassParameteroperation manipulate serious set methodAccountPassword

---

#### B7 - command cardandUserBindingCheck

**Test Steps:**
1. asAccount A Requestserious set command card TokenA
2. asAccount B Requestserious set command card TokenB
3. useuse TokenA butinRequestinspecified setAccount B ofidentifier identify -> whetherCanas serious set B ofPassword?
4. this test command cardwhetherandspecial setUsersevere formatBinding

---

### ChannelC:Secureask problem serious set

#### C1 - Secureask problemAnswerBrute Force

**Test Steps:**
1. ConfirmSecureask problem type(generate day/ / / item nameetc.)
2. assess assessAnswerEmptybetween:
 - "ofgenerate day is?"-> only constraint 36,500 typeCancan(100 x 365days)
 - "of?"-> innational primary need not super through 300
 - "of?"-> innational common seen constraint 100
3. useuse Burp Intruder forAnswerFieldinitiate initiateDictionaryattack attack
4. Checkwhether exists:
 - return timesnumber limit make?
 - error after lock set machine make?
 - CAPTCHAprotect protect?
 - Responsetime between error abnormal(correct confirmAnswer vs errorAnsweroftime sequence error abnormal)

---

#### C2 - Secureask problemAnswerinFrontendDisclosure

**Test Steps:**
1. advance injectSecureask problemValidatepage, ViewCompleteof HTTP Response
2. Check HTML source codeinhidden hiddenField:`<input type="hidden" name="answer" value="xxx">`
3. Check JavaScript change quantityinwhetherinclude includeAnswer
4. Check API Response JSON inwhetherReturndoneAnswer(special level isMobile Client API)
5. CheckBrowseropen initiate personTool Network page templateinother XHR RequestwhetherDisclosureAnswer

---

#### C3 - Secureask problemCanEnumeration

**Test Steps:**
1. output injectTargetUsername, ObserveReturnofSecureask problem
2. TraversalDifferentUsername -> whetherCanasEnumerationPlatformUser?(Username existinandofResponseerror abnormal)
3. CheckSecureask problemwhetherthrough for simple singleorAnswerEmptybetween through small
4. social transactionPlatformspecial risk:Secureask problemofAnswerCancaninUsercompany open resource in(generate day/ / etc.)

---

#### C4 - Secureask problemValidateBypass

**WooYun mode:** Stepskip through - Directskipto"Set New Password"Step(WooYun Prevalence:High)

**Test Steps:**
1. correct common toSecureask problem page, RecordStepof URL andParameter
2. not return ask problem, Directstructure forge"Set New Password"StepofRequestSend
3. testinRequestinDelete `answer` Parameter -> whetherstillCanPassValidate?
4. testSubmitEmptyAnswer `answer=` -> whetherPass?
5. testSubmit `answer=true` or `answer=1` -> whether haslogic logic determine judge error?

---

#### C5 - Secureask problemAnswerParametertamper change

**Test Steps:**
1. InterceptSecureask problemValidateRequest
2. Modifyhidden hiddenParameter(such as `question_id`)-> whetherCanas switch changetoupdate content easy guessingofask problem?
3. Addamount externalParameter `verified=true`, `skip=1`, `bypass=1` -> whetherbeBackendconnect affected?
4. ModifyResponseinofValidateResult(such as `{"correct":false}` -> `{"correct":true}`)-> Frontendwhetheraccording releaselines?

---

### crossChannelAttack Vector

#### D1 - Stepskip through(allChannelwilduse)

**WooYun mode:** Stepskip through - Directskipto"Set New Password"Step(WooYun Prevalence:High)

**Attack Principle:** Password Resetflow processofeachStepbetween missing ServerStatusValidate, attack attack persondirectly usableaccess ask most after one step.

**Test Steps:**
1. correct common complete onetimesCompleteofPassword Resetflow process, use Burp RecordEachStepofRequest
2. Identifymost after one step"Set New Password"ofRequest(URL/Parameter/Method)
3. innewSessionin, notExecutefirst pageofValidateStep, DirectSendmost after one stepofRequest
4. variant:
 - only skip throughValidateStep(protect retainNo. one stepofidentity copy output inject)
 - complete allfromzero open initialDirectSendset setPasswordRequest
 - inRequestinmobile dynamicAdd `step=3` or `verified=true` etc.Parameter
5. CheckServerwhetherinEachStepallValidatefirst setStepofcompleteStatus

**WooYun Case References:**
- under percent Password Resetvulnerability involving279network above networkUserData - Passskip step serious setArbitraryUserPassword

---

#### D2 - Responsetamper change(allChannelwilduse)

**WooYun mode:** Responseoperation manipulate - will `{"success":false}` changeas `{"success":true}`(WooYun Prevalence:Medium)

**Attack Principle:** Frontendroot accordingServerReturnofStatuscode/JSON Field setwhetheradvance inject under one step, but under one step not again byServerValidate.

**Test Steps:**
1. inValidateStepin meaning output inject errorofCAPTCHA/Answer
2. InterceptServerResponse(Burp -> Intercept Response)
3. ModifyResponsecontent:
 - `{"success":false}` -> `{"success":true}`
 - `{"code":1001}` -> `{"code":0}`
 - `{"status":"error"}` -> `{"status":"ok"}`
 - HTTP Statuscode `403` -> `200`
4. ObserveFrontendwhetheraccording advance injectSet New Passwordpage
5. inSet New PasswordpageSubmitnewPassword -> Serverwhetherconnect affected?

---

#### D3 - Channelmixuseattack attack

**Attack Principle:** exploituseoneChannelofValidateStatus, crossto oneChannelExecutePasswordModify.

**Test Steps:**
1. inChannel A(SMS Verification Code)incomplete identity copyValidate
2. inSet New PasswordStepin, ReplaceRequestcome source identifier identifyasChannel B or C ofParameterformat mode
3. test:useChannel A ObtainofSessionStatus/token, Direct CallChannel B ofset setPasswordInterface
4. CheckthreeChannelofset setPasswordInterfacewhether isSame -> such asif is, ValidateStatuswhetherChannelisolation?

---

#### D4 - Useridentifier identify symbol operation manipulate(allChannelwilduse)

**WooYun mode:** User ID operation manipulate(WooYun allDatacollectinPrevalence:Critical, this isPassword Resetvulnerability most common seenofroot because)

**Test Steps:**
1. Complete one self ownAccountofserious set flow process, RecordAllRequestinofidentity copy identifier identifyParameter
2. inflow processofEachStepinAttemptReplaceidentifier identify:
 - No. one step(output injectAccount):output injectTargetAccount
 - No. two step(Validate):useself ownofCAPTCHAbutReplacekey connectof user_id
 - No. three step(set setPassword):Replace user_id/phone/email asTargetAccount
3. special level inject meaning hidden hiddenParameterand Cookie inofidentity copy identifier identify
4. CheckEachRequestinwhether hasmany identity copy identifier identifyParameter(such assame time has `user_id` and `phone`)-> which priority first?Can not one cause?

---

#### D5 - Race Condition

**Attack Principle:** inCAPTCHAValidatePassofinstant same timeSendmany set setPasswordRequest, orincommand cardInvalidatefirstofwindow interface periodConcurrencyexploituse.

**Test Steps:**
1. ObtainValidCAPTCHA/command card
2. accurate prepare 10-50 Concurrencyofset setPasswordRequest(useuse Burp Turbo Intruder orself set defineScript)
3. same timeSendAllRequest -> Observe:
 - whethermanyRequestallSuccess?
 - command card/CAPTCHAwhetherbe manytimesuseuse?
4. Applicationscenario scene:Bypass"CAPTCHAsingletimesuseuse"limit make

---

#### D6 - Password Resetlink connect/CAPTCHAofInformation Disclosurechannel channel

**Test Steps:**
1. CheckBrowserhistory historyRecord -> serious set link connectwhetherprotect existinhistory historyin?
2. Check Web Serveraccess askLog -> serious set command cardwhetherRecordinLogin?
3. Check existHeader -> serious set pagewhetherset set done `Cache-Control: no-store`?
4. Check itemwhether isclear text pass output(Non- TLS)
5. Check Referer Headerwhetherinpage skip transfer timeDisclosurecommand card(seen B5)

---

#### D7 - AccountEnumeration

**Test Steps:**
1. inPassword ResetNo. one stepinpart level output inject:
 - existinofmobile number/Email/Username
 - not existinofmobile number/Email/Username
2. for ratioResponseerror abnormal:
 - ResponsetextDifferent?("CAPTCHAalreadySend" vs "thismobile numbernotRegistration")
 - Responsetime betweenDifferent?(check library vs DirectReturn)
 - HTTP StatuscodeDifferent?
 - Responselong degreeDifferent?
3. social transactionPlatformrisk release large:AccountEnumeration + company open resource -> CanBatchConfirmreal realUseridentity copy

---

#### D8 - newPasswordset set missing flaw

**Test Steps:**
1. inSet New PasswordStepintest:
 - whetherCanas set setandoldPasswordrelated sameofPassword?
 - whetherCanas set setBlank Password?
 - whetherCanas set set extreme weakPassword(such as `123456`)?
 - Passwordlong degree limit makewhetheronlyinFrontend?(Delete `maxlength` attributes afterSubmitsuper longPassword)
2. serious set afterCheck:
 - other set prepare aboveofSessionwhetherbe inject?(such asif not inject -> attack attack person alreadyLoginofSessionstill Valid)
 - whetherwild notifyUserPasswordalready beModify?(wild notifyMissing -> Userno method be attack attack)

---

## 3. Test Environmentaccurate prepare

### 3.1 must prepareTool

| Tool | Purpose |
|------|------|
| Burp Suite Professional | HTTP Intercept/ModifyRequest/Response/Intruder Brute Force/Turbo Intruder Race |
| Browseropen initiate personTool | FrontendCodeaudit plan/NetworkRequestAnalyze/Cookie/localStorage Check |
| mobile machine packet capture(Charles/mitmproxy) | Mobile Client APP flow quantityIntercept(APP commonReturnupdate manyData) |
| curl / Python requests | self dynamic izeValidateandrepeat current |

### 3.2 Test Accountaccurate prepare

| Account | Purpose |
|------|------|
| Account A(attack attack person) | Bindingattack attack personmobile numberandEmail, useforObtainCAPTCHA/command card |
| Account B(Target) | BindingDifferentmobile numberandEmail, useforValidatecrossUserattack attack |
| Account C(Observeperson) | useforValidatePasswordwhetherrealofbeModify(Logintest) |

---

## 4. Test Priority Ranking

based on WooYun DataStatisticsofPrevalenceandimpact response degree, byPriorityrank sequence:

| Priority | Attack Vector | WooYun Prevalence | impact response |
|--------|---------|--------------|------|
| P0-Critical | D4 Useridentifier identify symbol operation manipulate | Critical | Arbitrary User Password Reset |
| P0-Critical | A4 mobile numberParametertamper change | Critical | Arbitrary User Password Reset |
| P0-Critical | B6 EmailParametertamper change | Critical | Arbitrary User Password Reset |
| P0-Critical | A5/B1 CAPTCHA/command cardinResponseinDisclosure | Critical | Arbitrary User Password Reset |
| P1-High | D1 Stepskip through | High | BypassValidateDirectserious set |
| P1-High | B2 command cardPredictable | High | Arbitrary User Password Reset |
| P1-High | A1 CAPTCHABrute Force | High | Arbitrary User Password Reset |
| P1-High | B7 command cardandUserNot Bound | High | crossUsercommand card exploituse |
| P2-in | D2 Responsetamper change | Medium | BypassFrontendValidate |
| P2-in | A3 CAPTCHAcrossUsershared | Medium | crossUserCAPTCHAexploituse |
| P2-in | B4 Host Headerinject inject | Medium | take serious set command card |
| P2-in | C1 Secureask problemBrute Force | Medium | guessingAnswerserious setPassword |
| P2-in | C4 Secureask problemValidateBypass | Medium | skip through ask environment section |
| P3-Low | A2 CAPTCHAnot expired | Low-in | large attack attack window interface |
| P3-Low | B3 command card not expired/Canserioususe | Low-in | hold continue exploituse |
| P3-Low | B5 Referer Disclosurecommand card | Low | No. three method take |
| P3-Low | D5 Race Condition | Low | Bypasssingletimesuseuselimit make |
| P3-Low | D7 AccountEnumeration | Low | information collect collect/hidden private |

---

## 5. WooYun StatisticsDatatotal result

| Dimension | Data |
|------|------|
| Password Resetvulnerability totalCase Count | 777 |
| high-risk percentage | 88.0%(WooYun allDatacollectinrank nameNo. one) |
| identity copyAuthentication DomaintotalCase | 8,846(shareAllvulnerabilityof 40%) |
| CAPTCHA BypassCase | 384(44% High Risk) |
| most common seen root because | Useridentifier identify symbol operation manipulate(inserious setRequestinReplace user_id/phone/email) |
| No. two common seen root because | command card/CAPTCHAin HTTP ResponseinDisclosure |
| No. three common seen root because | flow processStepskip through(missing ServerStatusValidate) |

**key result comment:** Password Resetis WooYun allDatacollectinhigh-risk percentagemostHighofVulnerability Category(88.0%).social transactionPlatformbecauseUserbase number large/Accountprice valueHigh, Password ResetvulnerabilityofBusiness ImpactasSevere - oneCanexploituseofPassword Resetmissing flaw meaning PlatformaboveAllUserofAccountallCancan be connect manage.

---

## 6. supplement create protocol(by defense defense layertimes)

### Codelayer
- serious set command card:PasswordSecure machine number, long degree >= 32 character section, singletimesuseuse, 15 minutesexpired
- SMS Verification Code:6 characters number character, 5 minutesexpired, Bindingmobile number + Session, error 5 timesoperation
- Secureask problem: method mode(AnswerEmptybetween through small, social transactionPlatformaboveAnswereasyObtain), changeuse MFA
- AllStepofidentity copy identifier identifymustfromServerSessionRead, disable stop connect affectedClientpass injectof user_id/phone/email

### architecture structure layer
- EachStepmustbyServerValidatefirst setStepofcompleteStatus(Statusmachine mode)
- rate rate limit make:CAPTCHAValidateInterfacebyAccount + IP dualDimensionlimit make(5 times/15 minutes)
- serious set complete after strong make inject AllotherSession
- serious set complete after towardAllalreadyBindingofwild notify channel channelSendreport alert

### monitor control layer
- single IP large quantityRequestserious setInterface -> report alert
- singleAccountshort time between internal manytimestrigger initiate serious set -> report alert
- CAPTCHAValidateFailurerate increase -> report alert
- PasswordModifyafter standalone that isfromnew IP/set prepareLogin -> report alert

---

*versionTest Planbased on WooYun Business Logic Vulnerability Methodology v2.0, Datasource:WooYun vulnerabilityDatabase(20167), 22,132 real real vulnerabilityCase.*
