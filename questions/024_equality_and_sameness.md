# [24 - Equality & Sameness](https://bigfrontend.dev/quiz/Equality-Sameness)

## ❓ Question
```javascript
console.log(0 == '0')
console.log(0 === '0')
console.log(Object.is(0, '0'))

console.log(0 == 0)
console.log(0 === 0)
console.log(Object.is(0, 0))

console.log(0 == -0)
console.log(0 === -0)
console.log(Object.is(0, -0))

console.log(NaN == NaN)
console.log(NaN === NaN)
console.log(Object.is(NaN, NaN))

console.log(0 == false)
console.log(0 === false)
console.log(Object.is(0, false))
```

---

## ✅ Output

```
true
false
false
true
true
true
true
true
false
false
false
true
true
false
false
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

### **Group 1: `0` vs `'0'`**
- `0 == '0'` → `true` (loose equality coerces string `'0'` to number `0`)
- `0 === '0'` → `false` (strict equality: different types)
- `Object.is(0, '0')` → `false` (same as `===` for different types)

### **Group 2: `0` vs `0`**
- `0 == 0` → `true` (same value, same type)
- `0 === 0` → `true` (same value, same type)
- `Object.is(0, 0)` → `true` (same value, same type)

### **Group 3: `0` vs `-0`**
- `0 == -0` → `true` (loose equality treats them as equal)
- `0 === -0` → `true` (strict equality treats them as equal)
- `Object.is(0, -0)` → `false` (**Only `Object.is()` distinguishes `+0` from `-0`**)

### **Group 4: `NaN` vs `NaN`**
- `NaN == NaN` → `false` (NaN is never equal to anything, including itself)
- `NaN === NaN` → `false` (NaN is never equal to anything, including itself)
- `Object.is(NaN, NaN)` → `true` (**Only `Object.is()` treats NaN as equal to itself**)

### **Group 5: `0` vs `false`**
- `0 == false` → `true` (loose equality coerces `false` to `0`)
- `0 === false` → `false` (strict equality: different types)
- `Object.is(0, false)` → `false` (same as `===` for different types)

### 🔍 Internal Mechanics

- **`==` (Loose Equality)**: Performs type coercion using ToNumber/ToString conversion
- **`===` (Strict Equality)**: No coercion, but treats `+0 === -0` and `NaN !== NaN`
- **`Object.is()`**: "Same Value" algorithm - like `===` but fixes the `+0/-0` and `NaN` edge cases

---

## ⚠️ Things to Remember / Gotchas

- **Only `Object.is()`** correctly handles `NaN` and `+0/-0` edge cases.
- `NaN` is the **only value** that's not equal to itself in `==` and `===`.
- `+0` and `-0` are equal in `==` and `===` but different in `Object.is()`.
- `==` performs **unpredictable coercion** - avoid it except for `null/undefined` checks.
- `Object.is()` is the **most precise** equality check in JavaScript.
- Remember: `Object.is(NaN, NaN)` is `true`, but `NaN === NaN` is `false`!
