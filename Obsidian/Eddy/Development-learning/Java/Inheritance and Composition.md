Both inheritance and Composition are OOP concepts.

# Definition
## Composition
It’s a design technique in OOP to implement has-a relationship between objects
In Java, the composition is achieved by using instance variable of other objects
eg:
```java
public class Job{
// variables and methods
}

public class Person{
	private Job job;
}

```

## Inheritance
It’s a design technique to implement is-a relationship between objects.
In Java, the composition is achieved by using `extends` keyword.
eg:
```java
public class Animal {
// variables and methods
}

public class Cat extends Animal {
// override methods of Animal class if needed
// variables and methods
}
```

# Composition over Inheritance
- Inheritance is tightly coupled whereas composition is loosely coupled.
- Composition provides the access control over variables and methods. Inheritance can not provide that access control.
- Composition provides flexibility in invocation  of methods that is used in multiple subclass scenario

