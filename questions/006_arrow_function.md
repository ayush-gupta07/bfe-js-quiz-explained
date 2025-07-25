# [06 - Arrow Function](https://bigfrontend.dev/quiz/6-Arrow-Function)

## ❓Question
```js
const obj = {
  dev: 'bfe',
  a: function() {
    return this.dev
  },
  b() {
    return this.dev
  },
  c: () => {
    return this.dev
  },
  d: function() {
    return (() => {
      return this.dev
    })()
  },
  e: function() {
    return this.b()
  },
  f: function() {
    return this.b
  },
  g: function() {
    return this.c()
  },
  h: function() {
    return this.c
  },
  i: function() {
    return () => {
      return this.dev
    }
  }
}

console.log(obj.a())
console.log(obj.b())
console.log(obj.c())
console.log(obj.d())
console.log(obj.e())
console.log(obj.f()())
console.log(obj.g())
console.log(obj.h()())
console.log(obj.i()())
```

## ✅ Output

```
bfe
bfe
undefined
bfe
bfe
undefined
undefined
undefined
bfe
```

## 🧠 Step-by-step Explanation / Internal Implementation

1. `obj.a()` → Regular function → `this` refers to `obj` → returns `"bfe"`.
2. `obj.b()` → Shorthand method → same as regular function → returns `"bfe"`.
3. `obj.c()` → Arrow function → does not bind its own `this` → `this` is global → returns `undefined`.
4. `obj.d()` → Regular function containing an arrow function → `this` in arrow inherited from `d()` context → returns `"bfe"`.
5. `obj.e()` → Calls `this.b()` → works normally → returns `"bfe"`.
6. `obj.f()` → Returns method `b` → calling it without context → `this` is `undefined` → returns `undefined`.
7. `obj.g()` → Calls `this.c()` (an arrow function) → returns `undefined`.
8. `obj.h()` → Returns `this.c`, then invokes it → still arrow function without proper `this` → returns `undefined`.
9. `obj.i()` → Returns arrow function that closes over `this` (bound to `obj`) → returns `"bfe"`.

## ⚠️ Things to remember / Gotchas

- 🔥 **Arrow functions do not have their own `this`**. They inherit it from their enclosing lexical scope.
- ❗ Extracting method references (like `obj.f()()`) loses the original object binding unless explicitly bound.
- 📌 Functions defined using arrow syntax within another method will capture the outer `this` properly.
- 🧠 Method shorthand (`b() {}`) behaves same as `b: function() {}` in terms of `this`.
- ⚠ `obj.c` and `obj.c()` both use arrow functions with no `this` → resolves to `undefined`.
- ✅ Arrow functions returned from methods like `i` will still capture correct `this` if declared within a method call context.