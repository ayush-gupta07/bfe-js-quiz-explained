# [15 - Instanceof](https://bigfrontend.dev/quiz/instanceOf)

---

## ❓ Question

```js
console.log(typeof null)
console.log(null instanceof Object) 
console.log(typeof 1)
console.log(1 instanceof Number)
console.log(1 instanceof Object)
console.log(Number(1) instanceof Object)
console.log(new Number(1) instanceof Object)
console.log(typeof true)
console.log(true instanceof Boolean)
console.log(true instanceof Object)
console.log(Boolean(true) instanceof Object)
console.log(new Boolean(true) instanceof Object)
console.log([] instanceof Array)
console.log([] instanceof Object)
console.log((() => {}) instanceof Object)
```

---

## 🧾 Output

```
"object"
false
"number"
false
false
false
true
"boolean"
false
false
false
true
true
true
true
```

---

## 🔍 Step-by-step Explanation / Internal Implementation

### 🔸 `typeof null` and `null instanceof Object`
- `typeof null` → `"object"` (historical JavaScript bug).
- `null instanceof Object` → `false` because `null` has no prototype.

### 🔸 Primitive numbers vs Number objects
- `typeof 1` → `"number"` (primitive).
- `1 instanceof Number` → `false`, because primitive is not an object.
- `1 instanceof Object` → `false`.
- `Number(1)` → Converts to primitive `1`, so still `false`.
- `new Number(1)` → Returns a Number object, so `true`.

### 🔸 Booleans: primitive vs object
- `typeof true` → `"boolean"`.
- `true instanceof Boolean` → `false`, primitive.
- `true instanceof Object` → `false`.
- `Boolean(true)` → Converts to primitive `true`, so still `false`.
- `new Boolean(true)` → Boolean object wrapper → `true`.

### 🔸 Arrays and Functions
- `[] instanceof Array` → `true` (Arrays inherit from Array.prototype).
- `[] instanceof Object` → `true` (Array is also an Object).
- `(() => {}) instanceof Object` → `true` (functions are also objects).

---

## ✅ Things to Remember / Gotchas

- `typeof null` returns `"object"` – a **well-known bug** in JS.
- Primitives (`1`, `true`, etc.) are **not** instances of their constructor functions.
- Use `typeof` to check for primitive types.
- Use `instanceof` to check if an object was constructed by a particular constructor.
- `new Number(1)` or `new Boolean(true)` creates an **object wrapper**, which can behave differently.
- Avoid using `new Number()`, `new Boolean()`, `new String()` in real code – they cause confusion.
- Functions and Arrays are **objects**, hence `instanceof Object` is `true` for them.
