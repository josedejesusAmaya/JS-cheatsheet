### Clean Code examples in the 4 most popular languages (Java + C# + JS+ Python)
#### Java
**clean code can be summarized as a code that any developer can read and change easily**.
1. Project Structure
2. Naming Convention
3. Whitespaces
4. Indentation
5. Comments
6. Loggin
7. Test

[Clean Coding in Java | Baeldung](https://www.baeldung.com/java-clean-code)

#### C#
1. **Use meaningful names**
 
 [Clean Code Principles In C# Aka How To Write Projects That Don't Suck - ServoCode](https://servocode.com/blog/clean-code-principles-in-c-aka-how-to-write-projects-that-dont-suck)
 
 [20 Important Tips To Write Clean C# Code - MUST SHARE (codewithmukesh.com)](https://codewithmukesh.com/blog/write-clean-csharp-code/)
 
 #### JS
 1. Declaring and assigning variables from object properties.
```js
	❌  
	const a = foo.x, b = foo.y;

	✔️
	const { ['x']: a, ['y']: b } = foo;
```
 
[10 Clean code examples (Javascript). - DEV Community](https://dev.to/redbossrabbit/10-clean-code-examples-javascript-37kj)

2. Don't write to global variables or functions
 	Polluting globals is a bad practice in JavaScript because you could clash with another library.
	
	Bad:
	```js
		Array.prototype.diff = function diff(comparisonArray) {
  			const hash = new Set(comparisonArray);
  			return this.filter(elem => !hash.has(elem));
		};
	```
 
 Good:
 ```js
 	class SuperArray extends Array {
		diff(comparisonArray) {
			const hash = new Set(comparisonArray);
			return this.filter(elem => !hash.has(elem));
		}
	}
 ```
 [ryanmcdermott/clean-code-javascript: Clean Code concepts adapted for JavaScript (github.com)](https://github.com/ryanmcdermott/clean-code-javascript)
 
 #### Python
 1. Functions should have fewer than 4 arguments
 
 [Python Clean Code: 6 Best Practices to Make Your Python Functions More Readable | by Khuyen Tran | Towards Data Science](https://towardsdatascience.com/python-clean-code-6-best-practices-to-make-your-python-functions-more-readable-7ea4c6171d60)
 
 2. Check Big-O Analysis of Algorithms
 	[Analysis of Algorithms | Big-O analysis - GeeksforGeeks](https://www.geeksforgeeks.org/analysis-algorithms-big-o-analysis/)

3. Functions should do one thing.

[zedr/clean-code-python: Clean Code concepts adapted for Python (github.com)](https://github.com/zedr/clean-code-python)
 
### A list of easy-to-use principles for writing clean code
Following are some recommended practices that will help you embrace exceptions and make use of them and their abilities to keep your code:

-   **maintainability**: Allows us to easily find and fix new bugs, without the fear of breaking current functionality, introducing further bugs, or having to abandon the code altogether due to increased complexity over time.
-   **extensibility**: Allows us to easily add to our code base, implementing new or changed requirements without breaking existing functionality. Extensibility provides flexibility, and enables a high level of reusability for our code base.
-   **readability**: Allows us to easily read the code and discover it’s purpose without spending too much time digging. This is critical for efficiently discovering bugs and untested code.

[On Exception Handling and Clean Code | Toptal](https://www.toptal.com/abap/clean-code-and-the-art-of-exception-handling)

#### DRY & KISS
DRY stands for “Don's Repeat Yourself”. This principle states that **a piece of code should not be repeated across the software**.
KISS stands for “Keep It Simple, Stupid”. This principle states that **we should try to keep the code as simple as possible**.


### Advice on handling errors in code
Back in the days when programming was done in hardware, or via low-level programming languages, exceptions were used to alter the flow of the program, and to avoid hardware failures. Today, Wikipedia [defines exceptions](https://en.wikipedia.org/wiki/Exception_handling) as:
"anomalous or exceptional conditions requiring special processing – often changing the normal flow of program execution…"
- Always create your own `ApplicationError` hierarchy.
- Resist the urge to handle exceptions immediately.

[On Exception Handling and Clean Code | Toptal](https://www.toptal.com/abap/clean-code-and-the-art-of-exception-handling)

### Errors and exceptions - what’s the difference?
#### Errors
Programming errors where there is no way to recover/continue gracefully and usually need a  programmer to step into and change the code to make the fix. Errors can sometimes be turned into exceptions so that they can be handled within the code.

#### Exceptions
Take advantage of language specific semantics and represent when something exceptional has happened. Exceptions are thrown and caught so the code can recover and handle the situation and not enter an error state.

“It is an error to not handle an exception.”

[Henning Thielemann](https://wiki.haskell.org/Error_vs._Exception)

[How to handle errors and exceptions in large scale software projects (With good practices and examples) · Raygun Blog](https://raygun.com/blog/errors-and-exceptions/)
