# [26 - True or False](https://bigfrontend.dev/quiz/true-or-false)

## ❓ Question
```javascript
console.log([] == 0)
console.log([] == false)
console.log(!![])
console.log([1] == 1)
console.log(!![1])
console.log(Boolean([]))
console.log(Boolean(new Boolean([])))
console.log(Boolean(new Boolean(false)))
```

---

## ✅ Output

```
true
true
true
true
true
true
true
true
```

---

## 🧠 Step-by-step Explanation / Internal Implementation

1. **`[] == 0` → `true`**
   - Array `[]` is converted to primitive using `ToPrimitive()`
   - `[].toString()` returns `""` (empty string)
   - `""` is coerced to `0` using `ToNumber()`
   - `0 == 0` is `true`

2. **`[] == false` → `true`**
   - `false` is coerced to `0` using `ToNumber(false)`
   - Array `[]` follows same conversion as above: `[] → "" → 0`
   - `0 == 0` is `true`

3. **`!![]` → `true`**
   - First `!` converts `[]` to boolean: `![]` = `!true` = `false`
   - Second `!` negates: `!false` = `true`
   - Arrays are always truthy objects, so `Boolean([])` is `true`

4. **`[1] == 1` → `true`**
   - Array `[1]` is converted to primitive
   - `[1].toString()` returns `"1"`
   - `"1"` is coerced to `1` using `ToNumber()`
   - `1 == 1` is `true`

5. **`!![1]` → `true`**
   - Same logic as `!![]`: arrays are truthy objects
   - `![1]` = `!true` = `false`
   - `!false` = `true`

6. **`Boolean([])` → `true`**
   - `Boolean()` constructor converts to boolean
   - All objects (including empty arrays) are truthy
   - `Boolean([])` is `true`

7. **`Boolean(new Boolean([]))` → `true`**
   - `new Boolean([])` creates a Boolean object wrapper
   - `Boolean([])` is `true`, so `new Boolean([])` wraps `true`
   - `Boolean()` of any object (including Boolean objects) is `true`
   - Boolean objects are always truthy, regardless of their wrapped value

8. **`Boolean(new Boolean(false))` → `true`**
   - `new Boolean(false)` creates a Boolean object wrapping `false`
   - The Boolean object itself is truthy (it's an object)
   - `Boolean()` of any object returns `true`

### 🔍 Internal Mechanics

- **Loose Equality (`==`)**: Triggers complex type coercion rules
- **Array to Primitive**: `[] → [].toString() → "" → 0`
- **Boolean Objects**: Are always truthy, even when wrapping `false`
- **Double Negation (`!!`)**: Forces boolean conversion without creating objects
- **Object Truthiness**: All objects (arrays, Boolean objects) are truthy

---

## ⚠️ Things to Remember / Gotchas

- **Empty arrays are truthy** but convert to `0` in numeric context
- `Boolean(false)` is `false`, but `Boolean(new Boolean(false))` is `true`
- **Boolean objects vs primitives**: `new Boolean(false)` is truthy, `false` is falsy
- Array-to-primitive conversion uses `toString()` then `ToNumber()`
- **Avoid `==`** - it triggers unpredictable coercion chains
- Use `===` and explicit `Boolean()` conversion for predictable results
