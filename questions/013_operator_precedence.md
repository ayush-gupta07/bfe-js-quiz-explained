# [13 - Operator Precedence](https://bigfrontend.dev/quiz/operator-precedence)

## ❓ Question
```js
console.log(0 == 1 == 2)
console.log(2 == 1 == 0)
console.log(0 < 1 < 2)
console.log(1 < 2 < 3)
console.log(2 > 1 > 0)
console.log(3 > 2 > 1)
```

## ✅ Output

```
false
true
true
true
true
false
```

---

## 🧠 Step-by-Step Explanation / Internal Implementation

JavaScript evaluates operators **left to right**, and comparison operators (`==`, `<`, `>`) return a boolean (`true` or `false`), which can get **coerced into numbers** (`true → 1`, `false → 0`) when used in further comparisons.

### Equality Cases:
1. `0 == 1 == 2`
   - First: `0 == 1` → `false`
   - Then: `false == 2` → `0 == 2` → `false`

2. `2 == 1 == 0`
   - First: `2 == 1` → `false`
   - Then: `false == 0` → `0 == 0` → `true`

### Inequality Cases:
3. `0 < 1 < 2`
   - First: `0 < 1` → `true`
   - Then: `true < 2` → `1 < 2` → `true`

4. `1 < 2 < 3`
   - First: `1 < 2` → `true`
   - Then: `true < 3` → `1 < 3` → `true`

5. `2 > 1 > 0`
   - First: `2 > 1` → `true`
   - Then: `true > 0` → `1 > 0` → `true`

6. `3 > 2 > 1`
   - First: `3 > 2` → `true`
   - Then: `true > 1` → `1 > 1` → `false`

---

## ⚠️ Things to Remember / Gotchas

- JavaScript does not evaluate chained comparisons like `1 < x < 5` mathematically.
- Comparisons return booleans, and booleans are coerced to numbers in further evaluations.
- Use logical operators explicitly for range comparisons:  
  **`x > 1 && x < 5`** ✅ instead of **`1 < x < 5`** ❌
- `true` becomes `1`, `false` becomes `0` in numeric contexts.
- Be cautious when chaining comparison or equality operators.
