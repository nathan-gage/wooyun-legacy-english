# Logic Flaw Deep Analysis Manual

> Manual English version of the WooYun logic flaw manual.
> Original scope: design flaw and business logic cases, including password reset, authorization, CAPTCHA, payment, and state-machine failures.

Logic flaws occur when the implementation allows a business action that the rules should forbid. Scanners miss them because the request is often syntactically valid. Testing must model the business process, then challenge identity, ownership, state, amount, sequence, and timing assumptions.

## 1. Core Model

```text
Business rule -> server-side enforcement -> state transition -> audit trail
```

A vulnerability exists when the server trusts the client, skips an ownership check, accepts an invalid state transition, reuses a verification artifact, or performs a sensitive action before completing validation.

## 2. Password Reset Flaws

| Pattern | Test idea |
|---|---|
| Verification code returned in response | Inspect reset API response and traffic |
| Code not bound to account | Request code for attacker account, submit for victim account |
| Code not invalidated | Reuse the same code multiple times |
| Weak or brute-forceable code | Test rate limiting and lockout |
| Reset token not bound to session | Swap token, username, phone, or email parameters |
| Client-side step enforcement | Jump directly to the final reset endpoint |

Defenses: bind code to account, purpose, session, and expiration; invalidate after use; enforce server-side rate limits; and audit reset events.

## 3. Authorization and IDOR Logic

| Operation | Test direction |
|---|---|
| View | Replace IDs and tenant identifiers |
| Modify | Change profile, address, order, or configuration IDs |
| Delete | Attempt deletion of another user's object |
| Act as another user | Change `userId`, `uid`, `openid`, `account`, or nested JSON IDs |
| Batch operation | Insert unauthorized IDs into arrays |

Server-side rule: every object access must check ownership or permission at the point of use. UI hiding and client-side checks are not authorization.

## 4. CAPTCHA and Verification Bypass

Common WooYun patterns:

- CAPTCHA value returned in the response.
- CAPTCHA checked only on the client.
- CAPTCHA not refreshed after failure.
- CAPTCHA reusable across actions.
- Verification code accepts universal values such as `0000`, `1234`, or `8888`.
- No rate limit on SMS/email code submission.

Defenses: server-side verification, per-purpose binding, short expiry, one-time use, rate limits, and anomaly monitoring.

## 5. Payment and Amount Logic

High-risk fields:

```text
amount
price
total
discount
couponId
quantity
orderId
payStatus
refundStatus
balance
points
```

Test directions:

- Change amount to `0`, `0.01`, negative, very large, or high precision.
- Change quantity to `0`, negative, or very large.
- Swap product IDs after price calculation.
- Reuse coupons, credits, or points concurrently.
- Forge payment callbacks or change callback status.
- Skip from unpaid to paid, shipped, completed, or refunded states.

Defenses: compute all monetary values on the server, bind payment callbacks to signed provider data, verify order ownership, enforce state machines, and make balance/coupon operations transactional.

## 6. State Machine Testing

```text
pending -> paid -> shipped -> completed -> refunded
```

Invalid transitions to test:

```text
pending -> shipped
pending -> completed
paid -> refunded without refund approval
completed -> pending
refunded -> refunded again
```

For each transition, test direct API calls, replayed requests, hidden parameters, and concurrent submissions.

## 7. Authentication Bypass

Test areas:

- Trusting `X-Forwarded-For`, `X-Real-IP`, or `Client-IP` for internal-only logic.
- Response tampering where client trusts `success=true`.
- Front-end route guards without backend enforcement.
- Hardcoded tokens or weak signed parameters.
- OAuth redirect or callback validation gaps.

Defenses: authenticate and authorize every sensitive endpoint, ignore spoofable headers unless set by trusted proxies, verify signatures server-side, and use allowlists for redirects.

## 8. Report Template

```text
Title: Business logic flaw in [process]
Rule violated: [ownership, state, amount, sequence, timing]
Endpoint(s): [URLs and methods]
Manipulated input: [parameter, ID, status, code, sequence]
Expected behavior: [what the business rule requires]
Actual behavior: [what the server allowed]
Impact: [financial loss, account takeover, data modification]
Remediation: [server-side rule enforcement, binding, transaction, audit]
```

## 9. Key Takeaways

- The server must be the source of truth for identity, ownership, amount, and state.
- Every step in a user flow should be independently authorized; previous steps cannot be trusted.
- Race conditions are logic flaws in time; use transactions and idempotency keys.
- Good reports explain the broken business rule, not just the changed parameter.
