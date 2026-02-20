# Swift

- `Let` vs `var`
    
    `let`: defines a constant, need to assign in the moment of declare the constant
    
    `var1` : define a variable
    
    ```jsx
    let pi = 3.14
    var name = 'Thanh';
    ```
    
    <aside>
    💡
    
    function parameters are **constant** **by default**, try to change their value within function body → compile error
    
    </aside>
    
    ```jsx
    func hackInterview(for value:String){
    	value="android"
    }
    
    hackInterview(for: "ios");
    ```
    
    In Swift, converting a `let` to `var` by replace the `let` keyword with `var` keyword
    
    ```jsx
    let const = “initial value”
    
    var const = “initial value”
    
    const = “new value”
    ```
    
    <aside>
    💡
    
    Best practice: use `let` by default for safety and when needs to change, convert it into `var`
    
    </aside>
    
    ## Value and reference types
    
    - For `struct` : a `let` constant makes the entire instance immutable → cannot modify any properties
        
        ```jsx
        struct Person {
            var name: String
        }
        
        let p = Person(name: "Alice")
        p.name = "Bob" // Error — instance is immutable
        ```
        
    - For classes ( reference types): a `let` constant means the reference can’t change, but the object’s properties can still mutate if declared as `var`
        
        ```jsx
        class Person {
            var name: String
        }
        
        let p = Person()
        p.name = "Bob" // Valid, changing property not the reference
        ```
        
    
    ### String Interpolation
    
    Use variable inside a string with `\(variable)`
    
    ```jsx
    let user = "Thanh"
    let alarms = 3
    print("Hey \(user), you have \(alarms) alarms set.")
    ```
    
    ### Type safety and inference
    
    Need to cast the type of data before mixing
    
    ```jsx
    let a = 5
    let b = 2.5
    // let total = a + b // Error: can not add Int and Double
    let total = Double (a) + b
    ```
    
- Control flow
    
    ### If else
    
    ```jsx
    if ( condition ) {
    } else {
    }
    ```
    
    ### Switch statement
    
    ```jsx
    switch variable {
    	case {value}:
    		//code block
    	case {value1}..{value2} // from value 1 to value 2
    		// code block
    	case {value1}..<{value2} // from value 1 to under value 2
    		// code block
    }
    ```
    
    ### Loops
    
    ```jsx
    for i in {value1}..{value2} {
    	// code block
    }
    ```
    
    ```jsx
    let days = ["Mon", "Tue", "Wed"]
    
    for day in days { // equals foreach of Java
    	// code block
    }
    ```
    
    ```jsx
    // while loop
    while <condition> {
    	// code block
    }
    ```
    
- Collections
    
    ### Arrays
    
    ```jsx
    var alarmTimes = ["06:00", "09:00", "17:00"]
    alarmTimes.append("07:00")
    alarmTimes.remove(at: 1)
    ```
    
    ### Dictionaries
    
    Store key-value data structure ( like Map in Java)
    
    ```jsx
    var alarmDays = ["Mon": true, "Tue": false, "Wed": true]
    print(alarm["Mon"] ?? false) // true
    ```
    
    Loop through key/value:
    
    ```jsx
    for(day, isEnabled) in alarmDays {
    	print("\(day): \(isEnabled) ? "On" : "Off")")
    }
    ```
    
- Function
    
    Declare a function
    
    ```jsx
    func <function name> {
    	// code block
    }
    ```