---
name: wooyun-legacy
description: >-
  WooYun business logic vulnerability methodology - 22,132 real cases across 6 domains (authentication bypass, authorization bypass, payment tampering, information disclosure, logic flaws, misconfiguration) and 33 vulnerability classes.
  Use for ANY security testing, auditing, or code review of web apps, APIs, or business systems - even without explicit "security" keywords.
  Triggers: penetration testing, security audit, vulnerability, bug bounty, payment security, IDOR, password reset, weak credentials, unauthorized access, race condition, parameter tampering, code review, penetration testing, security audit, vulnerability discovery, payment security, authorization bypass, logic flaw, business security, SRC, code audit.
  Also triggers on implicit intent: "test this endpoint", "find bugs", "can I bypass this", "help me test this endpoint", "can this parameter be changed", "help me find bugs".
---

# WooYun Business Logic Vulnerability Methodology

> 22,132 real vulnerability cases - 6 domains - 33 vulnerability classes

**Extended trigger keywords (not in description due to length limits):**
Implicit black-box testing: "check whether this feature has problems", "does this flow have a vulnerability", "how can this restriction be bypassed", "order/payment/refund flow testing", "is this system secure", "does this API have risks", "check this API", "is this flow secure", "review this for issues".
Tools & techniques: packet capture analysis, Burp Suite, request interception, parameter modification, replay attacks, concurrency testing, ID enumeration, brute forcing, promo abuse, fake order generation, arbitrage, risk-control bypass, SMS bombing, API abuse, unauthenticated API, arbitrary file, data leakage, reconnaissance, subdomains, directory scanning, fingerprinting, intercept, replay, fuzz, enumerate, brute force, rate limiting bypass, coupon abuse.

Business logic vulnerabilities cannot be found by scanners. They exist in the gap between what developers intended and what the application actually allows. This methodology teaches you to think like the developer who wrote the code and attack like a user who abuses the application.

**Data basis:** WooYun (2010-2016), a large public vulnerability disclosure platform.

## Vulnerability Severity Priority

Testing should prioritize high-risk vulnerability classes. The table below is sorted by the share of high-severity findings in the WooYun dataset. A higher percentage indicates a greater likelihood of critical impact.

| Rank | Vulnerability class | Case count | High-severity share | Domain |
|------|---------------------|------------|---------------------|--------|
| 1 | Password reset | 777 | 88.0% | Authentication |
| 2 | Arbitrary account | 220 | 86.4% | Authorization |
| 3 | Withdrawal | 59 | 83.1% | Financial |
| 4 | Amount tampering | 176 | 83.0% | Financial |
| 5 | Balance tampering | 113 | 77.9% | Financial |
| 6 | Arbitrary user registration | 24 | 75.0% | Authorization |
| 7 | Logic flaw | 266 | 74.8% | Logic flow |
| 8 | Order tampering | 1,227 | 74.2% | Financial |
| 9 | Price tampering | 70 | 74.3% | Financial |
| 10 | Misconfiguration | 1,796 | 72.6% | Configuration |
| 11 | Arbitrary operation | 40 | 72.5% | Authorization |
| 12 | Payment bypass | 1,056 | 68.7% | Financial |
| 13 | Design flaw | 1,391 | 65.3% | Logic flow |
| 14 | Information disclosure | 4,858 | 64.7% | Information |
| 15 | Authorization bypass | 1,705 | 62.3% | Authorization |
| 16 | Weak password | 7,513 | 58.2% | Authentication |

## Four-Phase Method

Each phase builds on the previous one. Skipping any phase leads to shallow testing that misses logic vulnerabilities scanners cannot find.

### Phase 1: Business Flow Mapping

Before testing any endpoint, understand what the application does and how money, data, and permissions flow through it.

1. **Understand the business**
   - What does this application do? (e-commerce, banking, social, SaaS)
   - Who are the main actors? (anonymous users, normal users, administrators, merchants, API clients)
   - What is the revenue model? (How does money flow?)
   - Which data is sensitive? (personal information, financial data, medical data, credentials)

2. **Map user journeys**
   - Register -> log in -> core operation -> log out
   - Purchase -> pay -> fulfill -> refund
   - Password reset -> verify -> new password
   - Administrator -> user management -> permission assignment

3. **Identify state transitions**
   ```
   For each business process:
     - List all states (pending review, active, paid, shipped, refunded)
     - List all valid transitions (pending review -> paid, paid -> shipped)
     - Question: Can an invalid transition be forced? (pending review -> shipped)
     - Question: Can a transition be reversed? (paid -> pending review)
   ```

4. **Map trust boundaries**
   - Client vs server: Which validations happen only on the client?
   - User vs administrator: What separates privilege levels?
   - Tenant vs tenant: What prevents cross-tenant access?
   - Internal vs external: Which assumptions rely on a trusted internal source?

### Phase 2: Hypothesis Formation

Use the reference files below to form domain-specific hypotheses. Each domain file contains a detailed attack-pattern matrix, testing checklist, and defense patterns derived from thousands of real WooYun cases.

**Tier 1: Domain references (methodology + attack-pattern matrix)** - load first

| Domain | Reference file | Case count |
|--------|----------------|------------|
| Authentication bypass, credential flaws | [authentication-domain.md](references/authentication-domain.md) | 8,846 |
| Authorization bypass, IDOR, privilege escalation, arbitrary operations | [authorization-domain.md](references/authorization-domain.md) | 6,838 |
| Payment, order, balance, and price tampering | [financial-domain.md](references/financial-domain.md) | 2,919 |
| Personal information leakage, credential leakage, debug information | [information-domain.md](references/information-domain.md) | 6,446 |
| State-machine abuse, race conditions, flow bypass | [logic-flow-domain.md](references/logic-flow-domain.md) | 1,679 |
| Misconfiguration, default settings, hardening gaps | [configuration-domain.md](references/configuration-domain.md) | 1,796 |

**Tier 2: Deep-analysis manuals (technical details + root-cause analysis)** - load when deeper technical coverage is needed

| Technical domain | Knowledge file | Contents |
|------------------|----------------|----------|
| Command execution | [command-execution.md](../../knowledge/command-execution.md) | Full attack chain for OS command injection, code injection, and expression injection |
| File traversal | [file-traversal.md](../../knowledge/file-traversal.md) | Bypass techniques for path traversal and arbitrary file read/download |
| File upload | [file-upload.md](../../knowledge/file-upload.md) | Payload matrix for upload bypasses by type, extension, and content checks |
| Information disclosure | [info-disclosure.md](../../knowledge/info-disclosure.md) | Sensitive exposure paths, debug endpoints, configuration file leakage |
| Logic flaws | [logic-flaws.md](../../knowledge/logic-flaws.md) | Root-cause matrix for password reset, payment bypass, and verification-code bypass |
| SQL injection | [sql-injection.md](../../knowledge/sql-injection.md) | Injection-type taxonomy, WAF bypass, blind-injection techniques |
| Unauthenticated access | [unauthorized-access.md](../../knowledge/unauthorized-access.md) | Unauthenticated endpoint discovery and missing authorization-check patterns |
| XSS | [xss.md](../../knowledge/xss.md) | Input points and bypasses for stored, reflected, and DOM XSS |

**Tier 3: Vulnerability case library (real case titles + high-frequency payloads)** - load only when specific cases or payload patterns are needed

| Vulnerability type | Case file | Purpose |
|--------------------|-----------|---------|
| SQL injection | [sql-injection.md](../../categories/sql-injection.md) | 15 representative cases + high-frequency injection payloads |
| Command execution | [command-execution.md](../../categories/command-execution.md) | 15 representative cases + command-execution payloads |
| Unauthenticated access | [unauthorized-access.md](../../categories/unauthorized-access.md) | 15 representative cases + authorization-bypass patterns |
| Weak password | [weak-password.md](../../categories/weak-password.md) | 15 representative cases + high-frequency weak passwords |
| Information disclosure | [info-disclosure.md](../../categories/info-disclosure.md) | 15 representative cases + leakage paths |
| XSS | [xss.md](../../categories/xss.md) | 9 representative cases + XSS payloads |
| Misconfiguration | [misconfig.md](../../categories/misconfig.md) | 15 representative cases + misconfiguration patterns |
| Logic flaw | [logic-flaws.md](../../categories/logic-flaws.md) | 15 representative cases + logic bypasses |
| File upload | [file-upload.md](../../categories/file-upload.md) | 11 representative cases + upload-bypass payloads |
| SSRF | [ssrf.md](../../categories/ssrf.md) | SSRF attack patterns |
| CSRF | [csrf.md](../../categories/csrf.md) | CSRF exploitation patterns |
| File traversal | [file-traversal.md](../../categories/file-traversal.md) | 5 representative cases + traversal payloads |
| RCE | [rce.md](../../categories/rce.md) | 3 representative cases + RCE chains |
| XXE | [xxe.md](../../categories/xxe.md) | XXE injection patterns |
| Other | [other.md](../../categories/other.md) | 13 representative cases |

> **Progressive loading rule:** Read Tier 1 first to determine testing direction, then read Tier 2 as needed for technical details, and read Tier 3 only when specific cases or payloads must be referenced. Do not load all files at once.

**For each domain, use the following structure to form hypotheses:**

```
Hypothesis: [Business flow X] is vulnerable to [attack pattern Y]
Reason: [Evidence from reconnaissance: visible parameters, lack of server validation, predictable IDs]
WooYun pattern: [Matching pattern from the domain reference]
Impact: [Business impact: financial loss, data leakage, account takeover]
Test: [Specific manual testing steps]
```

### Phase 3: Targeted Manual Testing

Business logic requires manual testing because vulnerabilities exist in how the application interprets business rules, not in technical signatures a scanner can match.

1. **Prepare test accounts**
   - At least 2 accounts at the same privilege level (for horizontal testing)
   - At least 1 account per privilege level (for vertical testing)
   - Record all session tokens, cookies, and IDs

2. **Execute minimized tests**
   - Intercept the specific request (Burp/mitmproxy)
   - Modify only the parameter being tested
   - Observe: Does the server validate? Did the state change?
   - Record the exact request/response pair

3. **Analyze against business rules**
   - Does the application enforce business rules server-side?
   - Can state transitions be forced out of order?
   - Can another user's resource be accessed or modified?
   - Can financial value be tampered with?

4. **If confirmed -> Phase 4** - If disproven -> next hypothesis - If uncertain -> change approach

### Phase 4: Impact Assessment and Documentation

Prove business impact, not just a technical bypass.

```
## Finding: [Title]
- Severity: [Critical/High/Medium/Low]
- Domain: [Authentication/Authorization/Financial/Information/Logic/Configuration]
- WooYun pattern: [Historical pattern this finding matches]
- Business impact: [Financial loss, affected user count, data scope]
- Reproduction steps:
  1. [Exact steps and request/response]
  2. [...]
- Remediation: [Server-side fix, not a client-side bandage]
```

## Real Cases

These cases show why business logic testing matters. Each one represents a real vulnerability found by WooYun researchers:

| Case | Domain | Impact |
|------|--------|--------|
| A platform allowed authorization-bypass enumeration of large volumes of identity and vehicle-license documents | Authorization | Large document leakage through sequential file IDs |
| M1905 movie site: a 2,588-yuan package vulnerability allowed purchase for only 0.5 yuan | Financial | 5,000x price difference through backend self-approval bypass |
| TCL unified authentication platform allowed resetting all user passwords | Authentication | Full account takeover across N+ business systems |
| SQL injection in the Weitang main site affected 8.6M+ patients and 460K+ doctors | Information | 8.6 million patient records and 460,000 doctor records |
| A billing system allowed GetShell plus recharge-card generation | Financial | Arbitrary recharge-card generation + customer data leakage |
| Baihe.com app design flaw affected 1M+ women's phone numbers | Logic flow | 1M+ phone numbers leaked through a design flaw |

## Thinking Traps to Avoid

When testing business logic, watch for these common rationalizations that lead to shallow testing:

| Trap | Reality |
|------|---------|
| "Scanners can cover business logic" | Scanners find signatures, not logic flaws. No scanner can find "order status can skip payment." |
| "I tested the main flow, so it is secure" | 22,132 cases prove logic vulnerabilities live in edge cases. |
| "Just change the price to 0.01" | That is only one test. WooYun data shows 17+ payment attack patterns. |
| "IDOR is simple, just change the ID" | IDOR has encoding bypasses, parameter pollution, and nested JSON. Simple ID changes account for only 30% of cases. |
| "The frontend validated it, so it is fine" | 68.7% of payment vulnerabilities exist because validation occurs only client-side. |
| "The admin panel requires different credentials" | 58.2% of unauthenticated access cases involved admin backends with no authentication at all. |

## Quick Reference

| Phase | Key activity | Gate criterion |
|-------|--------------|----------------|
| **1. Map** | Business flows, state machines, trust boundaries | Complete flow diagram recorded |
| **2. Hypothesize** | Domain-specific theories based on WooYun patterns | At least 5 impact-ranked hypotheses |
| **3. Test** | Manual interception, single parameter, exact observation | Every hypothesis has supporting or disproving evidence |
| **4. Report** | Business impact, reproduction steps, remediation | Finding includes WooYun pattern classification |

<!-- Data source: WooYun vulnerability database (July 2016) - Methodology v2.0 -->
