# inline lesson Platform - Race ConditionandStatusmachine vulnerability specialitemsTest Plan

## 1. create model

### 1.1 Coupondomain take - Race Condition(Race Condition)

**business scale rule**: EachUserlimit domain oneitemsCoupon.

**attack attack pageAnalyze**:

| Attack Vector | description | Risk Level |
|---------|------|---------|
| TOCTOU(Check-useusetime between error) | Serverfirst check query"whetheralready domain take", againExecute" inject domain takeRecord", two step between existinTime Window | High |
| ConcurrencyReplay | SameUsersame timeSend N domain takeRequest, BypasssingletimesValidate | High |
| part deploy mode section point not one cause | many realcasespart deploy time, each section point exist/DB StatusDifferentstep, Causingserious repeat domain take | in |
| FrontendBypass | Frontendby set but not doBackendIdempotencyValidate | Low |

**root because**: missing Atomicityoperation. type vulnerabilityCodemode:

```python
# Vulnerability Pattern - Non-principle subCheck
def claim_coupon(user_id, coupon_id):
 existing = db.query("SELECT * FROM user_coupons WHERE user_id=? AND coupon_id=?", user_id, coupon_id)
 if existing: # <-- Check
 return "already_claimed"
 db.execute("INSERT INTO user_coupons...", user_id, coupon_id) # <-- useuse(two step between has window interface)
 return "success"
```

### 1.2 lesson process buy buy flow process - Statusmachine vulnerability(State Machine Bypass)

**expected periodStatusflow transfer**:

```
[lesson process] -> [add injectShopping Cart] -> [Create Order] -> [Pending Payment] -> [Paymentin] -> [Paid] -> [Completed]
 down down
 [alreadyCancel] [Refundin] -> [Refunded]
```

**attack attack pageAnalyze**:

| Attack Vector | description | Risk Level |
|---------|------|---------|
| Statusskip | Directfrom"Pending Payment"skipto"Completed", skip throughPaymentenvironment section | Severe |
| Statusreturn refund | will"Paid"Orderchange return"Pending Payment"after againCancel Refund | Severe |
| Payment Amount Tampering | PaymentCallbackinAmountnotandOrderAmountValidate, 0.01 yuanbuy buy lesson process | Severe |
| Concurrent Payment+Cancel | same time trigger initiatePaymentSuccessCallbackandCancelOrder, lesson process+Refund | High |
| serious repeatCallback | forgeryorReplayPaymentCallback, serious repeat initiate release lesson process permission | High |
| alreadyCancelOrderrepeat | for alreadyCancelOrderSendPaymentSuccesswild notify, use other"repeat " | High |
| Negative Numberquantity/negative price format | Shopping Cartincommerce product number quantityorprice formatasNegative Number, Causingtotal price abnormal common | in |

---

## 2. Test Planset plan

### 2.1 CouponRace Conditiontest matrix matrix

| Test ID | test scenario scene | Concurrencynumber | Expected Result | ValidateMethod |
|---------|---------|--------|---------|---------|
| RC-01 | singleUserConcurrencydomain takeSameCoupon | 50 | only 1 timesSuccess, 49 timesFailure | Databaseplan number = 1 |
| RC-02 | singleUserConcurrencydomain take + personas (model check query) | 20 | only 1 timesSuccess | Databaseplan number = 1 |
| RC-03 | manyUsereach selfConcurrencydomain takeSamelimit quantityCoupon(total quantity10items) | 100Userx5Concurrency | good initiate out10items | Databasetotal plan = 10 |
| RC-04 | SameUserDifferent session/token Concurrencydomain take | 10 | only 1 timesSuccess | Databaseplan number = 1 |
| RC-05 | Couponexpired boundary boundaryConcurrency(expired first1mslarge quantityRequest) | 30 | expired afterAllFailure | no new increaseRecord |

### 2.2 Order State Machinetest matrix matrix

| Test ID | test scenario scene | Method | Expected Result |
|---------|---------|------|---------|
| SM-01 | notPaymentOrderDirect Call"complete"Interface | API Direct Call | reject reject, ReturnStatusnot combine method |
| SM-02 | alreadyCancelOrderSendPaymentCallback | forgeryCallback | reject reject, OrdernotCanchange update |
| SM-03 | PaidOrderagaintimesPayment(serious repeatCallback) | ReplayCallback | Idempotencyhandle manage, not serious repeat initiate release |
| SM-04 | RefundedOrderAttemptagaintimesRefund | API Call | reject reject |
| SM-05 | Concurrency:PaymentCallback + CancelOrdersame time trigger initiate | Concurrencytest | only has one operationSuccess |
| SM-06 | ModifyPaymentAmount(CallbackAmount unicode-2260 OrderAmount) | tamper changeCallback | reject reject, Amountnot match config |
| SM-07 | Negative Numberquantity commerce product add injectShopping Cart | API Call | reject reject, number quantitymust > 0 |
| SM-08 | 0 yuanOrderDirectskip throughPayment | API Call | by business scale rule handle manage |
| SM-09 | towardStatusflow transferTraversal(AllNon-method transfer change) | self dynamic izeTraversal | AllNon-method transfer change be reject reject |
| SM-10 | ConcurrencyModifyShopping Cart + Create Order | Concurrencytest | OrderAmountandmost finalShopping Cartone cause |

---

## 3. ConcurrencytestScript

### 3.1 CouponRace ConditiontestScript(Python + asyncio)

```python
#!/usr/bin/env python3
"""
CouponRace ConditiontestScript
Test Objective:ValidateSameUserConcurrencydomain takeCoupontime, Systemwhethercan protect cert only domain take oneitems
"""

import asyncio
import aiohttp
import time
import json
from collections import Counter
from dataclasses import dataclass, field

@dataclass
class TestConfig:
 """testConfiguration"""
 base_url: str = "http://localhost:8000"
 claim_endpoint: str = "/api/v1/coupons/claim"
 query_endpoint: str = "/api/v1/coupons/user"
 user_token: str = "Bearer <test_user_token>"
 coupon_id: str = "COUPON_001"
 concurrency: int = 50
 timeout: int = 10

@dataclass
class TestResult:
 """Test Result"""
 total_requests: int = 0
 success_count: int = 0
 fail_count: int = 0
 error_count: int = 0
 status_codes: Counter = field(default_factory=Counter)
 response_details: list = field(default_factory=list)
 elapsed_seconds: float = 0.0

async def claim_coupon(session: aiohttp.ClientSession, config: TestConfig, request_id: int) -> dict:
 """SendsingletimesCoupondomain takeRequest"""
 headers = {
 "Authorization": config.user_token,
 "Content-Type": "application/json",
 "X-Request-ID": f"race-test-{request_id}-{time.time_ns()}"
 }
 payload = {"coupon_id": config.coupon_id}

 try:
 async with session.post(f"{config.base_url}{config.claim_endpoint}",
 json=payload,
 headers=headers,
 timeout=aiohttp.ClientTimeout(total=config.timeout)) as resp:
 body = await resp.text()
 return {
 "request_id": request_id,
 "status": resp.status,
 "body": body,
 "success": resp.status == 200
 }
 except Exception as e:
 return {
 "request_id": request_id,
 "status": -1,
 "body": str(e),
 "success": False,
 "error": True
 }

async def run_race_condition_test(config: TestConfig) -> TestResult:
 """
 audit core test:useuse asyncio.gather same timeSend N Request
 AllRequestsharedSame TCP continuous connect, Cancan same timetoreachServer
 """
 result = TestResult()
 connector = aiohttp.TCPConnector(limit=0, force_close=False)

 async with aiohttp.ClientSession(connector=connector) as session:
 # expected continuous connect(confirm protect TCP mobile not impact responseConcurrencytime sequence)
 try:
 await session.options(f"{config.base_url}/health")
 except Exception:
 pass

 # useuse Event real currentAllprotocol process same time enable dynamic(same step)
 barrier = asyncio.Event()

 async def gated_claim(req_id: int):
 await barrier.wait() # Allprotocol processinetc.pending
 return await claim_coupon(session, config, req_id)

 # CreateAllprotocol process
 tasks = [gated_claim(i) for i in range(config.concurrency)]
 gathered = asyncio.gather(*tasks)

 # release, AllRequestsame time initiate out
 start_time = time.monotonic()
 barrier.set()
 responses = await gathered
 result.elapsed_seconds = time.monotonic() - start_time

 # StatisticsResult
 result.total_requests = len(responses)
 for resp in responses:
 result.status_codes[resp["status"]] += 1
 if resp.get("error"):
 result.error_count += 1
 elif resp["success"]:
 result.success_count += 1
 else:
 result.fail_count += 1
 result.response_details.append(resp)

 return result

async def verify_database_state(config: TestConfig) -> dict:
 """ValidateDatabaseinthisUserofCoupondomain takeRecordnumber"""
 async with aiohttp.ClientSession() as session:
 headers = {"Authorization": config.user_token}
 async with session.get(f"{config.base_url}{config.query_endpoint}",
 headers=headers,
 params={"coupon_id": config.coupon_id}) as resp:
 data = await resp.json()
 return data

def print_report(result: TestResult, db_state: dict = None):
 """output out test report"""
 print("=" * 70)
 print(" CouponRace Conditiontest report")
 print("=" * 70)
 print(f" totalRequestnumber: {result.total_requests}")
 print(f" Successdomain take: {result.success_count}")
 print(f" be reject reject: {result.fail_count}")
 print(f" Networkerror: {result.error_count}")
 print(f" time: {result.elapsed_seconds:.3f}s")
 print(f" HTTPStatuscode part deploy: {dict(result.status_codes)}")
 print("-" * 70)

 # determine set
 if result.success_count == 1:
 print(" [PASS] Race Conditiondefense protectValid:only 1 timesdomain takeSuccess")
 elif result.success_count == 0:
 print(" [WARN] 0 timesSuccess - Cancan testConfigurationhas error(token/endpoint)")
 else:
 print(f" [FAIL] Race Conditionvulnerability!Successdomain take {result.success_count} times(expected period 1 times)")
 print(" [FAIL] existin TOCTOU vulnerability, requirescite injectDistributed LockorDatabaseunique constraint")

 if db_state:
 count = db_state.get("count", "unknown")
 print(f" Databasereal actualRecord: {count} condition")
 if count!= 1:
 print(f" [FAIL] DatabaseRecordnumber abnormal common!expected period 1 condition, real actual {count} condition")

 print("=" * 70)

async def main():
 config = TestConfig(base_url="http://localhost:8000",
 concurrency=50,)

 print(f"[*] open initialRace Conditiontest:{config.concurrency} ConcurrencyRequest")
 result = await run_race_condition_test(config)

 # Canselect:ValidateDatabaseStatus
 db_state = None
 try:
 db_state = await verify_database_state(config)
 except Exception as e:
 print(f"[!] DatabaseValidateskip through: {e}")

 print_report(result, db_state)

 # Returnrefund out code
 return 0 if result.success_count == 1 else 1

if __name__ == "__main__":
 exit_code = asyncio.run(main())
 exit(exit_code)
```

### 3.2 manyUser buy limit quantityCoupontestScript

```python
#!/usr/bin/env python3
"""
limit quantityCoupon buyRacetest
Test Objective:N itemslimit quantity coupon be M UserConcurrency buy, most final initiate release number <= N
"""

import asyncio
import aiohttp
import time
from collections import Counter

TOTAL_COUPONS = 10 # Couponlimit quantity
TOTAL_USERS = 100 # ConcurrencyUsernumber
REQUESTS_PER_USER = 3 # EachUserserious repeatRequesttimesnumber
BASE_URL = "http://localhost:8000"
CLAIM_ENDPOINT = "/api/v1/coupons/claim"
COUPON_ID = "LIMITED_COUPON_001"

async def user_claim(session, user_id: int, attempt: int):
 """model singleUserofdomain takeRequest"""
 headers = {
 "Authorization": f"Bearer test_token_user_{user_id}",
 "Content-Type": "application/json",
 }
 payload = {"coupon_id": COUPON_ID}
 try:
 async with session.post(f"{BASE_URL}{CLAIM_ENDPOINT}",
 json=payload,
 headers=headers,
 timeout=aiohttp.ClientTimeout(total=15)) as resp:
 return {"user_id": user_id, "attempt": attempt, "status": resp.status}
 except Exception as e:
 return {"user_id": user_id, "attempt": attempt, "status": -1, "error": str(e)}

async def main():
 connector = aiohttp.TCPConnector(limit=0)
 barrier = asyncio.Event()

 async with aiohttp.ClientSession(connector=connector) as session:
 async def gated(user_id, attempt):
 await barrier.wait()
 return await user_claim(session, user_id, attempt)

 tasks = [gated(uid, att)
 for uid in range(TOTAL_USERS)
 for att in range(REQUESTS_PER_USER)]

 start = time.monotonic()
 barrier.set()
 results = await asyncio.gather(*tasks)
 elapsed = time.monotonic() - start

 # Analyze
 success_users = set()
 total_success = 0
 status_dist = Counter()

 for r in results:
 status_dist[r["status"]] += 1
 if r["status"] == 200:
 total_success += 1
 success_users.add(r["user_id"])

 print("=" * 70)
 print(" limit quantityCoupon buyRacetest report")
 print("=" * 70)
 print(f" Couponlimit quantity: {TOTAL_COUPONS}")
 print(f" participateandUser: {TOTAL_USERS}")
 print(f" totalRequestnumber: {len(results)}")
 print(f" Successdomain take: {total_success} times({len(success_users)} DifferentUser)")
 print(f" time: {elapsed:.3f}s")
 print(f" Statuscode part deploy: {dict(status_dist)}")
 print("-" * 70)

 if total_success <= TOTAL_COUPONS and len(success_users) == total_success:
 print(f" [PASS] initiate release number({total_success}) <= limit quantity({TOTAL_COUPONS}), eachUsermost many1items")
 else:
 if total_success > TOTAL_COUPONS:
 print(f" [FAIL] super initiate!initiate release {total_success} items(limit quantity {TOTAL_COUPONS})")
 if len(success_users) < total_success:
 print(f" [FAIL] sameUserserious repeat domain take!{total_success} timesSuccessbut only has {len(success_users)} User")

 print("=" * 70)

if __name__ == "__main__":
 asyncio.run(main())
```

### 3.3 Go HighConcurrency testScript(update extreme endofRacetrigger initiate)

```go
// race_test.go - useuse Go principle generateConcurrencyreal current update precision confirmofRacetrigger initiate
package main

import ("bytes"
	"encoding/json"
	"fmt"
	"io"
	"net/http"
	"sync"
	"sync/atomic"
	"time")

const (baseURL = "http://localhost:8000"
	claimPath = "/api/v1/coupons/claim"
	userToken = "Bearer test_user_token"
	couponID = "COUPON_001"
	concurrency = 100)

type ClaimRequest struct {
	CouponID string `json:"coupon_id"`
}

func main() {
	var (successCount int64
		failCount int64
		errorCount int64
		wg sync.WaitGroup
		startGate = make(chan struct{}) //:All goroutine after same time release)

	client:= &http.Client{
		Timeout: 10 * time.Second,
		Transport: &http.Transport{
			MaxIdleConnsPerHost: concurrency,
			MaxConnsPerHost: concurrency,
		},
	}

	payload, _:= json.Marshal(ClaimRequest{CouponID: couponID})

	for i:= 0; i < concurrency; i++ {
		wg.Add(1)
		go func(id int) {
			defer wg.Done()
			<-startGate // etc.pending break open

			req, _:= http.NewRequest("POST", baseURL+claimPath, bytes.NewReader(payload))
			req.Header.Set("Authorization", userToken)
			req.Header.Set("Content-Type", "application/json")

			resp, err:= client.Do(req)
			if err!= nil {
				atomic.AddInt64(&errorCount, 1)
				return
			}
			defer resp.Body.Close()
			io.ReadAll(resp.Body)

			if resp.StatusCode == 200 {
				atomic.AddInt64(&successCount, 1)
			} else {
				atomic.AddInt64(&failCount, 1)
			}
		}(i)
	}

	// All goroutine -> same time release
	start:= time.Now()
	close(startGate)
	wg.Wait()
	elapsed:= time.Since(start)

	fmt.Println("====================================================")
	fmt.Println(" Go Race Condition test report")
	fmt.Println("====================================================")
	fmt.Printf(" Concurrencynumber: %d\n", concurrency)
	fmt.Printf(" Successdomain take: %d\n", successCount)
	fmt.Printf(" be reject reject: %d\n", failCount)
	fmt.Printf(" Networkerror: %d\n", errorCount)
	fmt.Printf(" time: %v\n", elapsed)
	fmt.Println("----------------------------------------------------")

	if successCount == 1 {
		fmt.Println(" [PASS] defense protectValid")
	} else {
		fmt.Printf(" [FAIL] Racevulnerability!Success %d times\n", successCount)
	}
	fmt.Println("====================================================")
}
```

### 3.4 Order State MachineNon-method transfer changeTraversaltest

```python
#!/usr/bin/env python3
"""
Order State MachineSecuretest
Test Objective:TraversalAllNon-methodStatustransfer change, confirm protectSystemreject reject each one
"""

import asyncio
import aiohttp
import json
from itertools import product

# ============================================================
# Statusmachine set define
# ============================================================

STATES = ["cart", # Shopping Cart
 "pending", # Pending Payment
 "paying", # Paymentin
 "paid", # Paid
 "completed", # Completed
 "cancelled", # alreadyCancel
 "refunding", # Refundin
 "refunded", # Refunded]

# combine methodofStatustransfer change(from_state -> to_state)
LEGAL_TRANSITIONS = {
 ("cart", "pending"), # SubmitOrder
 ("pending", "paying"), # initiate initiatePayment
 ("pending", "cancelled"), # CancelOrder
 ("paying", "paid"), # PaymentSuccess
 ("paying", "pending"), # Paymentsuper time/Failurereturn refund
 ("paid", "completed"), # Confirmcomplete
 ("paid", "refunding"), # pleaseRefund
 ("refunding", "refunded"), # RefundSuccess
 ("refunding", "paid"), # Refundreject reject
}

# AllCancanoftransfer change
ALL_TRANSITIONS = set(product(STATES, STATES))

# Non-method transfer change = All - combine method - self identitytoself identity
ILLEGAL_TRANSITIONS = ALL_TRANSITIONS - LEGAL_TRANSITIONS - {(s, s) for s in STATES}

BASE_URL = "http://localhost:8000"
ADMIN_TOKEN = "Bearer admin_test_token"

async def create_test_order(session, initial_state: str) -> str:
 """PassTest InterfaceCreatespecified set initialStatusofOrder"""
 headers = {
 "Authorization": ADMIN_TOKEN,
 "Content-Type": "application/json",
 }
 payload = {
 "course_id": "COURSE_001",
 "initial_state": initial_state, # Test EnvironmentspecialuseParameter
 "test_mode": True,
 }
 async with session.post(f"{BASE_URL}/api/v1/test/orders/create",
 json=payload,
 headers=headers,) as resp:
 data = await resp.json()
 return data.get("order_id")

async def attempt_transition(session, order_id: str, target_state: str) -> dict:
 """AttemptwillOrdertransfer changetoTargetStatus"""
 headers = {
 "Authorization": ADMIN_TOKEN,
 "Content-Type": "application/json",
 }

 # DifferentTargetStatusforshouldDifferentof API Endpoint
 endpoint_map = {
 "pending": f"/api/v1/orders/{order_id}/submit",
 "paying": f"/api/v1/orders/{order_id}/pay",
 "paid": f"/api/v1/orders/{order_id}/confirm-payment",
 "completed": f"/api/v1/orders/{order_id}/complete",
 "cancelled": f"/api/v1/orders/{order_id}/cancel",
 "refunding": f"/api/v1/orders/{order_id}/refund",
 "refunded": f"/api/v1/orders/{order_id}/confirm-refund",
 "cart": f"/api/v1/orders/{order_id}/revert-to-cart",
 }

 endpoint = endpoint_map.get(target_state, f"/api/v1/orders/{order_id}/transition")
 payload = {"target_state": target_state}

 try:
 async with session.post(f"{BASE_URL}{endpoint}",
 json=payload,
 headers=headers,
 timeout=aiohttp.ClientTimeout(total=10),) as resp:
 body = await resp.text()
 return {
 "status": resp.status,
 "body": body,
 "blocked": resp.status in (400, 403, 409, 422),
 }
 except Exception as e:
 return {"status": -1, "body": str(e), "blocked": False, "error": True}

async def test_illegal_transitions():
 """TraversalAllNon-methodStatustransfer change"""
 results = {"passed": [], "failed": [], "errors": []}

 async with aiohttp.ClientSession() as session:
 for from_state, to_state in sorted(ILLEGAL_TRANSITIONS):
 # Createhandle for from_state oftestOrder
 order_id = await create_test_order(session, from_state)
 if not order_id:
 results["errors"].append((from_state, to_state, "no methodCreatetestOrder"))
 continue

 # AttemptNon-method transfer change
 resp = await attempt_transition(session, order_id, to_state)
 label = f"{from_state} -> {to_state}"

 if resp.get("error"):
 results["errors"].append((from_state, to_state, resp["body"]))
 elif resp["blocked"]:
 results["passed"].append(label)
 else:
 results["failed"].append((label, resp["status"], resp["body"]))

 return results

async def test_payment_amount_tampering():
 """testPayment Amount Tampering"""
 async with aiohttp.ClientSession() as session:
 # Createcorrect commonOrder(false set lesson process price format 99.00)
 order_id = await create_test_order(session, "paying")

 # model PaymentCallback, butAmountnot match config
 tampered_amounts = [0.01, 0, -1, 98.99, 99.01, 9900]
 results = []

 for amount in tampered_amounts:
 payload = {
 "order_id": order_id,
 "paid_amount": amount,
 "payment_channel": "test",
 "transaction_id": f"TXN_TAMPER_{amount}",
 }
 async with session.post(f"{BASE_URL}/api/v1/payments/callback",
 json=payload,
 headers={"Content-Type": "application/json"},) as resp:
 blocked = resp.status in (400, 403, 409, 422)
 results.append({
 "amount": amount,
 "status": resp.status,
 "blocked": blocked,
 })

 return results

async def test_concurrent_pay_and_cancel():
 """Concurrencytest:same timePaymentandCancelSameOrder"""
 async with aiohttp.ClientSession() as session:
 order_id = await create_test_order(session, "paying")
 barrier = asyncio.Event()

 async def pay():
 await barrier.wait()
 return await attempt_transition(session, order_id, "paid")

 async def cancel():
 await barrier.wait()
 return await attempt_transition(session, order_id, "cancelled")

 # Createmany arrayConcurrencyany service(release largeRacewindow interface)
 pay_tasks = [pay() for _ in range(10)]
 cancel_tasks = [cancel() for _ in range(10)]
 all_tasks = asyncio.gather(*(pay_tasks + cancel_tasks))

 barrier.set()
 results = await all_tasks

 pay_success = sum(1 for r in results[:10] if not r.get("blocked", True))
 cancel_success = sum(1 for r in results[10:] if not r.get("blocked", True))

 return {
 "order_id": order_id,
 "pay_success": pay_success,
 "cancel_success": cancel_success,
 "total_success": pay_success + cancel_success,
 "verdict": "PASS" if (pay_success + cancel_success) <= 1 else "FAIL"
 }

def print_state_machine_report(illegal_results, amount_results, concurrent_result):
 """output outStatusmachine test report"""
 print("=" * 70)
 print(" Order State MachineSecuretest report")
 print("=" * 70)

 # Non-method transfer change
 print("\n[1] Non-methodStatustransfer changeTraversal")
 print(f" test total number: {len(ILLEGAL_TRANSITIONS)}")
 print(f" Pass: {len(illegal_results['passed'])}")
 print(f" Failure: {len(illegal_results['failed'])}")
 print(f" error: {len(illegal_results['errors'])}")

 if illegal_results["failed"]:
 print("\n!! the followingNon-method transfer change not be stop:")
 for label, status, body in illegal_results["failed"]:
 print(f" {label} => HTTP {status}")

 # Amount Tampering
 print("\n[2] Payment Amount Tamperingtest")
 if amount_results:
 for r in amount_results:
 status = "BLOCKED" if r["blocked"] else "ALLOWED"
 print(f" Amount {r['amount']:>10} => HTTP {r['status']} [{status}]")
 unblocked = [r for r in amount_results if not r["blocked"]]
 if unblocked:
 print(f" [FAIL] {len(unblocked)} tamper changeAmountnot beIntercept!")
 else:
 print(" [PASS] Alltamper changeAmountaverage beIntercept")

 # Concurrent Payment+Cancel
 print("\n[3] Concurrent Payment+Canceltest")
 print(f" PaymentSuccesstimesnumber: {concurrent_result['pay_success']}")
 print(f" CancelSuccesstimesnumber: {concurrent_result['cancel_success']}")
 print(f" determine set: [{concurrent_result['verdict']}]")
 if concurrent_result["verdict"] == "FAIL":
 print(" [FAIL] Ordersame time bePaymentandCancel - existinRace Condition!")

 print("=" * 70)

async def main():
 print("[*] open initialOrder State MachineSecuretest...\n")

 illegal_results = await test_illegal_transitions()
 amount_results = await test_payment_amount_tampering()
 concurrent_result = await test_concurrent_pay_and_cancel()

 print_state_machine_report(illegal_results, amount_results, concurrent_result)

if __name__ == "__main__":
 asyncio.run(main())
```

### 3.5 curl fast rateValidateScript(singlelinesCommand)

```bash
#!/usr/bin/env bash
# fast rateRace ConditionValidate - use curl ConcurrencySendRequest
# suitableusefor no has Python environment environmentoffast rateValidatescenario scene

BASE_URL="http://localhost:8000"
TOKEN="Bearer test_user_token"
COUPON_ID="COUPON_001"
CONCURRENCY=50
RESULTS_DIR="/tmp/race_test_$$"

mkdir -p "$RESULTS_DIR"

echo "[*] Send $CONCURRENCY ConcurrencyCoupondomain takeRequest..."

# useuse background jobs real currentConcurrency
for i in $(seq 1 $CONCURRENCY); do
 curl -s -o "$RESULTS_DIR/resp_$i.txt" -w "%{http_code}" \
 -X POST "$BASE_URL/api/v1/coupons/claim" \
 -H "Authorization: $TOKEN" \
 -H "Content-Type: application/json" \
 -d "{\"coupon_id\": \"$COUPON_ID\"}" \
 > "$RESULTS_DIR/status_$i.txt" 2>/dev/null &
done

# etc.pendingAllRequestcomplete
wait

# StatisticsResult
SUCCESS=0
FAIL=0
for i in $(seq 1 $CONCURRENCY); do
 code=$(cat "$RESULTS_DIR/status_$i.txt" 2>/dev/null)
 if ["$code" = "200"]; then
 SUCCESS=$((SUCCESS + 1))
 else
 FAIL=$((FAIL + 1))
 fi
done

echo "============================================"
echo " Success: $SUCCESS"
echo " Failure: $FAIL"
if ["$SUCCESS" -eq 1]; then
 echo " [PASS] Racedefense protectValid"
elif ["$SUCCESS" -eq 0]; then
 echo " [WARN] 0 timesSuccess, CheckConfiguration"
else
 echo " [FAIL] Racevulnerability!Success $SUCCESS times"
fi
echo "============================================"

# clear manage
rm -rf "$RESULTS_DIR"
```

---

## 4. Remediation Recommendation

### 4.1 CouponRace Conditionfix repeat

**method plan A:Databaseunique constraint(infer)**

```sql
-- in user_coupons table aboveAddunique constraint
ALTER TABLE user_coupons ADD UNIQUE INDEX uk_user_coupon (user_id, coupon_id);
```

```python
# Applicationlayer exploituseunique constraintofIdempotencywrite inject
def claim_coupon(user_id, coupon_id):
 try:
 db.execute("INSERT INTO user_coupons (user_id, coupon_id, claimed_at) VALUES (?,?, NOW())",
 user_id, coupon_id)
 return "success"
 except IntegrityError:
 return "already_claimed"
```

**method plan B:Redis Distributed Lock**

```python
import redis

def claim_coupon_with_lock(user_id, coupon_id):
 r = redis.Redis()
 lock_key = f"coupon_lock:{user_id}:{coupon_id}"

 # SET NX + EX real current principle sub lock
 if not r.set(lock_key, "1", nx=True, ex=10):
 return "already_claimed"

 try:
 # twotimesConfirm(defense stop lock expired afterofboundary boundary details)
 if db.query("SELECT 1 FROM user_coupons WHERE user_id=? AND coupon_id=?", user_id, coupon_id):
 return "already_claimed"
 db.execute("INSERT INTO user_coupons...", user_id, coupon_id)
 return "success"
 finally:
 r.delete(lock_key)
```

**method plan C:SELECT... FOR UPDATE(pessimistic lock)**

```python
def claim_coupon_pessimistic(user_id, coupon_id):
 with db.begin():
 # lineslevel lock, otherConcurrencyevent service
 coupon = db.query("SELECT * FROM coupons WHERE id=? FOR UPDATE",
 coupon_id)
 if coupon.remaining <= 0:
 return "sold_out"

 existing = db.query("SELECT 1 FROM user_coupons WHERE user_id=? AND coupon_id=?",
 user_id, coupon_id)
 if existing:
 return "already_claimed"

 db.execute("INSERT INTO user_coupons...", user_id, coupon_id)
 db.execute("UPDATE coupons SET remaining = remaining - 1 WHERE id=?", coupon_id)
 return "success"
```

### 4.2 Order State Machinefix repeat

**audit core principle rule:Statustransfer changemustis principle subof/has constraint of**

```python
# Statusmachine set define + Databaseoptimistic lock
class OrderStateMachine:
 TRANSITIONS = {
 "cart": {"pending"},
 "pending": {"paying", "cancelled"},
 "paying": {"paid", "pending"},
 "paid": {"completed", "refunding"},
 "refunding": {"refunded", "paid"},
 # "completed", "cancelled", "refunded" asfinal state, no out boundary
 }

 @classmethod
 def transition(cls, order_id: str, expected_from: str, target: str):
 allowed = cls.TRANSITIONS.get(expected_from, set())
 if target not in allowed:
 raise ValueError(f"Non-method transfer change: {expected_from} -> {target}")

 # optimistic lock:WHERE sub include include when firstStatus, defense stopConcurrencytamper change
 rows_affected = db.execute("""UPDATE orders
 SET status =?, updated_at = NOW(), version = version + 1
 WHERE id =? AND status =? AND version =?""",
 target, order_id, expected_from, current_version)

 if rows_affected == 0:
 raise ConcurrentModificationError("OrderStatusalready be other operationModify")

 return True
```

**PaymentCallbackAmountValidate**:

```python
def handle_payment_callback(callback_data):
 order = db.query("SELECT * FROM orders WHERE id=?", callback_data["order_id"])

 # 1. StatusValidate
 if order.status!= "paying":
 log.warning(f"Non-methodCallback:Order {order.id} Statusas {order.status}")
 return

 # 2. AmountValidate(part level level ratio, avoid point precision degree ask problem)
 expected_cents = int(order.total_price * 100)
 actual_cents = int(callback_data["paid_amount"] * 100)
 if expected_cents!= actual_cents:
 log.error(f"Amountnot match config:period {expected_cents}, real actual {actual_cents}")
 raise PaymentAmountMismatch()

 # 3. Idempotencyness(defense serious repeatCallback)
 if db.query("SELECT 1 FROM payment_records WHERE txn_id=?", callback_data["transaction_id"]):
 return # already handle manage through

 # 4. principle subStatustransfer change
 OrderStateMachine.transition(order.id, "paying", "paid")
```

---

## 5. testExecuteclear single

### No. onePhase:environment environment accurate prepare

- [] createTest Environment(andgenerate asset isolation)
- [] accurate prepareTest Accountand token
- [] ConfirmCouponandOrderof API Endpoint
- [] Createtest specialuseCoupon(Canserious set)
- [] part deployDatabasemonitor control(check query Log/locketc.pending)

### No. twoPhase:Race Conditiontest

- [] RC-01: singleUser 50 Concurrencydomain take(Python Script)
- [] RC-01: singleUser 100 Concurrencydomain take(Go Script, update extreme end)
- [] RC-02: inject inject 50ms after serious test
- [] RC-03: limit quantity coupon manyUser buy
- [] RC-04: many session Concurrency
- [] each rotate test afterCheckDatabasereal actualRecordnumber

### No. threePhase:Statusmachine test

- [] SM-01~SM-04: singleNon-method transfer change mobile dynamicValidate
- [] SM-09: self dynamic izeTraversalAll 48 typeNon-method transfer change
- [] SM-05: Concurrent Payment+Cancel(10rotate)
- [] SM-06: Amount Tampering(6typeAmount)
- [] SM-07: Negative Numberquantity/negative price formatShopping Cart
- [] SM-10: ConcurrencyModifyShopping Cart+under single

### No. fourPhase:return returnValidate

- [] fix repeat after serious AllFailureusecases
- [] testPassidentifier accurate:continuous continue 10 rotateAll PASS
- [] willtestScriptcollect completeto CI/CD flow horizontal line

---

## 6. Pass/Fail Criteria

| specified identifier | PASS | FAIL |
|------|------|------|
| singleUserConcurrencydomain take | Successtimesnumber = 1 | Successtimesnumber > 1 |
| limit quantity coupon initiate release | initiate release number <= limit quantity | initiate release number > limit quantity |
| Non-methodStatustransfer change | 100% be reject reject | any onePass |
| Amount Tampering | 100% beIntercept | any onePass |
| Concurrent Payment+Cancel | only one operationSuccess | two allSuccess |
| serious repeatPaymentCallback | Idempotencyhandle manage | serious repeat initiate release permission |
