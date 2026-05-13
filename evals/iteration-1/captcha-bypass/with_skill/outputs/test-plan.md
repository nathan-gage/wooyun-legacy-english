# CAPTCHAmachine makeSecureTest Plan

> Based on the methodology from 22,132 real WooYun vulnerability cases | Authentication Domain 8,846 Case + Logic Flow Domain 1,679 Case

## 1. background sceneandTarget

**when first defense protect current:**
- Loginpage:Image CAPTCHA
- Registrationpage:Image CAPTCHA
- SMS Verification CodeInterface:Image CAPTCHAfirst set protect protect

**Test Objective:** Comprehensiveassess assessCAPTCHAmachine makeofSecureness, cover coverImage CAPTCHAversion identity/SMS Verification Code/as involvingCAPTCHAandbusiness flow process result combineofAllinBypassmethod mode.

**Datasupport:** WooYun DatabaseinCAPTCHA/ValidateBypasstotal 384 Case, 44% asHigh Risk.CAPTCHA Bypass is attack attack linkofNo. one environment -- one, after continueBrute Force/Accountconnect manage/BatchRegistrationetc.attack attack of while come.

---

## 2. WooYun CAPTCHA BypassStatisticsapprox

| Bypasstype | WooYun Prevalence | Risk Level | type after if |
|---------|-------------|---------|---------|
| noServerendValidate | Critical | Severe | CAPTCHA same set, DirectBrute Force |
| CAPTCHACanserioususe | Critical | High | onetimesIdentify, no limit useuse |
| SMS Verification Codeno rate rate limit make | High | High | 4-6 characters number characterCanexpose powerEnumeration |
| SMS Verification Codeno expired | High | High | oldCAPTCHA Valid |
| Can OCR/AI Identify | High | in | self dynamic izeBypassImage CAPTCHA |
| ClientValidate | in | High | BypassFrontendDirectRequestBackend |
| CAPTCHAandSessionNot Bound | in | High | crossSession/crossUserrepeatuse |
| PredictableCAPTCHA | in | Severe | algorithm methodCan, no need toIdentify |
| SMS Verification CodecrossUsershared | in | Severe | A ofCAPTCHACanusefor B ofAccount |

**WooYun typeCaseciteuse:**

| Case | Vulnerability Type | impact response |
|------|---------|------|
| card cart network some serious needSystemset plan logic logic missing flawSuccessBypassCAPTCHAlimit make | CAPTCHA Bypass | enableuseBrute Force, CanTraversalUser |
| networkfromCAPTCHA BypassagaintoArbitrary DataExport | CAPTCHA Bypass | fromCAPTCHA Bypassescalate leveltoDataDisclosure |
| above Empty toolPersonal InformationDisclosure/Password Reset(Bypassshort informationValidate) | short informationValidateBypass | toolPersonal Information + internal partDocumentDisclosure |
| FMcompany PlatformArbitrary User Password Reset | CAPTCHA+serious setBypass | Arbitrary User Password Reset |
| TCLsystem one identity copyAuthenticationPlatformvulnerability, AllUserAccountPasswordCanserious set | ValidateBypasslink | cross N+ businessSystemCompleteAccountconnect manage |

---

## 3. Test ScopeandCategory

### 3.1 test matrix matrix

```
CAPTCHASecuretest
+-- A. Image CAPTCHAversion bodySecure(7 items)
+-- B. Image CAPTCHAServerlogic logic(6 items)
+-- C. SMS Verification CodeSecure(8 items)
+-- D. CAPTCHAandbusiness flow process result combine(6 items)
+-- E. many channel channel one cause ness(4 items)
+-- F. forResistance Toself dynamic ize can power(4 items)
 total plan 35 itemsTest Case
```

---

## 4. DetailedTest Case

### A. Image CAPTCHAversion bodySecure

| ID | Test Item | Test Method | expected periodSecurelinesas | WooYun mode |
|------|-------|---------|------------|------------|
| A-1 | OCR/AI CanIdentifyness | useuse Tesseract/ddddocr/commerce business break codePlatform(super level etc.)forCAPTCHABatchIdentify, StatisticsRecognition Rate | Recognition Rate < 5% | Can OCR IdentifyofCAPTCHA(character body simple single, no, no transfer) |
| A-2 | CAPTCHArepeat degree | Checkwhetherinclude include: change /Interference Lines/Noise/character symbol continuous/background scene mix | at leastinclude include 3 typeor more mobile | same above |
| A-3 | character symbol collect topup part ness | AnalyzeCAPTCHAcharacter symbol collectScope(number character / number character+character / include case) | character symbol collect >= number character+case character, long degree >= 4 | PredictableCAPTCHA |
| A-4 | CAPTCHAimage imageInformation Disclosure | CheckCAPTCHAimage image URL/HTTP ResponseHeader/HTML inject /hidden hiddenFieldinwhetherinclude includeAnswer | Answernot out currentinanyClientCanseen characters set | command cardin URL/Responsein |
| A-5 | CAPTCHAgenerate complete algorithm methodPredictableness | continuous continueRequest 100+ timesCAPTCHA, Analyzewhether existsscale law(Fixedsequence list/timestamp type sub/weak machine number) | noCanIdentifymode, useuse CSPRNG | PredictableCAPTCHA |
| A-6 | CAPTCHA Bypass | provide provide CAPTCHAselectitems, useuse transfer text(Whisper etc.)advancelinesself dynamicIdentify | CAPTCHAsame tool has of and | CAPTCHA Bypass |
| A-7 | CAPTCHAimage image exist | CheckCAPTCHAimage imageResponseHeaderin Cache-Control/ETag set set, whetherCanbe CDN/Browser exist repeatuse | set set no-cache, no-store, must-revalidate | - |

### B. Image CAPTCHAServerlogic logic

| ID | Test Item | Test Method | expected periodSecurelinesas | WooYun mode |
|------|-------|---------|------------|------------|
| B-1 | DeleteCAPTCHAParameter | useuse Burp InterceptLogin/RegistrationRequest, complete allDelete captcha related keyParameterafterSubmit | ServerReturnerror, reject rejectRequest | noServerendValidate |
| B-2 | SubmitEmptyvalueCAPTCHA | will captcha ParametersetasEmptycharacter symbol string `""` or `null` Submit | ServerReturnerror, not asValidatePass | noServerendValidate |
| B-3 | CAPTCHACanserioususe | correct confirm output injectCAPTCHAcomplete onetimesRequestafter, useuserelated sameofCAPTCHAvalue againtimesSubmit(not New CAPTCHA) | No. twotimesSubmitshouldFailure, CAPTCHAonetimesness useuse | CanserioususeCAPTCHA |
| B-4 | CAPTCHAandSessionBinding | inSession A inObtainCAPTCHA, inSession B inuseusethisCAPTCHASubmit | crossSessionCAPTCHAno valid | CAPTCHAandSessionNot Bound |
| B-5 | CAPTCHACase SensitivityBypass | such asifCAPTCHAinclude character, test caseDifferentwhetheraverageCanPass | linesasone cause(need Allcase sensitive sensitive, need Allnot sensitive sensitive), notCanexploituse | - |
| B-6 | CAPTCHAsuper time machine make | ObtainCAPTCHAafteretc.pending 5 minutes/10 minutes/30 minutesagainSubmit | super time(create protocol 5 minutes)afterCAPTCHAInvalidate | SMS Verification Codeno expired(same manage suitableuseforImage CAPTCHA) |

### C. SMS Verification CodeSecure

| ID | Test Item | Test Method | expected periodSecurelinesas | WooYun mode |
|------|-------|---------|------------|------------|
| C-1 | SMS Verification Codeexpose powerEnumeration | BypassImage CAPTCHAafter(B-1/B-2/B-3 existinvulnerability), for 4/6 charactersSMS Verification Codeadvancelinesexpose powerEnumeration(4 characters = 10,000 times, 6 characters = 1,000,000 times) | Serverin 5-10 timeserror after lock set, orset setCAPTCHAAttempttimesnumber limit make | SMS Verification Codeno rate rate limit make |
| C-2 | SMS Verification CodeValidity Period | SendSMS Verification Codeafter, part levelin 5 minutes/15 minutes/30 minutes/1 hoursafterAttemptuseuse | CAPTCHAin 5 minutesinternal expired | SMS Verification Codeno expired |
| C-3 | oldCAPTCHAValidness | RequestSendnewofSMS Verification Codeafter, useuseoldCAPTCHAadvancelinesValidate | New CAPTCHASendafter, oldCAPTCHAImmediately Invalidate | SMS Verification Codeno expired |
| C-4 | SMS Verification CodecrossUser/crossmobile numberuseuse | willSendtomobile number A ofCAPTCHA, useformobile number B ofValidateRequest | CAPTCHAandRequestofmobile numberBinding, cross number useuseno valid | SMS Verification CodecrossUsershared |
| C-5 | short informationSendRate Limit | continuous continue fast rateRequestSendSMS Verification Code, testwhether hasRate Limit(eachminutes/eachhours/eachdays) | Samemobile number 60 internal only allow allow 1 times, eachdaysabove limit 10 times | SMS Verification Codeno rate rate limit make |
| C-6 | SMS Bombing | testSMS Sending InterfacewhetherCanbeusefor forArbitrarymobile numberSendlarge quantity short information(short information) | Samemobile numberRate Limit + Same IP Rate Limit | - |
| C-7 | SMS Verification CodecontentDisclosure | CheckSendSMS Verification Codeof API ResponseinwhetherReturndoneCAPTCHAclear text | Responseinnot include includeCAPTCHA, onlyReturn"alreadySend"Status | command cardin URL/Responsein |
| C-8 | SMS Verification Codelong degreeandrepeat degree | ConfirmCAPTCHAcharacters number(4 characters vs 6 characters)andcharacter symbol collect(number character vs include character) | at least 6 characters number character, infer 6 characters number character+character mix combine | SMS Verification Codeno rate rate limit make |

### D. CAPTCHAandbusiness flow process result combine(Statusmachine test)

> WooYun Logic Flow Domain 1,391 State-Machine BypassCasetable clear:manyStepflow processinCAPTCHAStepcommon be skip through.

| ID | Test Item | Test Method | expected periodSecurelinesas | WooYun mode |
|------|-------|---------|------------|------------|
| D-1 | skip throughCAPTCHAStep | Loginflow processinnotCallCAPTCHAValidateInterface, DirectSubmitLoginRequesttoBackendAuthenticationInterface | Backendstrong makeValidateCAPTCHAalreadyPass, notValidaterule reject reject | State-Machine Bypass(skip throughStep) |
| D-2 | Password Resetflow processinBypassValidate | Password Resetflow process:Requestserious set -> CAPTCHA/short informationValidate -> Set New Password.DirectRequest"Set New Password"StepofInterface | ServerValidatewhen firstSessionalreadyPassValidateStep | Password ResetStepskip through(777 Case, 88% High Risk) |
| D-3 | Registrationflow processinBypassValidate | Registrationflow processinskip through short informationValidateStep, Direct CallRegistrationcompleteInterface | Backendstrong make need require short informationValidateCompleted | Registrationflow processState-Machine Bypass |
| D-4 | Responsetamper changeBypass | InterceptCAPTCHAValidateofResponse, willFailureResponseModifyasSuccessResponse(such as `{"success":false}` -> `{"success":true}`, or `{"code":400}` -> `{"code":200}`) | Serverbased on self identitySessionStatusdetermine judge, not affectedClientResponsetamper change impact response | Responseoperation manipulate(Password ResetMediumPrevalence) |
| D-5 | Parameter PollutionBypass | inRequestinsame timeSendmany captcha Parameter(such as `captcha=wrong&captcha=`), testServertake value logic logic | ServerforParameter Pollutionhas clear confirm handle manage policy strategy | Design Flaw |
| D-6 | CAPTCHAStepofRace Condition | ConcurrencySendmanyRequest:same timeSubmitCAPTCHAValidate + business operation, testwhether exists TOCTOU | CAPTCHAmessage fee operation tool hasAtomicity | Race Condition(266 Case, 74.8% High Risk) |

### E. many channel channel one cause ness

> WooYun Datatable clear:Web end hasCAPTCHAprotect protect, but move dynamic API/H5/small process sequence endCancanMissing.

| ID | Test Item | Test Method | expected periodSecurelinesas | WooYun mode |
|------|-------|---------|------------|------------|
| E-1 | Mobile Client API CAPTCHAone cause ness | capture take move dynamic App ofLogin/Registration API, Checkwhethersame need requireCAPTCHA | AllClientinject interface average strong makeCAPTCHA | many channel channel not one cause |
| E-2 | H5/small process sequence end one cause ness | test H5 pageandWeChatsmall process sequenceofLogin/Registrationwhether hasCAPTCHAprotect protect | same above | many channel channel not one cause |
| E-3 | old version API contentInterface | probe testwhether exists v1/v2 etc.old version API Interface, old version versionwhethermissing lessCAPTCHAValidate | old version API already under lineorsame strong makeCAPTCHA | Design Flaw(hidden modeAuthorization) |
| E-4 | Direct Callinternal partInterface | AttemptBypassGateway/BFF layer, Direct Call layer micro serviceofAuthenticationInterface | internal partInterfacenot for external expose exposure, orsame hasSecureValidate | internal part vs external partTrust Boundary |

### F. forResistance Toself dynamic ize can power

| ID | Test Item | Test Method | expected periodSecurelinesas | WooYun mode |
|------|-------|---------|------------|------------|
| F-1 | IP Rate LimitingBypass | useuse `X-Forwarded-For`/`X-Real-IP`/`X-Originating-IP` etc.Headerforgery come source IP, testwhetherCanBypass IP DimensionofRate Limiting | Serverbased on real realClient IP Rate Limiting, not information anyCanforgeryofRequestHeader | IP rotate change(X-Forwarded-For Headeroperation manipulate) |
| F-2 | User-Agent/Cookie rotate changeBypass | eachtimesRequestupdate change User-Agent andclear remove Cookie, testwhetherCanserious setRate Limitingplan number device | Rate Limitingbased on manyDimension(IP + Account + set prepare specified pattern), notCansingleDimensionBypass | Passpart deploy modeRequestBypassrate rate limit make |
| F-3 | AccountDimensionRate Limiting | forSameAccountfrommany IP initiate initiateLoginAttempt, testwhether hasAccountDimensionoflimit make | SameAccountno comment come source IP, planFailure N timesafter lock set | Credential topup attack attack |
| F-4 | CAPTCHAescalate level machine make | continuous continue manytimesFailureafter, CAPTCHA degreewhetherprovide escalate(such asfromImage CAPTCHAescalate levelto dynamicValidate/linesasValidate) | existin advance modeSecureescalate level policy strategy | - |

---

## 5. Test Priority Ranking

based on WooYun Datainofattack attack frequency rateandimpact responseSevereness rank sequence:

### P0 - muststandalone that is test(directly usableCausingAccountconnect manage/Batchattack attack)

| Priority | Test ID | Test Item | Reason |
|--------|---------|-------|------|
| P0-1 | B-1 | DeleteCAPTCHAParameter | WooYun inmost common seenofBypassmethod mode, CriticalPrevalence |
| P0-2 | B-3 | CAPTCHACanserioususe | CriticalPrevalence, onetimesIdentifyno limit useuse |
| P0-3 | D-1 | skip throughCAPTCHAStep | State-Machine Bypass, 1,391 Case |
| P0-4 | D-2 | Password ResetFlow Bypass | 88% High Risk, mostHighSevereness sub domain |
| P0-5 | C-7 | SMS Verification CodecontentDisclosure | DirectDisclosure = zero complete versionBypass |
| P0-6 | C-4 | SMS Verification CodecrossUseruseuse | DirectCausingArbitraryAccountconnect manage |

### P1 - HighPriority(Candisplay Lowattack attack complete version)

| Priority | Test ID | Test Item | Reason |
|--------|---------|-------|------|
| P1-1 | C-1 | SMS Verification Codeexpose powerEnumeration | 4 characters number character only 10,000 typeCancan |
| P1-2 | C-2/C-3 | SMS Verification CodeValidity Period | no expired = large attack attackTime Window |
| P1-3 | B-2 | EmptyvalueCAPTCHA | variantBypass, common be leak |
| P1-4 | E-1/E-2 | many channel channel one cause ness | Mobile Client/H5 common missing lessCAPTCHA |
| P1-5 | F-1 | IP Rate LimitingBypass | X-Forwarded-For forgery extremeascommon seen |
| P1-6 | D-4 | Responsetamper change | ClientValidateCanbeBypass |

### P2 - inPriority(provide escalate self dynamic ize attack attack valid rate)

| Priority | Test ID | Test Item | Reason |
|--------|---------|-------|------|
| P2-1 | A-1 | OCR/AI Recognition Rate | AI break code complete version hold continue Low |
| P2-2 | A-4 | image imageInformation Disclosure | Lowapprox rate butHighimpact response |
| P2-3 | A-5 | algorithm methodPredictableness | weak machine numberCausingCAPTCHAPredictable |
| P2-4 | C-5/C-6 | short informationSendfrequency rate/short information | resource source abuseuse + User |
| P2-5 | D-6 | Race Condition | ConcurrencyBypassCAPTCHAmessage fee |

### P3 - LowPriority(Hardeningitems)

| Priority | Test ID | Test Item |
|--------|---------|-------|
| P3-1 | A-2/A-3 | CAPTCHArepeat degree/character symbol collect |
| P3-2 | A-7 | exist ask problem |
| P3-3 | B-5 | Case Sensitivity |
| P3-4 | B-6 | Image CAPTCHAsuper time |
| P3-5 | F-4 | CAPTCHAescalate level machine make |

---

## 6. testToolclear single

| Tool | Purpose | Test ID |
|------|------|---------|
| Burp Suite Professional | Request Interception/Parametertamper change/Intruder Brute Force | All |
| Burp Turbo Intruder | HighConcurrencyRace Conditiontest | D-6 |
| ddddocr / Tesseract / PaddleOCR | Image CAPTCHA OCR Recognition Ratetest | A-1 |
| super level /break codePlatform API | commerce business break codeSuccessrate base accurate test | A-1 |
| Python + requests/aiohttp | self dynamic ize testScriptcompile write | B-1 ~ B-6, C-1 ~ C-8 |
| mitmproxy | Mobile Client/H5 flow quantity capture take | E-1, E-2 |
| Frida / objection | move dynamic App dynamic stateAnalyze, Bypass SSL Pinning | E-1 |
| Postman / curl | InterfacelevelCAPTCHAlogic logic test | D-1 ~ D-5, E-3, E-4 |

---

## 7. testExecuteflow process

```
No. 1 days: andmap map
+-- 1. capture takeAllinclude includeCAPTCHAofInterface(Login/Registration/Password Reset/short informationSend)
+-- 2. RecordEachInterfaceofRequest/Responseformat mode/Parametername name
+-- 3. IdentifyCAPTCHAtype(image / dynamic/linesas/short information)andreal current method mode
+-- 4. map mapCompletebusiness flow processStatusmachine

No. 2 days:P0 test(Serverlogic logic + Statusmachine)
+-- 5. Execute B-1, B-2, B-3(Delete/Emptyvalue/serioususe) - Image CAPTCHAlogic logic
+-- 6. Execute C-7, C-4(SMS Verification CodeDisclosure/crossUseruseuse)
+-- 7. Execute D-1, D-2, D-3(flow process skip through test)
+-- 8. Discover P0 vulnerability standalone that isRecordand wild report

No. 3 days:P1 test(rate rate limit make + many channel channel)
+-- 9. Execute C-1, C-2, C-3(expose powerEnumeration/Validity Period)
+-- 10. Execute E-1, E-2, E-3(many channel channel one cause ness)
+-- 11. Execute F-1, F-2, F-3(Rate LimitingBypass)
+-- 12. Execute D-4, D-5(Responsetamper change/Parameter Pollution)

No. 4 days:P2 + P3 test(forResistance Tocan power + Hardening)
+-- 13. Execute A-1 ~ A-7(Image CAPTCHAversion bodySecure)
+-- 14. Execute C-5, C-6, C-8(short information frequency rate/ /long degree)
+-- 15. Execute D-6(Race Condition)
+-- 16. Execute F-4 + All P3 itemsdirectory

No. 5 days:report output out
+-- 17. remit totalAllDiscover, bySevereness rank sequence
+-- 18. compile writeReproduction Steps(includeRequest/Responseintercept image)
+-- 19. provide outRemediation Recommendation
+-- 20. transaction pay test report
```

---

## 8. Discoverreport model template

EachDiscovershouldbythe followingresult structureRecord:

```
## Discover:[identifier problem]
- Severity:Severe / High / in / Low
- Test ID:[forshouldID]
- WooYun mode:[match configofhistory history mode]
- Business Impact:[Accountconnect manage / Brute Force / BatchRegistration / short information /...]
- Impact Scope:[affected impact responseofInterfaceandUserquantity]
- Reproduction Steps:
 1. [useuse Burp Intercept POST /api/login Request]
 2. [Delete captcha_code Parameter]
 3. [SubmitRequest, ObserveResponseas 200 OK, LoginSuccess]
- Request/ResponseEvidence:[intercept imageorprinciple text]
- Remediation Recommendation:[ConcreteofServerfix repeat method plan]
```

---

## 9. Remediation Recommendationframework architecture(based on WooYun fix repeatData)

### Image CAPTCHA

| ask problem | fix repeat method plan |
|------|---------|
| OCR CanIdentify | escalate levelaslinesasCAPTCHA(dynamic image/point select text character), oruseuse reCAPTCHA / hCaptcha / extreme validate |
| noServerValidate | Backendmuststrong makeValidateCAPTCHA, notCandepend relyFrontend |
| Canserioususe | CAPTCHAuseuseafter standalone that is operation, no commentValidateSuccessorFailure |
| andSessionNot Bound | CAPTCHAAnswerand Session ID BindingStoragein Redis, crossSessionno valid |
| no super time | set set 5 minutesValidity Period, expired self dynamicInvalidate |

### SMS Verification Code

| ask problem | fix repeat method plan |
|------|---------|
| Canexpose powerEnumeration | Samemobile numberCAPTCHAValidateFailure 5 timesafter lock set 30 minutes;CAPTCHAlong degree >= 6 characters |
| no expired | Validity Period 5 minutes;new codeSendafterOld CodeImmediately Invalidate |
| crossUseruseuse | CAPTCHAandmobile number + business scenario scene(Login/Registration/serious set)Binding |
| Sendfrequency rate no limit make | Samemobile number 60 between isolate limit make + eachdaysabove limit 10 condition;Same IP eachhoursabove limit 20 condition |
| clear textReturn | API ResponseinonlyReturnSendStatus, reject notReturnCAPTCHAcontent |

### architecture structure layer

| ask problem | fix repeat method plan |
|------|---------|
| State-Machine Bypass | Servermaintain protect display modeStatusmachine, each step operationValidatefirst setStatuswhetherCompleted |
| many channel channel not one cause | AllClient(Web/App/H5/small process sequence)system one SameCAPTCHAValidateGateway |
| IP Rate LimitingCanBypass | based on real realClient IP(fromreverse toward code manageObtain), not information any X-Forwarded-For |
| no monitor control report alert | monitor controlCAPTCHAFailurerate increase/same IP large quantityRequest/short informationSendabnormal commonetc.specified identifier |

---

## 10. Appendix:WooYun DataStatistics

**CAPTCHArelated key vulnerabilityin WooYun Databaseinofpart deploy:**

- **identity copyAuthentication DomaintotalCase:** 8,846(share all library 40%)
- **CAPTCHA/ValidateBypassspecialitems:** 384 Case, 44% High Risk
- **Password Reset(includeValidateBypass):** 777 Case, 88% High Risk - all library mostHigh Risksub domain
- **weakCredential(CAPTCHA BypassafterCanexploituse):** 7,513 Case, 58.2% High Risk
- **State-Machine Bypass(includeValidateStepskip through):** 1,391 Case, 65.3% High Risk
- **Race Condition:** 266 Case, 74.8% High Risk

**audit core result comment:** CAPTCHAnot is one independent standaloneofSecurearray item, while isAuthenticationlinkinofone environment.WooYun Datareverse repeat cert clear:CAPTCHA Bypass less is most finalTarget, total is wild toward updateSeverevulnerability(Accountconnect manage/BatchRegistration/Brute Force/DataDisclosure)ofskip template.because, testCAPTCHASecurenessmustwillother releaseinCompletebusiness flow processinassess assess, whileNon- standalone only "Image CAPTCHAcancannotIdentify".

---

*version method plan based on WooYun Business Logic Vulnerability Methodology(22,132 Case)generate complete, Test Casecover coverAuthentication Domain 9 typeCAPTCHA Bypassmode + Logic Flow DomainState-Machine Bypass + Race Condition, total plan 35 itemstest.*
