# electronic commerce under singleInterfaceCodeaudit check report

## audit check for

`POST /api/order/create` - electronic commerce under singleInterface

---

## vulnerability clear single

### 1. Negative Number/zero number quantity inject inject - price format operation manipulate

**Severity: Severe (Critical)**

`quantity` not do anyValidate.attack attack personCanpass injectNegative Numberorzero:
- `quantity = -10` -> `total_price` changeasNegative Number, Platformreverse toward""User
- `quantity = 0` -> zeroyuanunder single, take commerce product
- point number `quantity = 0.001` -> extremeLowprice format buy buy

```python
# vulnerability trigger initiate
POST {"product_id": 1, "quantity": -5}
# total_price = 100 * (-5) = -500
```

**Remediation Recommendation:**
```python
quantity = data.get('quantity')
if not isinstance(quantity, int) or quantity <= 0:
 return jsonify({'error': 'number quantitymustascorrect integer number'}), 400
```

---

### 2. CouponAmountnot do under limit protect protect - negative priceOrder

**Severity: Severe (Critical)**

Coupondiscount deductDirectfromtotal priceinreduce, no hasCheck Resultwhether isnegative:
- commerce product total price 50 yuan, Couponpage amount 100 yuan -> `total_price = -50`
- config combineNegative Numbernumber quantityCanadvance one step release large

```python
# when first logic logic
total_price -= coupon.discount_amount # no under limit protect protect
```

**Remediation Recommendation:**
```python
total_price -= coupon.discount_amount
total_price = max(total_price, 0) # orset mostLowPaymentAmountsuch as 0.01
```

---

### 3. Couponno useusetimesnumber/return attributeValidate - no limit repeatuse & use

**Severity: Severe (Critical)**

CoupononlyCheck `is_valid`, existinthe followingask problem:
- **no limit repeatuse**: SameCouponCanreverse repeat useuse, not identifier recordasalready useuse
- **noUserBinding**: anyUserCanuseuseother personofCouponcode
- **no useusecondition**: notCheckCouponsuitableusecommerce product/mostLowmessage fee etc.

**Remediation Recommendation:**
```python
coupon = Coupon.query.filter_by(code=coupon_code).first()
if not coupon:
 return jsonify({'error': 'Couponnot existin'}), 400
if not coupon.is_valid:
 return jsonify({'error': 'CouponalreadyInvalidate'}), 400
if coupon.used_count >= coupon.max_usage:
 return jsonify({'error': 'Couponalready reach useuseabove limit'}), 400
if coupon.user_id and coupon.user_id!= current_user.id:
 return jsonify({'error': 'no permission useuseCoupon'}), 403
if coupon.min_amount and total_price < coupon.min_amount:
 return jsonify({'error': 'not reachCouponmostLowmessage fee'}), 400

# under singleSuccessafter identifier recordCouponalready useuse
coupon.used_count += 1
```

---

### 4. commerce product not existintime NoneType - reject reject service

**Severity: High (High)**

`Product.query.get(product_id)` Return `None` time, under onelines `product.price * quantity` Direct `AttributeError`, Causing 500 error.attack attack personCanusenot existinof `product_id` reverse repeat trigger initiateServerabnormal common.

**Remediation Recommendation:**
```python
product = Product.query.get(product_id)
if not product:
 return jsonify({'error': 'commerce product not existin'}), 404
```

---

### 5. noInventoryValidate - super

**Severity: High (High)**

complete all no hasCheckcommerce productInventory, CanCausing:
- super:Inventoryas 0 stillCanunder single
- large quantity no method constraintofOrder

**Remediation Recommendation:**
```python
if product.stock < quantity:
 return jsonify({'error': 'InventoryInsufficient'}), 400

# under single time deduct reduceInventory(need config combineDatabaselock)
product.stock -= quantity
```

---

### 6. no commerce productStatusValidate - under architecture commerce productCanbuy buy

**Severity: High (High)**

notCheckcommerce productwhetherabove architecture/Can.already under architecture/disable /expected not open initialofcommerce product averagedirectly usablebuy buy.

**Remediation Recommendation:**
```python
if not product.is_on_sale:
 return jsonify({'error': 'commerce product already under architecture'}), 400
```

---

### 7. Race Condition - Concurrencyunder singleCausingsuper /Couponsuperuse

**Severity: High (High)**

ReadInventory/CouponStatusandwrite inject between no lock protect protect.HighConcurrencyscenario scene under:
- manyRequestsame time readtoInventory=1, each self under singleSuccess -> super
- manyRequestsame time useuseSameCoupon -> Couponsuper amount useuse

**Remediation Recommendation:**
```python
# method plan1: Databaselineslevel lock(pessimistic lock)
product = Product.query.with_for_update().get(product_id)

# method plan2: optimistic lock(version Field)
Product.query.filter_by(id=product_id, version=product.version)\.update({'stock': product.stock - quantity, 'version': product.version + 1})

# method plan3: Redis Distributed LockuseforCoupon
```

---

### 8. output injectParameterMissingtime - reject reject service

**Severity: in (Medium)**

`data['product_id']` and `data['quantity']` useusehard take value, Missingtime `KeyError`.`request.json` in Content-Type not for timeReturn `None`, advance while `TypeError`.

**Remediation Recommendation:**
```python
data = request.json
if not data:
 return jsonify({'error': 'Request BodycannotasEmpty'}), 400

product_id = data.get('product_id')
quantity = data.get('quantity')
if not product_id or not quantity:
 return jsonify({'error': 'missing less must needParameter'}), 400
```

---

### 9. product_id type notValidate - SQL inject inject / abnormal common

**Severity: in (Medium)**

`product_id` not do typeValidate. SQLAlchemy ORM of `.get()` wild commonSecure, but pass injectNon-expected period type(character symbol string/number array/Dictionary)CancanCausingabnormal commonorinother ORM operationincite initiate ask problem.

**Remediation Recommendation:**
```python
if not isinstance(product_id, int) or product_id <= 0:
 return jsonify({'error': 'product_id mustascorrect integer number'}), 400
```

---

### 10. price format useuseFrontendComputeResult - price format tamper change risk

**Severity: in (Medium)**

 when firstCodefromDatabasetake price format(`product.price`), but price formatininternal existinComputeafterDirectexist injectOrder, inbetween no has twotimesValidatemachine make.such asif businessinexistinlimit time price/ priceetc.dynamic state set price logic logic, missing system one price formatComputeservice Causingprice format not one cause.

**Remediation Recommendation:**
```python
# useusesystem one price formatComputeservice
total_price = PriceService.calculate(product, quantity, current_user, coupon)
```

---

### 11. no buy buy number quantity above limit - meaning goods / integer number out

**Severity: in (Medium)**

`quantity` no above limit limit make, attack attack personCanpass inject extreme large number value:
- `quantity = 999999999` -> meaning goods
- extreme end large numberCancanCausingprice formatCompute out

**Remediation Recommendation:**
```python
MAX_QUANTITY_PER_ORDER = 99
if quantity > MAX_QUANTITY_PER_ORDER:
 return jsonify({'error': f'singletimesbuy buy not super through{MAX_QUANTITY_PER_ORDER}item'}), 400
```

---

### 12. no serious repeat under single defense protect - serious repeatSubmit

**Severity: in (Medium)**

noIdempotencyness protect protect.UserNetwork dynamicor meaning serious repeatSubmitCanCreatemany related sameOrder.

**Remediation Recommendation:**
```python
# method plan1: Frontendgenerate complete oneRequestID, Backend serious
idempotency_key = data.get('idempotency_key')
existing = Order.query.filter_by(idempotency_key=idempotency_key).first()
if existing:
 return jsonify({'order_id': existing.id, 'total': existing.total_price})

# method plan2: Redis Distributed Lock + TTL
```

---

### 13. event service notComplete - Datanot one cause

**Severity: in (Medium)**

when first only has `add + commit`, such asif after continuerequiresdeductInventory/identifier recordCouponalreadyuse/CreatePaymentsingleetc.operation, any oneFailureCausingDatanot one cause.missing lessCompleteofevent service manage manage.

**Remediation Recommendation:**
```python
try:
 product.stock -= quantity
 coupon.used_count += 1
 db.session.add(order)
 db.session.commit()
except Exception:
 db.session.rollback()
 return jsonify({'error': 'under singleFailure, please serious test'}), 500
```

---

### 14. noLogandaudit plan - no method abnormal commonlinesas

**Severity: Low (Low)**

under single operation no anyLogRecord.out current single/ etc.abnormal commonlinesastime no method.

**Remediation Recommendation:**
```python
import logging
logger = logging.getLogger('order')
logger.info(f'User{current_user.id}under single: product={product_id}, qty={quantity}, '
 f'coupon={coupon_code}, total={total_price}')
```

---

### 15. ResponseInformation Disclosure - information collect collect

**Severity: Low (Low)**

when commerce product not existinorCouponno valid time(fix repeat after), error messageshouldsystem one, avoid attack attack personPassDifferentResponseEnumerationValidofcommerce productIDorCouponcode.

**Remediation Recommendation:** for external part output injectoferror useusesystem oneofmodel error message, Detailedinformation only writeLog.

---

## vulnerabilitySeverityremit total

| level level | number quantity | vulnerabilityID |
|------|------|---------|
| Severe (Critical) | 3 | #1 Negative Numbernumber quantity, #2 negative priceOrder, #3 Couponabuseuse |
| High (High) | 4 | #4 Emptyspecified, #5 super, #6 under architectureCanbuy, #7 Race Condition |
| in (Medium) | 6 | #8 ParameterMissing, #9 typeValidate, #10 price format one cause ness, #11 number quantity above limit, #12 serious repeat under single, #13 event serviceCompleteness |
| Low (Low) | 2 | #14 audit planLog, #15 Information Disclosure |

**total plan: 15 Business Logic Vulnerability**

---

## fix repeatPrioritycreate protocol

1. **standalone that is fix repeat** (P0): #1, #2, #3, #4, #5, #7 - Directimpact response resource fundsSecureandDataCompleteness
2. ** fast fix repeat** (P1): #6, #8, #9, #11, #12, #13 - impact response business correct confirm ness
3. **plan fix repeat** (P2): #10, #14, #15 - increase strong nessandCanoptimistic test ness
