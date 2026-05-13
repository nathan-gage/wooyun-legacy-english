# cloud principle generate environment environmentConfigurationSecureCheckclear single

> suitableusescenario scene:pass system business move Alibaba Cloud ACK(Kubernetes)+ micro service architecture structure
> cover coverScope:K8s Cluster/Docker Image/Service Mesh/API Gateway/OSS Object Storage/CI/CD/Logaudit plan

---

## 1. Kubernetes ClusterSecure

### 1.1 ClusterAccess Control

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| API Server whetherexpose exposurePublic Internet | Severe | `kubectl cluster-info`;ACK ConsoleViewClusteraccess ask mode | onlyInternal Networkaccess ask, orPass SLB + IP Whitelistlimit make |
| API Server name access askwhetherkey close | Severe | `kubectl auth can-i --list --as=system:anonymous` | Anonymous Userno anyPermission |
| whether enabled RBAC | Severe | `kubectl api-versions \| grep rbac` | existin `rbac.authorization.k8s.io/v1` |
| whether exists cluster-admin abuseuse | High | `kubectl get clusterrolebindings -o json \| jq '.items[] \| select(.roleRef.name=="cluster-admin") \|.subjects'` | only limitAdministrator SA andmust need array itemBinding |
| kubeconfig FilePermission | High | CheckAlloperations person version `~/.kube/config` Permissioninvolving part initiate method mode | 600 Permission, disable stop clear text shared, useuse RAM subAccount + kubeconfig generate complete |
| whether enabledaudit planLog | High | ACK Console -> Clustermanage manage -> Logaudit plan | already open enable, audit planLog recursive SLS |
| Dashboard whetherexpose exposure | Severe | `kubectl get svc -n kubernetes-dashboard` | not existinoronly ClusterIP, disable stop NodePort/LoadBalancer |
| etcd whetheradd secretStorage | High | ACK manage version default auth add secret;self createClusterCheck `--encryption-provider-config` | Secret Data state add secret |

### 1.2 Pod Securepolicy strategy

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| whetheruseuse Pod Security Standards (PSS) | Severe | `kubectl get ns -o jsonpath='{range.items[*]}{.metadata.name}: {.metadata.labels.pod-security\.kubernetes\.io/enforce}{"\n"}{end}'` | generate asset namespace set setas `restricted` or `baseline` |
| Containerwhetheras root operatelines | Severe | `kubectl get pods -A -o jsonpath='{range.items[*]}{.metadata.namespace}/{.metadata.name}: runAsUser={.spec.containers[*].securityContext.runAsUser}{"\n"}{end}'` | AllbusinessContainer `runAsNonRoot: true`, specified setNon-zero UID |
| whether enabledspecial permissionContainer | Severe | `kubectl get pods -A -o json \| jq '.items[] \| select(.spec.containers[].securityContext.privileged==true) \|.metadata.name'` | no special permissionContainer(only allow allow base foundation set array itemcasesexternal) |
| whether hostPath | High | `kubectl get pods -A -o json \| jq '.items[] \| select(.spec.volumes[]?.hostPath!= null) \| "\(.metadata.namespace)/\(.metadata.name)"'` | business Pod not hostPath |
| whetherlimit make capabilities | High | Check `securityContext.capabilities.drop` | AllContainer `drop: ["ALL"]`, only by need add |
| whetherset set readOnlyRootFilesystem | in | Check Pod spec | create protocol enableuse, need write injectofdirectory recorduse emptyDir/volume |
| whetherlimit make hostNetwork/hostPID/hostIPC | Severe | `kubectl get pods -A -o json \| jq '.items[] \| select(.spec.hostNetwork==true or.spec.hostPID==true or.spec.hostIPC==true)'` | business Pod not useuse host fatal nameEmptybetween |
| whetherConfiguration seccomp profile | in | Check `securityContext.seccompProfile` | set setas `RuntimeDefault` orself set define profile |

### 1.3 Networkpolicy strategy

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| whether enabled NetworkPolicy | High | `kubectl get networkpolicy -A` | Eachbusiness namespace at leasthas default auth reject reject policy strategy |
| default auth reject reject inject flow quantity | High | Checkwhether exists `default-deny-ingress` policy strategy | existin, Allinject need display mode releaselines |
| default auth reject reject out flow quantity | in | Checkwhether exists `default-deny-egress` policy strategy | existin, DNS (53) andmust need external part service display mode releaselines |
| cross namespace access askwhetheraffected control | High | Check NetworkPolicy of `namespaceSelector` | only allow allow must needofcross namespace wild information |
| CNI itemwhethersupport hold NetworkPolicy | High | ACK Cluster CNI type(Terway/Flannel) | useuse Terway Network item(principle generate support hold NetworkPolicy) |

### 1.4 resource sourceandisolation

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| whetherset set Resource Limits/Requests | High | `kubectl get pods -A -o json \| jq '.items[] \| select(.spec.containers[].resources.limits == null)'` | AllContainerset set CPU/Memory limits |
| whetherConfiguration LimitRange | in | `kubectl get limitrange -A` | Each namespace Configurationdefault auth limit make |
| whetherConfiguration ResourceQuota | in | `kubectl get resourcequota -A` | generate asset namespace Configurationconfig amount above limit |
| namespace isolation | High | `kubectl get ns` | by business/environment environment/ part namespace, Non- default part deploy |
| section point isolation | in | ACK Console -> section point | key business useuseindependent standalone section point + pollution point(Taint) debug degree |

---

## 2. Docker ImageSecure

### 2.1 Imagecome sourceandstructure create

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| base foundationImagewhethercome sourceCaninformation | Severe | audit checkAll Dockerfile of FROM specified command | useuseAlibaba Cloud ACR methodImageorinternal part base foundationImage, disable stop `latest` tag |
| base foundationImagewhethermost small ize | High | Checkbase foundationImagetype | useuse `alpine`/`distroless`/`slim` variant, Non-Complete OS Image |
| whetheruseusemanyPhasestructure create | in | audit check Dockerfile | compile Toollink not advance inject most finalImage |
| whetherFixedImageversion version | High | Check FROM anddepend rely version version | useuseconfirm setof tag + digest(such as `nginx:1.25.3@sha256:...`) |
| structure create timewhetherDisclosureSensitive Information | Severe | audit check Dockerfile inof COPY/ADD/ENV/ARG | noKey/cert certificate/ConfigurationFilehardEncoding;useuse BuildKit `--secret` |
|.dockerignore whethercomplete | in | Check Itemdirectory root directory record `.dockerignore` | rank remove `.git`/`.env`/`node_modules`/KeyFileetc. |

### 2.2 ImageScanandaccurate inject

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| ACR ImagevulnerabilityScan | Severe | Alibaba CloudContainerImageservice -> SecureScan | AllImageno Critical/High CVE, set periodScan |
| whether enabledImageSignature | High | ACR business version -> content information any | enableuse Cosign/Notation Signature, part deploy firstValidate |
| ClusterImageaccurate inject control make | Severe | Check ACK Imageaccurate injectConfigurationor OPA/Kyverno policy strategy | only allow allowfromspecified set ACR repository library takeImage |
| Imagerepository library access askPermission | High | ACR -> Access Control | most smallPermissionprinciple rule, open initiate/generate asset environment environment isolation repository library |
| whetheruseuse root Useroperatelines | Severe | Dockerfile inCheck USER specified command | existin `USER nonroot` ornumber character UID |

### 2.3 operatelinestimeSecure

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| Containeroperatelinestime version version | High | `kubectl get nodes -o wide`(CONTAINER-RUNTIME list) | containerd >= 1.7, no already notify CVE |
| whether enabledoperatelinestimeSecuremonitor control | High | Checkwhetherpart deploy cloudSecureincoreContainerSecureor Falco | abnormal commonlinesas(reverse shell/abnormal common advance process)real time report alert |
| ContainerFileSystemCompleteness | in | Check `readOnlyRootFilesystem` + operatelinestime monitor control | operatelinestimeFilechange updateCancheck test |

---

## 3. Service Mesh Secure(Istio/ASM)

### 3.1 mTLS andflow quantity add secret

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| whetherall global enableuse mTLS STRICT mode | Severe | `kubectl get peerauthentication -A` | existin mesh level level `STRICT` mode policy strategy |
| whether exists PERMISSIVE mode service | High | `kubectl get peerauthentication -A -o yaml \| grep -A5 mtls` | no long period PERMISSIVE Configuration(only move through period allow allow) |
| cert certificate rotate change cycle period | in | Check Istio/ASM cert certificateConfiguration | cert certificateValidity Period <= 24h, self dynamic rotate change |
| external part flow quantity inject interface TLS | Severe | `kubectl get gateway -A -o yaml` | Ingress Gateway strong make TLS 1.2+, ConfigurationValidcert certificate |

### 3.2 Authorizationpolicy strategy

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| whetherConfiguration AuthorizationPolicy | Severe | `kubectl get authorizationpolicy -A` | Eachservice has display modeAuthorizationpolicy strategy, default auth reject reject |
| whether exists allow-all policy strategy | Severe | audit checkAll AuthorizationPolicy of rules | no `action: ALLOW` + Empty rules(etc.same allow-all) |
| service betweenCallwhetherbased on identity copyValidate | High | Check `principals`/`namespaces` Field | based on ServiceAccount identity copy do detail degreeAuthorization |
| external partRequest JWT Validate | High | `kubectl get requestauthentication -A` | external part API Requeststrong make JWT Validate, Configuration issuer and jwksUri |

### 3.3 Sidecar Configuration

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| Sidecar inject injectwhetherall cover cover | High | `kubectl get ns -L istio-injection` | Allbusiness namespace identifier record `istio-injection=enabled` |
| whetherlimit make Sidecar out Scope | in | `kubectl get sidecar -A` | Configuration `egress.hosts` limit makeCanaccess askofexternal part service |
| Envoy manage managePortwhetherexpose exposure | High | Check 15000/15004 PortCanreach ness | only localhost access ask, notCanfromClusterexternaltoreach |

---

## 4. API GatewaySecure

### 4.1 Authenticationandappraise permission

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| All API whetherstrong makeAuthentication | Severe | audit checkGatewayrouteConfiguration | remove CheckexternalAllroute needAuthentication(OAuth2/JWT/API Key) |
| JWT Keymanage manage | Severe | Check JWT signing key Storagecharacters set | Storagein KMS/Secret Manager, Non-environment environment change quantityorConfigurationFile |
| API Key rotate change machine make | High | Check Key manage manage policy strategy | support hold many Key total exist, set period rotate change, Canthat is time |
| whetherreal RBAC/ABAC | High | audit checkAuthorizationpolicy strategyConfiguration | DifferentRole/Tenantaccess askDifferent API sub collect |

### 4.2 flow quantity defense protect

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| whetherConfigurationRate Limiting(Rate Limiting) | High | CheckGatewayRate Limitingpolicy strategy | byUser/IP/API degreeRate Limiting, defense stop resource source |
| whether enabled WAF | High | Alibaba Cloud WAF -> defense protectConfiguration | BindingGateway SLB, enableuse SQL inject inject/XSS/RCE defense protect scale rule |
| Request Bodylarge small limit make | in | CheckGateway `client_max_body_size` oretc.priceConfiguration | limit make combine manage large small(such as 10MB), defense stop large include attack attack |
| whetherthrough filter sensitive sensitive Header | in | CheckGateway header handle manage scale rule | move remove/not transfer initiate `X-Forwarded-For` forgery/internal part header |
| CORS Configuration | in | Check `Access-Control-Allow-Origin` | Non- `*`, Whitelistspecified set allow allowofDomain Name |
| super timeandserious test policy strategy | in | CheckGatewayall global/route level level super time | continuous connect super time <= 5s, Requestsuper time <= 30s, serious test <= 3 times |

### 4.3 TLS Configuration

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| mostLow TLS version version | High | `nmap --script ssl-enum-ciphers -p 443 <gateway-domain>` | TLS >= 1.2, disableuse SSLv3/TLS 1.0/1.1 |
| cert certificateValidness | Severe | `echo \| openssl s_client -connect <domain>:443 2>/dev/null \| openssl x509 -dates` | cert certificate not expired, self dynamic continue periodConfigurationcorrect common |
| HSTS Header | in | `curl -I https://<domain>` | Return `Strict-Transport-Security: max-age=31536000; includeSubDomains` |
| HTTP self dynamic skip transfer HTTPS | High | `curl -I http://<domain>` | 301/308 skip transfer HTTPS |

---

## 5. Object Storage(OSS)Secure

### 5.1 Bucket Access Control

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| Bucket whethercompany openCanread | Severe | `aliyun oss stat oss://<bucket>` orConsoleCheck ACL | ACL as `private`, Non- `public-read`/`public-read-write` |
| Bucket Policy whetherthrough for | Severe | Console -> Bucket -> Permissionmanage manage -> Bucket Policy | no `"Effect": "Allow", "Principal": "*"` ofpolicy strategy |
| whether enabledServeradd secret(SSE) | High | `aliyun oss bucket-encryption --method get --bucket <bucket>` | enableuse SSE-KMS or SSE-OSS |
| cross domain(CORS)Configuration | in | Console -> Bucket -> cross domain set set | `AllowedOrigin` Non- `*`, limit set businessDomain Name |
| Referer defense link | in | Console -> Bucket -> defense link | Configuration Referer Whitelist, disable stopEmpty Referer |
| whetheropen enable version version control make | in | Console -> Bucket -> version version control make | serious needData Bucket enableuseversion version control make |
| whetherConfigurationgenerate fatal cycle period policy strategy | Low | Console -> Bucket -> generate fatal cycle period | timeFileself dynamic expiredDelete, history history version version set period clear manage |

### 5.2 access askLogandmonitor control

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| whetheropen enable access askLog | High | Console -> Bucket -> Logmanage manage | enableuse, LogStoragetoindependent standaloneofLog Bucket |
| abnormal common access ask report alert | in | cloud monitor control -> OSS monitor control | Configurationabnormal commonDownloadquantity/Requestquantity report alert |
| STS timeCredentialaccess ask | High | audit checkApplicationCodein OSS Client initial ize method mode | useuse STS AssumeRole timeCredential, Non-long period AK/SK |

### 5.3 DataSecure

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| pass output add secret | High | Check OSS endpoint protocol protocol | strong make useuse HTTPS endpoint |
| sensitive sensitiveDataCategoryStorage | High | audit check Bucket scale | PII/FinancialDataindependent standalone Bucket, add strongAccess Control |
| whether existssensitive sensitiveFileDisclosure | Severe | Enumeration Bucket File(such as `.env`/`backup.sql`/KeyFile) | noConfigurationFile/prepare copy/Keyetc.sensitive sensitiveData |

---

## 6. Secrets manage manage

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| K8s Secret whetheradd secretStorage | High | ACK Console -> Secret add secret | enableuse KMS add secret etcd inof Secret |
| whetheruseuseexternal part Secret manage manage | High | Checkwhethercollect completeAlibaba Cloud KMS/credential according manage | sensitive sensitive credential accordingPass External Secrets Operator or CSI Secret Store inject inject |
| Secret whetheras environment environment change quantity inject inject | in | Check Pod spec | priority first volume mount whileNon- env(env Cancan beLog/core dump Disclosure) |
| Secret access askwhether has RBAC limit make | High | `kubectl auth can-i get secrets -A --as=<sa>` | onlyAuthorizationof ServiceAccount Canaccess ask forshould namespace of Secret |
| whether existshardEncodingcredential according | Severe | Coderepository libraryScan(git-secrets/trufflehog) | noPassword/Token/AK/SK hardEncodinginCodeorConfigurationin |
| Imageinwhetherinclude include credential according | Severe | `docker history --no-trunc <image>` audit check layer | no layer include includeKeyFileorsensitive sensitive environment environment change quantity |

---

## 7. CI/CD flow horizontal lineSecure

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| flow horizontal line credential according manage manage | Severe | Check CI/CD change quantityConfiguration | useuse protected/masked change quantity, Non-clear text |
| structure create environment environment isolation | High | Check Runner/Agent Configuration | eachtimesstructure create useuseindependent standaloneContainer, structure create after |
| make productCompleteness | High | CheckwhetherSignaturemake product | Image push afterSignature, part deploy firstValidate |
| part deployPermissionmost small ize | Severe | Check CI/CD useuseof K8s credential according | ServiceAccount only hasTarget namespace of deployment UpdatePermission |
| part support protect protect | High | Coderepository library set set | main/master part support need Code Review + CI Pass can combine and |
| depend relySecureScan | High | Checkflow horizontal lineStep | collect complete SCA Tool(such as Trivy/Snyk)Scandepend rely vulnerability |
| SAST stateAnalyze | in | Checkflow horizontal lineStep | collect completeCodeSecureScan(SonarQube/Semgrep) |

---

## 8. Logandaudit plan

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| K8s audit planLog | High | ACK Console -> Logincore | open enable, recursive SLS, protect retain >= 180 days |
| ApplicationLogcollectin collect | in | CheckLog collect array item(Logtail/Fluent Bit) | AllbusinessContainerLog collect SLS/ES |
| Loginwhetherleak sensitive | High | CheckLogcontent | noPassword/Token/Identity Card/mobile numberetc.clear text |
| report alert scale rule cover cover | High | SLS -> report alertConfiguration | cover cover:abnormal commonLogin/Permissionchange update/Pod CrashLoop/Image takeFailure |
| operation audit plan(ActionTrail) | High | Alibaba CloudConsole -> ActionTrail | open enable, RecordAll API Call(special level is RAM/KMS/ACK operation) |
| LogStorageAccess Control | High | SLS Project Permissionset set | Log Project onlySecure/operations has readPermission, ApplicationnoDeletePermission |

---

## 9. RAM andidentity copy manage manage(Alibaba Cloudlayer page)

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| primaryAccountwhetherday common useuse | Severe | audit checkLoginRecord | primaryAccountonlyusefor account single/top layer manage manage, day commonuse RAM subAccount |
| RAM User MFA | Severe | RAM Console -> Usermanage manage | AllConsoleLoginUserenableuse MFA |
| AK/SK useuseaudit plan | Severe | RAM -> User -> AccessKey manage manage | disable stop primaryAccount AK, subAccount AK set period rotate change(90 days) |
| RAM Rolemost smallPermission | High | Check RAM Policy content | no `"Action": "*"` or `"Resource": "*"` ofself set define policy strategy |
| cross service access ask useuse RAM Role | High | Check ECS/Containeruseuse Instance RAM Role | ApplicationPassrealcasesRoleObtain timeCredential, Non- state AK/SK |
| setAccountclear manage | in | RAM -> Userlist -> most afterLogintime between | 90 daysnot useuseofAccountdisableuseorDelete |

---

## 10. NetworkSecure

| Check Item | Risk Level | Check Method | Expected Result |
|--------|---------|---------|---------|
| VPC Networkscale | High | VPC Console | generate asset/test/open initiate environment environment independent standalone VPC orindependent standalone VSwitch |
| Securearray scale rule | Severe | ECS/ACK section pointSecurearray | no `0.0.0.0/0` inject scale rule(22/3389/allPort), most small ize open release |
| SLB expose exposure page | High | SLB list -> monitor Configuration | only expose exposure 80/443, BackendPortnotDirectexpose exposure |
| Clustersection pointPublic Internet IP | High | ACK section point list | Worker section point noPublic Internet EIP, Pass NAT Gatewayout |
| DNS Secure | in | Domain Namedecode Recordaudit check | no decode Record(DNS), internal part service useuse PrivateZone |
| out flow quantity manage control | High | NAT Gateway + Securearray out method toward scale rule | limit make out Target, disable stop meaning access ask external network |

---

## CheckExecutecreate protocol

### Priorityrank sequence

1. **P0(standalone that is fix repeat)**:Allidentifier recordas"Severe"ofitems - Directexpose exposure attack attack pageorCausingDataDisclosure
2. **P1(1 cycle internal fix repeat)**:Allidentifier recordas"High"ofitems - manipulate deep defense defenseMissing, be exploituseafter impact response serious large
3. **P2(1 internal fix repeat)**:Allidentifier recordas"in/Low"ofitems - Hardeningitems, provide escalate integer bodySecurehorizontal characters

### self dynamic izeToolinfer

| Tool | Purpose | part deploy method mode |
|------|------|---------|
| **kube-bench** | CIS Kubernetes Benchmark self dynamicCheck | DaemonSet or Job |
| **Trivy** | Imagevulnerability + K8s ConfigurationScan | CI/CD collect complete + Operator |
| **Kyverno / OPA Gatekeeper** | K8s policy strategy that isCode, accurate inject control make | Admission Webhook |
| **Falco** | operatelinestime check test | DaemonSet |
| **kubeaudit** | K8s Secureaudit plan | CLI Scan |
| **cloud_enum / ossutil** | OSS Bucket EnumerationandPermissioncheck test | mobile dynamic/set periodScript |
| **Alibaba CloudSecureincore** | all stackSecuremonitor control(primary machine+Container+cloud service) | SaaS, ACK collect complete |

### set period repeat check section

- **each day**:operatelinestime report alertCheck/Pod abnormal commonStatus check
- **each cycle**:ImagevulnerabilityScanResultrepeat audit/Securearray change update audit plan
- **each **:RAM Permissionaudit plan/Secret rotate changeStatusCheck/OSS Bucket Permissionrepeat check
- **each degree**:all quantitySecurity Configurationbase lineScan(kube-bench + Trivy)/ test
