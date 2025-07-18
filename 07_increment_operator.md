### 📘 07_increment_operator.md

```js
let a = 1
const b = ++a
const c = a++
console.log(a)
console.log(b)
console.log(c)
```

---

### ✅ Output

```
3
2
2
```

---

### 🔍 Step-by-Step Explanation

1. `let a = 1;`  
   ➤ Variable `a` is initialized with `1`.

---

2. `const b = ++a;`  
   ➤ This is a **prefix increment**.  
   ➤ It increments `a` to `2` **first**, then assigns the value to `b`.  
   ➤ So `a = 2`, `b = 2`.

---

3. `const c = a++;`  
   ➤ This is a **postfix increment**.  
   ➤ It assigns current `a` (which is `2`) to `c`, and **then** increments `a` to `3`.  
   ➤ So `c = 2`, and now `a = 3`.

---

4. `console.log(a)` → `3`  
5. `console.log(b)` → `2`  
6. `console.log(c)` → `2`

---

### ⚙️ What JavaScript Does Internally

#### `++a` is interpreted as:

```js
a = a + 1        // Read `a`, add 1, assign back to `a`
return a         // Return new value (2)
```

#### `a++` is interpreted as:

```js
let temp = a     // Store original value (2)
a = a + 1        // Increment `a` → now 3
return temp      // Return original value (2)
```

Even when not assigning to a new variable, the increment affects `a` directly because of the hidden memory update.

---

### 🧠 Things to Remember

- `++a` (prefix) → Increments first, then returns.
- `a++` (postfix) → Returns first, then increments.
- JavaScript **always updates `a` internally**, even if result is not assigned.
- Internal transformation: `++a → a = a + 1`, `a++ → return temp = a; a = a + 1`.

---

### ❗ Gotchas to Watch Out For

- **Don’t assume** `a++` does nothing if not assigned — `a` **does** get incremented!
- These hidden assignments happen behind the scenes even if the result is not used.
- `const b = ++a` and `const c = a++` behave differently because of **return value order**.

---
