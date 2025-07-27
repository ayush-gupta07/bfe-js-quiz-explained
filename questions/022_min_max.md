# [22 - Min Max](https://bigfrontend.dev/quiz/min-max)

## ❓ Question
```javascript
console.log(Math.min())
console.log(Math.max())
console.log(Math.min(1))
console.log(Math.max(1,2))
console.log(Math.min([1,2,3]))
```

---

## ✅ Output

```
Infinity
-Infinity
1
2
NaN
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

1. `Math.min()` with **no arguments** returns `Infinity`:
   - This is the identity value for min operations (any number compared to Infinity will be smaller).
   - Think of it as "the smallest possible starting point" for comparison.

2. `Math.max()` with **no arguments** returns `-Infinity`:
   - This is the identity value for max operations (any number compared to -Infinity will be larger).
   - Think of it as "the largest possible starting point" for comparison.

3. `Math.min(1)` with **one argument** simply returns that value: `1`.

4. `Math.max(1,2)` with **multiple arguments** returns the largest: `2`.

5. `Math.min([1,2,3])` with an **array argument** returns `NaN`:
   - `Math.min` expects individual numbers, not arrays.
   - Arrays are coerced to strings first: `[1,2,3]` becomes `"1,2,3"`.
   - `"1,2,3"` cannot be converted to a valid number, so it becomes `NaN`.
   - Any comparison with `NaN` returns `NaN`.

### 🔍 Internal Mechanics

- `Math.min/max` use **identity values** when no arguments are provided.
- These functions **don't automatically spread arrays** - you need `Math.min(...array)`.
- Type coercion follows: Array → String → Number → NaN (if invalid).
- `NaN` propagates through all mathematical operations.

---

## ⚠️ Things to Remember / Gotchas

- `Math.min()` returns `Infinity`, `Math.max()` returns `-Infinity` (seems counterintuitive!).
- Arrays are **not automatically spread** - use `Math.min(...[1,2,3])` instead.
- Passing non-numeric values (including arrays) results in `NaN`.
- These identity values ensure that `Math.min(Infinity, x) = x` and `Math.max(-Infinity, x) = x`.
- Remember: Empty calls return the "neutral" starting values for comparisons.
