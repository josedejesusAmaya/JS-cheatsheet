### Creating a TypeScript project
Typed superset of JavaScript. Meaning that it only extends JS's functionality.
It' doesn't change the way JS works.
TypeScript also refers to the compiler, wich transcompile code written in the TypeScripts syntax to JS, which is widely supported across most browsers.
TypeScript is transpile to JS.

* TS validates your JS ahead of time
* Provides auto-complete for untyped libraries
* Describe the shape of objects and functions 
* Supports rich type-checking in JSX environments like React
* Strong typing
* Object-oriented features

```
	npm install -g typescript
	tsc --version 
	tsc main.ts | node main.js
```
There really aren’t any browsers or other runtimes that can just run TypeScript unmodified. That’s why TypeScript needs a compiler in the first place - it needs some way to strip out or transform any TypeScript-specific code so that you can run it.

****Remember**: Type annotations never change the runtime behavior of your program.**

Even through we have a compilation error the TS compiler still generated main.js

#### Adding TS to an existing application
1. Create a tsconfig.json file:
	```json
		{
			"compilerOptions": {
				"target": "es5",
				"outDir": "dist"
			}
		}
	```
2. Create module.ts and write your code that it's going to be transcompile to JS in another JS file with the same name in *dist* folder.

#### Type inference
TS is able to figure out the type of many variables without you having to provide any information at all.

```ts
	let a; // a: any
```

#### Type Assertions
Sometimes, you as a programmer might know more about the type of a variable than TypeScript can infer. Usually, this happens when you know the type of an object is more specific than its current type. In such cases, you can tell the TypeScript compiler not to infer the type of the variable by using type assertions.
Type assertions simply let the TypeScript compiler know the type of the variable.

TypeScript provides two forms to assert the types.
-   as syntax:
```ts
let value: unknown = "Foo";
let len: number = (value as string).length;
```
-   <> syntax:
```ts
let value: unknown = "Foo";
let len: number = (<string>value).length;
```

#### In line annotation:
```ts
	let drawPoint = (point: {x: number, y: number}) {
		// ...
	}
	
	// or define the interface
	interface Point { // Pascal naming convention
		x: number,
		y: number
	}
```

#### Literal Types
A literal is a more concrete sub-type of a collective type. What this means is that `"Hello World"` is a `string`, but a `string` is not `"Hello World"` inside the type system.
There are three sets of literal types available in TypeScript today: strings, numbers, and booleans; by using literal types you can allow an exact value which a string, number, or boolean must have.
```ts
	type Size = 8 | 16 | 32;
	interface MapConfig {
		lng: number;
		lat: number;
		tileSize: Size;
	}

	const createMap = (lng: number, lat: number, tileSize: number): MapConfig => {
		const newMap: MapConfig = {
			lng,
			lat,
			tileSize: tileSize as Size // cast
		}
		return newMap;
	}
	
	const fool = createMap(1,2,3);
	console.log(fool);
```

#### Types in TS
1. Boolean
2. Number
3. String
4. Void: The void type can have undefined or null as a value where as never cannot have any value.
5. Any
6. Never: which indicates the values that will never occur. The never type is used when you are sure that something is never going to occur. For example, you write a function which will not return to its end point or always throws an exception.
	```ts
		function throwError(errorMsg: string): never { 
            throw new Error(errorMsg); 
		}
		
		function keepProcessing(): never { 
            while (true) { 
         		console.log('I always does something and never ends.')
     		}
		}
	```
7. Null: Empty value
8. Tuple: Are a special type in TypeScript. They are similar to arrays with a fixed number of elements with a known type. However, the types need not be the same. Tuple can contain two or more values of different data types.
	```ts
		// Declare a tuple type and initialize it 
		let values: [string, number] = 	["Foo", 15];
		
		values[0]; // "Foo"
	```
10. Enum: 
11. Unknown: It's less permissive than `any` type. The `unknown` type is only assignable to the `any` type and the `unknown` type itself.
	```ts
		// all this code works perfectly for any type
		let value: unknown;
		value.foo.bar; // Error 
		value.trim(); // Error 
		value(); // Error 
		new value(); // Error 
		value[0][1]; // Error
	```
	This is the main value proposition of the `unknown` type: TypeScript won't let us perform arbitrary operations on values of type `unknown`.
11. Object
12. Array

[TypeScript: Documentation - Everyday Types (typescriptlang.org)](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

#### Array
```ts
	let fruits: string[] = ['apple', 'watermelon', 'strawberry'];
	let fruits2: Array<string> = [];
	
```

#### Enum
Enums are a feature added to JavaScript in TypeScript which makes it easier to handle named sets of **constants**.
To put all the related variables or constants
```ts
	enum Color {
		Red,
		Green,
		Blue
	}
```

By default an enum is number based, starting at zero, and each option is assigned an  increment by one. This is useful when the value is not important.
```ts
	enum UserResponse {
		No = 0,
		Yes = 1,
	}
	
	function respond(recipient: string, message: UserResponse): void {
		// ...
	}

	respond("Princess Caroline", UserResponse.Yes);
```

#### Gradual typing
Is what allows you to choose when and how TypeScript applies typing to your code. In other words, to tell TS to butt out whenever you need it to.

#### Interfaces
Interfaces definitions have no impact on the code that's rendered. In fact the very first thing that the TS compiler does is digest these interfaces to remember them for later, and then completly removes them from the code.

The more information you can give to TS the better it can help you. 

Interfaces can inherit properties from another Interface.
```ts
	interface User {
		name: string;
		age: number;
	}

	interface Employee extends User {
		job: string;
	}

	const user = Employe = {
		name: "Pepe",
		age: "27",
		job: "software developer"
	}
```

Interfaces are blueprints of a class
```ts
	interface Authentication {
		apihost?: string;
		login(email: string, password: string): string | null;
		register(data: { email: string; password: string }): boolean;
	}

	class AuthenticationClient implements Authentication {
		apihost?: string;
		
		login(email: string, password: string): string | null {
			return null;
		}
		
		register(data: { email: string; password: string }): boolean {
			return false;
		}
	}
```

#### Downleveling
Template strings are a feature from a version of ECMAScript called ECMAScript 2015 (a.k.a. ECMAScript 6, ES2015, ES6, etc. - _don’t ask_). TypeScript has the ability to rewrite code from newer versions of ECMAScript to older ones such as ECMAScript 3 or ECMAScript 5 (a.k.a. ES3 and ES5). This process of moving from a newer or “higher” version of ECMAScript down to an older or “lower” one is sometimes called _downleveling_.

By default TypeScript targets ES3, an extremely old version of ECMAScript.

#### noImplicitAny
Recall that in some places, TypeScript doesn’t try to infer any types for us and instead falls back to the most lenient type: `any`. This isn’t the worst thing that can happen - after all, falling back to `any` is just the plain JavaScript experience anyway.

However, using `any` often defeats the purpose of using TypeScript in the first place. The more typed your program is, the more validation and tooling you’ll get, meaning you’ll run into fewer bugs as you code. ***Turning on the `noImplicitAny` flag will issue an error on any variables whose type is implicitly inferred as `any`.***

### Reviewing ES6 language features
[TypeScript: Documentation - TypeScript for JavaScript Programmers (typescriptlang.org)](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)
[TypeScript: Documentation - Everyday Types (typescriptlang.org)](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

### Specifying JavaScript types
There are already a small set of primitive types available in JavaScript: 
	1. `boolean`, 
	2. `bigint`, 
	3. `null`, 
	4. `number`, 
	5. `string`, 
	6. `symbol`, and 
	7. `undefined`, 
	Which you can use in an interface. TypeScript extends this list with a few more, such as: 
	8. `any` (allow anything), 
	9. [`unknown`](https://www.typescriptlang.org/play#example/unknown-and-never) (ensure someone using this type declares what the type is), 
	10. [`never`](https://www.typescriptlang.org/play#example/unknown-and-never) (it’s not possible that this type could happen), and 
	11. `void` (a function which returns 
	12. `undefined` or has no return value).

### Defining custom and anonymous types
TS offers three ways to define custom types:
- interfaces
- classes
	```ts
		class Person {
			firstName: string;
			lastName: string;
			age: number;
		}
	```
- enums

### Difference between interface and classes
At it's most basic, a **class** is essentially an _object factory_ (ie. a blueprint of what an object is supposed to look like and then implemented), whereas an **interface** is a structure used solely for _type-checking_.

While a **class** may have initialized properties and methods to help create objects, an **interface** essentially defines the properties and type an object can have.
[When use a interface or class in Typescript - Stack Overflow](https://stackoverflow.com/questions/51716808/when-use-a-interface-or-class-in-typescript)

#### Anonymous Types
You can actually declare interfaces right inline anywhere that accepts a type
```ts
	var todo = { name: string, age: number };
	todo = { age: 41 }; // throws an error 'cause name property is not present
	
	function totalLength(x: {length: number}, y: (string | any[])) { 
		// ...
	}
```

```ts
	interface User {
		name: 'Pepe' | 'Emi';
	}

	let user: User = { name: 'Ana' }; // Type '"Ana"' is not assignable to type '"Pepe" | "Emi"'.
```

#### null and undefined
JavaScript has two primitive values used to signal absent or uninitialized value: `null` and `undefined`.
TypeScript has two corresponding _types_ by the same names. How these types behave depends on whether you have the `strictNullChecks` option on.

##### `strictNullChecks`off
With `strictNullChecks` _off_, values that might be `null` or `undefined` can still be accessed normally, and the values `null` and `undefined` can be assigned to a property of any type. This is similar to how languages without null checks (e.g. C#, Java) behave. The lack of checking for these values tends to be a major source of bugs; we always recommend people turn `strictNullChecks` on if it’s practical to do so in their codebase.

##### `strictNullChecks`on
With `strictNullChecks` _on_, when a value is `null` or `undefined`, you will need to test for those values before using methods or properties on that value. Just like checking for `undefined` before using an optional property, we can use _narrowing_ to check for values that might be `null`:
```ts
	function doSomething(x: string | null) {
		if (x === null) {
		// do nothing
		} else {
			console.log("Hello, " + x.toUpperCase());
		}
	}
```

#### Union Types
The first way to combine types you might see is a _union_ type. A union type is a type formed from two or more other types, representing values that may be _any one_ of those types. We refer to each of these types as the union’s _members_.

Let’s write a function that can operate on strings or numbers:
```ts
	function printId(id: number | string) {
		console.log("Your ID is: " + id);
	}

	// OK
	printId(101);

	// OK
	printId("202");

	// Error
	printId({ myID: 22342 });
```
Argument of type '{ myID: number; }' is not assignable to parameter of type 'string | number'. Type '{ myID: number; }' is not assignable to type 'number'.

#### Type Aliases
We’ve been using object types and union types by writing them directly in type annotations. This is convenient, but it’s common to want to use the same type more than once and refer to it by a single name.

A _type alias_ is exactly that - a _name_ for any _type_. The syntax for a type alias is:
```ts
	type Point = {
		x: number;
		y: number;
	};
	
	// Exactly the same as the earlier example
	function printCoord(pt: Point) {
		console.log("The coordinate's x value is " + pt.x);
		console.log("The coordinate's y value is " + pt.y);
	}
	printCoord({ x: 100, y: 100 });
```
You can actually use a type alias to give a name to any type at all, not just an object type. For example, a type alias can name a union type:
```ts
	type ID = number | string;
```

### Diference between type alias and interfaces
1. Declaration merging: One thing that’s possible to do with interfaces but are not with types is declaration merging. Declaration merging happens when the TypeScript compiler merges two or more interfaces that share the same name into only one declaration.
	Let’s imagine that we have two interfaces called `Song`, with different properties.
	```ts
	interface Song { artistName: string; }; 
	interface Song { songName: string; }; 
	
	const song: Song = { artistName: "Freddie", songName: "The Chain" };
	```
	TypeScript will automatically merge both interfaces declarations into one, so when we use this `Song` interface, we’ll have both properties.
	Declaration merging does not work with types. If we try to create two types with the same names, but with different properties, TypeScript would still throw us an error.
	```ts
	Duplicate identifier Song.
	```
	
	[Types vs. interfaces in TypeScript - LogRocket Blog](https://blog.logrocket.com/types-vs-interfaces-in-typescript/)
	
### Intersection types
`interface`s allowed us to build up new types from other types by extending them. TypeScript provides another construct called _intersection types_ that is mainly used to combine existing object types.
An intersection type is defined using the `&` operator.
```ts
interface Colorful {
	color: string;
}

interface Circle {
	radius: number;
}

type ColorfulCircle = Colorful & Circle;
```
Here, we’ve intersected `Colorful` and `Circle` to produce a new type that has all the members of `Colorful` _and_ `Circle`.

### Interfaces vs. Intersections
With interfaces, we could use an `extends` clause to extend from other types, and we were able to do something similar with intersections and name the result with a type alias. The principle difference between the two is how conflicts are handled.

```ts
interface NumberToStringConverter {
	convert: string;
}

interface BidirectionalStringNumberConverter extends NumberToStringConverter {
	convert: number;
}
```
The `extends` above results in an error because the derriving interface declares a property with the same key as one in the derived interface but with an incompatible signature.

However, if we employ intersection types:
```ts
type NumberToStringConverter {
	convert: string;
}

type BidirectionalStringNumberConverter = NumberToStringConverter & {
	convert: number;
};
```
This is not error. Now convert property accepts string | number

[types - Difference between extending and intersecting interfaces in TypeScript? - Stack Overflow](https://stackoverflow.com/questions/52681316/difference-between-extending-and-intersecting-interfaces-in-typescript)

### Defining and implementing TypeScript classes
#### Convention
In JS we are using underscore to indicate "private" members
```js
	class InvertoryStore {
		_categories: Category[] = [];
		_items: InventoryItem[] = [];
		_isInitialized: Promise<any>;
	}
```

In TS we are using _access modifiers_
* private
	Only visible to members within the same class.
* protected
	Visible to member within the same class and derived or extended classes. 
* public (default)
	Visible to all consumers.
* abstract 
	Abstract classes are base classes from wich other classes may ve derived. They may not be instatiated directly. Unlike an interface, an abstract class may contain implementation details for its members. Methods can be defined as abstracts, too. 
```ts
	class InvertoryStore {
		private _categories: Category[] = [];
		private _items: InventoryItem[] = [];
		private _isInitialized: Promise<any>;
	}
```

### Working with generics
Is a way to decorate a component with a type syntaxt in such a way that it can describe a variety of types rather than a single one.
```ts
	function clone<T>(source: T): T {
		const serialized = JSON.stringify(source);
		return JSON.parse(serialized);
	}
	
	const cloned = clone<InventoryItem>(inventoryItem);
```

Also, we can use it with classes and interfaces:
```ts
	// class KeyValuePair<TKey, TValue> {
	interface KeyValuePair<TKey, TValue> {
		Key: TKey;
		Value: TValue;
	}
	
	var keyValue: KeyValuePair<string, number> = { Key: "something", Value: 1234 };
	var keyValue2: KeyValuePair<number, boolean> = { Key: 1234, Value: true };
```

So next time you see this syntax, you'll now that you're getting advanced typing support.

### Organizing code with namespaces (Internal modules)
Namespaces are a TypeScript-specific way to organize code.  
Namespaces are simply named JavaScript objects in the global namespace. This makes namespaces a very simple construct to use. Unlike modules, they can span multiple files, and can be concatenated using `--outFile`. Namespaces can be a good way to structure your code in a Web Application, with all dependencies included as `<script>` tags in your HTML page.

Just like all global namespace pollution, it can be hard to identify component dependencies, especially in a large application.

[TypeScript: Documentation - Namespaces (typescriptlang.org)](https://www.typescriptlang.org/docs/handbook/namespaces.html)

A TypeScript namespace is really nothing more than syntactic sugar to create an IIFE. That means that everything you write within the namespace declaration is automatically kept within the same scope and not allowed to leak out of that scope, unless you explicitly expose it yourself.

#### Internal vs External Modules
* Both encourage encapsulation and organization.
* Different implementations:
	Internal - namespaces funtion scope
	External - file scope
* Both require components to be exported.
* Both require components to be imported.

#### TypeScript Module Import Syntax
* Require (like Node.js)
	```ts
		import Model = require('./model.js');
		import Todo = Model.Todo;
	```
* ECMAScript 2015 (ECMAScript standar) <- prefered
	```ts
		import { Todo as TodoTask, TodoState } from './model';
	```
* Functionally equivalent (They generate the same code).

#### TS Module Export Syntax
* Require (like Node.js)
```ts
	module.exports = class Vector {
		// ...
	}
```
* ECMAScript 2015 (ECMAScript standar) <- prefered
```ts
	export class Point {
		// ...
	}
```

### Switching form internal to external modules
You need to add a module compiler setting in tsconfig.ts file
```ts
	"compilerOptions": {
		"target": "es5",
		"module": "system"
	}
```
Then, separete by files each module and now you can delete the namespace keyword.
 **System.js** module loader.
 Attempst to implement the proposed ECMAScript specification

### Importing modules
[Home | DefinitelyTyped](http://definitelytyped.org/)
In TypeScript, just as in ECMAScript 2015, any file containing a top-level `import` or `export` is considered a module.
[TypeScript: Documentation - Modules (typescriptlang.org)](https://www.typescriptlang.org/docs/handbook/modules.html)

### Debugging TypeScript
[TypeScript debugging with Visual Studio Code](https://code.visualstudio.com/docs/typescript/typescript-debugging)
[TypeScript tutorial with Visual Studio Code](https://code.visualstudio.com/docs/typescript/typescript-tutorial)

### Implementing decorators
Decorators provide a way to add both annotations and a meta-programming syntax for class declarations and members.
**NOTE:**  Decorators are an experimental feature that may change in future releases.
A _Decorator_ is a special kind of declaration that can be attached to a [class declaration](https://www.typescriptlang.org/docs/handbook/decorators.html#class-decorators), [method](https://www.typescriptlang.org/docs/handbook/decorators.html#method-decorators), [accessor](https://www.typescriptlang.org/docs/handbook/decorators.html#accessor-decorators), [property](https://www.typescriptlang.org/docs/handbook/decorators.html#property-decorators), or [parameter](https://www.typescriptlang.org/docs/handbook/decorators.html#parameter-decorators). Decorators use the form `@expression`, where `expression` must evaluate to a function that will be called at runtime with information about the decorated declaration.
[TypeScript: Documentation - Decorators (typescriptlang.org)](https://www.typescriptlang.org/docs/handbook/decorators.html)

The following is an example of a class decorator (`@sealed`) applied to a `BugReport` class:
```ts
	@sealed
	class BugReport {
		type = "report";
		title: string;
		
		constructor(t: string) {
			this.title = t;
		}
	}
```
When `@sealed` is executed, it will seal both the constructor and its prototype which would not allow the class to be sub-classed at runtime.

### Which of the following is true about Modules in JavaScript?
-   They encourage more explicit dependencies.

### Namespaces cause naming collisions.
-   FALSE

### Which of the following is not true about external modules?
- They need to implement spacenames  function scope.

### Which of the following statements do I use to bring everything that is exported in an existing "Model" module into the scope of the current module I am in?
-   import Model = require('./model');

### How to make object properties immutable in TypeScript?
You can mark object properties as immutable by using the readonly keyword before the property name. For example:
```ts
	interface Coordinate {
		readonly x: number;
	}
	
```

When you mark a property as readonly, it can only be set when you initialize the object. Once the object is created, you cannot change it.
```ts
	let c: Coordinate = { x: 5, y: 15 };
	c.x = 20; // Cannot assign to 'x' because it is a read-only property.(2540)
```

```ts
	class Person() {
		// dni: number; we don't need to add this property it'll be added automatically
		constructor(readonly dni: number) {
			// this.dni = dni;
		}
	}

	const user: Person = new Person(234535);
	user.dni = 12546; // Cannot assign to 'dni' because it is a read-only property.(2540)
```
