# cloud principle generate environment environmentConfigurationSecureCheckclear single

> Alibaba Cloud ACK (Kubernetes) + micro service architecture structure move specialitemsSecureassess assess
>
> Methodcomment base foundation:WooYun 22,132 real real vulnerabilityCase -- Configuration Domain 1,796 cases(72.6% High Risk)

---

## 1. total body risk determine judge

pass system part deploy movetocloud principle generate architecture structure, attack attack page initiate generate result structure ness change ize:

| Dimension | pass system part deploy | cloud principle generate architecture structure | new increase risk |
|------|---------|-----------|---------|
| Networkboundary boundary | clear confirmof DMZ/defense | level ize Pod Network, toward flow quantity increase | toward move dynamic complete version extremeLow |
| identity copyAuthentication | primary machine level SSH + ApplicationlayerAuthentication | ServiceAccount + RBAC + mTLS | credential according type mode increase long |
| Configurationmanage manage | mobile dynamic operations, Configurationcollectin | YAML clear mode, Configurationpart innumber percent resource sourcein | Configuration move/Secret Disclosure |
| expose exposure page | IP + Port | NodePort/LoadBalancer/Ingress/API Server | manage manage page expose exposure risk increase |
| provideshouldlink | RPM/DEB include | ContainerImage(base foundationImage + many layer depend rely) | Image /CVE pass |

**WooYun history history lesson lesson:** Configuration Domain 1,796 Casein, mostHighfrequencyofcause fatal mode is"Default Credentials + expose exposure manage manage boundary page".incloud principle generate environment environmentin, this mode map mapas:Kubernetes Dashboard Unauthorized Access/Docker Remote API expose exposure/etcd not add secret wild informationetc..

---

## 2. Kubernetes ClusterSecureCheck

### 2.1 API Server Hardening

| # | Check Item | Risk Level | Check Method | WooYun key connect mode |
|---|--------|---------|---------|----------------|
| K-01 | API Server whetherexpose exposureinPublic Internet | Severe | `kubectl cluster-info`;Check ALB/SLB Bindingof EIP | WooYun mode:expose exposureofmanage manage boundary page(Jenkins/JBoss ConsoleDirectexpose exposurePublic Internet, type ratio API Server expose exposure) |
| K-02 | nameAuthenticationwhether disabled | Severe | Check `--anonymous-auth=false` | Case References:"DaoCloudWeak Credentials+docker remote APIUnauthorized Access"-- Docker API No AuthenticationCausingContainer |
| K-03 | RBAC whether enabled(Non- ABAC) | High | `kubectl api-versions \| grep rbac` | Default Credentialsmodeof:no RBAC = All SA etc.sameAdministrator |
| K-04 | Admission Controller whetherConfiguration | High | Check `--enable-admission-plugins` whetherinclude include PodSecurity/NodeRestriction | missing less accurate inject control make = allow allow special permissionContainerpart deploy |
| K-05 | Audit Log whether enabled | High | Check `--audit-policy-file` and `--audit-log-path` | WooYun mode:missing monitor controlCausinginject long period notDiscover |
| K-06 | etcd wild informationwhetheradd secret + Authentication | Severe | Check etcd whether enabled `--client-cert-auth` and TLS | etcd StorageAllCluster Secret, not add secret = all quantity credential accordingDisclosure |

### 2.2 RBAC andPermissioncontrol make

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| K-07 | whether exists cluster-admin BindingtoNon-must need ServiceAccount | Severe | `kubectl get clusterrolebindings -o json \| jq '.items[] \| select(.roleRef.name=="cluster-admin")'` |
| K-08 | default ServiceAccount whetherself dynamic Token | High | Check Pod spec in `automountServiceAccountToken` whether is false |
| K-09 | whether existswild config symbolPermission(`*` verbs or `*` resources) | High | audit planAll ClusterRole/Role inofwild config symbol scale rule |
| K-10 | each fatal nameEmptybetweenwhether hasindependent standaloneof ServiceAccount | in | `kubectl get sa --all-namespaces`, Checkwhetherallinuseuse default SA |

**WooYun Casemap map:** WooYun Configuration Domainin"wild config symbolPermission(Action: "\*", Resource: "\*")"be listascloud IAM High RiskMisconfigurationmode.K8s RBAC inof `*` wild config symboland AWS/Alibaba Cloud IAM of `Action: "*"` essence related same -- reverse most smallPermissionprinciple rule.

### 2.3 Networkpolicy strategy

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| K-11 | whetherset define done NetworkPolicy | High | `kubectl get networkpolicy --all-namespaces`(Empty = All Pod wild) |
| K-12 | whetherreal deny-all default auth policy strategy | High | check whether there is `podSelector: {}` + Empty ingress ofdefault auth reject reject policy strategy |
| K-13 | manage manage fatal nameEmptybetween(kube-system)whetherandbusiness isolation | High | Check kube-system of NetworkPolicy whetherlimit make business Pod access ask |
| K-14 | Pod whethercanDirectaccess ask cloud Metadata API(169.254.169.254) | Severe | from Pod internal `curl http://169.254.169.254/latest/meta-data/`;Check IMDS defense protect |

**WooYun Casemap map:** Configuration Domainclear confirm list out"IMDS v1 Canaccess ask(no need tocommand card)"ascloudConfigurationHigh Riskitems.in ACK in, not limit make Pod access ask Metadata API, attack attack personCanPass SSRF orContainer Obtain RAM Role time credential according, etc.same for"Webhook SSRF access askInternal Network"mode.

### 2.4 Pod Secure

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| K-15 | whether existsspecial permissionContainer(privileged: true) | Severe | `kubectl get pods --all-namespaces -o json \| jq '.items[] \| select(.spec.containers[].securityContext.privileged==true) \|.metadata.name'` |
| K-16 | whetheras root operatelinesContainer | High | Check `runAsNonRoot: true` and `runAsUser` Configuration |
| K-17 | whether done primary machinePath(hostPath) | Severe | audit checkAll volume inof hostPath |
| K-18 | whether done Docker Socket | Severe | check whether there is `/var/run/docker.sock` |
| K-19 | whetherlimit make done Linux Capabilities | High | Check securityContext inwhether has `drop: ["ALL"]` + by need add |
| K-20 | whetherset set done resource source limit make(CPU/Memory Limits) | in | CheckAll Deployment of resources.limits whetherset set |
| K-21 | whether enableddone only read rootFileSystem | in | Check `readOnlyRootFilesystem: true` |

### 2.5 Secret manage manage

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| K-22 | Secret whetheras clear textStoragein etcd | Severe | Check `--encryption-provider-config` whetherConfiguration |
| K-23 | Secret whetherPassenvironment environment change quantity inject inject(whileNon- volume) | in | environment environment change quantity out currentin `/proc/1/environ`, beLog/coredump Disclosure |
| K-24 | whetheruseuseexternal partKeymanage manage(Alibaba Cloud KMS / External Secrets) | High | Checkwhethercollect complete KMS Provider or External Secrets Operator |
| K-25 | Git repository libraryinwhether existsclear text Secret YAML | Severe | inCoderepository libraryinsearch `kind: Secret` Fileinof base64 Encodingvalue |

**WooYun Casemap map:** Information Disclosuredomain 4,858 Casein, "Source Code/Configuration Disclosure"share most large ratiocases.Git repository libraryinofclear text Secret YAML(base64 not is add secret)etc.same for WooYun in"/.git/config expose exposureCausingall quantity source codeDisclosure"mode -- one repository libraryDisclosure, All Secret that is Invalidate.

### 2.6 Kubernetes Dashboard andmanage manage array item

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| K-26 | Kubernetes Dashboard whether | High | `kubectl get deploy -n kubernetes-dashboard` |
| K-27 | Dashboard whether enableddone skip Login | Severe | Check Dashboard part deployParameterinwhether has `--enable-skip-login` |
| K-28 | Dashboard ServiceAccount Permissionwhetherthrough large | Severe | Check Dashboard SA Bindingof ClusterRole |
| K-29 | Dashboard whetherexpose exposureinPublic Internet(NodePort/LoadBalancer) | Severe | `kubectl get svc -n kubernetes-dashboard` |

**WooYun DirectCase:** Configuration DomainDefault Credentialstableinclear confirmRecord"Kubernetes Dashboard(command cardBypass)"asMediumfrequency rate out currentofMisconfiguration.Case"DaoCloudWeak Credentials+docker remote APIUnauthorized Access"Direct show doneContainermanage manage boundary page expose exposureCausingContainer ofCompleteattack attack link.

---

## 3. Docker ImageSecureCheck

### 3.1 base foundationImageSecure

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| D-01 | base foundationImagewhethercome selfCaninformation source(method / business ACR) | High | audit checkAll Dockerfile of FROM specified command |
| D-02 | base foundationImagewhetheruseuseFixed tag(Non- latest) | High | Dockerfile inwhether is `FROM image:latest` |
| D-03 | base foundationImagewhether ismost small ize(alpine / distroless / scratch) | in | CheckImageinwhetherinclude include shell/include manage manage deviceetc.Non-must needTool |
| D-04 | base foundationImagewhether existsalready notify CVE | High | useuse Trivy/Grype Scan:`trivy image <image>` |

### 3.2 structure createSecure

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| D-05 | Dockerfile inwhether hashardEncodingcredential according | Severe | search ENV/ARG inofPassword/API Key/Token |
| D-06 | whetheruseusemanyPhasestructure create(avoidDisclosurestructure createToolandsource code) | in | Check Dockerfile whether has `FROM... AS builder` mode |
| D-07 | whetherasNon- root Useroperatelines(USER specified command) | High | Check Dockerfile most afterwhether has `USER nonroot` |
| D-08 | whether exists.dockerignore rank remove sensitive sensitiveFile | High | Check.dockerignore whetherrank remove.git/.env/*.key etc. |
| D-09 | ImagelayerwhetherDisclosureinbetween credential according | Severe | `docker history <image>` check whether there is secret retaininsome one layer |

**WooYun Casemap map:** Information Disclosuredomainin"version version control makeDisclosure(/.git/config)"and"prepare copyFileDisclosure"modeinContainerscenario scene under map mapas:not useuse.dockerignore Causing.git directory record/ConfigurationFilebe break include advanceImage.attack attack person takeImageafter that isCanObtainCompletesource codeandcredential according.

### 3.3 Imagerepository librarySecure

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| D-10 | ACR(ContainerImageservice)whether enabledPublic InternetAccess Control | High | Alibaba CloudConsoleCheck ACR realcasesofNetworkaccess ask policy strategy |
| D-11 | Image takewhetherstrong make useuse imagePullSecrets | High | Check Pod spec inwhetherConfiguration imagePullSecrets |
| D-12 | whether enabledImageSignatureValidate(Notation / Cosign) | in | Checkwhetherpart deploySignatureValidate Admission Webhook |
| D-13 | whetherConfigurationImagevulnerability self dynamicScan | High | ACR SecureScanfunction canwhether enabled |
| D-14 | whetherlimit makecan only take specified set repository libraryofImage | in | Check OPA/Kyverno policy strategywhetherlimit make image registry |

### 3.4 operatelinestimeSecure

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| D-15 | Containeroperatelinestimewhether isSecureversion version(containerd/CRI-O) | High | `kubectl get nodes -o wide` View Container Runtime |
| D-16 | whether enabled Seccomp Profile | in | Check Pod annotation or securityContext inof seccompProfile |
| D-17 | whether enabled AppArmor / SELinux | in | Checksection point levelSecuremodel blockConfiguration |
| D-18 | whether existsContainer Path | Severe | combineCheck:privileged + hostPID + hostNetwork + hostPath + docker.sock |

---

## 4. Service Mesh SecureCheck(Istio / ASM)

### 4.1 mTLS Configuration

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| SM-01 | whether enabled STRICT mTLS(Non- PERMISSIVE) | Severe | `kubectl get peerauthentication --all-namespaces`;PERMISSIVE mode allow allow clear text wild information |
| SM-02 | whether hasfatal nameEmptybetween level levelof mTLS cover cover | High | Checkeach fatal nameEmptybetweenwhether hascover cover all global STRICT as PERMISSIVE ofConfiguration |
| SM-03 | cert certificate rotate changewhethercorrect common tool operation | High | Check Citadel/istiod ofcert certificateValidity Periodandself dynamic rotate changeConfiguration |

### 4.2 Authorizationpolicy strategy

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| SM-04 | whetherset define done AuthorizationPolicy | High | `kubectl get authorizationpolicy --all-namespaces`(Empty = Allservice wild) |
| SM-05 | whether exists allow-all policy strategy | Severe | check whether there is `action: ALLOW` + Empty rules ofpolicy strategy |
| SM-06 | sensitive sensitive servicewhether hasdetail degreeofAccess Control | High | Databasecode manage/Paymentserviceetc.whetherlimit make doneCallsource |
| SM-07 | whetherlimit make done egress flow quantity | in | Check ServiceEntry and Sidecar of egress Configuration |

**WooYun Casemap map:** Authorization Domainin"Authorization Bypass"(1,705 cases, 62.3% High Risk)ofaudit core mode is"missing Serverappraise permission, information anyClientidentity copy".in Service Mesh scenario scene under, missing less AuthorizationPolicy etc.same for:any be attack flawof Pod all canCallClusterinternalArbitraryservice, toward move dynamic zero complete version.

### 4.3 Sidecar inject injectandnetwork formatCompleteness

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| SM-08 | whetherAllbusiness Pod all inject inject done Sidecar | High | `kubectl get pods --all-namespaces -o json \| jq '.items[] \| select(.spec.containers \| length == 1) \|.metadata.name'` |
| SM-09 | whether has Pod Pass annotation skip through inject inject | High | search `sidecar.istio.io/inject: "false"` |
| SM-10 | Envoy manage managePort(15000/15004)whetherexpose exposure | High | Check Envoy admin InterfacewhetherCanbeNon- localhost access ask |

---

## 5. API GatewaySecureCheck

### 5.1 Authenticationandappraise permission

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| GW-01 | All API routewhetherallConfigurationdoneAuthentication | Severe | one by oneCheckGatewayrouteConfiguration, IdentifyNot BoundAuthentication itemofroute |
| GW-02 | JWT ValidatewhetherinGatewaylayerExecute | High | CheckGatewaywhetherConfiguration JWT Validate item + Keycome source |
| GW-03 | whether existsBypassGatewayDirectaccess askBackendserviceofPath | Severe | CheckBackend Service typewhether is ClusterIP(Non- NodePort/LoadBalancer) |
| GW-04 | API Key / OAuth Token whetherinGatewaylayerValidate | High | test no Token Requestwhetherbe reject reject |

**WooYun DirectCase:** Case"ChinaCachea systemJBossMisconfiguration Leading ToGetshell"ofaudit core ask problem is manage manageConsoleDirectexpose exposure and useuseDefault Credentials.inmicro service architecture structurein, BackendservicePass NodePort expose exposure whileNon-onlyPassGatewayroute, etc.same forBypassdoneAllGatewaylayerSecurepolicy strategy.

### 5.2 flow quantity control make

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| GW-05 | whetherConfigurationdoneRate Limiting(Rate Limiting) | High | CheckGatewayofRate Limiting itemConfiguration |
| GW-06 | whetherConfigurationdoneRequest Bodylarge small limit make | in | Check `client_max_body_size` oretc.validConfiguration |
| GW-07 | whether enableddone WAF defense protect | in | CheckAlibaba Cloud WAF whetherconnect injectGateway |
| GW-08 | whetherConfigurationdone IP /Whitelist | in | manage manage API whetherlimit make come source IP |

### 5.3 Information Disclosuredefense protect

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| GW-09 | ResponseHeaderwhetherDisclosureBackendinformation | in | Check Server/X-Powered-By/X-Real-Server etc.Header |
| GW-10 | errorResponsewhetherDisclosureinternal part | High | Send Request, Check 502/503 Responseinwhetherexpose exposure internal part service name/IP |
| GW-11 | Swagger/OpenAPI Documentwhetherexpose exposureingenerate asset environment environment | High | access ask `/swagger-ui.html`/`/api-docs`/`/openapi.json` |
| GW-12 | debuggingEndpointwhetherCanfromexternal part access ask | Severe | Check `/actuator`/`/debug`/`/metrics` whetherPassGatewayexpose exposure |

**WooYun Casemap map:** Information Disclosuredomainin"debugging/testEndpoint"isHighfrequencyDisclosuretoward quantity.Casein Spring Boot Actuator(No Authentication by Default, Criticalfrequency rate out current)inmicro serviceinbe large quantity useuse. `/actuator/env`(Disclosureenvironment environment change quantity includeDatabasePassword)and `/actuator/heapdump`(Disclosureinternal existinofcredential according)PassGatewayexpose exposuretoPublic Internet, willDirectCausingall quantity credential accordingDisclosure.

### 5.4 CORS andcross domain

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| GW-13 | CORS whetheruseusewild config symbol `*` | High | Check Access-Control-Allow-Origin Configuration |
| GW-14 | CORS whetherallow allow with credential according(credentials: true + wild config symbol) | Severe | two person same time existin = Arbitrary point takeUserData |
| GW-15 | whetherfor expected checkRequesthas combine manage exist | Low | Check Access-Control-Max-Age set set |

---

## 6. Object Storage(OSS)SecureCheck

### 6.1 Bucket Access Control

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| OSS-01 | whether existscompany open read/writeof Bucket | Severe | `aliyun oss ls` + one by oneCheck Bucket ACL and Bucket Policy |
| OSS-02 | Bucket Policy whether exists `Principal: "*"` | Severe | audit checkAll Bucket Policy JSON |
| OSS-03 | whetheruseuse STS time credential according(whileNon- AK/SK) | High | CheckApplicationCodein OSS Clientof initial ize method mode |
| OSS-04 | UploadPathwhetherPredictable/CanEnumeration | High | CheckFilefatal name policy strategywhetheruseuse UUID/ machine character symbol string |

**WooYun Directmap map:** Configuration Domain"cloudMisconfiguration"modeinclear confirm list out"OSS(Alibaba Cloud)Storage ACL Misconfiguration".same time, Case"Tongcheng Travel system misconfiguration allowed arbitrary file uploadgetshell/rootPermission" show doneUploadfunction canMisconfigurationsuch aswhatCausing RCE -- in OSS scenario scene under notDirect RCE, but company open writeof Bucket Canbe inject meaningFile, result combine CDN part initiate rule impact responseAllUser.

### 6.2 Dataprotect protect

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| OSS-05 | sensitive sensitiveData Bucket whether enabledServeradd secret(SSE-KMS) | High | Check Bucket add secretConfiguration |
| OSS-06 | whether enabledversion version control make(defense error delete/ search) | in | Check Bucket version version control makeStatus |
| OSS-07 | whetherConfigurationdone generate fatal cycle period policy strategy(Log/ timeFileself dynamic clear manage) | in | Check Lifecycle scale rule |
| OSS-08 | Signature URL ofValidity Periodwhethercombine manage(< 1 hours) | High | audit checkCodein `generate_presigned_url` of expires Parameter |
| OSS-09 | whetherConfigurationdone defense link(Referer Whitelist) | in | Check Bucket Referer Configuration |

### 6.3 Logandmonitor control

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| OSS-10 | whether enabled OSS access askLog | High | Check Bucket Logging Configuration |
| OSS-11 | whetherfor abnormal common access ask mode report alert(BatchDownload/Scan) | in | Check SLS/CloudMonitor report alert scale rule |

---

## 7. Alibaba Cloud RAM(IAM)SecureCheck

### 7.1 AccountandPermission

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| IAM-01 | rootAccountwhether enabled MFA | Severe | ConsoleCheckrootAccountSecureset set |
| IAM-02 | whether existswild config symbolPermissionpolicy strategy(`Action: "*"`, `Resource: "*"`) | Severe | audit checkAllself set define Policy |
| IAM-03 | RAM Userwhetheruseuseindependent standalone AK/SK(Non-rootAccount) | Severe | CheckrootAccountwhetherCreatedone AccessKey |
| IAM-04 | long period not useuseof AK/SK whetherclear manage | High | Check AccessKey most after useusetime between |
| IAM-05 | crossAccountRoleinformation any policy strategywhetherthrough for | High | audit check AssumeRole information any policy strategyinof Principal |
| IAM-06 | serviceAccount AK/SK whetherhardEncodinginCode/Imagein | Severe | CodelibraryandImagelayer search LTAI openHeaderofcharacter symbol string |

**WooYun Casemap map:** Configuration Domainclear confirm list out"wild config symbolPermission(Action: "\*", Resource: "\*")"and"serviceAccountKeyexpose exposureinCode/Configurationin"ascloud IAM High Riskmode.Case"Sunshine InsuranceSensitive InformationDisclosureCausingSuccessadvance injectInternal NetworkSystem(vertical many platform operations primary machine)" show done credential accordingDisclosuresuch aswhatCausing toward move dynamic -- inCloud Environmentin, Disclosureof AK/SK etc.same for taketodone forshould RAM UserofAllPermission.

---

## 8. CI/CD flow horizontal lineSecureCheck

### 8.1 structure create environment environment

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| CI-01 | CI/CD Tool(Jenkins/GitLab Runner)whetherexpose exposureinPublic Internet | Severe | Check CI serviceofNetworkexpose exposure page |
| CI-02 | CI/CD credential accordingwhetheruseuse Secret manage manage(Non-clear text) | Severe | audit check Pipeline Configurationinofcredential according citeusemethod mode |
| CI-03 | structure create section pointwhetherandgenerate asset environment environmentNetworkisolation | High | Check CI Runner ofNetwork |
| CI-04 | whetherfor combine inject primary ofCodestrong make Code Review | in | Checkpart support protect protect scale rule |
| CI-05 | whethercollect complete SAST/SCA Scan | in | Check Pipeline inwhether hasSecureScanStep |

**WooYun DirectCase:** Configuration DomainDefault Credentialstablein Jenkins(No Authentication by Default, Criticalfrequency rate)characters list.Case"ChinaCachea systemJBossMisconfiguration Leading ToGetshell"ofmode complete all suitableusefor Jenkins:expose exposure manage manageConsole + default auth/weakCredential = Pass Script Console Direct RCE.

### 8.2 provideshouldlinkSecure

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| CI-06 | depend rely includewhether hasvulnerabilityScan | High | Checkwhethercollect complete Snyk/Trivy/Grype etc. SCA Tool |
| CI-07 | whetheruseuseprivate has depend rely code manage(defense depend rely mix attack attack) | in | Check npm/pip/maven whetherConfigurationprivate has registry priority first |
| CI-08 | Imagewhetherininfer first advancelinesvulnerabilityScan | High | Check Pipeline in image push firstwhether hasScanStep |

---

## 9. Log/monitor controlandshouldResponse

### 9.1 Logcollect collect

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| LOG-01 | Clusteraudit planLogwhetherconnect inject SLS | High | Check ACK audit planLogConfiguration |
| LOG-02 | ApplicationLogwhethercollectincollect collect | in | Check DaemonSet Log collect device(Logtail/Filebeat) |
| LOG-03 | Loginwhetherleak sensitive(not includePassword/Token/Identity Cardnumber) | High | CheckLogcontent |
| LOG-04 | Logprotect retain period limitwhether combine scale need require(>=180 days) | in | Check SLS Logstore protect retain policy strategy |

### 9.2 Securereport alert

| # | Check Item | Risk Level | Check Method |
|---|--------|---------|---------|
| LOG-05 | whether enabledAlibaba CloudSecureincore(cloudSecure) | High | CheckSecureincore Agent part deployStatus |
| LOG-06 | K8s abnormal commonlinesascheck testwhether enabled | High | Checkwhetherpart deploy Falco oruseuse ACK Securecan power |
| LOG-07 | whether hasContainer check test | Severe | CheckoperatelinestimeSecurepolicy strategyandreport alert scale rule |
| LOG-08 | SecureeventshouldResponseflow processwhetherset define | in | check whether there isDocumentizeof IR flow process |

---

## 10. CheckExecutePriority

based on WooYun 72.6% High RiskrateofConfiguration DomainDataandcloud principle generate special has risk, create protocol bythe followingPriorityExecute:

### P0 -- standalone that isCheck(attack that is all flaw)

| Check Item | Reason |
|--------|------|
| K-01 API Server Public Exposure | etc.same for Databasemanage manage boundary page Public Internet, WooYun Default Credentialsmode |
| K-14 Pod access ask Metadata API | IMDS credential accordingDisclosure = RAM RolePermissionall |
| K-22 Secret clear textStorage etcd | etc.same forConfigurationFileinofclear textPassword |
| K-25 Git inofclear text Secret | WooYun.git Disclosuremodeof K8s version version |
| OSS-01 company open read write Bucket | WooYun cloudMisconfigurationmode, DirectDataDisclosure |
| IAM-02 wild config symbol RAM Permission | WooYun IAM wild config symbolPermissionmode |
| D-18 Container Path | privileged + hostPath + docker.sock three item |

### P1 -- 48 hoursinternal complete(Canbe exploituseadvancelines toward move dynamic)

| Check Item | Reason |
|--------|------|
| K-07 cluster-admin through degreeAuthorization | one Pod flaw = ClusterAdministrator |
| K-11 missing less NetworkPolicy | toward move dynamic zero complete version |
| SM-01 mTLS Non- STRICT | inbetween person attack attack / flow quantity |
| GW-03 BackendserviceBypassGatewayCanreach | BypassAllAuthentication / WAF |
| CI-01 Jenkins expose exposurePublic Internet | WooYun Jenkins No Authentication by Default -> RCE |
| GW-12 Actuator Public InternetCanreach | credential accordingDisclosure + internal exist transfer |

### P2 -- one cycle internal complete(manipulate deep defense defense layer)

AllMediumriskitems + monitor control report alert body system create set.

---

## Appendix A:WooYun Caseandcloud principle generate risk map map total table

| WooYun principle initial mode | Case Count | cloud principle generateetc.valid risk | version clear single forshouldCheck Item |
|----------------|-------|--------------|----------------|
| Default Credentials(Tomcat/JBoss/Jenkins/Redis/MongoDB) | Criticalfrequency | K8s Dashboard skip login/Grafana admin/admin/etcd No Authentication | K-27, K-06 |
| Docker Remote API Unauthorized | Highfrequency | Containeroperatelinestime API expose exposure/special permissionContainer | D-18, K-15, K-18 |
| manage manage boundary page expose exposurePublic Internet | Criticalfrequency | API Server/Dashboard/Jenkins/Actuator Public InternetCanreach | K-01, K-29, CI-01, GW-12 |
| Source Code/Configuration Disclosure(.git/.svn/prepare copyFile) | 4,858 cases | Git inclear text Secret/Dockerfile hardEncodingcredential according/Imagelayer retain | K-25, D-05, D-08, D-09 |
| CORS wild config symbol | Highfrequency | API Gateway CORS Misconfiguration | GW-13, GW-14 |
| debuggingEndpointexpose exposure(Actuator/phpinfo/debug) | Criticalfrequency | Spring Boot Actuator PassGatewayexpose exposure | GW-11, GW-12 |
| wild config symbol IAM Permission | Highfrequency | RAM `Action: "*"` + K8s RBAC `*` verbs | IAM-02, K-09 |
| cloudStorage ACL Misconfiguration | Highfrequency | OSS Bucket company open read/write | OSS-01, OSS-02 |
| SSRF -> Internal Networkaccess ask | Highfrequency | Pod SSRF -> Metadata API -> RAM time credential according | K-14 |
| Personal InformationDisclosure(API through degreeObtain/LogCanaccess ask) | 1,588 cases | Lognot leak sensitive/API Responsethrough degreeReturn | LOG-03, GW-10 |

---

## Appendix B:self dynamic izeCheckToolinfer

| Tool | Purpose | collect complete method mode |
|------|------|---------|
| **kube-bench** | CIS Kubernetes Benchmark combine scaleCheck | part deployas Job, set period operatelines |
| **kube-hunter** | K8s test(Discoverexpose exposure page) | fromClusterexternal partandinternal part part level operatelines |
| **Trivy** | Image CVE + K8s Configurationaudit plan + Secret Scan | CI Pipeline + Operator mode |
| **Falco** | operatelinestime abnormal commonlinesascheck test(Container /abnormal common advance process) | DaemonSet part deploy |
| **OPA/Kyverno** | Policy as Code(accurate inject control make) | Admission Webhook |
| **kubeaudit** | K8s resource sourceSecureaudit plan | set periodScan + CI collect complete |
| **Prowler** | Alibaba CloudSecurity Configurationaudit plan(type AWS ScoutSuite) | set period operatelines, output out report |

---

## Appendix C:audit core principle rule(source self WooYun 1,796 MisconfigurationCase)

1. **EachserviceofDefault Configurationall isas exploit whileNon-Secureset planof** -- such asif no has clear confirmHardening, existinvulnerability
2. **manage manage boundary page + Default Credentials = remote processCodeExecute** -- thisin WooYun time code is Tomcat/JBoss/Jenkins, incloud principle generate time code is Dashboard/etcd/Envoy Admin
3. **credential according not attribute forCoderepository library** -- no comment is.env File is K8s Secret YAML, base64 not is add secret
4. **Networkisolation is mostValidofConfigurationSecure ** -- manage manage boundary page only limitInternal Networkaccess ask, this one condition can message remove 50% or moreofConfigurationtype vulnerability
5. **most smallPermissionnot is create protocol, is line** -- RBAC wild config symbol/RAM `Action: "*"`/privileged Container, each one all is attack attack personofprovide permission skip template
