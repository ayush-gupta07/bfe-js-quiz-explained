# [08 - Implicit Coercion 1](https://bigfrontend.dev/quiz/Implicit-Conversion-1)

## Question

```js
console.log(Boolean('false'))
console.log(Boolean(false))
console.log('3' + 1)
console.log('3' - 1)
console.log('3' - ' 02 ')
console.log('3' * ' 02 ')
console.log(Number('1'))
console.log(Number('number'))
console.log(Number(null))
console.log(Number(false))
```

## Output

```
true
false
'31'
2
1
6
1
NaN
0
0
```

## Step by Step Explanation / Internal Implementation

1. `Boolean('false')` → `'false'` is a non-empty string → coerced to `true`
2. `Boolean(false)` → explicitly `false`
3. `'3' + 1` → string concatenation → `'3' + '1'` = `'31'`
4. `'3' - 1` → string is coerced to number → `3 - 1` = `2`
5. `'3' - ' 02 '` → both strings coerced to numbers (`3 - 2`) → `1`
6. `'3' * ' 02 '` → both strings coerced to numbers (`3 * 2`) → `6`
7. `Number('1')` → valid numeric string → `1`
8. `Number('number')` → invalid numeric string → `NaN`
9. `Number(null)` → null coerces to `0` → `0`
10. `Number(false)` → false coerces to `0` → `0`

## Things to Remember / Gotchas

- `Boolean('false')` is `true` because **non-empty strings are truthy**, regardless of content.
- `+` operator with strings leads to **string concatenation**, not numeric addition.
- `-` and `*` cause implicit coercion to **number**.
- `Number(' ')` (space-only string) → coerces to `0`.
- `null` and `false` both convert to `0` when passed to `Number()`.
- `Number('number')` fails because it's **not a numeric string**, resulting in `NaN`.