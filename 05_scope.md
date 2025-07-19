# [05 - Scope and Closures with `var` vs `let`](https://bigfrontend.dev/quiz/block-scope-1)

---

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

## Output

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

## Step-by-step Explanation / Internal Implementation

### Part 1: `var` loop

```js
for (var i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 0)
}
```

- `var` is **function-scoped**, not block-scoped.
- The `setTimeout` callback is scheduled for **later**, after the loop completes.
- By the time all `setTimeout`s run, the loop has already finished and `i = 5`.
- So each callback logs `5`.

📌 **Internal Behavior**:  
All 5 callbacks refer to the same binding of `i` (hoisted to the function/global scope), and the final value is `5`.

---

### Part 2: `let` loop

```js
for (let i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 0)
}
```

- `let` is **block-scoped** and creates a new binding for `i` on each iteration.
- Each iteration has a separate `i` value (thanks to TDZ and block scope).
- Thus, `0, 1, 2, 3, 4` are logged in order.

📌 **Internal Behavior**:  
JavaScript internally creates a new environment record for each iteration with its own copy of `i`.

---

## Things to Remember / Gotchas

- `var` does **not** create a new scope per iteration — all timeouts share the same `i`.
- `let` **does** create a new block scope in every loop iteration.
- This difference is crucial in asynchronous patterns like `setTimeout`.
- Use `let` to avoid unexpected closures when using loops with callbacks.
