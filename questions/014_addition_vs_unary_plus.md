# [14 - Addition vs Unary Plus](https://bigfrontend.dev/quiz/Addition-vs-Unary-Plus)

---

### ❓ Question

```js
console.log(1 + 2)
console.log(1 + + 2)
console.log(1 + + + 2)
console.log(1 + '2')
console.log(1 + + '2')
console.log('1' + 2)
console.log('1' + + 2)
console.log(1 + true)
console.log(1 + + true)
console.log('1' + true)
console.log('1' + + true)
console.log(1 + null)
console.log(1 + + null)
console.log('1' + null)
console.log('1' + + null)
console.log(1 + undefined)
console.log(1 + + undefined)
console.log('1' + undefined)
console.log('1' + + undefined)
console.log('1' + + + undefined)
```

---

### ✅ Output

```
3
3
3
'12'
3
'12'
'12'
2
2
'1true'
'11'
1
1
'1null'
'10'
NaN
NaN
'1undefined'
'1NaN'
'1NaN'
```

---

### 🧠 Step-by-step Explanation / Internal Implementation

#### Basic Unary Plus Behavior
- `+` as a unary operator converts the operand to a number.
- `1 + 2` → `3`
- `1 + +2` → `1 + 2` → `3`
- `1 + + +2` → `1 + 2` → `3`

#### String Coercion
- `1 + '2'` → `number + string` → string concatenation → `'12'`
- `1 + + '2'` → `'2'` → number `2` → `1 + 2 = 3`
- `'1' + 2` → string + number → `'12'`
- `'1' + +2` → `'1' + 2` → `'12'`

#### Boolean Coercion
- `1 + true` → `1 + 1` → `2`
- `1 + +true` → `1 + 1` → `2`
- `'1' + true` → `'1true'`
- `'1' + +true` → `'1' + 1` → `'11'`

#### Null Coercion
- `1 + null` → `null → 0` → `1 + 0 = 1`
- `'1' + null` → `'1null'`
- `'1' + +null` → `null → 0` → `'1' + 0 = '10'`

#### Undefined Coercion
- `undefined → NaN`
- `1 + undefined` → `NaN`
- `1 + +undefined` → `NaN`
- `'1' + undefined` → `'1undefined'`
- `'1' + +undefined` → `'1NaN'`
- `'1' + + +undefined` → `'1NaN'`

---

### ⚠️ Things to Remember / Gotchas

- Unary plus (`+value`) is used to convert values to numbers.
- `undefined` coerces to `NaN`; `null` coerces to `0`.
- When either operand of `+` is a string, JS performs **string concatenation**.
- Multiple unary plus signs still evaluate to number coercion.
- Be cautious with expressions like `'1' + +value` — they **coerce and concatenate**.
- Using `+` on non-numeric strings or undefined results in `NaN`.