#javascript 
- Use `let` keyword to create variable in JS
`let name = ‘Thanh’;`

# Naming
- name must contain only letters, digits, symbol $ or _
- first character must not be a digit
# Constant
- name with `const` keyword
- name must be UPPERCASE with _
# Hoisting
- A variable can be declared after it has been used
- default behavior of moving all declarations to the top of the current scope
- Variables defined with `let` and `const` are hoisted to the top of the block but **NOT** initialized
	- Using `let` variable before it is declared will result *ReferenceError*
	- using `const` variable before it is declared, is a syntax error
- Javascript only hoists *declaration*, not *initialized*
eg: 
```
var x = 5;

elem = document.getElementById(“demo”);
elem.innerHTML = x + “ ” + y;

var y = 7;
```
=> this will give error due to y is **NOT** initialized
> Always **DECLARED** variables at the top;
