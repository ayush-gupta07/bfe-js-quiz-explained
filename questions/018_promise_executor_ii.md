# [18 - Promise Executor II](https://bigfrontend.dev/quiz/Promise-executor-II)

---

## ❓ Question
```js
const p1 = Promise.resolve(1)
const p2 = new Promise((resolve) => resolve(p1))
const p3 = Promise.resolve(p1)
const p4 = p2.then(() => new Promise((resolve) => resolve(p3)))
const p5 = p4.then(() => p4)

console.log(p1 == p2)
console.log(p1 == p3)
console.log(p3 == p4)
console.log(p4 == p5)
```

## Output
```
false
true
false
false
```

## Step-by-step Explanation / Internal Implementation

### Step 1: `const p1 = Promise.resolve(1)`
- `p1` is a resolved Promise with the value `1`.

### Step 2: `const p2 = new Promise((resolve) => resolve(p1))`
- `p2` is a new Promise that resolves **with** `p1`, not `1`. 
- So `p2` will eventually settle to the same value as `p1`, but it’s a **different object**.

### Step 3: `const p3 = Promise.resolve(p1)`
- `Promise.resolve` detects that `p1` is already a Promise.
- So instead of creating a new one, it **returns the same instance**.
- ✅ `p1 === p3` is `true`.

### Step 4: `const p4 = p2.then(() => new Promise((resolve) => resolve(p3)))`
- `p2.then()` always returns a **new** Promise.
- Even though the callback returns `p3`, a new wrapper Promise (`p4`) is created.
- So `p3 !== p4`.

### Step 5: `const p5 = p4.then(() => p4)`
- Again, `.then()` creates a **new** Promise (`p5`), even if the returned value is a Promise (`p4`).
- `p5` resolves to `p4` but they are different objects.

### Final Console Logs:
```js
console.log(p1 == p2) // false, different objects
console.log(p1 == p3) // true, same object
console.log(p3 == p4) // false, different Promise objects
console.log(p4 == p5) // false, different Promise objects
```

## Things to remember / Gotchas

- `Promise.resolve(somePromise)` returns the **same promise** if `somePromise` is already a resolved Promise.
- `.then()` **always returns a new Promise**, regardless of the return value.
- Promises are objects — equality checks compare **references**, not resolved values.
- Resolving a Promise with another Promise chains their resolutions but **does not merge** them into the same object.