# [19 - This](https://bigfrontend.dev/quiz/this)

### ❓ Question
```js
const obj = {
  a: 1,
  b: function() {
    console.log(this.a)
  },
  c() {
    console.log(this.a)
  },
  d: () => {
    console.log(this.a)
  },
  e: (function() {
    return () => {
      console.log(this.a);
    }
  })(),
  f: function() {
    return () => {
      console.log(this.a);
    }
  }
}

console.log(obj.a)
obj.b()
;(obj.b)()
const b = obj.b
b()
obj.b.apply({a: 2})
obj.c()
obj.d()
;(obj.d)()
obj.d.apply({a:2})
obj.e()
;(obj.e)()
obj.e.call({a:2})
obj.f()()
;(obj.f())()
obj.f().call({a:2})
```

---

### ✅ Output

```txt
1
1
1
undefined
2
1
undefined
undefined
undefined
undefined
undefined
undefined
1
1
1
```

---

### 🧠 Step-by-Step Explanation / Internal Implementation

- `obj.a`: Returns `1`
- `obj.b()`: Traditional function, `this` is bound to `obj`, logs `1`
- `(obj.b)()`: Same as above due to grouping operator, logs `1`
- `const b = obj.b; b()`: Loses `this`, defaults to `undefined` in strict mode
- `obj.b.apply({a:2})`: `this` is explicitly set to `{a:2}`, logs `2`
- `obj.c()`: Method shorthand behaves like normal function, logs `1`
- `obj.d()`: Arrow function inherits `this` from global scope (undefined), logs `undefined`
- `(obj.d)()`: Same as above
- `obj.d.apply({a:2})`: Arrow function ignores apply, logs `undefined`
- `obj.e()`: Arrow function returned from IIFE, captures `this` from IIFE (global), logs `undefined`
- `(obj.e)()`: Same
- `obj.e.call({a:2})`: Arrow function ignores call binding, logs `undefined`
- `obj.f()()`: Returns arrow function from method, arrow function captures `this` as `obj`, logs `1`
- `(obj.f())()`: Same as above
- `obj.f().call({a:2})`: Call ignored by arrow function, `this` still refers to `obj`, logs `1`

---

### ⚠️ Things to Remember / Gotchas

- Regular functions (`b`, `c`, `f`) bind `this` based on how they're **called**.
- Arrow functions (`d`, `e`) **lexically bind** `this` — they **ignore** `.call()`, `.apply()`, `.bind()`.
- Assigning a method to a variable detaches it from its object context.
- `this` in IIFE is global (or `undefined` in strict mode).
- Use arrow functions cautiously inside objects when `this` context is required.
