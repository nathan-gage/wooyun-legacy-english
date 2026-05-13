# Telecom Penetration Testing Approach

> Based on analysis of 22,132 real WooYun cases

## 1. Attack Surface Overview

```
                        Telecom Attack Surface
                              |
    +---------+---------+-----+-----+---------+---------+
    v         v         v           v         v         v
 Internet   Mobile   Value-Added  Internal    IoT     Supply
 Portal      App       Services    Systems  Platform   Chain
                       Platform
    |         |         |           |         |         |
 +-- Online  +-- Self  +-- SP/CP   +-- OA   +-- IoT   +-- Outsourcing
 |   Hall    |   App   |           |        |   SIM   |
 +-- Points  +-- H5    +-- SMS     +-- Mail +-- M2M   +-- Vendors
 |           |         |   Gateway |        |         |
 +-- Promo   +-- SDK   +-- Billing +-- VPN  +-- V2X   +-- Operations
     Pages               APIs                          Providers
```

## 2. Common Vulnerability Types

### 1. Weak Passwords (7,513 cases, 58.2% high-severity)

| Target System | Common Weak Passwords | GetShell Likelihood |
|---------------|------------------------|---------------------|
| BOSS backend | admin/admin, employee_id/123456 | High |
| Network management platform | root/root, huawei/huawei | High |
| Database | sa/empty, root/root | High |
| Docker API | no authentication | High |

**Detection method:**
```bash
# Batch brute force
hydra -L users.txt -P top1000.txt target ssh
hydra -l admin -P passwords.txt target http-post-form
```

### 2. Authorization Bypass (1,705 cases, 62.3% high-severity)

**Telecom-specific authorization bypass points:**

| Function | Key Parameters | Impact |
|----------|----------------|--------|
| Balance inquiry | `phone`, `mobile` | View any user's account balance |
| Call records | `cust_id`, `user_id` | Obtain any user's call records |
| Plan change | `order_id` | Modify another user's plan |
| Real-name identity data | `id_card` | Expose ID card photos |

**Bypass techniques:**
```
Parameter pollution: ?uid=1&uid=2 (backend uses the latter)
Array injection: uid[]=target_id
Nested JSON: {"user":{"id":target_id}}
```

### 3. Unauthenticated Access (1,891 cases, 58.2% high-severity)

**Frequently exposed paths:**
```
/admin           -> backend administration
/api/swagger     -> API documentation
/console         -> console
/manager         -> Tomcat manager
/zabbix          -> monitoring system
```

## 3. Uncommon but High-Value Attack Surfaces

### 1. SP/CP Value-Added Service Platforms
- Third-party access points often have lower security requirements.
- They connect directly to billing systems.
- Entry points: SMS/MMS delivery platforms and data top-up package APIs.

### 2. IoT SIM Card Management Platforms
- IoT device management backends.
- Bulk activation APIs.
- M2M platform APIs.

### 3. Network Management Systems (NMS)
- Huawei U2000/M2000.
- Power and environment monitoring systems.
- A successful compromise can control core network devices.

## 4. GetShell Paths

### Path 1: Web RCE
```
Priority order:
1. Struts2 RCE (S2-045/046/048/052)
2. WebLogic deserialization
3. Shiro deserialization (rememberMe)
4. Fastjson RCE
5. File upload bypass
6. SQL injection -> xp_cmdshell/into outfile
```

### Path 2: Perimeter Device Compromise
```
VPN device vulnerabilities:
+-- Pulse Secure CVE-2019-11510
+-- Fortinet CVE-2018-13379
+-- Citrix CVE-2019-19781
+-- Sangfor VPN arbitrary password reset

Network devices:
+-- Huawei device default passwords
+-- Cisco Smart Install protocol abuse
+-- SNMP community string leakage
```

### Path 3: Supply Chain Attack
```
Third-party outsourcing company -> development/test environment -> production environment
Operations staff workstation -> internal lateral movement
```

## 5. Lateral Movement Targets

| Target System | Value | Difficulty |
|---------------|-------|------------|
| BOSS system | user data, billing control | High |
| AAA authentication center | network-wide user credentials | High |
| SMS gateway | SMS hijacking | High |
| Core network devices | network control plane | Very high |
| DNS servers | traffic hijacking | Medium |

## 6. Practical Checklist

### Information Gathering
- [ ] Subdomain enumeration, such as `*.10086.cn`.
- [ ] Port scanning, including non-standard ports.
- [ ] GitHub/Gitee code leakage.
- [ ] Internet asset mapping with Shodan/Fofa.

### Vulnerability Discovery
- [ ] Weak-password brute force.
- [ ] Authorization bypass testing, such as phone number or user ID enumeration.
- [ ] Unauthenticated access.
- [ ] Framework vulnerability scanning.

### After GetShell
- [ ] Persistence.
- [ ] Internal network information gathering.
- [ ] Credential acquisition.
- [ ] Proxy tunneling.
- [ ] Lateral movement.

---

**Reference methodologies:**
- [Weak Passwords](../categories/weak-password.md)
- [Authorization Bypass](../categories/unauthorized-access.md)
- [Unauthenticated Access](../categories/unauthorized-access.md)
