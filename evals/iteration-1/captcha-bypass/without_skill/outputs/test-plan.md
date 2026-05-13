# Image CAPTCHASecureTest Plan

## 1. Test Scope

| business scenario scene | CAPTCHAtype | protect protect for |
|---------|-----------|---------|
| Loginpage | Image CAPTCHA | defenseBrute Force |
| Registrationpage | Image CAPTCHA | defenseBatchRegistration |
| SMS Verification CodeSendInterface | Image CAPTCHA | defenseSMS Bombing |

---

## 2. Test Casematrix matrix

### 2.1 CAPTCHAgenerate fatal cycle period missing flaw

#### TC-01: CAPTCHAserious repeat useuse(mostHighPriority)

**Attack Principle**: CAPTCHAinValidateSuccessafter notInvalidate, Canbe serious repeatSubmit.

**Test Steps**:
1. ObtainCAPTCHA, person toolIdentifycorrect confirmAnswer
2. SubmitLoginRequest(correct confirmCAPTCHA + errorPassword), RecordRequest
3. not New CAPTCHA, ModifyPasswordFieldafterReplayRequest
4. ObservewhetherstillReturn"Passworderror"whileNon-"CAPTCHAerror"

**Pass/Fail Criteria**: SameCAPTCHAvalueintimesValidateaftershouldImmediately Invalidate.No. twotimesSubmitmustReturnCAPTCHAerror.

**variant test**:
- ValidateSuccessafter serioususe(LoginSuccessscenario scene)
- ValidateFailureafter serioususe(LoginFailurescenario scene)
- crossInterfaceserioususe(LoginpageObtainofCAPTCHAuseforRegistrationInterface)

---

#### TC-02: CAPTCHAnot expired / TTL Too Long

**Attack Principle**: CAPTCHAlong time betweenValid, attack attack person has topup time betweenIdentifyorexpose power decode.

**Test Steps**:
1. ObtainCAPTCHAandRecordtimestamp
2. etc.pendingDifferenttime between between isolate afterSubmit(1min / 5min / 10min / 30min / 1h)
3. ObserveCAPTCHAwhetherstill Valid

**Pass/Fail Criteria**: CAPTCHAValidity Periodshould <= 5 minutes.infer 2 minutes.

---

#### TC-03: CAPTCHAandSessionBindingMissing

**Attack Principle**: CAPTCHANot Boundtospecial set Session/Token, attack attack personCanuseself ownofCAPTCHAReplaceTargetUserofCAPTCHA.

**Test Steps**:
1. Browser A break openLoginpage, ObtainCAPTCHA A and Session A
2. Browser B break openLoginpage, ObtainCAPTCHA B and Session B
3. use Session A + CAPTCHA B ofAnswerSubmitRequest
4. ObservewhetherValidatePass

**Pass/Fail Criteria**: CAPTCHAmustandgenerate complete timeof Session/Token severe formatBinding.cross Session useusemustFailure.

---

### 2.2 Validatelogic logicBypass

#### TC-04: DeleteCAPTCHAParameter

**Attack Principle**: ServerinCAPTCHAParameterMissingtime skip throughValidate.

**Test Steps**:
1. correct common packet captureObtainLogin/RegistrationRequest
2. DeleteRequestinofCAPTCHAField(such as `captcha`/`code`/`verifyCode`)
3. SendRequest, ObserveResponse

**Pass/Fail Criteria**: missing lessCAPTCHAParametertimemustreject rejectRequest, not skip throughValidate.

---

#### TC-05: CAPTCHAParametersetEmpty

**Attack Principle**: ServerforEmptyvalueValidatenot severe format.

**Test Steps**:
1. willCAPTCHAFieldset setasthe followingvalue part level test:
 - Emptycharacter symbol string `""`
 - `null`
 - `undefined`
 - `0`
 - `false`
 - Emptyformat `" "`
 - Emptynumber array `[]`

**Pass/Fail Criteria**: Allabnormal common value averageshouldReturnCAPTCHAerror.

---

#### TC-06: ten-thousand canCAPTCHA / test after

**Attack Principle**: open initiate environment environment retainoftestCAPTCHA(such as `0000`/`1234`/`9999`/`test`)notingenerate asset environment environment move remove.

**Test Steps**:
1. Attemptthe followingcommon seen after value: `0000`, `1234`, `4567`, `6666`, `8888`, `9999`, `test`, `admin`, `captcha`
2. CheckConfigurationFile/FrontendCodeinwhether hasCAPTCHAWhitelist
3. Checkwhether existsspecial Header(such as `X-Skip-Captcha: true`)Canskip throughValidate

**Pass/Fail Criteria**: should notexistinany hardEncodingofPassvalue.

---

#### TC-07: CAPTCHACase Sensitivitytest

**Attack Principle**: not part case LowBrute ForceofCharacter Space(36^n as 10+26=36 as 10+1=not change, real actual isfrom 62^n 36^n).

**Test Steps**:
1. Obtaininclude include character ofCAPTCHA
2. part levelSubmitall large write/all small write/mix combine case version version
3. Observewhich some be connect affected

**Pass/Fail Criteria**: Recordwhen first policy strategy.such asnot part case, need assess assess forSecurenessofimpact response andConfirmCharacter Spacewhether.

---

### 2.3 ClientSecure

#### TC-08: CAPTCHAAnswerClient-Side Disclosure

**Attack Principle**: CAPTCHAAnswerPass HTTP Response/Cookie/Hidden Field etc.method modeDisclosuretoClient.

**Test Steps**:
1. ObtainCAPTCHAimage image time, CheckComplete HTTP Response:
 - Response Body(JSON Fieldinwhetherinclude includeAnswer)
 - Response Headers(such as `X-Captcha-Code`/`X-Verify-Code` etc.self set define Header)
 - Set-Cookie(Cookie valueinwhetherinclude includeCAPTCHAclear textorCanEncoding)
2. Check HTML source codein hidden input whetherinclude includeAnswer
3. Check JavaScript change quantity/localStorage/sessionStorage
4. CheckCAPTCHAimage imageofFilename/URL whetherinclude includeAnswer(such as `/captcha?code=a3Xk`)

**Pass/Fail Criteria**: CAPTCHAAnswershould notas any mode pass outputtoClient.

---

#### TC-09: CAPTCHAFrontend Validation

**Attack Principle**: CAPTCHAonlyinFrontend JavaScript Validate, ServernotValidate.

**Test Steps**:
1. useuseBrowseropen initiate personTooldisableuse JavaScript
2. Directstructure forge HTTP Request(without going throughFrontendtable single)SubmittoBackendInterface
3. useuse Burp Suite / packet captureToolBypassFrontendDirectSendRequest

**Pass/Fail Criteria**: Servermustindependent standaloneValidateCAPTCHA, not depend relyFrontend.

---

#### TC-10: CAPTCHAimage imagePredictable

**Attack Principle**: CAPTCHAgenerate complete algorithm method useusePredictableof machine type suborFixedsequence list.

**Test Steps**:
1. continuous continueRequest 100 itemsCAPTCHAimage image
2. Analyzewhether existsserious repeat mode
3. Checkwhether existsFixedofCAPTCHA(such asonly has 100 itemsimage follow environment useuse)
4. CheckCAPTCHA URL inofParameterwhetherPredictable(such asrecursive increase ID)

**Pass/Fail Criteria**: CAPTCHAshoulduseusePasswordSecureof machine number generate complete device, not existinPredictablemode.

---

### 2.4 Brute Forcedefense protect

#### TC-11: CAPTCHACharacter SpaceInsufficient

**Attack Principle**: number character 4 charactersCAPTCHAonly has 10^4 = 10000 typeCancan, Caninshort time between internalExhaustive Guessing.

**Test Steps**:
1. ObserveCAPTCHAarray complete(number character/character +number character/includeSpecial Characters)
2. StatisticsCAPTCHAlong degree
3. ComputetotalCharacter Space

**Pass/Fail Criteria**:

| array combine method mode | characters number | Emptybetween large small | Secureassess price |
|---------|------|---------|---------|
| number character | 4 | 10,000 | extremeInsecure |
| number character | 6 | 1,000,000 | strong |
| character +number character | 4 | 1,679,616 | one |
| character +number character | 6 | 2,176,782,336 | Secure |

infer: character +number character mix combine, at least 4 characters, config combineRate Limit.

---

#### TC-12: noRate Limit / limit makeInsufficient

**Attack Principle**: InterfacenoRequestRate Limit, allow allowHighrate expose power decodeCAPTCHA.

**Test Steps**:
1. useScriptforLoginInterfaceeach Send 10/50/100 timesRequest(eachtimesuseuseDifferentCAPTCHAvalue)
2. Observewhethertrigger initiateRate Limiting(HTTP 429 / disable / Response)
3. test forCAPTCHAObtainInterfaceofRate Limit(short time between large quantityRequestNew CAPTCHA)
4. testRate LimitingDimension:
 - by IP Rate Limiting
 - byAccountRate Limiting
 - by Session Rate Limiting

**Pass/Fail Criteria**: shouldinthe followingany oneDimensionreal Rate Limit:
- single IP eachminutesRequesttimesnumber above limit
- singleAccounteachminutesAttempttimesnumber above limit
- CAPTCHAConsecutive Errors N timesafter lock set(create protocol 5 times)

---

#### TC-13: Rate LimitingBypass

**Attack Principle**: Rate LimitCanPassspecial set mobile Bypass.

**Test Steps**:
1. **IP rotate change**: useusecode manage rotate change IP, testwhetheronly by IP Rate Limiting
2. **Header forgery**: Add `X-Forwarded-For`/`X-Real-IP`/`X-Client-IP` etc. Header forgery come source IP
3. **case/Encodingvariant**: will URL Pathcase change change/URL Encoding(such as `/Login` vs `/login` vs `/%6Cogin`)
4. **Parameter Pollution**: Addno meaning defineParameterBypass exist key(such as `?_=timestamp`)
5. **protocol protocol switch change**: HTTP vs HTTPS whethersharedRate Limitingplan number device
6. **Session serious create**: clear remove Cookie Obtainnew Session whetherserious setRate Limitingplan number

**Pass/Fail Criteria**: Rate Limitingmachine makeshould notbe above description any mobile Bypass.

---

### 2.5 OCR/AI IdentifyforResistance To

#### TC-14: CAPTCHAResistance To OCR can power

**Attack Principle**: simple singleCAPTCHACanbe OCR cite or AI model typeHighaccurate confirm rateIdentify.

**Test Steps**:
1. BatchDownload 200 itemsCAPTCHAimage image
2. useusethe followingTool/service advancelinesIdentify:
 - Tesseract OCR(open source base line)
 - ddddocr(special attackCAPTCHAofopen source library)
 - Multimodal LLM(GPT-4o / Claude / Qwen-VL)
 - Third-Party CAPTCHA-Solving Platform(super level etc.)
3. StatisticseachToolofIdentifyaccurate confirm rate

**Pass/Fail Criteria**:

| Recognition Rate | Risk Level | linesdynamic create protocol |
|-------|---------|---------|
| > 80% | High Risk | mustupdate changeCAPTCHAmethod plan |
| 50-80% | Medium Risk | increase add yuanorescalate level method plan |
| 20-50% | Low Risk | Acceptable, hold continue monitor control |
| < 20% | Secure | no need tolinesdynamic |

**assess assessDimension**:
- Character Distortion Level
- Interference Lines/Noisestrong degree
- Character Adhesion Level
- Background Complexity
- Font Diversity

---

#### TC-15: CAPTCHAimage imageInformation Disclosure

**Attack Principle**: CAPTCHAimage imageyuanDataorattributesDisclosureAnswerinformation.

**Test Steps**:
1. Checkimage image EXIF yuanData
2. Checkimage image alt attributes/title attributes
3. Checkimage image base64 Encodinginwhether hasscale law(related sameAnswer = related sameEncoding = FixedImage Library)
4. userelated sameAnswerObtainmanyitemsimage image, for ratio image image hash whetherone cause(IdentifyImage Librarymode)

**Pass/Fail Criteria**: image imageshould notinclude include anyCaninferExportAnswerofyuanDataormode.

---

### 2.6 Interfacelogic logic missing flaw

#### TC-16: SMS InterfaceofCAPTCHAValidateBinding

**Attack Principle**: Image CAPTCHAValidateandSMS Sending InterfacenotAtomicBinding, CanStepwise Bypass.

**Test Steps**:
1. correct common flow process: output injectImage CAPTCHA -> CallSMS Sending Interface -> ServerValidateImage CAPTCHA -> Sendshort information
2. attack attack flow process:
 - usecorrect confirmofImage CAPTCHACallSMS Sending Interfaceonetimes(PassValidate)
 - notRefreshImage CAPTCHA, Directserious repeatCallSMS Sending Interface
 - Observewhethercan continuous continueSendshort information(BypassImage CAPTCHAlimit make)

**Pass/Fail Criteria**: eachtimesCallSMS Sending Interfaceallshouldindependent standaloneValidateImage CAPTCHA.Image CAPTCHAinsingletimesshort informationSendaftershouldImmediately Invalidate.

---

#### TC-17: CAPTCHAandBusiness ParameterDecoupling

**Attack Principle**: CAPTCHAValidatePassafter, after continue businessRequestnot again key connectCAPTCHAResult, Cantamper changeBusiness Parameter.

**Test Steps**:
1. usemobile number A + correct confirmCAPTCHASendshort information -> Success
2. intercept Request, Modifymobile numberas B, Resendrelated sameRequest(protect holdCAPTCHAnot change)
3. Observeshort informationwhetherSendtomobile number B

**Pass/Fail Criteria**: CAPTCHAValidateshouldBindingkeyBusiness Parameter(such asmobile number).Parameterchange update afterCAPTCHAshouldInvalidate.

---

#### TC-18: Concurrent Race Condition

**Attack Principle**: exploituseConcurrencyRequestinCAPTCHAInvalidatefirst manytimesuseuseSameCAPTCHA.

**Test Steps**:
1. ObtainoneValidCAPTCHA
2. same timeSend 20-50 ConcurrencyRequest, All with related sameofcorrect confirmCAPTCHA
3. StatisticsSuccessPassValidateofRequestnumber

**Pass/Fail Criteria**: SameCAPTCHAinConcurrencyscenario scene under shouldcan onlySuccessuseuseonetimes(needAtomicValidate+Invalidateoperation).

---

### 2.7 Flow Bypass

#### TC-19: Direct CallDownstream Interface

**Attack Principle**: BypassCAPTCHApage, Direct CallLogin/RegistrationofBackendInterface.

**Test Steps**:
1. AnalyzeFrontendCode, toreal actualofBackendInterfaceAddress
2. without going throughCAPTCHAObtain/ValidateStep, Directstructure forgeRequestCall:
 - LoginInterface (`/api/login`)
 - RegistrationInterface (`/api/register`)
 - SMS Sending Interface (`/api/sms/send`)
3. test not withCAPTCHArelated keyFieldtimeInterfaceofResponse

**Pass/Fail Criteria**: BackendInterfacemuststrong makeValidateCAPTCHA, no commentRequestcome source.

---

#### TC-20: Step Skipping

**Attack Principle**: manyStepflow processinskip throughCAPTCHAStep.

**Test Steps**:
1. AnalyzeRegistration/Loginwhether ismanyStepflow process(such as Step1: CAPTCHA -> Step2: fill in information -> Step3: Submit)
2. Directskipto Step2/Step3, notExecute Step1
3. CheckServerwhetherValidateStepCompleteness

**Pass/Fail Criteria**: Servershouldmaintain protectStepStatus, reject reject skip Execute.

---

### 2.8 special scenario scene

#### TC-21: CAPTCHARefreshafterOld CodeValid

**Attack Principle**: point attackRefreshObtainNew CAPTCHAafter, oldCAPTCHAstill Valid.

**Test Steps**:
1. ObtainCAPTCHA A andRecordAnswer
2. point attackRefresh, ObtainCAPTCHA B
3. useCAPTCHA A ofAnswerSubmitRequest
4. ObservewhetherValidatePass

**Pass/Fail Criteria**: New CAPTCHAtime, oldCAPTCHAmustImmediately Invalidate.

---

#### TC-22: Multiple Concurrent CAPTCHAs

**Attack Principle**: Same Session Cansame time generate complete manyValidCAPTCHA.

**Test Steps**:
1. inSame Session underConcurrencyRequest 10 CAPTCHA
2. part levelAttemptuseEachCAPTCHAofAnswerSubmit
3. Observehas many lessCAPTCHAsame timeValid

**Pass/Fail Criteria**: Same Session inSametime betweenshouldonly has most new generate completeofoneCAPTCHAValid.

---

#### TC-23: Abnormal Inputhandle manage

**Attack Principle**: Abnormal InputCausingServererrororBypassValidate.

**Test Steps**:
1. Submitsuper longCAPTCHAvalue(1000+ character symbol)
2. SubmitSpecial Characters(`<script>`, `' OR 1=1--`, `../`, `%00`)
3. SubmitNon-character symbol string type(number array `["a","b"]`/for `{"code":"1234"}`/integer number)
4. Submit Unicode character symbol(all number character/Homoglyph Attack)

**Pass/Fail Criteria**: AllAbnormal InputshouldReturnsystem oneofCAPTCHAerrorResponse, should nottrigger initiate 500 errororInformation Disclosure.

---

## 3. Test Priority Ranking

### P0 - muststandalone that is test(Bypassthat isHigh Risk)

| ID | Test Item | risk |
|-----|-------|------|
| TC-01 | CAPTCHAserious repeat useuse | complete all loss defense protect, Canno limitBrute Force |
| TC-04 | DeleteCAPTCHAParameter | complete allBypassCAPTCHA |
| TC-05 | CAPTCHAParametersetEmpty | complete allBypassCAPTCHA |
| TC-08 | AnswerClient-Side Disclosure | self dynamic izeObtainAnswer, CAPTCHA same set |
| TC-09 | Frontend Validation | BackendnotValidateetc.for no defense protect |
| TC-16 | SMS InterfaceCAPTCHABinding | BypassImage CAPTCHAreal currentSMS Bombing |
| TC-18 | Concurrent Race Condition | single code manyuse, Batchattack attack |
| TC-19 | Direct CallDownstream Interface | complete all skip throughCAPTCHAflow process |

### P1 - priority first test(inHighrisk)

| ID | Test Item | risk |
|-----|-------|------|
| TC-03 | Session BindingMissing | crossSessionReplaceCAPTCHA |
| TC-06 | ten-thousand canCAPTCHA | after DirectBypass |
| TC-12 | noRate Limit | Exhaustive GuessingCAPTCHA |
| TC-14 | Resistance To OCR can power | self dynamic izeBatchIdentify |
| TC-17 | Business ParameterDecoupling | tamper changemobile numberSendshort information |
| TC-21 | RefreshafterOld CodeValid | large attack attackTime Window |

### P2 - common scale test(inLowrisk)

| ID | Test Item | risk |
|-----|-------|------|
| TC-02 | TTL Too Long | largeIdentify/ decode window interface |
| TC-07 | Case Sensitivity | smallCharacter Space |
| TC-10 | CAPTCHAPredictable | modeIdentifyBypass |
| TC-11 | Character SpaceInsufficient | LowExhaustive Guessingcomplete version |
| TC-13 | Rate LimitingBypass | Rate LimitInvalidate |
| TC-15 | image imageInformation Disclosure | self dynamic izeIdentify |
| TC-20 | Step Skipping | Flow Bypass |
| TC-22 | Multiple Concurrent CAPTCHAs | large decode page |
| TC-23 | Abnormal Inputhandle manage | abnormal commonlinesas / Information Disclosure |

---

## 4. Test Toolchain

| Purpose | Tool |
|------|-----|
| packet capture/Replay | Burp Suite / mitmproxy |
| Concurrencytest | Burp Intruder / Turbo Intruder / self compileScript |
| OCR base line | Tesseract / ddddocr |
| AI Identify | GPT-4o / Claude Vision / Qwen-VL |
| Scriptself dynamic ize | Python requests + threading |
| Browserself dynamic ize | Playwright / browser-use |

---

## 5. Remediation Recommendations Overview

when testDiscoverask problem after, participate referencethe followingfix repeat method toward:

| Issue Category | fix repeat method plan |
|---------|---------|
| CAPTCHAserious repeat useuse | ValidateSuccess/Failureafter standalone that isfrom Redis/DB Delete, ValidateandDeleteasprinciple sub operation |
| Session Not Bound | generate complete timewillCAPTCHAand SessionID BindingStorage, Validatetime severe format match config |
| Client-Side Disclosure | CAPTCHAAnsweronly existServer(Redis), Response inonlyReturnCAPTCHAimage imageor Token |
| Rate LimitMissing | IP + AccountdualDimensionRate Limiting, config combine dynamic window interface algorithm method, Consecutive Errorsescalate levelasAccount Lockout |
| Resistance To OCR Insufficient | escalate levelaslinesasmodeCAPTCHA(block/point select/ transfer)orconnect inject special businessCAPTCHAservice(reCAPTCHA / hCaptcha / extreme validate) |
| Concurrency | useuse Redis SETNX orDistributed Lockprotect certCAPTCHAValidate+InvalidateofAtomicity |
| SMS Bombing | Image CAPTCHAsingletimesValid + same number code 60s Cooldown + Daily Limit |

---

## 6. Test Report Template

each conditionTest CaseExecuteafter, bythe followingformat modeRecord:

```
Test ID: TC-XX
Test Item: xxx
Test Time: YYYY-MM-DD HH:MM
Test Interface: POST /api/xxx
Test Result: Pass / Fail
Risk Level: High Risk / Medium Risk / Low Risk
Reproduction Steps:
 1....
 2....
Evidence:
 - Requestreport text intercept image/text
 - Responsereport text intercept image/text
Remediation Recommendation: xxx
```
