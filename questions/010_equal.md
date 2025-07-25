# [10 - Equal (`==`) Behavior in JavaScript](https://bigfrontend.dev/quiz/Equal-1)

## ❓ Question
```js
console.log(0 == false)
console.log('' == false)
console.log([] == false)
console.log(undefined == false)
console.log(null == false)
console.log('1' == true)
console.log(1n == true)
console.log(' 1     ' == true)
```

## ✅ Output
```txt
true
true
true
false
false
true
true
true
```

---

## 🧠 Step-by-Step Explanation / Internal Implementation

### 1. `0 == false`
- Coercion occurs.
- `false` converts to `0` → `0 == 0` → ✅ `true`.

### 2. `'' == false`
- `''` (empty string) coerces to `0`.
- `false` coerces to `0`.
- `0 == 0` → ✅ `true`.

### 3. `[] == false`
- `[]` becomes `''` via `toString()`, then coerced to `0`.
- `false` becomes `0`.
- `0 == 0` → ✅ `true`.

### 4. `undefined == false`
- No coercion rule that equates `undefined` to `false`.
- ❌ `false`.

### 5. `null == false`
- Similar to `undefined`, `null` does **not** equal `false`.
- ❌ `false`.

### 6. `'1' == true`
- `'1'` becomes `1`.
- `true` becomes `1`.
- `1 == 1` → ✅ `true`.

### 7. `1n == true`
- `1n` (BigInt) coerces to `1`.
- `true` becomes `1`.
- `1 == 1` → ✅ `true`.

### 8. `' 1     ' == true`
- String is trimmed and becomes `'1'` → number `1`.
- `true` becomes `1`.
- ✅ `1 == 1` → `true`.

---

## ⚠️ Things to Remember / Gotchas

- `==` performs **type coercion**, which leads to unexpected results.
- `0`, `''`, and `[]` are **loosely equal** to `false` due to coercion to `0`.
- `undefined` and `null` are only equal to **each other** using `==`.
- Whitespace in strings like `' 1 '` is **trimmed** during coercion to number.
- **BigInt (`1n`)** can be coerced in loose comparisons but not with strict equality.
- ❗ **Best Practice**: Use `===` for predictable and consistent behavior.