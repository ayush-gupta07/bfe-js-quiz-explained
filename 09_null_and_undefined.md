# 09 - Null and Undefined in JavaScript

This code explores the subtle but crucial differences between `null` and `undefined` in JavaScript, demonstrating how they behave with JSON serialization, equality comparisons, and numeric operations. These distinctions often catch developers off guard.

---

### ✅ Output:

```js
console.log(JSON.stringify([1,2,null,3]))         // [1,2,null,3]
console.log(JSON.stringify([1,2,undefined,3]))    // [1,2,null,3]

console.log(null === undefined)   // false
console.log(null == undefined)    // true
console.log(null == 0)            // false
console.log(null < 0)             // false
console.log(null > 0)             // false
console.log(null <= 0)            // true
console.log(null >= 0)            // true

console.log(undefined == 0)       // false
console.log(undefined < 0)        // false
console.log(undefined > 0)        // false
console.log(undefined <= 0)       // false
console.log(undefined >= 0)       // false
```

---

### 🔍 Step-by-Step Explanation

#### 🧩 JSON.stringify
- `null` is a valid JSON value and is preserved during serialization.
- `undefined` is not a valid JSON type, so:
  - In arrays → it gets converted to `null`
  - In objects → it gets removed entirely

#### ⚖️ Equality Checks
- `null === undefined` → false (strict equality checks value **and** type)
- `null == undefined` → true (loose equality treats them as equivalent)
- `null == 0` → false (null is not loosely equal to 0)
- `undefined == 0` → false

#### 🔢 Numeric Comparisons
- `null` → coerced to `0` when used in numeric contexts
  - So: `null < 0`, `null > 0` → false
  - But: `null <= 0`, `null >= 0` → true
- `undefined` → coerced to `NaN`
  - All comparisons with `NaN` return `false`

---

### 🧠 Internal Implementation Insight

#### 🔧 How JavaScript treats `null` and `undefined` internally:

1. **In JSON.stringify:**
   - If array element is `undefined`, it's converted to `null`
   - If object property is `undefined`, it's omitted entirely

2. **In numeric contexts:**
   - `null` → coerced to `+0`
     ```js
     Number(null) // 0
     ```
   - `undefined` → coerced to `NaN`
     ```js
     Number(undefined) // NaN
     ```

3. **In comparisons:**
   - Comparisons like `>=` and `<=` convert both sides to numbers
   - Comparisons like `==` with `null` and `undefined` have special loose equality rules

---

### 📌 Things to Remember

- `null` and `undefined` are only loosely equal (`==`), but not strictly equal (`===`).
- `null` becomes `0` in numeric operations, `undefined` becomes `NaN`.
- JSON doesn’t recognize `undefined`, so it either removes it or converts it.
- Avoid using `==` for comparisons—always prefer `===` to avoid surprises.

---

### ⚠️ Gotchas & Interview Traps

- `undefined` in arrays becomes `null` in `JSON.stringify`, but disappears in objects.
- `null <= 0` is `true`, while `null == 0` is `false` due to different coercion logic.
- All comparisons involving `undefined` and numbers are `false` because of `NaN`.

---
