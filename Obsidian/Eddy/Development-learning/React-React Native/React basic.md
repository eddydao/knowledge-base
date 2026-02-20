
### 1. Functional Components

**Definition:**
Functional components are the modern standard for writing React components. At their core, they are simply JavaScript functions that accept an optional `props` object as an argument and return a React element (typically written using JSX) describing what should be rendered on the screen.

**Syntax:**
You can define them using either the traditional `function` keyword or, more commonly now, using ES6 arrow functions:

```javascript
// Using the 'function' keyword (as you provided)
function MyComponent(props) {
  // Component logic and Hooks can go here
  return <View><Text>Hello from MyComponent!</Text></View>;
}

// Using ES6 Arrow Function (very common)
const AnotherComponent = (props) => {
  // Component logic and Hooks can go here
  return <View><Text>Hello from AnotherComponent!</Text></View>;
};

// Often props are destructured directly in the function signature
const Welcome = ({ name }) => {
  return <View><Text>Welcome, {name}!</Text></View>;
};
```

**Key Characteristics & Advantages:**

1.  **Simplicity & Readability:** They are generally shorter and easier to read than their older counterpart, Class Components, especially for simpler UI elements.
2.  **Hooks:** Functional components leverage **Hooks** (like `useState`, `useEffect`, `useContext`, etc.) to manage state, handle side effects (like data fetching or subscriptions), access context, and tap into other React features without needing to write a class. This was a major shift introduced in React 16.8.
3.  **Pure Functions (Often):** Simple functional components that only depend on their props are often pure functions – given the same props, they will always render the same output. This makes them easier to test and reason about.
4.  **Performance:** While the difference might be negligible in many cases, functional components can sometimes have slight performance benefits due to being lighter than classes.
5.  **Current Standard:** The React team recommends using functional components with Hooks for all new development.

**Role in React Native:**
They are the primary way you build UI screens and reusable UI pieces (like buttons, cards, list items) in React Native applications. Each screen or distinct part of your UI will likely be a functional component.

---

### 2. JSX (JavaScript XML)

**Definition:**
JSX is a syntax extension for JavaScript recommended by React for describing what the UI should look like. It *looks* very similar to HTML or XML but is **not** HTML. It's syntactic sugar over `React.createElement()` calls.

**Syntax Example:**
```jsx
// This JSX:
const element = (
  <View style={{ padding: 20 }}>
    <Text style={{ fontSize: 18, fontWeight: 'bold' }}>
      Hello, {userName}!
    </Text>
    <Button title="Click Me" onPress={handleClick} />
  </View>
);

// Gets transpiled (usually by Babel) into something like this JavaScript:
const element = React.createElement(
  View,
  { style: { padding: 20 } },
  React.createElement(
    Text,
    { style: { fontSize: 18, fontWeight: 'bold' } },
    "Hello, ", userName, "!"
  ),
  React.createElement(Button, { title: "Click Me", onPress: handleClick })
);
```

**Key Characteristics & Rules:**

1.  **Embedding Expressions:** You can embed any valid JavaScript expression within JSX by wrapping it in curly braces `{}`. Examples: `{userName}`, `{2 + 2}`, `{user.firstName}`, `{myFunction()}`.
2.  **Attributes/Props:**
    *   JSX uses attributes to pass information (props) to components.
    *   Attribute names generally follow **camelCase** convention (e.g., `fontSize`, `onClick`, `onPress`).
    *   String literals can be passed in quotes: `title="Click Me"`.
    *   JavaScript expressions (variables, objects, functions) must be passed in curly braces: `style={{ padding: 20 }}`, `onPress={handleClick}`, `isEnabled={true}`.
3.  **Nesting:** You can nest JSX elements just like in HTML to create complex UI structures.
4.  **Single Root Element:** A component's `return` statement must return **only one** top-level JSX element. If you need to return multiple adjacent elements, wrap them in a **Fragment**:
    ```jsx
    // Using Fragment shorthand <>...</>
    return (
      <>
        <Text>First Line</Text>
        <Text>Second Line</Text>
      </>
    );

    // Or using the explicit <React.Fragment>...</React.Fragment>
    return (
      <React.Fragment>
        <Text>First Line</Text>
        <Text>Second Line</Text>
      </React.Fragment>
    );
    ```
5.  **Self-Closing Tags:** Tags with no children can be self-closed, like in XML: `<Image source={...} />`.
6.  **Component Naming:** User-defined components **must** start with a capital letter (e.g., `<MyComponent />`, not `<myComponent />`). Lowercase tags are interpreted as built-in elements (like `<view>`, `<text>` in React Native DOM, or `<div>`, `<span>` in web React).

**Why Use JSX?**
It allows developers to visualize the UI structure directly within their JavaScript code, making it more intuitive and readable than creating nested `React.createElement` calls manually.

---

### 3. Props (Properties)

**Definition:**
Props (short for "properties") are the mechanism for passing data **down** the component tree, from a parent component to a child component. They allow you to configure and customize child components, making them dynamic and reusable.

**Passing Props:**
You pass props to a child component using attributes in JSX, similar to how you pass attributes to HTML elements.

```jsx
// ParentComponent.js
import ChildComponent from './ChildComponent';

const ParentComponent = () => {
  const userName = "Alice";
  const userAge = 30;
  const handlePress = () => console.log("Button pressed!");

  return (
    <View>
      {/* Passing props to ChildComponent */}
      <ChildComponent
        name={userName} // Passing a variable
        age={userAge}    // Passing another variable
        isAdmin={true}   // Passing a boolean literal
        message="Welcome!" // Passing a string literal
        onAction={handlePress} // Passing a function
      />
    </View>
  );
};

export default ParentComponent;
```

**Receiving Props:**
Functional components receive props as a single object argument (conventionally named `props`). You can access individual props using dot notation (`props.propertyName`) or, more commonly, by destructuring the props object in the function signature.

```jsx
// ChildComponent.js
import React from 'react';
import { View, Text, Button } from 'react-native';

// Receiving props using destructuring (common practice)
const ChildComponent = ({ name, age, isAdmin, message, onAction }) => {
  return (
    <View style={{ margin: 10, padding: 10, borderWidth: 1, borderColor: 'grey' }}>
      <Text>{message}</Text>
      <Text>Name: {name}</Text>
      <Text>Age: {age}</Text>
      {isAdmin && <Text>Status: Administrator</Text>} {/* Conditional rendering based on prop */}
      <Button title={`Action for ${name}`} onPress={onAction} />
    </View>
  );
};

// Alternative: Receiving the whole props object
// const ChildComponent = (props) => {
//   return (
//     <View>
//       <Text>{props.message}</Text>
//       <Text>Name: {props.name}</Text>
//       {/* ... etc ... */}
//     </View>
//   );
// };

export default ChildComponent;
```

**Key Characteristics:**

1.  **Read-Only:** Props are **immutable** within the child component that receives them. A component should never modify its own `props`. This ensures a predictable one-way data flow (top-down). If a component needs to change data based on user interaction or other events, it should use **state** (managed via the `useState` Hook) or call functions passed down via props (like `onAction` in the example) to notify the parent.
2.  **Data Flow:** They facilitate the unidirectional data flow principle in React. Data flows down from parent to child.
3.  **Reusability:** Props make components reusable. You can render the same `ChildComponent` multiple times with different props to display different data.
4.  **Default Props:** You can define default values for props in case they are not provided by the parent component.
    ```javascript
    const MyButton = ({ title = "Default Title", color = "blue" }) => {
      // ... use title and color
    };
    ```
5.  **Prop Types / TypeScript:** While JavaScript allows passing anything, it's good practice (especially in larger applications) to define the expected types for props. This can be done using the `prop-types` library (less common now) or, more robustly, using **TypeScript**. This helps catch errors early and improves code maintainability.

---
Okay, let's dive into State, Lifecycle Hooks (specifically `useEffect`), and Event Handling in React/React Native. These concepts are essential for building dynamic and interactive user interfaces.

---

### 4. State (`useState` Hook)

**Definition:**
State refers to data that is **managed within a component** and can change over time, usually in response to user actions or network responses. Unlike props (which are passed *down* from a parent and are read-only in the child), state originates and is updated *within* the component itself. When state changes, React automatically re-renders the component to reflect the new data.

**Purpose:**
State allows components to be dynamic, remember information, and react to interactions. It's used for things like:
*   Storing user input from forms (`TextInput`).
*   Tracking whether a button is toggled or an item is selected.
*   Holding data fetched from an API.
*   Managing UI states like loading indicators or error messages.

**Syntax (`useState` Hook):**
The `useState` hook is the standard way to add state to functional components.

1.  **Import:** You need to import it from React:
    ```javascript
    import React, { useState } from 'react';
    ```
2.  **Usage:** Call `useState` inside your functional component. It takes one argument: the **initial state value**. It returns an array containing two elements:
    *   The **current state value**.
    *   A **function to update** that state value.
    You typically use array destructuring to get these two elements.

**Example:** A simple counter component.

```javascript
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

const Counter = () => {
  // 1. Call useState with the initial state (0)
  // 2. Destructure the returned array into 'count' (state variable)
  //    and 'setCount' (update function)
  const [count, setCount] = useState(0);

  const increment = () => {
    // Use the update function to set the new state
    setCount(count + 1);
  };

  const decrement = () => {
    // It's safer to use a functional update when the new state
    // depends on the previous state, especially for rapid updates.
    setCount(prevCount => prevCount - 1);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.text}>Count: {count}</Text> {/* Read the state value */}
      <View style={styles.buttonRow}>
        <Button title="Decrement" onPress={decrement} />
        <Button title="Increment" onPress={increment} />
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: { alignItems: 'center', marginVertical: 10 },
  text: { fontSize: 20, marginBottom: 10 },
  buttonRow: { flexDirection: 'row', justifyContent: 'space-around', width: '60%' }
});

export default Counter;
```

**Key Concepts & Rules:**

1.  **Initialization:** `useState(initialValue)` sets the state only on the *first* render.
2.  **Reading State:** Access the current state using the state variable (e.g., `count`).
3.  **Updating State:** Call the update function (e.g., `setCount(newValue)`).
    *   **Asynchronous:** State updates *may* be asynchronous. React might batch multiple `setState` calls for performance. Don't rely on the state being updated immediately after calling the function.
    *   **Functional Updates:** When the new state depends on the previous state, use the functional update form: `setState(prevState => newState)`. This guarantees you're working with the most up-to-date previous state value.
    *   **Triggers Re-render:** Calling the update function tells React to schedule a re-render of the component (and its children) with the new state value. React optimizes this to only update the actual UI elements that changed.
4.  **Hook Rules:** Call `useState` only at the top level of your functional component (not inside loops, conditions, or nested functions).

---

### 5. Lifecycle (Hooks) - `useEffect`

**Definition:**
The `useEffect` hook lets you perform **side effects** in functional components. Side effects are operations that interact with the "outside world" beyond the component's rendering logic, such as:
*   Fetching data from an API.
*   Setting up or cleaning up subscriptions (e.g., timers, event listeners).
*   Manually changing the DOM (less common/needed in React Native compared to web React).
*   Logging.

`useEffect` essentially combines the purposes of `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` from older class components.

**Purpose:**
To handle operations that need to happen *after* rendering, or in response to changes in props or state, or when the component is removed.

**Syntax:**

1.  **Import:**
    ```javascript
    import React, { useState, useEffect } from 'react';
    ```
2.  **Usage:** Call `useEffect` inside your functional component. It takes two arguments:
    *   A **callback function** containing the side effect logic.
    *   An optional **dependency array**.

	```javascript
	useEffect(() => {
	  // Your side effect logic goes here...
	  console.log('Component rendered or dependency changed');
	
	  // Optional: Return a cleanup function
	  return () => {
		console.log('Cleanup before effect runs again or component unmounts');
		// e.g., clearInterval(timerId), removeEventListener(...)
	  };
	}, [dependency1, dependency2]); // Dependency array
	```


**The Dependency Array - Crucial:**
The dependency array tells React *when* to re-run the effect:

1.  **`[]` (Empty Array):** The effect runs **only once**, after the initial render. Mimics `componentDidMount`. Ideal for initial data fetching, setting up global listeners.
    ```javascript
    useEffect(() => {
      console.log('Component did mount');
      fetchData(); // Fetch initial data
      return () => {
        console.log('Component will unmount');
        // Cleanup listeners if any were set up
      };
    }, []); // Runs only once
    ```

2.  **`[prop, state]` (With Dependencies):** The effect runs after the initial render **and** whenever any value inside the dependency array changes between renders. Mimics `componentDidMount` + `componentDidUpdate`. Use this when your effect depends on specific props or state values.
    ```javascript
    useEffect(() => {
      console.log(`User ID changed to: ${userId}`);
      fetchUserDetails(userId); // Fetch data when userId changes

      // Cleanup specific to this userId might go here
      return () => {
        console.log(`Cleaning up effect for previous userId`);
      }
    }, [userId]); // Runs when userId changes
    ```

3.  **Omitted (No Array):** The effect runs after **every single render** (initial render and all updates). Use this very carefully, as it can easily lead to performance issues or infinite loops if the effect itself triggers a state update.
    ```javascript
    useEffect(() => {
      console.log('Component rendered');
      // Avoid this unless you specifically need it and understand the implications.
    }); // Runs after every render
    ```

**Cleanup Function:**
The optional function returned from the `useEffect` callback is the cleanup function. React runs it:
*   Before the component unmounts (is removed from the UI).
*   Before running the effect *again* due to a dependency change.
This is essential for preventing memory leaks by cleaning up resources like timers, subscriptions, or event listeners.

**Example: Fetching Data**

```javascript
import React, { useState, useEffect } from 'react';
import { View, Text, ActivityIndicator, FlatList } from 'react-native';

const UserList = () => {
  const [users, setUsers] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    // Define the async function inside useEffect or outside
    const fetchUsers = async () => {
      setIsLoading(true); // Start loading
      setError(null);
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        const data = await response.json();
        setUsers(data);
      } catch (err) {
        setError(err.message);
      } finally {
        setIsLoading(false); // Stop loading regardless of success/failure
      }
    };

    fetchUsers(); // Call the async function

    // No cleanup needed for a simple fetch in this case
  }, []); // Empty array: fetch only once on mount

  if (isLoading) {
    return <ActivityIndicator size="large" style={{ marginTop: 20 }} />;
  }

  if (error) {
    return <Text style={{ color: 'red', margin: 20 }}>Error: {error}</Text>;
  }

  return (
    <FlatList
      data={users}
      keyExtractor={(item) => item.id.toString()}
      renderItem={({ item }) => (
        <View style={{ padding: 10, borderBottomWidth: 1, borderBottomColor: '#ccc' }}>
          <Text>{item.name} ({item.username})</Text>
          <Text>{item.email}</Text>
        </View>
      )}
    />
  );
};

export default UserList;
```

---

### 6. Handling Events

**Definition:**
Event handling is how your application responds to user interactions with UI elements. React Native provides components (like `Button`, `TextInput`, `TouchableOpacity`, `ScrollView`) that expose specific props to handle common events.

**Purpose:**
To make the application interactive by triggering actions (like updating state, navigating, calling functions) when the user performs an action (like tapping, typing, scrolling).

**Syntax:**
You pass a **function** as a prop to the component for the specific event you want to handle. The prop name usually starts with `on` (e.g., `onPress`, `onChangeText`).

**Common Events & Components:**

*   **`onPress`:** Triggered on a tap/click. Used with:
    *   `<Button title="Click Me" onPress={handlePress} />`
    *   `<TouchableOpacity onPress={handlePress}><Text>Tap Me</Text></TouchableOpacity>`
    *   `<Pressable onPress={handlePress}>...</Pressable>` (More versatile)
*   **`onChangeText`:** Triggered when the text in an input changes. Receives the new text value directly as an argument. Used with:
    *   `<TextInput value={text} onChangeText={setText} placeholder="Enter text" />`
    *   `<TextInput value={inputValue} onChangeText={(newText) => setInputValue(newText)} />`
*   **`onSubmitEditing`:** Triggered when the user presses the submit button on the keyboard. Used with `<TextInput>`.
*   **`onScroll`:** Triggered when a scrollable view is scrolled. Receives an event object with scroll position data. Used with `<ScrollView>`, `<FlatList>`.
*   **`onValueChange`:** Triggered when the value of a picker or switch changes. Used with `<Picker>`, `<Switch>`.

**Example: Handling Text Input and Button Press**

```javascript
import React, { useState } from 'react';
import { View, Text, TextInput, Button, Alert, StyleSheet } from 'react-native';

const SimpleForm = () => {
  const [name, setName] = useState('');

  // Event handler for the TextInput's onChangeText event
  const handleTextChange = (inputText) => {
    setName(inputText); // Update the state with the new text
  };

  // Event handler for the Button's onPress event
  const handleSubmit = () => {
    if (name.trim()) {
      Alert.alert('Submitted', `Hello, ${name}!`);
      // setName(''); // Optionally clear the input after submission
    } else {
      Alert.alert('Error', 'Please enter your name.');
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.label}>Enter your name:</Text>
      <TextInput
        style={styles.input}
        placeholder="e.g., Jane Doe"
        value={name} // Controlled component: value linked to state
        onChangeText={handleTextChange} // Call handler on text change
      />
      <Button
        title="Submit"
        onPress={handleSubmit} // Call handler on button press
        disabled={!name.trim()} // Disable button if input is empty
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { padding: 20 },
  label: { fontSize: 16, marginBottom: 5 },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    padding: 10,
    marginBottom: 15,
    fontSize: 16,
  },
});

export default SimpleForm;
```


**Key Concepts:**

1.  **Event Handler Functions:** These are the JavaScript functions you define to execute when an event occurs.
2.  **Passing Functions as Props:** You pass the *reference* to your handler function (e.g., `onPress={handleSubmit}`) or define an inline arrow function (`onPress={() => console.log('Pressed!')}`). Inline functions are convenient but can have minor performance implications if not used carefully (a new function instance is created on each render).
3.  **Event Object (Sometimes):** Some event handlers (like `onScroll`, `onLayout`) receive an event object containing details about the interaction. Others (like `onChangeText`, `onValueChange`) often pass the relevant value directly.
4.  **Connecting to State:** Event handlers are the primary place where you'll call your `setState` functions to update the component's state based on user input.
