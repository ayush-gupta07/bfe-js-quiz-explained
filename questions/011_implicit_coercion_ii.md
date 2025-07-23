# [11 - Implicit Coercion II](https://bigfrontend.dev/quiz/Implicit-Conversion-II)

---

## ❓ Question

```js
console.log([] + []);
console.log([] + 1);
console.log([[]] + 1);
console.log([[1]] + 1);
console.log([[[[2]]]] + 1);
console.log([] - 1);
console.log([[]] - 1);
console.log([[1]] - 1);
console.log([[[[2]]]] - 1);
console.log([] + {});
console.log({} + {});
console.log({} - {});
```

---

## ✅ Output

```
""
"1"
"1"
"11"
"21"
-1
-1
0
1
"[object Object]"
"[object Object][object Object]"
NaN
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

### ➕ Array Addition (`+`)
- `[] + []` → `"" + ""` → `""`
- `[] + 1` → `"" + "1"` → `"1"`
- `[[]] + 1` → `"" + "1"` → `"1"` (inner empty array becomes `""`)
- `[[1]] + 1` → `"1" + "1"` → `"11"` (`[1]` becomes `"1"`)
- `[[[[2]]]] + 1` → `"2" + "1"` → `"21"` (deep nesting flattens to `"2"`)

### ➖ Array Subtraction (`-`)
- `[] - 1` → `0 - 1` → `-1` (empty array coerces to `0`)
- `[[]] - 1` → `0 - 1` → `-1` (still treated as empty → `0`)
- `[[1]] - 1` → `1 - 1` → `0`
- `[[[[2]]]] - 1` → `2 - 1` → `1`

### 🟰 Object Operations
- `[] + {}` → `"" + "[object Object]"` → `"[object Object]"`
- `{ } + {}` → Interpreted as expression → `"[object Object][object Object]"`
- `{ } - {}` → `NaN - NaN` → `NaN` (objects can't be coerced to numbers)

---

## 🔍 Things to Remember / Gotchas

- Arrays convert to strings via `.toString()` when used with `+`.
- Arrays convert to numbers using `Number()` when used with `-`.
- `[[]].toString()` → `""`, `[[1]].toString()` → `"1"`, `[[[[2]]]].toString()` → `"2"`
- `[]` coerces to `0` in numeric context, becomes `""` in string context.
- `{}` when used with `+` gets converted to `"[object Object]"`.
- Object subtraction like `{} - {}` results in `NaN` because `Number({}) → NaN`.
- The parser may treat `{}` as a block or an object literal. Wrap in parentheses for clarity if needed.

---