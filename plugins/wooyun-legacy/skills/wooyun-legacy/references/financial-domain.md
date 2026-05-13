# Financial Domain

## Overview

Financial logic vulnerabilities cause direct monetary loss. In 2,919 WooYun cases, 68-83% were high severity, proving that money-related logic is consistently among the easiest logic to exploit.

**Core principle:** Any financial value appearing in a client request is an assumption waiting to be validated. Price, quantity, discount, balance, fee: if the client sends it, the client can modify it.

## Iron Rules for Financial Testing

```
Never trust client-side financial calculations.
If the server accepts price/amount/quantity from the client -> assume it is vulnerable unless verified.
```

## Attack-Pattern Matrix

### Payment Tampering (1,056 cases, 68.7% high severity)

**Systematic payment testing checklist:**

```
1. Price tampering
   - [ ] Change amount to 0.01 (minimum accepted amount)
   - [ ] Change amount to 0 (zero-cost purchase)
   - [ ] Change amount to a negative number (refund to attacker)
   - [ ] Change amount to a very large negative number (overflow)
   - [ ] Change currency code if multiple currencies are supported
   - [ ] Modify unit price and total price separately

2. Quantity tampering
   - [ ] Set quantity to 0 (free goods)
   - [ ] Set quantity to -1 (negative purchase = refund)
   - [ ] Set quantity to a very large number (integer overflow)
   - [ ] Set quantity to a decimal (0.001 items)
   - [ ] Set quantity inconsistent with the implied price

3. Discount/coupon abuse
   - [ ] Apply the same coupon repeatedly
   - [ ] Apply a coupon to an already discounted item
   - [ ] Modify discount percentage in the request (discount=100)
   - [ ] Use an expired coupon by replaying a valid request
   - [ ] Use a coupon intended for a different product category
   - [ ] Stack multiple promotion types

4. Race conditions (Turbo Intruder / concurrent requests)
   - [ ] Double spend: submit payment twice at the same time
   - [ ] Coupon race: apply the same single-use coupon in parallel
   - [ ] Balance race: withdraw the same balance concurrently
   - [ ] Inventory race: buy the last item in parallel

5. State-machine bypass
   - [ ] Skip payment step: jump from cart directly to order confirmation
   - [ ] Modify order status: change status=pending to status=paid
   - [ ] Replay successful payment callback for a different order
   - [ ] Modify order after payment but before fulfillment
```

**Key parameters:** `amount`, `price`, `total`, `quantity`, `discount`, `coupon_code`, `currency`, `fee`, `status`, `order_id`, `payment_id`

### Order Tampering (1,227 cases, 74.2% high severity)

**Order state-machine attacks:**

```
Expected flow:
  Cart -> Pending payment -> Paid -> Processing -> Shipped -> Delivered -> Completed

Attack vectors:
  Cart -> Completed (skip payment entirely)
  Paid -> Cart (restore cart to modify items after payment)
  Shipped -> Paid (restore state to obtain refund while keeping goods)
  Any -> Cancelled + refund (cancel after receiving goods)
```

**Testing protocol:**

```
For every state transition:
1. Capture the request that triggers the transition
2. Can it be triggered in the wrong order?
3. Can it be triggered for another user's order?
4. Can it be triggered multiple times?
5. Can order contents be modified between states?
```

### Balance / Withdrawal (113+59 cases, 77-83% high severity)

**Key patterns:**

| Attack | Method | Impact |
|--------|--------|--------|
| Negative transfer | transfer amount=-100 (recipient debited, sender credited) | Direct theft |
| Withdrawal race condition | Concurrent withdrawal requests exceeding balance | Double spend |
| Balance calculation bypass | Modify balance parameter in client request | Unlimited funds |
| Withdraw to arbitrary account | Change target account in withdrawal request | Fund diversion |
| Decimal precision | Withdraw 0.001 x 10000 times (rounding exploit) | Cumulative theft |

### Pricing / Recharge (218+176+70 cases)

**Price tampering patterns:**

```
1. Recharge exploitation
   - [ ] Modify recharge amount in the request
   - [ ] Replay successful recharge callback
   - [ ] Use test payment gateway credentials
   - [ ] Modify payment-gateway response before server receives it

2. Price inconsistency
   - [ ] Different prices across cart, checkout, and payment
   - [ ] Change item_id to a cheaper product with the same quantity
   - [ ] Add items to cart after price calculation
   - [ ] Currency confusion (CNY 1 vs $1 vs 1 point)
```

## Race Condition Testing Guide

**Financial race conditions require special techniques:**

```python
# Conceptual method for concurrent payment testing
# Use Burp Turbo Intruder or a custom script

# Step 1: Prepare request, such as withdrawal
# Step 2: Send N identical requests simultaneously
# Step 3: Check: did the server process more than one?

# Vulnerability indicators:
# - Balance decreased by N x amount (should be 1 x amount)
# - Multiple success responses for a single-use operation
# - Multiple transaction records created
```

**Tools:** Burp Turbo Intruder, custom Python threading scripts, `curl` run in the background with `&`

## Real Cases

| Case | Subdomain | Impact |
|------|-----------|--------|
| M1905 movie site 2,588-yuan package could be purchased for 0.5 yuan, with backend permission to self-approve orders | Order | 5,000x price difference through self-approval |
| Weitang main-site SQL injection involved 8.6M+ patients, 460K+ doctors, and 120K+ order records | Order | 8.6 million patients + 460,000 doctor records |
| Large third-party payment institution exam system SOAP injection with DBA privileges across 9 databases | Payment | Full DBA access to 9 databases |
| Allinpay file traversal read vulnerability in Oracle EBS system | Payment | Oracle EBS file read |
| Two Zhongyuan Bank vulnerabilities allowed GetShell and affected Tenpay/Alipay payments | Payment | Banking system remote code execution |
| China Tietong billing system GetShell plus recharge-card generation | Recharge | Arbitrary recharge-card generation |
| eXin WiFi multi-system vulnerabilities involved more than one million users and more than one million recharge card secrets | Recharge | 1M+ users + 1M+ recharge cards |
| Shenzhou private-car recharge flow skipped credit-card transaction password entry, enabling malicious cash-out | Recharge | Credit-card cash-out bypass |
| Baidu Smart Micro-school plus China Youth Foundation system allowed donation amount tampering | Amount | Donation amount tampering |
| YupaoPao app arbitrary user login affected user account balances through sign bypass | Balance | Account balance tampering |
| Ningbo Bank direct banking allowed viewing arbitrary card balances | Balance | Arbitrary bank-card balance viewing |
| Baixing Pharmacy vulnerability endangered 20M personal-detail records plus membership-card balances | Balance | 20 million personal records + balance data |
| Weixiaobao app XSS could control 190,000 WeChat accounts, including withdrawal/deduction operations | Withdrawal | Withdrawal control over 190,000 WeChat accounts |
| ETCP parking unauthenticated access exposed parking user data and withdrawable user income | Withdrawal | User income withdrawal |
| Ping An validation-logic issue leaked millions of sensitive records and allowed product price management | Price | 1M+ personal records + price tampering |

## Defense Patterns

### Code Level
- **Server-side calculation only:** price = database price x quantity, never from client
- **Idempotency key:** unique transaction ID, reject duplicates
- **Optimistic locking:** `UPDATE balance SET amount=amount-X WHERE amount >= X` (atomic operation)
- **State-machine enforcement:** strict finite-state machine with an allowlist of valid transitions
- **Signature verification:** payment callbacks must verify cryptographic signatures

### Architecture Level
- **Distributed locks:** Redis SETNX / Zookeeper for financial operations
- **Message queues:** asynchronous payment processing with exactly-once semantics
- **Two-phase commit:** debit -> verify -> fulfill; roll back on any failure
- **Reconciliation:** automated daily reconciliation with payment gateways

### Monitoring
- **Abnormal amount:** orders with amount <= 0.01
- **High frequency:** multiple orders/withdrawals per user per minute
- **Abnormal state:** orders reaching "completed" without passing through "paid"
- **Balance inconsistency:** real-time balance does not match transaction totals
