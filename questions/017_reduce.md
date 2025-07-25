# [17 - Reduce](https://bigfrontend.dev/quiz/reduce)

## ❓ Question
```js
[1,2,3].reduce((a,b) => {
  console.log(a,b)
});

[1,2,3].reduce((a,b) => {
  console.log(a,b)
}, 0);
```

## ✅ Output
```
1 2
undefined 3
0 1
undefined 2
undefined 3
```

## 🧠 Step-by-step Explanation / Internal Implementation

### First `reduce` Call (No Initial Value):
- The first element (`1`) is used as the initial accumulator `a`.
- The reducer starts with `a=1`, `b=2` and logs `1 2`.
- But since the reducer does not return anything, `a` becomes `undefined` for the next iteration.
- Now, `a=undefined`, `b=3` is logged.

### Second `reduce` Call (With Initial Value 0):
- The accumulator starts at `0` (`a=0`), first value is `b=1`, logs `0 1`.
- Again, no return means `a=undefined` in next round: logs `undefined 2`
- Again, `a=undefined`, `b=3` is logged.

### Internal Behavior:
- When you omit the return statement in a reducer, `undefined` is used as the accumulator for the next step.
- If no initial value is passed, the first array element is the initial accumulator and iteration starts from index 1.
- If an initial value is provided, iteration starts from index 0.

## ⚠️ Things to Remember / Gotchas
- Always return a value inside `reduce`; otherwise, accumulator becomes `undefined`.
- Use `forEach` if you only want side effects like `console.log`, not accumulation.
- Passing an initial value is safer, especially for empty arrays.
- `reduce` without initial value throws an error on empty arrays.