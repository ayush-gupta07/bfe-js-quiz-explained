# [05 - Scope and Closures with `var` vs `let`](https://bigfrontend.dev/quiz/block-scope-1)

## ❓ Question

```js
for (var i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 0)
}

for (let i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 0)
}
```

---

## ✅ Output

```
5
5
5
5
5
0
1
2
3
4
```

---

## 🧠 Step-by-Step Explanation

### 🔹 Part 1 – Using `var`

```js
for (var i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 0);
}
```

- `var` is function-scoped or globally-scoped, **not block-scoped**.
- All `setTimeout` callbacks capture the same reference to the variable `i`.
- By the time the callbacks run, the loop has already completed, and `i` is `5`.
- So `console.log(i)` prints `5` five times.

### 🔹 Part 2 – Using `let`

```js
for (let i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 0);
}
```

- `let` is block-scoped.
- For every iteration, a new block scope is created with a new binding of `i`.
- So each callback captures a **different** `i` for each loop.
- Hence, the output is `0 1 2 3 4`.

---

## 🧪 Key Learnings

- `var` is **not block-scoped**; `let` and `const` are.
- `setTimeout` uses the event loop, so callbacks execute **after** the loop finishes.
- The value of variables in closures depends on **when and how** they were declared.

---

## ⚠️ Gotchas to Watch Out For

- `var`-declared variables are **shared** across all iterations when used with asynchronous code.
- To "fix" the `var` behavior, use `let` or wrap each iteration in an IIFE (Immediately Invoked Function Expression).

---

## ✅ Final Output Recap

```
5
5
5
5
5
0
1
2
3
4
```
05_scope.md
Displaying 05_scope.md.