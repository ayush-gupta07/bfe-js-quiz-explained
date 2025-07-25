# [20 - Name for Function Expression](https://bigfrontend.dev/quiz/name-for-Function-expression)

## ❓ Question
```js
function a(){
}
const b = function() {

}

const c = function d() {
  console.log(typeof d)
  d = 'e'
  console.log(typeof d)
}

console.log(typeof a)
console.log(typeof b)
console.log(typeof c)
console.log(typeof d)
c()
```

---

## ✅ Output

```
function
function
function
undefined
function
string
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

1. `function a() {}` is a **function declaration**, hoisted to the top of the scope. So `typeof a` is `"function"`.

2. `const b = function() {}` is an **anonymous function expression**, assigned to the variable `b`. So `typeof b` is `"function"`.

3. `const c = function d() { ... }` is a **named function expression**:
   - The function is assigned to the variable `c`.
   - The internal name `d` is only accessible **inside** the function's own body.

4. `typeof c` → `"function"` because `c` holds a function.

5. `typeof d` outside the function → `undefined` because `d` is not defined in the outer scope. It's scoped only within the body of the function `d`.

6. Calling `c()`:
   - Inside the function, `typeof d` logs `"function"` because `d` refers to the function itself.
   - `d = 'e'` attempts to reassign `d`. In **non-strict mode**, this assignment **shadows** the internal binding and turns `d` into a string.
   - `typeof d` then logs `"string"`.

Note: In **strict mode**, reassigning `d` would throw a `TypeError`.

---

## ⚠️ Things to Remember / Gotchas

- **Named Function Expressions**: The name (`d` in `const c = function d() {}`) is **only accessible inside the function**.
- The internal name `d` is **not accessible outside** the function.
- Reassigning the named function variable inside itself is **allowed in non-strict mode** but throws in **strict mode**.
- `typeof d` outside returns `"undefined"` because `d` is not defined in that scope.