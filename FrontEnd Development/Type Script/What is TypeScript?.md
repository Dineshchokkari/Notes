TypeScript stands in an unusual relationship to [[JavaScript]]. TypeScript offers all of JavaScript’s features, and an additional layer on top of these: TypeScript’s type system.

>This means that your existing working JavaScript code is also TypeScript code. The main benefit of TypeScript is that it can highlight unexpected behaviour in your code, lowering the chance of bugs.

The most common kinds of errors that programmers write can be described as type errors: a certain kind of value was used where a different kind of value was expected. This could be due to simple typos, a failure to understand the API surface of a library, incorrect assumptions about runtime behaviour, or other errors.

JavaScript is dynamically typed. This means JavaScript does not know what type a variable is until it is actually instantiated at run-time. This also means that it may be too late. TypeScript adds type support to JavaScript and catches type errors during compilation to JavaScript.

>In other words, TypeScript is a tool that runs before your code runs (static) and ensures that the types of the program are correct (type-checked).
