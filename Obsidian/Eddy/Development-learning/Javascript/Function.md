#javascript 
# Function Expression
- Allow to create a new function in the middle of any expression
eg: 
```
let sayHi = function(){
	alert(“hello”);
}
```

> Function is a value

```
function sayHi() {
	alert(‘Hello’);
}

alert( sayHi); // show the function code, not run the code
```
- copy the function by `let newFunc = sayHi`
- if the code is `let func = sayHi()` then it will show the result of the function `sayHi`

# Callback function 
```
function ask(question, yes, no) {
	if(confirm(question) yes())
	else no();
}

function showOk() {
	alert(“OK);
}

function showCancel() {
	alert(“Cancel”);
}

ask(“are you ok?”, showOk, showCancel);
```

The argument `showOk` and `showCancel` are called **callback function**

> The function expression is created when the execution reaches it and is usable only from that moment
