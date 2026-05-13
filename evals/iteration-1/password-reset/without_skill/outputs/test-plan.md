# social transactionPlatformPassword Resetfunction can - Attack VectorandTest Plan

## directory record

1. [SMS Verification Codeserious set](#1-SMS Verification Codeserious set)
2. [Emaillink connect serious set](#2-Emaillink connect serious set)
3. [Secureask problem serious set](#3-Secureask problem serious set)
4. [cross serious set method mode wilduseAttack Vector](#4-cross serious set method mode wilduseAttack Vector)
5. [business logic logic layerAttack Vector](#5-business logic logic layerAttack Vector)
6. [ClientAttack Vector](#6-ClientAttack Vector)

---

## 1. SMS Verification Codeserious set

### 1.1 CAPTCHABrute Force

**Attack Vector:** CAPTCHAas number character and characters number short(4-6characters), attack attack personCanExhaustive GuessingAllCancan value.

**Test Steps:**
1. output injectTargetmobile number, trigger initiateSendCAPTCHA
2. InterceptCAPTCHAValidateRequest(such as `POST /api/reset/verify-sms`)
3. useuse Burp Suite Intruder forCAPTCHAFieldadvancelinesexpose powerEnumeration(0000-9999 or 000000-999999)
4. Observewhether existsRate Limit(Rate Limiting):
 - continuous continueSubmit 10 timeserrorCAPTCHAafterwhetherbe lock set
 - whetherReturnDifferentof HTTP Statuscodeorerror information
5. Checklock set machine makewhetherCanbeBypass:
 - update change IP(Passcode manage)afterwhetherserious set plan number
 - update change User-Agent afterwhetherserious set plan number
 - Add `X-Forwarded-For` / `X-Real-IP` HeaderwhetherBypass IP limit make
 - inCAPTCHAFieldfirst afterAddEmptyformat/changelinessymbol(`%20`/`%0a`)whetherBypassoutput injectValidate

### 1.2 CAPTCHAPredictableness

**Attack Vector:** CAPTCHAgenerate complete algorithm methodInsecure, Canbe predictionorinfer.

**Test Steps:**
1. Samemobile numbercontinuous continueRequest 20 timesCAPTCHA, RecordAllcollecttoofCAPTCHA
2. Analyzewhether existsPredictableofmode(recursive increase/timestamp related key/ machine type subCaninfer)
3. Differentmobile numbersame timeRequestCAPTCHA, Checkwhether existsrelated sameCAPTCHA
4. CheckCAPTCHAwhetherinResponseincludeinDirectReturn(ViewResponse Body/Headers/Set-Cookie)

### 1.3 CAPTCHAtime valid ness

**Attack Vector:** CAPTCHAValidity PeriodToo Longorno expired machine make, largeBrute Forcewindow interface.

**Test Steps:**
1. RequestCAPTCHAafter, etc.pending 5 minutes/10 minutes/30 minutes/1 hoursafter part levelAttemptuseuse
2. RecordCAPTCHAreal actualValidity Period
3. RequestNew CAPTCHAafter, test oldCAPTCHAwhetherstill Valid(CAPTCHAnotInvalidate/cover cover)
4. Samemobile numbercontinuous continueRequestmanyCAPTCHA, testAllCAPTCHAwhetherall can useuse

### 1.4 CAPTCHAandmobile numberBindingValidate

**Attack Vector:** ServernotValidateCAPTCHAandmobile numberofBindingkey system.

**Test Steps:**
1. usemobile number A RequestCAPTCHA, collecttoCAPTCHA X
2. usemobile number B RequestCAPTCHA, collecttoCAPTCHA Y
3. Attemptusemobile number A + CAPTCHA Y SubmitValidate(transaction useuse)
4. InterceptValidateRequest, willmobile numberFieldReplaceasTargetUsermobile number, CAPTCHAuseuseself own collecttoofCAPTCHA
5. CheckwhethercanPassValidateand advance injectPassword Resetpage

### 1.5 CAPTCHAReplay

**Attack Vector:** already useuseofCAPTCHAnotInvalidate, Canserious repeat useuse.

**Test Steps:**
1. correct common useuseCAPTCHAcomplete onetimesPassword Reset
2. useuserelated sameofCAPTCHAagaintimesSubmitValidateRequest
3. Observewhethercan againtimesPassValidate

### 1.6 SMS Bombing

**Attack Vector:** SendCAPTCHAInterfacenoRate Limit, CanbeuseforSMS Bombing.

**Test Steps:**
1. forSamemobile numbercontinuous continueCallSendCAPTCHAInterface, Observelimit make policy strategy
2. forDifferentmobile numberBatchCall, check whether there isall globalRate Limit
3. testwhetherCanPassthe followingmethod modeBypasslimit make:
 - mobile numberfirst add `+86`/`086`/`0086`/Emptyformat/continuous character symbol
 - mobile number add `%00`(Emptycharacter section intercept judge)
 - Parameter Pollution(same time pass recursive manymobile numberParameter)

### 1.7 ValidateStepskip through

**Attack Vector:** CAPTCHAValidateandPassword Resetis part step operation, directly usableskiptoserious setStep.

**Test Steps:**
1. initiate initiatePassword Resetflow process, Obtainflow processinofAllRequest
2. notSubmitCAPTCHA, Directstructure forgePassword ResetRequest(wild common is flow processofmost after one step)
3. CheckServerwhetherinPassword ResetStepindependent standaloneValidatedoneCAPTCHAalreadyPass
4. ModifyClientStatus(such as JS change quantity/LocalStorage/Cookie inof step identifier identify)Attemptskip throughValidateStep

### 1.8 mobile numberformat modeBypass

**Attack Vector:** mobile numberoutput inject not identifier accurate ize, Differentformat mode be asDifferentUser.

**Test Steps:**
1. testthe followingmobile numberformat mode variantwhetherspecified towardSameUser:
 - `13800138000`
 - `+8613800138000`
 - `008613800138000`
 - `138 0013 8000`(includeEmptyformat)
 - `138-0013-8000`(include continuous character symbol)
2. CheckDifferentformat modewhethersharedRate Limitplan number device
3. CheckDifferentformat modewhethercan connect collect and useuseSameCAPTCHA

---

## 2. Emaillink connect serious set

### 2.1 serious set Token Predictableness

**Attack Vector:** serious set link connectinof Token generate complete algorithm methodInsecure, Canbe predictionorcollision collision.

**Test Steps:**
1. forSameEmailcontinuous continueRequest 20 timesserious set link connect, collect collectAll Token
2. Analyze Token ofarray complete(long degree/character symbol collect/whether Base64 Encoding)
3. decode code Token, Checkwhetherinclude includePredictableinformation(UserID/timestamp/Emailhash hash)
4. Check Token whether is UUID v1(based on timestamp, Canpart part prediction)
5. DifferentUsersame timeRequest, Check Token whether existsscale law ness
6. test Token of value:such asif long degree < 20 character symbol and character symbol collect has limit, assess assessBrute ForceCanlinesness

### 2.2 serious set link connect Token Brute Force

**Attack Vector:** Token Emptybetween not largeorServernot limit makeAttempttimesnumber.

**Test Steps:**
1. Obtainone combine method Token offormat modeandlong degree
2. toward serious setPasswordof URL Sendlarge quantity with has machine Token ofRequest
3. ObserveServerofResponse:
 - whether hasRate Limit
 - no valid Token andValid Token ofResponsewhether hasCan part error abnormal(time between error/Responselong degree)
4. such asif Token short(such as 6-8 characters number character), useuse Intruder advancelinesEnumeration

### 2.3 Token time valid ness

**Attack Vector:** serious set Token long periodValidormanytimesValid.

**Test Steps:**
1. Requestserious set link connect after, etc.pendingDifferenttime between (1hours/6hours/24hours/48hours)afterAttemptuseuse
2. useuse Token completePassword Resetafter, againtimesuseuseSame Token, CheckwhetherstillValid
3. Requestnewofserious set link connect after, Checkold Token whetherInvalidate
4. UserPassother method mode(such asSMS Verification Code)SuccessModifyPasswordafter, CheckEmail Token whetherInvalidate

### 2.4 Token andUserBindingValidate

**Attack Vector:** Token notandspecial setUserBinding, Cantamper changeTargetUser.

**Test Steps:**
1. useself ownofEmailRequestserious set link connect, Obtain Token
2. inserious setPasswordRequestin, willEmail/UserIDFieldModifyasTargetUser
3. Checkwhethercan serious setTargetUserofPassword
4. such asif serious set URL include includeUseridentifier identifyParameter(such as `?token=xxx&email=yyy`), AttemptModify email Parameter

### 2.5 Host Header inject inject

**Attack Vector:** Serverroot according Host Header generate complete serious set link connect, attack attack personCanwilllink connect specified toward meaningDomain Name.

**Test Steps:**
1. InterceptPassword ResetRequest, Modify Host Header asattack attack person control makeofDomain Name
 ```
 Host: evil.com
 ```
2. CheckSendtoUserEmailofserious set link connectwhetheruseusedone `evil.com` Domain Name
3. testthe followingvariant:
 - `Host: evil.com`(DirectReplace)
 - `Host: legitimate.com\r\nHost: evil.com`(dual Host Header)
 - `X-Forwarded-Host: evil.com`
 - `X-Host: evil.com`
 - `Forwarded: host=evil.com`
 - `Host: legitimate.com@evil.com`
 - `Host: legitimate.com.evil.com`
4. such asifSuccess, attack attack scenario scene:affected person point attack link connect -> Token Sendtoattack attack personServer

### 2.6 serious set link connectParametertamper change

**Attack Vector:** serious set link connectinofParameterCanbe tamper change.

**Test Steps:**
1. Analyzeserious set link connectofCompleteresult structure, IdentifyAllParameter
2. one-by-oneModifyParametervalue, ObserveServerlinesas:
 - Modify `user_id` / `uid` Parameter
 - Modify `email` Parameter
 - Modify `timestamp` / `expires` Parameter(longValidity Period)
3. DeleteSignature/ValidateParameter, Check Token whetherstillValid
4. testParameter Pollution:Addserious repeatParameter(such as `?email=victim@x.com&email=attacker@x.com`)

### 2.7 Referer Disclosure Token

**Attack Vector:** serious set page include include external part resource source citeuse, Token Pass Referer Header Disclosure.

**Test Steps:**
1. break open serious setPasswordpage(with Token of URL)
2. Checkpagewhetheradd external part resource source(No. three method JS/CSS/image image/iframe)
3. Checkpagewhetherinclude include external link(social transaction part by / report link connect)
4. such asif existinexternal part resource source/external link, CheckRequestof Referer Header whetherinclude include Token
5. Checkpagewhetherset set done `Referrer-Policy` Header

### 2.8 Emailcase / level nameBypass

**Attack Vector:** EmailAddresshandle manage not one cause, CausingSecurelogic logic beBypass.

**Test Steps:**
1. testEmailcase variant:`User@Example.com` vs `user@example.com`
2. test Gmail special hasof `+` level name:`user+tag@gmail.com` vs `user@gmail.com`
3. test Gmail ignore point numberofspecial ness:`u.s.e.r@gmail.com` vs `user@gmail.com`
4. Checkthis some variantwhether:
 - beIdentifyasSameUser
 - sharedRate Limit
 - generate completeof Token whetherCan change useuse

---

## 3. Secureask problem serious set

### 3.1 Secureask problemAnswerBrute Force

**Attack Vector:** Secureask problemAnswerEmptybetween has limit(such as"ofout generate "), Canexpose powerEnumeration.

**Test Steps:**
1. confirm setTargetUserofSecureask problem
2. root according ask problem type accurate prepareDictionary:
 - out generate -> innational primary need list(~300)
 - -> innational common seen list(~100)
 - small name name -> +common seen small name array combine
 - item name character -> common seen item nameDictionary
 - most ofelectronic impact/certificate -> operation product list
3. useuse Burp Intruder forAnswerFieldadvancelinesDictionaryattack attack
4. CheckRate Limitandlock set machine make
5. test lock setBypassMethod(same 1.1 inofBypasstechnique)

### 3.2 Secureask problemInformation Disclosure

**Attack Vector:** Secureask problem version identityDisclosuredoneUserhidden private information.

**Test Steps:**
1. output injectTargetUsername/mobile number/Email, advance injectSecureask problemValidatepage
2. CheckSecureask problemwhetherDirectdisplay(attack attack personCanexploituseask problem content advancelinesSocial Engineering)
3. CheckSecureask problemwhetherin API ResponseinReturnCompleteask problem text
4. AttemptEnumerationDifferentUser, Batchcollect collectSecureask problem information

### 3.3 Secureask problemAnswerValidatemissing flaw

**Attack Vector:** Answermatch config logic logic through for orexistinmissing flaw.

**Test Steps:**
1. testAnswerwhether part case
2. testAnswerwhetherignore first afterEmptyformat
3. testEmptyAnswerwhethercanPassValidate
4. test super longAnswerwhetherCausingintercept judge after match config(such asAnsweras" ", output inject" "because intercept judgeas" "whilePass)
5. test SQL inject inject:`' OR '1'='1`/`' OR 1=1--`/`" OR ""="`
6. test NoSQL inject inject:`{"$gt": ""}` / `{"$ne": null}`
7. testSpecial Characters:`%00`(Emptycharacter section intercept judge)/Unicode variant character symbol

### 3.4 Secureask problemAnswerinResponseinDisclosure

**Attack Vector:** ServerinResponseinReturndone correct confirmAnswerorprovide show.

**Test Steps:**
1. SubmiterrorAnswer, detailCheckResponseincludeofAllcontent:
 - Response Body(include hidden hiddenField/inject)
 - Response Headers
 - Set-Cookie value
2. Checkerror provide showwhetherDisclosureinformation(such as"Answeroffirst two character correct confirm")
3. CheckFrontend JS source codeinwhetherinclude includeAnswerValidatelogic logicorAnswerhash hash value
4. Checkpage HTML source codeinwhether hashidden hiddenoftable singleFieldinclude includeAnswer

### 3.5 Secureask problemBypass

**Attack Vector:** Canas skip throughSecureask problemValidateDirectserious setPassword.

**Test Steps:**
1. AnalyzePassword Resetflow processofAll API Request
2. skip throughSecureask problemValidateStep, DirectSendserious setPasswordRequest
3. ModifyRequestinof `step` / `phase` / `verified` Parameter
4. DeleteRequestinofSecureask problem related keyParameter, CheckServerwhetherneed require

### 3.6 Social Engineering attack attack

**Attack Vector:** Secureask problemofAnswerCanPasssocial transaction body/company open informationObtain.

**Test Steps:**
1. list outAllCanuseofSecureask problem type
2. assess assessEachask problemofAnswerwhetherCanfromcompany open informationObtain:
 - out generate -> social transaction body resource /simple history
 - -> social transaction key system
 - small name name -> social transaction body/same record
 - item name character -> social transaction body photo image
3. assess assess total bodySecureness:requiresmany less company open information that isCan outAnswer

---

## 4. cross serious set method mode wilduseAttack Vector

### 4.1 UserEnumeration

**Attack Vector:** Password ResetInterfaceCanbeuseforEnumerationValidUser.

**Test Steps:**
1. part level output inject alreadyRegistrationandnotRegistrationofmobile number/Email/Username
2. for ratioResponseerror abnormal:
 - Responsecontent error abnormal("CAPTCHAalreadySend" vs "thismobile numbernotRegistration")
 - Responsetime between error abnormal(alreadyRegistrationUserCancan because amount external check query time update long)
 - HTTP Statuscode error abnormal
 - Responselong degree error abnormal
3. CheckwhetherAllserious set method modeofinject interface all existinEnumerationask problem
4. testBatchEnumerationofCanlinesness(Rate Limit)

### 4.2 serious setCredentialinResponseinDisclosure

**Attack Vector:** CAPTCHAor Token in HTTP ResponseinDirectReturn.

**Test Steps:**
1. RequestSendCAPTCHA/serious set link connect
2. detailCheckResponseofAllcharacters set:
 - Response Body(JSON Field/HTML inject)
 - Response Headers(self set define Header)
 - Set-Cookie
3. useuse Burp Suite of Search function caninResponseinsearchCAPTCHAnumber character
4. Check WebSocket continuous connectwhetherinfer doneCAPTCHA

### 4.3 Password Resetafter Session manage manage

**Attack Vector:** Password Resetafter old Session notInvalidate.

**Test Steps:**
1. inBrowser A inLoginTargetAccount
2. inBrowser B inExecutePassword Reset
3. CheckBrowser A of Session whetherstill Valid
4. CheckMobile Client Token(such as JWT/Refresh Token)whetherstill Valid
5. Check API Token whetherstill Valid

### 4.4 newPasswordpolicy strategy missing flaw

**Attack Vector:** serious setPasswordtimeofPasswordpolicy strategy weak for correct commonRegistrationtimeofpolicy strategy.

**Test Steps:**
1. Attemptset set weakPassword(`123456`/`password`/andUsername related same)
2. Attemptset setBlank Password
3. Attemptset setandoldPasswordrelated sameofPassword
4. testPasswordlong degree limit make(most short/most long)
5. for ratio serious set flow processandRegistrationflow processofPasswordpolicy strategywhetherone cause

### 4.5 serious set flow processof CSRF

**Attack Vector:** Password ResetRequestmissing less CSRF protect protect, attack attack personCanstructure forge meaning page self dynamicSubmit.

**Test Steps:**
1. CheckPassword ResetofkeyRequestwhetherinclude include CSRF Token
2. Delete CSRF Token afterSubmitRequest, Checkwhetherstill be connect affected
3. useuseotherUserof CSRF Token SubmitRequest
4. Check CSRF Token whetherand Session Binding
5. structure forge PoC HTML page test self dynamicSubmit

### 4.6 Race Condition (Race Condition)

**Attack Vector:** ConcurrencyRequestCausingValidatelogic logic beBypass.

**Test Steps:**
1. CAPTCHAuseusetimesnumber limit makeBypass:
 - ObtainoneValidCAPTCHA
 - useuse Burp Suite Turbo Intruder orself set defineScriptsame timeSend 50+ useusethisCAPTCHAofRequest
 - check whether there ismanyRequestSuccessPassValidate
2. Rate LimitBypass:
 - same timeSendlarge quantitySendCAPTCHAofRequest
 - Checkwhethersuper through done correct commonofSendRate Limit
3. Token onetimesness useuseBypass:
 - useuserelated same Token ConcurrencySubmitmanyPassword ResetRequest, set setDifferentofnewPassword
 - Checkmost finalPasswordbe set setaswhich value

### 4.7 serious set method mode switch change logic logic missing flaw

**Attack Vector:** Differentserious set method mode betweenofStatusmanage manage existinmissing flaw.

**Test Steps:**
1. Passshort information method mode initiate initiate serious set, Obtainto"ValidatePass"of Session/Token Status
2. switch changetoSecureask problem method mode, Checkwhetherprotect retain done"alreadyValidate"Status
3. inone type method modeinPassValidateafter, Attemptuse one type method modeofInterfacecompletePassword Reset
4. CheckDifferentmethod modeofRate Limitwhetherindependent standalone(such asshort information be lock after switch changetoSecureask problemwhethernot affected limit)

---

## 5. business logic logic layerAttack Vector

### 5.1 Parametertamper change

**Attack Vector:** ModifyRequestParameteras operation control serious set flow process.

**Test Steps:**
1. InterceptAllserious set flow processRequest, IdentifykeyParameter
2. testthe followingtamper change:
 - Modify `user_id` / `uid` / `account` asotherUser
 - Modify `phone` / `email` asotherUserofconnect system method mode
 - Modify `step` / `stage` / `verified` Parameterskip throughValidate
 - Modify `method` / `type` Parameterswitch changeValidatemethod mode
 - Add `admin=true` / `role=admin` etc.PermissionParameter
3. testParametertype mix:
 - character symbol string changeasnumber array:`phone=13800138000` -> `phone[]=13800138000`
 - character symbol string changeasfor:`phone=13800138000` -> `phone[key]=13800138000`
 - number character changeascharacter symbol string:`code=123456` -> `code="123456"`

### 5.2 manyStepValidateofStatusmanage manage

**Attack Vector:** manyStepflow processin, eachStepofValidateStatusmanage manageInsecure.

**Test Steps:**
1. correct common completeNo. one step(output injectmobile number/Email)
2. AnalyzeNo. two stepRequestin withofStatusinformation(Cookie/Token/Session ID)
3. AttemptDirectstructure forgeNo. two steporNo. three stepofRequest, skip through first setStep
4. useuseself ownAccountcompleteAllValidateStep, Obtain"alreadyValidate"Status
5. ReplaceRequestinofTargetUseridentifier identifyasaffected person, SubmitPassword Reset
6. Check Token/Session whetherBindingdoneUseridentity copy andServerindependent standaloneValidate

### 5.3 Password Reset Token andAuthentication Token mixuse

**Attack Vector:** Login Token CanbeuseoperationPassword ResetCredential, orreverse of.

**Test Steps:**
1. Obtaincorrect commonLoginof Session Token
2. AttemptwillotheruseforPassword ResetInterface
3. ObtainPassword Reset Token
4. AttemptwillotheruseforrequiresAuthenticationofotherInterface(such asModifyPersonal Information)

### 5.4 Batchserious set / reject reject service

**Attack Vector:** Batchtrigger initiatePassword ResetCanCausingUserbe lock setorresource source.

**Test Steps:**
1. forSameUserfrequency trigger initiatePassword Reset, CheckwhetherCausingAccount Lockout
2. BatchforDifferentUsertrigger initiatePassword Reset, check whether there isall global limit make
3. Checkshort information/ itemSendwhether hascomplete version control make(defense stop meaning message short information config amount)
4. assess assesswhetherCanPassPassword Resetflow process stop combine methodUsercorrect common useuse

### 5.5 OAuth / No. three methodLoginandPassword Reset

**Attack Vector:** PassPassword Resetasonly useuseNo. three methodLoginofAccountset setPassword, holdAccount.

**Test Steps:**
1. ConfirmPlatformwhethersupport holdNo. three methodLogin(WeChat/QQ/micro etc.)
2. CheckonlyPassNo. three methodLoginRegistrationofAccountwhether hasBindingmobile number/Email
3. such asif hasBinding, AttemptPassPassword Resetflow processasthisAccountset setPassword
4. set setPasswordafter, whetherCanasusemobile number/Email + PasswordDirectLogin, BypassNo. three methodAuthentication

---

## 6. ClientAttack Vector

### 6.1 FrontendValidateBypass

**Attack Vector:** SecureValidateonlyinFrontendExecute, CanPassModifyFrontendCodeorDirect Call API Bypass.

**Test Steps:**
1. CheckCAPTCHAValidatewhetherinFrontend JS incomplete
2. CheckFrontendwhether hasStepcontrol make logic logic(such asroot according JS change quantity determine judgewhetherCanadvance inject under one step)
3. useuseBrowseropen initiate personToolModify JS change quantity/ numberReturnvalue
4. Directuseuse curl/Postman Call API, skip throughAllFrontendValidate
5. CheckFrontendwhether exist doneCAPTCHAor Token

### 6.2 CAPTCHA/Token ClientStorageDisclosure

**Attack Vector:** Sensitive InformationStorageinClientCanaccess askofcharacters set.

**Test Steps:**
1. Check LocalStorage / SessionStorage inwhetherStoragedoneCAPTCHAor Token
2. Check Cookie inwhetherinclude includeSensitive Information(andwhetheridentifier recordas HttpOnly / Secure)
3. Check URL Parameterinwhetherinclude include Token(CanPassBrowserhistory historyRecordDisclosure)
4. CheckBrowseropen initiate personTool Network page templateinofRequest/Response

### 6.3 CORS Configurationerror

**Attack Vector:** Password Reset API of CORS Configurationthrough for.

**Test Steps:**
1. fromNon-Authorization DomainSendcross domainRequesttoPassword Reset API
2. Check `Access-Control-Allow-Origin` ResponseHeader:
 - whether is `*`
 - whetherreverse map `Origin` RequestHeader
 - whetherallow allow `null` Origin
3. Check `Access-Control-Allow-Credentials` whether is `true`
4. such asif CORS Configuration, structure forge meaning pagefromUserBrowserSendserious setRequest

### 6.4 point attack hold (Clickjacking)

**Attack Vector:** Password ResetpageCanbe injectto meaning iframe in.

**Test Steps:**
1. CheckPassword ResetpageofResponseHeaderwhetherinclude include `X-Frame-Options`
2. check whether there is `Content-Security-Policy` of `frame-ancestors` specified command
3. structure forge include includeTargetserious set page iframe of PoC HTML
4. testwhetherCanas Userinnot notify detailsofdetails under completePassword Resetoperation

---

## testToolclear single

| Tool | Purpose |
|------|------|
| Burp Suite Professional | Request Interception/Intruder Brute Force/Turbo Intruder Racetest |
| OWASP ZAP | self dynamic izeScan/be dynamicScan/Fuzzer |
| Postman / curl | API Direct Call/Parametertamper change |
| Python + requests | self dynamic izeScript/Batchtest |
| Hydra / ffuf | Dictionaryattack attack/Brute Force |
| Browseropen initiate personTool | FrontendAnalyze/JS debugging/Networkflow quantityAnalyze |

## Severeetc.level assess assess identifier accurate

| etc.level | description | Example |
|------|------|------|
| **Critical** | no need toUsertransaction that isCanserious setArbitraryUserPassword | Token Predictable/ValidateStepCanskip through/Parametertamper changeDirectserious set |
| **High** | requiresless quantity condition that isCanserious set other personPassword | Host Header inject inject/CAPTCHABrute Forceno limit make/IDOR |
| **Medium** | Can attack attackorforge completeInformation Disclosure | UserEnumeration/Secureask problemDisclosure/SMS Bombing/Session notInvalidate |
| **Low** | impact response has limitorrequires condition | weakPasswordpolicy strategy/Referer Disclosure/CORS Misconfiguration |
| **Info** | Security Recommendations | missing less rate rate limit makeLog/CAPTCHAValidity PeriodToo Long |
