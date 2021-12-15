-   Can you explain how useEffect works?
	
	
-   What is a fragment in React?
	The fragment is a feature to allow us not to kind of junk up the DOM by adding to many elements. Fragments let you group a list of children without adding extra nodes to the DOM.
	```jsx
		render() {
  			return (
    			<React.Fragment>
      				<ChildA />
      				<ChildB />
      				<ChildC />
    			</React.Fragment>
  			);
		}
	```
-   What useReducer does?
	An alternative to [`useState`]. Accepts a reducer of type `(state, action) => newState`, and returns the current state paired with a `dispatch` method.
```jsx
	const initialState = {count: 0};
	function reducer(state, action) {
  		switch (action.type) {
    		case 'increment':
      			return {count: state.count + 1};
    		case 'decrement':
      			return {count: state.count - 1};
    		default:
      			throw new Error();
  		}
	}

	function Counter() {
  		const [state, dispatch] = useReducer(reducer, initialState);
  			return (
    			<>
      				Count: {state.count}
      				<button onClick={() => dispatch({type: 'decrement'})}>-</button>
      				<button onClick={() => dispatch({type: 'increment'})}>+</button>
    			</>
  		);
	}
	
```
dispatch() is the method used to dispatch actions and trigger state changes to the store.

-   What is the differences between useReducer and useState?
	If I only use it to directly set a value, both functions are equal.
	The setter returned by `useState` is being created newly on each update or render.
	And uses call backs but you would need to take care of closure issues, instead `useReducer` use dispach functions. React guarantees that `dispatch` function identity is stable and won’t change on re-renders.
	
-   What is React context?
	Context provides a way to pass data through the component tree without having to pass props down manually at every level.
	Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.
```jsx
// Context lets us pass a value deep into the component tree
// without explicitly threading it through every component.
// Create a context for the current theme (with "light" as the default).const ThemeContext = React.createContext('light');
class App extends React.Component {
  render() {
    // Use a Provider to pass the current theme to the tree below.    
	// Any component can read it, no matter how deep it is.    
	// In this example, we're passing "dark" as the current value.    
	return (
      <ThemeContext.Provider value="dark">        
	  <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

// A component in the middle doesn't have to// pass the theme down explicitly anymore.function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // Assign a contextType to read the current theme context.  
  // React will find the closest theme Provider above and use its value.  
  // In this example, the current theme is "dark".  
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;  }
}
```

-   What do you think could be some of the limitation for React Context?
	Using context will make your code harder to understand because it makes the data flow less clear. It is similar to using global variables to pass state through your application.

-   How do you make reference to the DOM in React?
	Importing ReactDOM from 'react-dom' in index.js file then
	ReactDOM.render(
		// here we can put the main component that is going to be render
		document.getElementById('root') // reference to div with id="root" inside 
																// public/index.html
	)
-   How do you sent and HTTP Request in React?
	We can use fetch as we know it from JS, XMLHttpRequest or Axios (HTTP request library).

-   Is it possible to create custom hooks in React?
	A custom hook allows you to extract some components logic into a reusable function.
	A custom hook is a Javascript function that starts with _use_ and that call can other hooks. Remember that components and hooks are functions, so we are really not creating any new concepts here. We are just refactoring our code into another function to make it reusable.
	- I'll create a new file called _useWindowWidth.js_
```jsx
import { useState, useEffect } from "react";

const useWindowsWidth = () => {
  const [isScreenSmall, setIsScreenSmall] = useState(false);

  let checkScreenSize = () => {
    setIsScreenSmall(window.innerWidth < 600);
  };
  useEffect(() => {
    checkScreenSize();
    window.addEventListener("resize", checkScreenSize);

    return () => window.removeEventListener("resize", checkScreenSize);
  }, []);

  return isScreenSmall;
};

export default useWindowsWidth;
```
We extracted this functionality inside this _useWindowWidth_ function. Now, we can import it anywhere we want to use it!
```jsx
import React from 'react'
import useWindowWidth from './useWindowWidth.js'

const MyComponent = () => {
  const onSmallScreen = useWindowWidth();

  return (
    // Return some elements
  )
}
```

-   What is Redux?
	Redux itself is a standalone library and a state management tool. State management is essentially a way to facilitate communication and sharing of data across components.
	
-   What is a hook?
	They let you use state and other React features without writing a class.
	Hooks are **functions** that let you “hook into” (**to become connected to**) React state and lifecycle features from function components. Hooks don’t work inside classes — they let you use React without classes.

### React 16 solves this with **Fragments**. This new features allows you to wrap a list of children without adding an extra node.

### React HOC
### React Fragment vs Div
A div has the prototype chain:
*HTMLDivElement - HTMLElement - Element - Node - EventTarget*

Whereas a document-fragment has:
*DocumentFragment - Node - EventTarget*

**This means a div has more methods and properties available (like innerHTML).**

The **Fragments** eliminate the wrapper div which can cause problems with invalid HTML and stayling of the components plus the fact that they are faster and the DOM is less cluttered (mess up).
```jsx
	<React.Fragment>
   		Hello world
	</React.Fragment>
```
Short Syntax:
```jsx
	<>
   		Hello world
	</>
```

**You can't add properties like key with this syntax.**

### Why Props are immutable?
A component should manage its own state, but it should not manage its own props. `props` is essentially "state that is managed by the component owner." That's why props are _immutable_.

React docs also recommends to treat state as if it's immutable. That is because by manipulating `this.state` directly you are circumventing React’s state management, which can be potentially dangerous as calling `setState()` afterwards may replace the _mutation_ you made.
[reactjs - Why are React props immutable? - Stack Overflow](https://stackoverflow.com/questions/47471131/why-are-react-props-immutable)
[Components and Props – React (reactjs.org)](https://reactjs.org/docs/components-and-props.html#props-are-read-only)

### What's virtual DOM?
The virtual DOM (VDOM) is a programming concept where an ideal, or “virtual”, representation of a UI is kept in memory and synced with the “real” DOM by a library such as ReactDOM. This process is called [reconciliation](https://reactjs.org/docs/reconciliation.html).

This approach enables the declarative API of React: You tell React what state you want the UI to be in, and it makes sure the DOM matches that state.

### The Diffing Algorithm

When diffing two trees, React first compares the two root elements. The behavior is different depending on the types of the root elements.
