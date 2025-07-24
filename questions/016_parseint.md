# [16 - ParseInt](https://bigfrontend.dev/quiz/parseInt)

---

## ❓ Question
```js
console.log(['0'].map(parseInt))
console.log(['0','1'].map(parseInt))
console.log(['0','1','1'].map(parseInt))
console.log(['0','1','1','1'].map(parseInt))
```

## 🟩 Output
```
[0]
[0, NaN]
[0, NaN, 1]
[0, NaN, 1, 1]
```

---

## 🧠 Step-by-Step Explanation / Internal Implementation

### 🔍 How `map` and `parseInt` Interact

- `Array.prototype.map` passes **three arguments** to the callback:
  1. Current element
  2. Index
  3. The array itself

- `parseInt` takes:
  1. A string to parse
  2. An optional **radix** (base)

Because `map` passes the index as the second argument, that index ends up being interpreted as the **radix**!

---

### 🧪 Line-by-line Breakdown

#### `['0'].map(parseInt)`
- `parseInt('0', 0)` → 0 (base 10 is inferred when radix is 0)

#### `['0', '1'].map(parseInt)`
- `parseInt('0', 0)` → 0
- `parseInt('1', 1)` → NaN (base 1 is invalid)

#### `['0', '1', '1'].map(parseInt)`
- `parseInt('0', 0)` → 0
- `parseInt('1', 1)` → NaN
- `parseInt('1', 2)` → 1 (binary 1)

#### `['0', '1', '1', '1'].map(parseInt)`
- `parseInt('0', 0)` → 0
- `parseInt('1', 1)` → NaN
- `parseInt('1', 2)` → 1
- `parseInt('1', 3)` → 1 (valid in base 3)

---

## ⚠️ Things to Remember / Gotchas

- `map(parseInt)` is a classic JS gotcha! ❌
- Always wrap `parseInt` like this: `array.map(x => parseInt(x))` ✅
- Radix passed incorrectly = unexpected `NaN`
- `parseInt('1', 1)` → NaN because base-1 is invalid
- `parseInt('1', 2)` → 1 (binary)
- `map` passes more arguments than you expect—know your function signatures

---
