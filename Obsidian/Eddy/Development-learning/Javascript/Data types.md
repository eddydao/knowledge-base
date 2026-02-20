#javascript 
# Number
`let n = 123;`
- Number type present both integer and float point numbers
- Special numeric values: `Infinity`, `-Infinity`, `NaN`

# BigInt
- From -(2^53 -1) to (2^53 - 1)

# String
```
let str = “Hello”;
let str2 = ‘Single quotes are ok’
let str3 = `Hello {}`
```
- double and single quotes are simple quotes and have no different between
- Backsticks are extended functionality that used to embedded variable and expressions into a string by wrapping in `${}`

# Boolean
- has only two values: `true` and `false`

# Null value
- represent “nothing”

# undefined
- = value is not assigned

## Type conversions
## String conversion
- Happens when we need the string form of a value
- eg: 
```
	let value = true;
	alert(typeof value); // boolean

	value = String(value);
	alert(typeof value); // string
```

## Numeric conversion
- Happen automatically in mathematical functions and expressions
- eg: 
```
alert (“6“ / “2”); // 3- auto converts to numbers 
```
- Explicit convert number by using `Number(value)`

## Boolean conversion
- Happens in logical operations, can be explicit perform by Boolean(value)
> String with “0” is true

