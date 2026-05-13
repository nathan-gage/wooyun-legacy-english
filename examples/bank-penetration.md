# Banking Penetration Testing Approach

> Based on analysis of 22,132 real WooYun cases

## 1. Layered Banking Attack Surface Model

```
+-------------------------------------------------------------------------+
|                         Layer 1: Internet Edge                          |
+-------------------------------------------------------------------------+
| Online Banking | Mobile Banking | WeChat Banking | Direct Bank | Cards  |
| Official Site / Campaign Pages                                          |
+-------------------------------------------------------------------------+
                                    |
                                    v
+-------------------------------------------------------------------------+
|                         Layer 2: Interface / Channel                    |
+-------------------------------------------------------------------------+
| Payment APIs | UnionPay Channels | Quick Pay | Withholding/Payouts      |
| Aggregated Payments | Open Banking APIs                                  |
+-------------------------------------------------------------------------+
                                    |
                                    v
+-------------------------------------------------------------------------+
|                         Layer 3: Internal Systems                       |
+-------------------------------------------------------------------------+
| Core Banking | Credit System | Risk Control | AML | Customer CRM        |
| Reporting System                                                        |
+-------------------------------------------------------------------------+
```

## 2. High-Risk Vulnerability Types

### Tier 1: Funds-Related Vulnerabilities (68-88% high-severity)

| Vulnerability Type | High-Severity % | Banking-Specific Scenarios |
|--------------------|-----------------|----------------------------|
| Password reset | 88.0% | online/mobile banking login passwords, transaction passwords |
| Withdrawal exploit | 83.1% | transfer limit bypass, withdrawal validation defects |
| Amount tampering | 83.0% | transfer amounts, wealth-management amounts, repayment amounts |
| Payment vulnerability | 68.7% | quick pay, withholding/payouts, interbank transfers |

### Payment Vulnerability Detection (1,056 cases)

**Manual test checklist:**
```
1. Modify amount parameters: amount=0.01 (test server-side validation)
2. Modify quantity to a negative number: quantity=-1 (negative transfer)
3. Replay a successful payment request (test idempotency)
4. Submit the same order concurrently (race condition)
5. Modify recipient account/user ID (unauthorized transfer)
6. Tamper with callback notification (forge successful payment)
```

**Key parameters:**
- `amount` / `price` / `total` -> amount fields
- `to_account` / `payee_id` -> recipient
- `sign` / `signature` -> signature

**Bypass techniques:**
```
Negative-number attack: transfer amount = -1000
Decimal overflow: amount = 0.001
Race condition: concurrent transfers from multiple threads
State tampering: modify status=SUCCESS
Signature bypass: delete or empty the signature field
```

### Tier 2: Authentication and Authorization

| Vulnerability Type | Cases | Attack Scenario |
|--------------------|-------|-----------------|
| Weak passwords | 7,513 | online banking backends, operations systems |
| Authorization bypass | 1,705 | view other users' account information |
| CAPTCHA/OTP | 334 | login, transfer, password reset |

## 3. Banking-Specific Attack Surfaces

### 1. Mobile Banking App Security

```
Client-side security
+-- Anti-decompilation protection (hardening strength)
+-- Local storage (sensitive information)
+-- Log leakage
+-- Certificate validation (SSL Pinning)

Communication security
+-- Encryption algorithms (hardcoded keys)
+-- Request signatures (algorithm reversing)
+-- Replay attacks

Business logic
+-- Login authentication (password/fingerprint/face)
+-- Transaction verification
+-- Transfer limits
```

**App penetration approach:**
```
1. Packet-capture breakthrough: bypass SSL Pinning (Frida/Objection)
2. Reverse engineering: unpacking -> signature algorithm reversing -> key extraction
3. Hook testing: bypass face/fingerprint verification and modify limit checks
```

### 2. Online Banking Systems

```
Attack approach:
+-- ActiveX control vulnerabilities
+-- Front-end encryption bypass (JS reversing)
+-- Password control bypass
+-- USB security key driver vulnerabilities
+-- Bulk transfer API authorization bypass
+-- Unauthorized download of statements/receipts
```

### 3. Third-Party Payment Interfaces

```
Attack points:
+-- Merchant key leakage (GitHub search)
+-- Callback signature verification defects
+-- Asynchronous notification replay
+-- Missing amount validation
+-- Merchant ID authorization bypass
```

## 4. Verification Bypass Techniques

### SMS OTP
```
+-- Brute force (4-6 digits, feasible)
+-- Concurrency (bypass attempt limits)
+-- Reuse (same OTP used multiple times)
+-- Echo (returned in response)
+-- Universal OTP (0000/1234)
```

### Facial Recognition
```
+-- Photo attack
+-- Video attack
+-- Hook return values
+-- API replay
+-- Replace face data
```

### Transaction Signatures
```
+-- Hardcoded signature key
+-- Critical fields left unsigned
+-- Optional signature verification
+-- Signature downgrade attack
```

## 5. Penetration Paths

### Path 1: External Web Breakthrough
```
Information gathering -> subdomains/ports/fingerprints
    |
Vulnerability exploitation (priority):
+-- 1. Weak-password brute force
+-- 2. Struts2/WebLogic RCE
+-- 3. Business logic vulnerabilities
+-- 4. File upload / SQL injection
```

### Path 2: Mobile Breakthrough
```
Static analysis -> decompilation, key search, API extraction
Dynamic analysis -> pinning bypass, packet capture, hooks
Business testing -> login/transfer/password reset
```

### Path 3: Supply Chain Attack
```
Outsourcing company -> code/environment leakage
Equipment vendor -> preconfigured accounts
Service provider -> SMS/identity verification
```

## 6. High-Value Targets

| Target System | Value | What Can Be Done |
|---------------|-------|------------------|
| Core banking | Very high | account balances, transaction records |
| Credit system | High | loan approval, credit-limit adjustment |
| Risk control system | High | blacklists, rule configuration |
| CRM system | Medium | KYC data |

## 7. Practical Checklist

### Information Gathering
- [ ] Subdomain enumeration.
- [ ] GitHub code leakage.
- [ ] App download analysis.
- [ ] WeChat official account / mini program APIs.

### Vulnerability Detection
- [ ] Weak-password testing.
- [ ] Business logic for payment, transfer, and password reset.
- [ ] Authorization bypass testing.
- [ ] API security, including signatures and encryption.
- [ ] App client-side security.

### Deep Exploitation
- [ ] Payment amount tampering.
- [ ] OTP bypass.
- [ ] Facial recognition bypass.
- [ ] Concurrent race conditions.

---

**Reference methodologies:**
- [Payment](../categories/logic-flaws.md)
- [Amount](../categories/logic-flaws.md)
- [Password Reset](../categories/logic-flaws.md)
- [Authorization Bypass](../categories/unauthorized-access.md)

**Representative cases:**
- Zhongyuan Bank system vulnerabilities allowing GetShell, affecting Tenpay/Alipay payments.
- Baidu Smart Micro-School to China Youth Development Foundation system, allowing donation amount tampering.
