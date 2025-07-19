# [07 - Increment Operator](https://bigfrontend.dev/quiz/Increment-Operator)

## ❓ Question

What does the code snippet below output via `console.log`?

```js
let a = 1
const b = ++a
const c = a++
console.log(a)
console.log(b)
console.log(c)
```

---

## Output

```
3
2
2
```

---

## Step by Step Explanation / Internal Implementation

### Initial State:
- `a = 1`

### Step 1: `const b = ++a`
- `++a` is **pre-increment**, meaning `a` is incremented **before** its value is assigned to `b`.
- `a` becomes `2`, then `b` is assigned `2`.
- Internally:
  - `a = a + 1 // a is now 2`
  - `b = a`

### Step 2: `const c = a++`
- `a++` is **post-increment**, meaning the value of `a` is assigned to `c` **before** `a` is incremented.
- `c` gets `2`, then `a` becomes `3`.
- Internally:
  - `c = a // c gets 2`
  - `a = a + 1 // a is now 3`

### Step 3: Final `console.log` statements:
- `console.log(a)` → `3`
- `console.log(b)` → `2`
- `console.log(c)` → `2`

---

## Things to Remember / Gotchas

- `++a` (**pre-increment**): Increments the value, **then** returns it.
- `a++` (**post-increment**): Returns the value, **then** increments it.
- Internally, even without assigning to a variable, post/pre increment directly mutates the variable in-place.
- `a++` is not just a value-returning expression; it also mutates `a` after usage.
- If you're debugging or tracing, remember: **the change happens even if you don’t capture it in another variable.**