#javascript 
# String comparison
- Compared letter-by-letter
- eg: 
```
‘Z’ > ‘A’ // true
‘Glow’ > ‘Glee’
‘Bee’ > ‘Be’
```
# Comparison of different types
- JS converts the values to numbers
- `true` becomes `1`, `false` becomes `0`

# Strict equality
- regular equality check ( == ) will converts different types into number 
- strict equality check ( === ) check the equality without type conversions
=> if a and b are of different types, it always return `false`

> null == undefined //true
> null === undefined // false

> null becomes 0, undefined becomes NaN when apply with `>` , `<`, `<=`, `>=`

```
null > 0 // false
null == 0 // false
null >= 0 // true
```

```
undefined > 0 // false (1)
undefined < 0 // false (2)
undefined == 0 // false (3)
```
> (1) and (2) returns false because `undefined` get converted to `NaN` and return false for all comparison
> (3) returns false because `undefined` only equals `null`, `undefined`

> Treat any comparison with `undefined/null` except the strict equality with exceptional care
> Do **NOT** use comparison `>=, <=, <, >` with a variable which may be `null/undefined`