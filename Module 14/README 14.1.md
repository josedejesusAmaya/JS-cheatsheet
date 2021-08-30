Design patterns are comprised of object-oriented basics. What are the object-oriented basics?
* Inheritance [Inheritance (IS-A) vs. Composition (HAS-A) Relationship - w3resource](https://www.w3resource.com/java-tutorial/inheritance-composition-relationship.php)
* Polymorphism
* Abstraction
* Encapsulation

# Design Principles
General guidelines

# Design Patterns
Specific solutions

### What about Interfaces?
- An interface defines the methods an objects must have in order to be considered a particular type.
- An interface is an abstract type that specifies a behavior that must implement.
- Interfaces allow different classes to share similarities.
- Not all classes need to have the same behavior.


# Separate what varies and encapsulate it
- If some aspect of your code is changing, that's a sign you should pull it out and separate it.
- By separating out the parts of your cide that change, you can extend or alter them without affecting the rest of your code.
- This principle is fundamental to almost every design pattern.

# Program to an Interface, Not an Implementation

# HAS-A Is Better Than IS-A

# Loose coupling
# Cohesion

# Class
Groups variables (properties) and funtions (methods) that are highly related.

# Constructor
Is basically a method that is called when we create an instance of that class

### Creational Patterns
-	Factory method: This pattern defines an interface for creating an object, but lets subclasses decide wich class to instantiate. Factory Method lets a class defer instantiation to subclasses.

### Structural Patterns
- Adapter: This pattern converts the interface of a class into another interface that clients expect. It allows classes to work together that couldn't otherwise because of incompatible interfaces.
- Decorator: This pattern attaches additional responsabilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality. 

### Behavioral Patter
- Iterator: This pattern provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

	Build-in Iterator in JS
	```
		for... of statement	
	```
- Observer: This pattern defines a one-of-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.
	The Subject interface defines the three methods necessary to comply with this pattern: **attach , detach , and notify** .
- Strategy: This pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. This lets the algorithm vary independently from clients that use it.

The Factory Pattern also has a Simple Factory Pattern. What is the Simple Factory Pattern?
-   The Simple Factory Pattern decouples the process of creating and using objects from the clients.

Why does the Factory pattern provide loose coupling and high cohesion?
-   The Factory pattern encapsulates object creation logic, which makes it easy to change later.

# Object oriented design
# Head First Design Patterns
by Kathy Sierra, Bert Bates, Elisabeth Robson, Eric Freeman.

# Enterprise Patterns
# Distributed Computing Patterns
