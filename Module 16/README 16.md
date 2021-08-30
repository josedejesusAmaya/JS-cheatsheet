Among all other JavaScript libraries, React.js stands out. It relies on reusable components, not templates, for UI development, allowing developers to render views where data changes over time. React applications are more scalable and more maintainable, making developers more efficient and users more satisfied.

React create SPA, instead of creating different files for different pages. We are going to create a single page and JS is going to load information and change the UI.

[javascript - Can anyone explain the difference between Reacts one-way data binding and Angular's two-way data binding - Stack Overflow](https://stackoverflow.com/questions/34519889/can-anyone-explain-the-difference-between-reacts-one-way-data-binding-and-angula)

What does the `npx` part of the command stand for?
`npx` is a package runner that is used to create a new React application.

```bash
	npx create-react-app my-app
```

### 2.4) Refactoring elements with JSX
XML-like syntax called JSX
JSX or JavaScript as XML is a language extension that allows you to write tags directly in JS.
Babel compile JSX to JS 'cause JSX doesn't run in your browser natively.

### 3.1) Creating components
A component is a building block. It's a little piece of the UI.
Component are functions that return a little bit of UI.
Then we can compose these functions or component together to create a larger application.

### 3.2) Adding component properties and methods
Every react componet has access to this object called props.
The props object is going to hold all of the different properties for our component.

The fragment is a feature to allow us not to kind of junk up the DOM by adding to many elements.

#### Destructuring

```jsx
	function App ({authorized}) {
		return (
			<>
				{authorized ? <SecretComponent /> : < RegularComponent />}
			</>
		);
	} 
```

### Working with props and state
#### Managing state - Understanding the useState Hook
Returns a stateful value, and a function to update it.
The `useState` Hook allows a developer to create and use states in a React.js application.
At first it returns an array.
```jsx
import React, { useState } from 'react';
function Example() {
  // Declare a new state variable, which we'll call "count"  
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

#### useEffect
Accepts a function that contains imperative, possibly effectful code.
```js
	useEffect(() => {
		console.log(`It's ${emotion} around here!`);
 }, [emotion]);
```
What is the purpose of the `useEffect` Hook?
-   to manage side effects that are not related to the component's render
-   The `useEffect` Hook is useful to perform additional work behind the scenes, without affecting the appearance of the webpage.

#### Reducer function
It takes in the current state and it returns a new state

### Displaying child components
The React docs say that you can use `props.children` on components that represent ‘generic boxes’ and that don’t know their children ahead of time. For me, that didn’t really clear things up. I’m sure for some, that definition makes perfect sense but it didn’t for me.

My simple explanation of what `this.props.children` does is that _it is used to display whatever you include between the opening and closing tags when invoking a component.
```javascript
	const Picture = (props) => {
  		return (
    		<div>
      			<img src={props.src}/>
      			{props.children}
    		</div>
  		)
	}
```
This component contains an `<img>` that is receiving some `props` and then it is displaying `{props.children}`.

Whenever this component is invoked `{props.children}` will also be displayed and this is just a reference to what is between the opening and closing tags of the component.
```javascript
		//App.js
		render () {
  			return (
    			<div className='container'>
      				<Picture key={picture.id} src={picture.src}>
          				//what is placed here is passed as props.children  
      				</Picture>
    			</div>
  			)
		}
```
Instead of invoking the component with a self-closing tag `<Picture />` if you invoke it will full opening and closing tags `<Picture> </Picture>` you can then place more code between it.

This **de-couples** the `<Picture>` component from its content and makes it more reusable.

[javascript - What is {this.props.children} and when you should use it? - Stack Overflow](https://stackoverflow.com/questions/49706823/what-is-this-props-children-and-when-you-should-use-it)

### Specifying Children with JSX
If a tag is empty, you may close it immediately with `/>`, like XML:
```
const element = <img src={user.avatarUrl} />;
```
JSX tags may contain children:
```
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```
[Introducing JSX – React (reactjs.org)](https://reactjs.org/docs/introducing-jsx.html#specifying-children-with-jsx)

### JSX Children
We can also pass in JSX children in between the opening and closing tags.
For example, we can write:
```js
class Bar extends React.Component {  
  render() {  
    return <p>bar</p>;  
  }  
}

class Foo extends React.Component {  
  render() {  
    return this.props.children;  
  }  
}

class App extends React.Component {  
  render() {  
    return (  
      <Foo>  
        <Bar />  
      </Foo>  
    );  
  }  
}
```
[Adding Child Components with JSX. We look at various ways to pass things… | by John Au-Yeung | DataSeries | Medium](https://medium.com/dataseries/adding-child-components-with-jsx-cc34f2dd9c1e)

### 4.1) Conditional rendering
```jsx
	function App(props) {
		if (props.authorized) {
			return <Footer year={new Date().getFullYear()}/>
		} else {
			return (
				<div className="App">
					<Header name="Pepe" />
					<Main dishes={dishObjects}/>
				</div>
			);
		}
	}
```

#### Ternary if statetment
 ```jsx
	function App (props) {
		return (
			<>
				{props.authorized ? <SecretComponent /> : < RegularComponent />}
			</>
		);
	} 
```

### Using Create React App as a testing platform
File .test.js
Run npm test.
It  comes with Jest library wich is automatically included by default.
React testing library

When the following statement is added to the `App.test.js` file, which types of tests will you be able to perform with the React Testing Library?
```jsx
	import { render } from "@testing-library/react";
```
The `render` component from the React Testing Library allows you to assert whether specific words, phrases, or html tags were rendered.

You want to create a test that determines what happens after a checkbox has been clicked. What is the correct statement to include in your test function?
```jsx
	`fireEvent.click(checkbox)`
```
The `fireEvent.click` method will simulate an end user clicking a checkbox on a webpage form. From there, you can write assertion tests.

The following code describes which type of test?
```jsx
	expect(timesTwo(4)).toBe(8);
```
an assertion test.
The provided example is testing a math function, but testing for html tags and form events is also possible.

When Create React App is installed, it comes with a testing platform. Which file is installed by default to perform tests on?
App.test.js

What does the `Link` component from the React Router tool allow you to do?
-   It creates hyperlinks that allow users to navigate to other pages on the website.
-   Once you have set up the routes for each page of your website, you can use the `Link` component to create clickable webpage links.

Why would you wrap your app component in the router?
to give the app access to all the properties of the router
