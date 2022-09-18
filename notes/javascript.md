# Javascript

A multi paradigm interpreted or JIT programming language with [first class functions](https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function).
Created Brendan Eich as scripting language for Netscape, it is the primary language of the web and is also using as scripting or serverside language thanks to runtimes like Node and Deno.

## Main features

1. inheritance implemented using prototype chain.
2. single-threaded.
3. dynamically typed language.
4. multi-paradigm: imperative, OOP and FP.

## Equality

That are 4 algorithms defined in JS + 2 that not defined in the language but are commonly used.

1. [IsLooselyEqual](https://tc39.es/ecma262/#sec-islooselyequal), operator `==`.
2. [IsStrictlyEqual](https://tc39.es/ecma262/#sec-isstrictlyequal), operator `===`, used by `Array.prototype.indexOf`, `Array.prototype.lastIndexOf`, and case-matching.
3. [SameValueZero](https://tc39.es/ecma262/#sec-samevaluezero), used by %TypedArray% and ArrayBuffer constructors, as well as Map and Set operations, and also String.prototype.includes and Array.prototype.includes.
4. [SameValue](https://tc39.es/ecma262/#sec-samevalue), used by `Object.is`.

### IsLooselyEqual features

1. uses `IsStrictlyEqual` if the operands have the same type.
2. coerces the operands if they do not have the same type.
3. `null == undefined` is always `true`.

### IsStrictlyEqual

1. For primitive types checks that they are equal
2. For reference types checks that both operands reference the same object.
3. `NaN === NaN` is always `false`.
4. `-0 === 0` is always `true`.

### SameValueZero

Used by the crud methods of Map and Set

1. `NaN eq NaN` is always `true`.
2. `-0 eq 0` is always `true`.
3. Same behaviour of `SameValue` except for `1.` and `2.`.

### Same Value

Two operands are the same if one of the following holds:

- both undefined
- both null
- both true or both false
- both strings of the same length with the same characters in the same order
- both the same object (meaning both values reference the same object in memory)
- both numbers and
- both +0
- both -0
- both NaN
- both non-zero and both not NaN and both have the same value


## Closures

A closure is the combination of a function bundled with references to its surrounding state, the [lexical environment](#lexical-environment).

A closure is a reference within a function body to variables defined in the upper scope, the lexical environment.

Every closure has three scopes:

- Local scope (Own scope)
- Enclosing scope (can be block, function, or module scope)
- Global scope

### Lexical environment

A lexical environemnt is a data structure that holds `identifier-variable` mapping of the function scope and a reference
to the upper scope.

## Event loop

```ts
// Pseudo implementation of the event loop.
let task: MacroTask;
const microTaskQueue: MicroTaskQueue;

while((task = taskQueue.poll())) {
  execTask(task);

  while(microTaskQueue.size > 0) {
    execMicroTask(microTaskQueue.shift());
  }
}
```

A every spin of the event loop a task if present is processed then all queued microtasks are [processed from the oldest](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model) hence microtasks have higher priority than macrotasks.