# [09 - Null and Undefined in JavaScript](https://bigfrontend.dev/quiz/null-and-undefined)

## ❓ Question
```js
console.log(JSON.stringify([1, 2, null, 3]));
console.log(JSON.stringify([1, 2, undefined, 3]));
console.log(null === undefined);
console.log(null == undefined);
console.log(null == 0);
console.log(null < 0);
console.log(null > 0);
console.log(null <= 0);
console.log(null >= 0);
console.log(undefined == 0);
console.log(undefined < 0);
console.log(undefined > 0);
console.log(undefined <= 0);
console.log(undefined >= 0);
```

---

## ✅ Output

```
[1,2,null,3]
[1,2,null,3]
false
true
false
false
false
true
true
false
false
false
false
false
```

---

## 🧠 Step-by-Step Explanation / Internal Implementation

### JSON.stringify behavior:

- `null` is preserved in arrays.
- `undefined` is converted to `null` in arrays (omitted in objects).

```js
JSON.stringify([1, 2, null, 3]);        // → "[1,2,null,3]"
JSON.stringify([1, 2, undefined, 3]);   // → "[1,2,null,3]"
```

### Equality comparisons:

- `null === undefined` → `false` (strict comparison checks both value and type)
- `null == undefined` → `true` (special coercion rule in loose equality)

### `null` in numeric operations:

- `null` is coerced to `0` in numeric comparisons.
- So:
  - `null == 0` → `false` (equality check doesn't coerce `null` to number)
  - `null < 0` / `null > 0` → both `false` because `0 < 0` and `0 > 0` are false
  - `null <= 0` / `null >= 0` → both `true` because `0 <= 0` and `0 >= 0`

### `undefined` in numeric operations:

- `undefined` becomes `NaN` in numeric context.
- Any comparison with `NaN` is `false`, so:
  - `undefined == 0` → false
  - `undefined < 0`, `undefined > 0`, `undefined <= 0`, `undefined >= 0` → all false

---

## ⚠️ Things to Remember / Gotchas

- `undefined` is not a valid JSON type — it becomes `null` in arrays or is omitted in objects.
- `null` is a valid value and is preserved during serialization.
- `undefined` coerces to `NaN` in arithmetic, making all numeric comparisons return `false`.
- `null` coerces to `0` in numeric context, but not during equality checks (`null == 0` → `false`).
- Always prefer `===` to avoid confusing coercion between `null` and `undefined`.