# electronic commerce under singleInterfaceSecureaudit plan report

> **Methodcomment:** WooYun Business Logic Vulnerability Methodology v2.0(22,132 real realCase)
> **audit planTarget:** `POST /api/order/create` under singleInterface
> **audit plan day period:** 2026-03-06

---

## No. onePhase:business flow process map map

### business manage decode

- **Applicationtype:** electronic commercePlatform
- **audit core flow process:** commerce product -> under single -> Payment -> lines
- **participateandperson:** alreadyLoginUser(`@login_required`)
- **resource funds flow toward:** UserPayment `total_price` buy buy commerce product

### InterfaceStatustransfer move

```
ClientSubmit(product_id, quantity, coupon_code)
 -> check query commerce product price format
 -> Computetotal price
 -> ApplicationCoupondiscount deduct
 -> Create Order(status='pending')
 -> Return order_id + total
```

### Trust BoundaryAnalyze

| boundary boundary | when firstStatus | risk |
|------|---------|------|
| Client -> Server | `quantity` byClientDirectpass inject, noValidate | High |
| Client -> Server | `product_id` no existinnessValidate | in |
| Client -> Server | `coupon_code` no return attribute/useusetimesnumberValidate | Severe |
| Database -> business logic logic | no event service isolation, existinRacewindow interface | High |
| business scale rule -> output out | `total_price` Canasnegative/zero, no under limitValidate | Severe |

---

## No. twoPhase:false set completeandvulnerabilityDiscover

totalIdentify **9 Business Logic Vulnerability**, bySevereness sequence rank list.

---

### vulnerability 1:AmountCantamper changeasNegative Number - Coupondiscount deduct no above limit

- **Severity:** Severe(Critical)
- **Domain:** Financial - Amount Tampering
- **WooYun mode:** Amount Tampering(176 Case, 83.0% High Risk)+ Payment Bypass(1,056 Case, 68.7% High Risk)

**Vulnerability Analysis:**

```python
total_price = product.price * quantity # false set product.price=10, quantity=1 -> 100
total_price -= coupon.discount_amount # such asif coupon.discount_amount=200 -> total_price = -100
```

Codein `total_price -= coupon.discount_amount` after no has any under limitValidate.such asifCouponof `discount_amount` greater thancommerce product total price, `total_price` willchangeas**Negative Number**.attack attack personCanas:

1. select Lowprice commerce product(such as ¥1), configHighpage amountCoupon
2. generate complete negativeAmountOrder, inPayment/result algorithm environment sectionCancan trigger initiate**reverse towardTransfer**(PlatformtowardUserpay payment)

**WooYun Case References:**
- "Baidu can micro +innational less base fundsSystemCantamper change paymentAmount" - Amountno under limitCausingtamper change
- "M1905Movie site value2588Packageonly costs5jiao" - price format error abnormal 5000

**StatisticsData:** WooYun Amount TamperingDomain 176 Casein 83.0% asHigh Risk, Financialtest law clear confirm specified out:"reject not information anyClientfinance serviceCompute".

**Remediation Recommendation:**

```python
# 1. Serverend strong make price format under limit
total_price = max(total_price, 0.01) # mostLow 1 part

# 2. Coupondiscount deductcannotsuper through commerce product total price
if coupon.discount_amount >= product.price * quantity:
 discount = product.price * quantity - 0.01 # most many reduceto 0.01
else:
 discount = coupon.discount_amount
total_price -= discount
```

---

### vulnerability 2:Couponno useusetimesnumber limit make - Canno limit serious repeat useuse

- **Severity:** Severe(Critical)
- **Domain:** Financial - discount deduct/Couponabuseuse
- **WooYun mode:** Payment Tampering - discount deduct abuseuseCheckclear singleNo. 3 items(1,056 Case, 68.7% High Risk)

**Vulnerability Analysis:**

```python
if coupon_code:
 coupon = Coupon.query.filter_by(code=coupon_code).first()
 if coupon and coupon.is_valid:
 total_price -= coupon.discount_amount
 # <- Missing:coupon.is_valid not be setas False
 # <- Missing:notRecordCouponandOrder/UserofBindingkey system
 # <- Missing:notCheckthisUserwhetheralready useusethrough Coupon
```

attack attack personCanas:
1. SameCouponcodeinmanyOrderin**serious repeat useuse**
2. useother personofCouponcode under single(no return attributeValidate)
3. willexpiredCouponand `is_valid` not correct confirm maintain protectofdetails result combine exploituse

**WooYun Case References:**
- Financialdomain participate referenceFile"discount deduct/Couponabuseuse"Checkclear single:`serious repeatApplicationSameCoupon`/`useuseexpiredCoupon`/`useuse forDifferentproductCategoryofCoupon`
- "Datebao official site business-logic vulnerability allowed buying insurance for free or at an extremely low price" - priority logic logicBypass

**StatisticsData:** Payment Tampering 1,056 Casein, Couponabuseuseis most common seenofsubAttack Vectorof one.

**Remediation Recommendation:**

```python
# 1. CheckCouponuseusetimesnumber/UserBinding
if coupon.used_count >= coupon.max_uses:
 return jsonify({'error': 'Couponalreadyusecomplete'}), 400
if CouponUsage.query.filter_by(coupon_id=coupon.id, user_id=current_user.id).first():
 return jsonify({'error': ' already useusethrough thisCoupon'}), 400

# 2. under singleSuccessafter identifier recordCouponalready useuse
coupon.used_count += 1
db.session.add(CouponUsage(coupon_id=coupon.id, user_id=current_user.id, order_id=order.id))

# 3. CheckCouponsuitableuseScope(product type/mostLowmessage fee)
if coupon.min_amount and total_price < coupon.min_amount:
 return jsonify({'error': 'not reachtoCouponmostLowmessage fee'}), 400
```

---

### vulnerability 3:Race Condition - Coupon/InventoryConcurrencymessage

- **Severity:** Severe(Critical)
- **Domain:** logic logic flow - Race Condition / TOCTOU
- **WooYun mode:** Race Condition(266 Case, 74.8% High Risk)

**Vulnerability Analysis:**

```python
# line process A # line process B
coupon = query(code='SAVE50') coupon = query(code='SAVE50')
coupon.is_valid -> True coupon.is_valid -> True (not beAmessage)
total_price -= 50 total_price -= 50
order = Order(...) order = Order(...)
db.session.commit() db.session.commit()
# Result:oneitemsonetimesnessCouponbe twoOrdersame time useuse
```

integer `check queryCoupon -> Validate -> deduct reduce -> Create Order` flow process no has anyConcurrencycontrol make:
- noDatabaseevent service isolation(`SELECT... FOR UPDATE`)
- noDistributed Lock(Redis SETNX)
- no optimistic lock(version version numberValidate)

same manage, such asif commerce product hasInventorylimit make, existin**Inventorysuper **ofRacewindow interface.

**WooYun Case References:**
- logic logic flow domain participate referenceFile TOCTOU mode:`line processA:CheckBalance(100) -> -> deduct payment(100)` and `line processB` ConcurrencyCausingdual flower
- Financialdomain"Race Condition"Checkclear single:`Coupon rate:andlinesApplicationSamesingletimesuseuseCoupon`/`Inventory rate:andlinesbuy buy most after one item commerce product`

**StatisticsData:** Race Conditiontype vulnerability 266 Casein 74.8% asHigh Risk, inFinancialoperationin other cause fatal.

**Remediation Recommendation:**

```python
# method plan A:Databasepessimistic lock
coupon = Coupon.query.filter_by(code=coupon_code).with_for_update().first()

# method plan B:optimistic lock(principle subUpdate)
result = db.session.execute("UPDATE coupons SET used_count = used_count + 1 "
 "WHERE code =:code AND used_count < max_uses",
 {"code": coupon_code})
if result.rowcount == 0:
 return jsonify({'error': 'CouponalreadyInvalidate'}), 400

# method plan C:Distributed Lock(Redis)
with redis_lock(f"coupon:{coupon_code}", timeout=5):
 # Check + deduct reduce + Create Order
```

---

### vulnerability 4:number quantity(quantity)noValidate - Negative Number/zero/small number/ out

- **Severity:** High(High)
- **Domain:** Financial - number quantity tamper change
- **WooYun mode:** Payment Tampering - number quantity tamper changeCheckclear single(1,056 Case, 68.7% High Risk)

**Vulnerability Analysis:**

```python
quantity = data['quantity'] # no typeValidate/noScopeValidate
total_price = product.price * quantity # quantity=-1 -> total_price asnegative
```

Attack Vector:

| attack attack output inject | valid if |
|---------|------|
| `quantity = 0` | `total_price = 0`, avoid fee under single |
| `quantity = -1` | `total_price` asNegative Number, Cancan trigger initiate reverse towardPayment |
| `quantity = 0.001` | small number buy buy, CancanBypassInventoryinteger numberCheck |
| `quantity = 99999999` | integer number outorInventorysuper |
| `quantity = "abc"` | type errorCausing 500 Serverabnormal common |

**WooYun Case References:**
- FinancialdomainCheckclear single clear confirm list out:`number quantity setas 0(avoid fee commerce product)`/`number quantity setas -1(Negative Numberbuy buy = Refund)`/`number quantity setasNon-common largeofnumber character(integer number out)`/`number quantity setassmall number(0.001 item)`
- " sub a locationSeverelogic logic vulnerability" - electronic commerce number quantity/Amountlogic logicBypass

**StatisticsData:** number quantity tamper change isPayment Tampering 1,056 CaseinofNo. 2 large attack attack page, onlytimesfor price formatDirecttamper change.

**Remediation Recommendation:**

```python
# severe formatofServerend output injectValidate
if not isinstance(quantity, int) or quantity <= 0:
 return jsonify({'error': 'number quantitymustascorrect integer number'}), 400
if quantity > MAX_ORDER_QUANTITY: # business above limit, such as 999
 return jsonify({'error': 'super out singletimesbuy buy above limit'}), 400
```

---

### vulnerability 5:missing less commerce product existinnessandStatusValidate

- **Severity:** High(High)
- **Domain:** logic logic flow - Design Flaw / Business Rule Bypass
- **WooYun mode:** Design Flaw(1,391 Case, 65.3% High Risk)

**Vulnerability Analysis:**

```python
product = Product.query.get(product_id)
total_price = product.price * quantity # such asif product as None -> AttributeError (500)
```

ask problem clear single:
1. **product as None time no handle manage** - not existinof `product_id` Causing 500 error, CancanDisclosureServerstack stack information
2. **notCheckcommerce productStatus** - already under architecture/not above architecture/already ofcommerce product stillCanunder single
3. **notCheckcommerce productInventory** - CancanCausingsuper
4. **product_id type notValidate** - pass injectNon-integer numberCancan trigger initiateDatabaseabnormal common

**WooYun Case References:**
- logic logic flow domain"Design Flaw"mode:`Serverinformation anyClientprovide provideof:price format/Role/user_id/Permissionlevel level`
- "114Ticketing site logic flaw used payment timeout to leak sensitive information for tens of thousands of users" - StatusValidateMissing

**StatisticsData:** Design Flaw 1,391 Casein 65.3% asHigh Risk.

**Remediation Recommendation:**

```python
product = Product.query.get(product_id)
if not product:
 return jsonify({'error': 'commerce product not existin'}), 404
if product.status!= 'active':
 return jsonify({'error': 'commerce product already under architecture'}), 400
if product.stock < quantity:
 return jsonify({'error': 'InventoryInsufficient'}), 400
```

---

### vulnerability 6:missing lessIdempotencyness control make - serious repeat under single

- **Severity:** High(High)
- **Domain:** Financial - Order Tampering
- **WooYun mode:** Order Tampering(1,227 Case, 74.2% High Risk)+ Race Condition

**Vulnerability Analysis:**

Interfaceno has anyIdempotencyness machine make:
- noIdempotencykey(idempotency key)
- noRequest serious
- noFrontenddefense afterofServer

User(orattack attack person)Canas forSameRequestfast rate serious repeatSubmit, Createlarge quantity serious repeatOrder.result combineCouponvulnerability, CanasuseSameitemsCouponCreate N break discountOrder.

**WooYun Case References:**
- Financialdomain defense defense mode clear confirm need require:`Idempotencykey: one transaction easy ID, reject reject serious repeat`
- Order Tamperingtest protocol protocol:`whether canmanytimestrigger initiate?`

**StatisticsData:** Order Tampering 1,227 Casein 74.2% asHigh Risk.

**Remediation Recommendation:**

```python
# Clientgenerate complete oneRequest ID, ServerValidate
idempotency_key = data.get('idempotency_key')
if not idempotency_key:
 return jsonify({'error': 'missing lessIdempotencykey'}), 400

existing = Order.query.filter_by(idempotency_key=idempotency_key).first()
if existing:
 return jsonify({'order_id': existing.id, 'total': existing.total_price})
```

---

### vulnerability 7:missing lessUserDimensionofOrderRate Limit

- **Severity:** in(Medium)
- **Domain:** logic logic flow - Business Rule Bypass
- **WooYun mode:** Business Rule Bypass(266 Case, 74.8% High Risk)

**Vulnerability Analysis:**

Interfaceno has anyRate Limit(rate limiting), attack attack personCanas:
1. ScriptizeBatchunder single, Inventory(meaning goods)
2. config combineCouponvulnerabilityBatch
3. forSysteminitiate initiate resource source attack attack(eachtimesunder single all writeDatabase)

**WooYun Case References:**
- Financialdomain monitor control need require:`Highfrequency rate:EachUsereachminutesmanyOrder/Withdrawal`
- logic logic flow domain"infer abuseuse"modeofvariant - Batchself dynamic ize exploituse

**StatisticsData:** Business Rule Bypass 266 Casein 74.8% asHigh Risk.

**Remediation Recommendation:**

```python
# Redis dynamic window interfaceRate Limiting
from flask_limiter import Limiter
limiter = Limiter(app, key_func=lambda: current_user.id)

@app.route('/api/order/create', methods=['POST'])
@login_required
@limiter.limit("10/minute") # eachminutesmost many 10 single
def create_order():...
```

---

### vulnerability 8:Order ID Predictable(order sequence integer number)

- **Severity:** in(Medium)
- **Domain:** Authorization - IDOR / Information Disclosure
- **WooYun mode:** horizontal levelPermissionBypass / IDOR(1,705 Case, 62.3% High Risk)

**Vulnerability Analysis:**

```python
return jsonify({'order_id': order.id, 'total': total_price})
```

`order.id` isDatabaseself increase primary key(order sequence integer number), attack attack personCanas:
1. PassEnumeration `order_id` infer judgePlatformOrderquantity
2. such asif otherInterface(such ascheck queryOrderdetailed details)not do return attributeValidate, CanTraversalAllOrder(IDOR)
3. Pass ID error value assess algorithm for mobileofbusiness quantity

**WooYun Case References:**
- "Beijing Hyundai platform allowed unauthorized traversal of millions of identity documents/vehicle registration documents" - order sequence ID CausingBatchTraversal
- Authorization Domain IDOR Checkclear single:`ID Enumeration:Traversal ID Scope`/`UUID prediction(such asif useusedone order sequence UUID)`

**StatisticsData:** IDOR 1,705+230 Casein, order sequence ID is most common seenofroot because.Authorization Domainparticipate referenceFilespecified out:"simple single change ID only shareCaseof 30%", but this 30% is mostLowcomplete versionofattack attack.

**Remediation Recommendation:**

```python
import uuid

class Order(db.Model):
 id = db.Column(db.Integer, primary_key=True) # internal part useuse
 order_no = db.Column(db.String(36), default=lambda: str(uuid.uuid4()), unique=True)

# for external only expose exposure order_no
return jsonify({'order_id': order.order_no, 'total': total_price})
```

---

### vulnerability 9:missing less output inject base foundationValidate - Abnormal InputCausingServererror

- **Severity:** in(Medium)
- **Domain:** logic logic flow - Design Flaw
- **WooYun mode:** Design Flaw - Clientinformation any(1,391 Case, 65.3% High Risk)

**Vulnerability Analysis:**

```python
data = request.json # such asif Content-Type not is JSON -> None -> TypeError
product_id = data['product_id'] # such asifMissing -> KeyError -> 500
quantity = data['quantity'] # such asifMissing -> KeyError -> 500
```

not ofabnormal common Causing:
1. **500 errorDisclosurestack stack information** - Cancan expose exposureFilePath/Databaseresult structure/framework architecture version version
2. **reject reject service** - meaning structure forgeofRequest Bodyhold continue trigger initiate abnormal common
3. **type mix ** - `product_id` pass inject number arrayorfor Cancan trigger initiate ORM Non-expected periodlinesas

**WooYun Case References:**
- logic logic flow domain"type mix "mode:`character symbol string "0" vs integer number 0 vs deploy value false`
- Design Flawmode:`Validatenot one cause - FrontendValidate, BackendnotValidate`

**StatisticsData:** Design Flaw 1,391 Casein 65.3% asHigh Risk, Among them"Clientinformation any"is out current frequency rate mostHighofroot because mode.

**Remediation Recommendation:**

```python
from marshmallow import Schema, fields, validate

class CreateOrderSchema(Schema):
 product_id = fields.Integer(required=True, strict=True)
 quantity = fields.Integer(required=True, strict=True, validate=validate.Range(min=1, max=999))
 coupon_code = fields.String(load_default=None, validate=validate.Length(max=50))

schema = CreateOrderSchema()
errors = schema.validate(request.json or {})
if errors:
 return jsonify({'errors': errors}), 400
```

---

## No. threePhase:vulnerability remit total matrix matrix

| # | vulnerability | Severity | Domain | WooYun Casebase number | high-risk percentage |
|---|------|---------|------|---------------|---------|
| 1 | AmountCanasNegative Number(Coupondiscount deduct no above limit) | **Severe** | Financial | 176 | 83.0% |
| 2 | Couponno limit serious repeat useuse | **Severe** | Financial | 1,056 | 68.7% |
| 3 | Race Condition(Coupon/InventoryConcurrency) | **Severe** | logic logic flow | 266 | 74.8% |
| 4 | number quantity noValidate(Negative Number/zero/ out) | **High** | Financial | 1,056 | 68.7% |
| 5 | commerce product existinness/StatusnotValidate | **High** | logic logic flow | 1,391 | 65.3% |
| 6 | missing lessIdempotencyness(serious repeat under single) | **High** | Financial | 1,227 | 74.2% |
| 7 | noOrderRate Limit | **in** | logic logic flow | 266 | 74.8% |
| 8 | Order ID Predictable(order sequence integer number) | **in** | Authorization | 1,705 | 62.3% |
| 9 | missing less output inject base foundationValidate | **in** | logic logic flow | 1,391 | 65.3% |

---

## No. fourPhase: combine fix repeat method plan

### fix repeat afterofparticipate referenceCode

```python
from marshmallow import Schema, fields, validate
from sqlalchemy import and_
import uuid

class CreateOrderSchema(Schema):
 product_id = fields.Integer(required=True, strict=True)
 quantity = fields.Integer(required=True, strict=True, validate=validate.Range(min=1, max=999))
 coupon_code = fields.String(load_default=None, validate=validate.Length(max=50))
 idempotency_key = fields.String(required=True, validate=validate.Length(min=16, max=64))

@app.route('/api/order/create', methods=['POST'])
@login_required
@limiter.limit("10/minute")
def create_order():
 # [fix repeat9] output injectValidate
 schema = CreateOrderSchema()
 data = schema.load(request.json or {})

 product_id = data['product_id']
 quantity = data['quantity']
 coupon_code = data.get('coupon_code')
 idempotency_key = data['idempotency_key']

 # [fix repeat6] IdempotencynessValidate
 existing = Order.query.filter_by(idempotency_key=idempotency_key).first()
 if existing:
 return jsonify({'order_id': existing.order_no, 'total': float(existing.total_price)})

 # [fix repeat5] commerce product existinness + StatusValidate
 product = Product.query.get(product_id)
 if not product or product.status!= 'active':
 return jsonify({'error': 'commerce product not existinoralready under architecture'}), 400

 # [fix repeat5] InventoryValidate(pessimistic lock defenseRace)
 product = Product.query.filter_by(id=product_id).with_for_update().first()
 if product.stock < quantity:
 return jsonify({'error': 'InventoryInsufficient'}), 400

 # [fix repeat4] number quantity already by Schema Validateascorrect integer number

 # ServerendComputetotal price(reject not information anyClient)
 total_price = product.price * quantity
 discount = 0

 if coupon_code:
 # [fix repeat3] pessimistic lock defenseCouponRace
 coupon = Coupon.query.filter_by(code=coupon_code).with_for_update().first()

 if not coupon or not coupon.is_valid:
 return jsonify({'error': 'Couponno valid'}), 400

 # [fix repeat2] Checkuseusetimesnumber + UserDimension serious
 if coupon.used_count >= coupon.max_uses:
 return jsonify({'error': 'Couponalreadyusecomplete'}), 400
 if CouponUsage.query.filter_by(coupon_id=coupon.id, user_id=current_user.id).first():
 return jsonify({'error': ' already useusethrough thisCoupon'}), 400

 # [fix repeat1] discount deductcannotsuper through commerce product total price, and total pricecannotasnegative
 discount = min(coupon.discount_amount, total_price - Decimal('0.01'))
 total_price -= discount

 # identifier recordCouponalready useuse
 coupon.used_count += 1

 # [fix repeat1] most final:total pricemust > 0
 if total_price <= 0:
 return jsonify({'error': 'OrderAmountabnormal common'}), 400

 # deduct reduceInventory
 product.stock -= quantity

 # [fix repeat8] useusenotPredictableofOrdernumber
 order = Order(user_id=current_user.id,
 product_id=product_id,
 quantity=quantity,
 total_price=total_price,
 status='pending',
 order_no=str(uuid.uuid4()),
 idempotency_key=idempotency_key)
 db.session.add(order)

 if coupon_code:
 db.session.add(CouponUsage(coupon_id=coupon.id,
 user_id=current_user.id,
 order_id=order.id))

 db.session.commit()

 return jsonify({'order_id': order.order_no, 'total': float(total_price)})
```

### architecture structure layer pageHardeningcreate protocol

| | Targetvulnerability | real current method mode |
|------|---------|---------|
| Distributed Lock | Race Condition | Redis SETNX, Financialoperationmuststringlinesize |
| message list | Idempotencyness + one cause ness | OrderCreateabnormal step ize, good onetimes define |
| for accountSystem | Amount Tampering | each day self dynamic for account:OrderAmount vs real actual collect payment |
| abnormal common monitor control | All | report alert scale rule:Amountunicode-22640.01 / singleUserHighfrequency under single / Couponabnormal common useuse |
| WAF scale rule | output injectValidate | InterceptNon- JSON Request Body/super large payload |

---

## WooYun Statisticstotal result

versiontimesaudit plan cover coverof WooYun Vulnerability Patterninvolving forshouldCasetotal quantity:

| mode | WooYun Case Count | versionInterfacefatalin |
|------|-------------|-----------|
| Payment Tampering(includeAmount/number quantity/Coupon) | 1,056 | vulnerability 1, 2, 4 |
| Order Tampering | 1,227 | vulnerability 6 |
| Race Condition / TOCTOU | 266 | vulnerability 3 |
| Design Flaw | 1,391 | vulnerability 5, 9 |
| IDOR / Horizontal Authorization Bypass | 1,705 | vulnerability 8 |
| Business Rule Bypass | 266 | vulnerability 7 |
| **combine plan cover cover** | **5,911** | **9 vulnerability** |

> 28 linesCode, 9 Business Logic Vulnerability.WooYun 22,132 Casereverse repeat cert clear:**Business Logic Vulnerabilityno methodPassScandeviceDiscover, we hiddeninopen initiate personof"version meaning"andCode"real actual allow allow"betweenofEmptyin.**
