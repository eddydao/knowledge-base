# Introduction to React
- Using Vite tool to create a React app `npm create vite@latest <app name> — — template react`
- Run `npm install` to install necessary libs into the project
- Start the app `npm run dev`
- Vite start the app in default port 5173

## Component
- The core concepts of React, the smallest element that build a SPA
- Combine markup, CSS, Javascript into custom “component”, reusable UI elements for the app
- Define:
```javascript
export default function Profile() {
	// code block
	return (
		<>
			// code block
		</>
	)
}
```

## JSX
- The layout of React is mostly written using JSX
- JSX returned by React components is **compiled into Javascript**
- The compile process is handled by [[Babel]]
- Every tag in JSX need to be closed ( like XML)
- Can embed dynamic content by writing JS in `{ }` ( like Thymeleaf in Java)

## Multiple components
- The core philosophy of React is composing applications from specialized reusable components
```javascript
const Hello = () => {
	return (
		<>
			<p>Hello world</>
		</>
	)
}

const App = () => {
	return (
		<>
			<Hello/>
		</>
	)
}
```

## props: passing data
```javascript
const Hello = (props) => {
	return (
		<>
			<p> Hello {props.name}</p>
		</>	
	)
}

// usage
<Hello name=‘Thanh’/>
```
- The function defining the component has a param props.
- This props, as an argument, receives an object, which has field corresponding ( eg: name)
- The value can be hard-coded or being result of a Javascript expressions.
```javascript
const Hello = () => {
	return (
		<>
			<p>
				Hello {props.name}, {props.age}!
			</p>
		</>
	)
}

const App = () => {
	const name = ‘Thanh’;
	const age = 10;

	return (
		<>
			<Hello name={name} age={age+19}/>	
		</>
	)
}
```

> Do not render Object

# Component state, event handlers

## Component helper functions
- The helper function is defined within another function that determines the component’s behavior.
- eg:
```javascript
const Hello = (props) => {
	// helper function defined here
	const bornYear = () => {
		const yearNow = new Date().getFullYear();
		return yearNow - props.age
	}

	// direct access in the JSX code
	return (
		<>
			<p>Hello {props.name}, you are {props.age} years old.</P>
			<p>So you are born in {bornYear()}</p>
		</>
	)
}
```

## Destructuring
```javascript
const Hello = (props) => {
	// destructure the props
	//const name = props.name;
	//const age = props.age;
	const {name, age} = props
	
	// helper function defined here
	// using shorter form with arrow function
	const bornYear = () => new Date().getFullYear() - age;

	// direct access in the JSX code
	return (
		<>
			<p>Hello {name}, you are {age} years old.</P>
			<p>So you are born in {bornYear()}</p>
		</>
	)
}
```

- Take a step further, directly destructured into variables
```javascript
const Hello = ({name, age}) => …
```

## Page re-rendering/ Stateful component
- State of component changed cause the re-render of the page
- Add state into the component by using React state hook `import {useState} from ‘react`
```typescript
import { useState } from ‘react’ //(1)

const App = () => {
	const [counter, setCounter] = useState(0) //(2)

	setTimeout( //(3)
		() => setCounter(counter + 1),
		1000
	)

	return (
		<>{counter}</>
	)
}
```

- (1) import the useState function
- (2) define the component begins with the function call => add *state* to the component and renders with the init value of 0
	- counter is assigned the initial value of state
	- setCounter is assigned a function that will be use to modify the *state*
 - (3) the *setCounter* function is called and change the value of counter => React re-render the page	

## Event handling
