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
# Function
Declare
```Swift
func greet() {
	print("Good morning")
}

greet() // call the function
```

## Function with params
Declare
```Swift
func greet(name: String){
	print("Hello \(name)")
}

greet(name: "Thanh")
```

Every parameter must have a type, Swift enforces that type at compile time

## Return values
A function can return a value by using `->`
```Swift
func add(a: Int, b: Int) -> Int{
	return a + b;
}
let result = add(a: 3, b: 5)
print(result) // 8
```


## External and Internal Parameter names
Swift function can have external and internal param names
```Swift
function <func name> (_ x: Int, enternalName internalName y: Int){

}
```

`_` use for hide the external name

```Swift
func multiply(_ x:Int, by y: Int) -> Int {
	return x * y;
}

let total = multiply(3, by 5);
```

External param name improves readability
Internal param name use inside the function code block

## Default param values
Give the default value for param
```Swift
func alarmMessage(for name: String = "User") -> String {
	return "Wake up, \(name)! It's time"
}

print(alarmMessage()) // Wake up, User!
print(alarmMessage(for: "Thanh")) // Wake up, Thanh!
```


# Optionals
An **Optional** represents a value that might be `nil` ( null - similar to Optional in Java)
```Swift
var note: String? = "Morning run"
print(note) // Optional("Morning run")

note = nil
print(note) // nil
```


Swift force to safety handle `nil` before using it - preventing crashes

## Unwrapping optionals
### Safe Unwrapping with `if let`
```Swift
var label: String? = "Work alarm"

if let safelabel = label {
	print("Label \(safeLabel))
} else {
	print("No label found")
}
```

### Using guard let
Used inside functions to **exit early** if a value is missing
```Swift
func printLabel(_ label: String?){
	guard let label = label else {
		print("Missing label.")
		return
	}
	print("Label: \(label)")
}
```

### Using default value with ??
If `optional` is `nil`, provide a fallback
```swift
let mission: String? = nil
print(mission ?? "No mission assigned")
```

### Optional chaining
Access optional properties safety using `?.`
```Swift
struct Alarm {
	var label: String?
}

let morning = Alarm(label: "Workout")
print(morning.label?.uppercased() ?? "Unnamed alarm")
```

# Structs and Classes; App models

Struct and class are custom types:
- Struct -> value type (copied on assignment)
- class -> reference type ( shared reference on assignment) supports inheritance, deinit
## Structs
Store values directly
When copy or pass a Struct, it duplicated the data, created 2 independent copies
Swift standard library built on Struct - avoid unexpected shared mutations
**Best practice:**
- Model objects
- Lightweight data containers acts like immutable copies
- Views in SwiftUI

```Swift
struct Alarm {
	var id: UUID = .init()
	var time: Date
	var label: String
	var isEnabled: Bool
	var snoozeEnabled: Bool
	// computed property
	var displayTime: String {
		let df = DateFormatter()
		df.dateFormat - "HH:mm"
		return df.string(from: time)
	}

	// mutating method ( allows changing properties inside struct)
	mutating func toggle(){
		isEnabled.toggle()
	}
}
```

### Mutating methods
Allows changing properties inside struct
If change data inside struct method, mark with `mutating` - because we are modifying a copy
```Swift
struct Counter {
	private(set) var value = 0
	mutating func increment() {value += 1}
}
```

### Custom initializer
Swift gives a default initializer ( like default constructor in Java) and we can create custom initializer

```Swift
init(hour: Int, minute: Int, label: String?){
	var comps = DateComponents()
	comp.hours = hours; comp.minutes = minute
	self.time = Calendar.current.data(from: comps) ?? Date()
	self.label = label
	self.isEnabled = true
}
```

### Common protocols
[[Protocols]] will be learn in later
Common protocols:
- Identifiable: For SwiftUI List
- Equatable: For comparison in Logic/tests
- Codable: For saving/loading data
- Hashable: for sets/dictionaries
## Classes
assigned variable point to the same interface ( class in Java)
Best practice: good for shared state/ single source of truth
Can subclass, have `deinit`, identity sematics
```Swift
final class AlarmManager {
	var alarm: [Alarm} = []
	func add(_ alarm: Alarm) {alarms.append(alarm)}
}
```
