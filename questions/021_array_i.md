# [21 - Array I](https://bigfrontend.dev/quiz/Array-I)

## ❓ Question
```javascript
const a = [0]
console.log(a.length)
a[3] = 3
console.log(a.length)
for (let item of a) {
  console.log(item)
}
a.map(item => {console.log(item)})
a.forEach(item => {console.log(item)})
console.log(Object.keys(a))
delete a[3]
console.log(a.length)
a[2] = 2
a.length = 1
console.log(a[0], a[1], a[2])
```

---

## ✅ Output

```
1
4
0
undefined
undefined
3
0
3
0
3
[ '0', '3' ]
4
0 undefined undefined
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

1. `const a = [0]` initializes an array with one element at index 0.
2. `console.log(a.length)` logs `1` as there's only one element.
3. `a[3] = 3` creates a **sparse array**. It sets index 3 to 3, leaving indices 1 and 2 empty (holes).
4. `console.log(a.length)` logs `4` because the array's length becomes the highest index + 1.
5. `for (let item of a)` iterates over indices 0 to 3:
   - Outputs `0`, `undefined`, `undefined`, `3`.
6. `a.map(...)` and `a.forEach(...)` skip holes:
   - Only log `0` and `3`, skipping undefined slots at 1 and 2.
7. `Object.keys(a)` logs only the existing property keys: `['0', '3']`.
8. `delete a[3]` removes index 3 from the array (a "hole" is created), but does **not** reduce the length.
9. `console.log(a.length)` logs `4` (still the same length).
10. `a[2] = 2` fills the hole at index 2.
11. `a.length = 1` truncates the array — all elements after index 0 are removed.
12. `console.log(a[0], a[1], a[2])` logs `0 undefined undefined` because only index 0 still exists.

---

## ⚠️ Things to Remember / Gotchas

- Assigning to a high index creates a sparse array — intermediate indices become "holes".
- `for...of` iterates over all indices, including holes (returns `undefined`).
- `map` and `forEach` **skip holes** — they only process present elements.
- `delete` removes the element but doesn't reduce the `length`.
- Setting `length` manually truncates the array and deletes elements beyond the new length.
- `Object.keys()` reflects actual set indices (as string keys), not array length or holes.