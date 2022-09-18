# General programming knowledge

## Object oriented programming

A programming paradigm at the core of many languages, such as Java.
OOP is about modelling the domain as collection of objects,
every object models a specific aspect of the system.

In broad terms object can have functions, commonly referred as methods or
data known as members or fields.

In class-based object oriented programming object are defined using a blueprint
called **class**.
An object created from a class is called **instance** of that specific class.
A class can have 1 or more instances that shares the methods defined in the class.

Code reuse is based on the concept of inheritance or composition.
classes can extends other classes inheriting all the methods and members.

## Functional programming

A programming paradigm that models problems using a more mathematical approach instead
of treating them as a sequence of imperative statements (condititional jumps etc...).

At the core of functional programming are 3 main concepts.
Purity/Referencial transparency and functions as first class citizens.

### Function Purity

In functional programming functions must be **pure**:

1. Do not perform sideEffects, such as I/O mutating objects outside their scope etc..
2. Return always the same value if the input is the same.

### Referential transparency

An expression is referentially transperent if can **always** be replaced with its return value. 
Pure functions do not have side effects and every call expression is referentially transparent.

Pure functions do not have side effects and can always be memoized.

### Functions as first class citizens

In functional programming functions are first class citizens, they can be referenced, composed and can be argument
or return type of other functions.

A function that either returns a function or expects a function as argument is called higher-order functions.

### Taming complexity

In FP complex problems are decomposed in units and functional composition is the key to resolve complex problems

## Inversion of control

Programming principle that inverts the flow of control as compared to traditional control flow. 
In IoC systems the business logic is not defined at compile time, it is instead dynamic and built to be more resient.

Inversion of control serves the following design purposes:

- To decouple the execution of a task from implementation.
- To focus a module on the task it is designed for.
- To free modules from assumptions about how other systems do what they do and instead rely on contracts.
- To prevent side effects when replacing a module.

## Dependency injection

design pattern in which the instance or function receives externally its dependencies.
DI is a form of IoC and DI solutions have dependencies provided at runtime.

### Benefits

- loose coupling between systems.
- reusable code.
- testing becomes a lot more easier.

## REST and Restful api

### What is REST

REST is a set of architectural constraints, not a protocol or a standard.
In order for an API to be considered RESTful it needs to conform to the following criterias:

1. A client-server architecture made up of clients, servers, and resources, with requests managed through HTTP.
2. Stateless client server communication, meaning no client information is stored between get requests and each request is separate and unconnected.
3. Cacheable data that streamlines client-server interactions.
4. A uniform interface between components so that information is transferred in a standard form.
