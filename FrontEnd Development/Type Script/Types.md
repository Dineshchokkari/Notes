> The **primitives**

- `string` --> Represents string values.
- `number` --> represents both `int` and `float`.
- `boolean` --> representation for `true` and `false`.

`String`, `Number`, `Boolean` are also legal, but they refer to the built-in types. Always use the above ones that start with small letters.

> **Arrays**

There are different notations based on the type such as `number[]`, `string[]`. Also we can write it as `Array<number>`.

>**any**

We can use whenever we don’t want a particular value to cause type-checking errors. When a value is of type `any`, we can access any properties of it (which will in turn be of type `any`).

>Type Annotations on Variables
---
```TypeScript
const name: string = 'John Doe';
const age: number = 25;
const isLogin: boolean = true;
const obj: any = {x: 0};
const marks: number[] = [1,2,3,4];
```

# Functions
---
> **Parameter** Type Annotations

We can add type annotations after each parameter to declare what types of parameters the function accepts.

```TypeScript
function greet(name: string) {
	console.log("Hello, " + name.toUpperCase() + "!!");
}
```

> **Return** Type Annotations

```TypeScript
function getFavoriteNumber(): number {
	return 26;
}
```

We usually don’t need a return type annotation because TypeScript will infer the function’s return type based on its `return` statements.

> Functions which return **Promises**

```TypeScript
async function getFavoriteNumber(): Promise<number> {
	return 26;
}
```

>**Anonymous** functions

```TypeScript
const names = ["Alice", "Bob", "Eve"];

// Contextual typing for function - parameter s inferred to have type string
names.forEach(function (s) {
	console.log(s.toUpperCase());
});

// Contextual typing also applies to arrow functions

names.forEach((s) => {
	console.log(s.toUpperCase());
});
```

Even though the parameter `s` didn’t have a type annotation, TypeScript used the types of the `forEach` function, along with the inferred type of the array, to determine the type `s` will have. This process is called _contextual typing_ because the _context_ that the function occurred within informs what type it should have.

# Object
---
for a function that takes login-credentials;
```TypeScript
const login = (creds: {username: string, password: string}) => {
	console.log(`username is ${username}`);
	console.log(`password is ${password}`);
}
```

We annotated the parameter with a type with two properties - `username` and `password` - which are both of type `string`. We can use `,` or `;` to separate the properties. If we don’t specify a type, it will be assumed to be `any`.

> Optional Properties

To make some of the properties optional, add a `?` after the property name.
```TypeScript
function printName(obj: { first: string; last?: string }) {
	// ...
}
// Both OK
printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });
```

While accessing the optional property make sure to `check` if it exists, this makes the code more compact.

# Union
---

>A union type is a type formed from two or more other types, representing values that may be _any one_ of those types. We refer to each of these types as the union’s _members_.

```TypeScript
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

TypeScript will only allow an operation if it is valid for _every_ member of the union.

```TypeScript
function printId(id: number | string) {
	console.log(id.toUpperCase());
	// cannot use it as number do not contain that method.
}
```

The solution is to _narrow_ the union with code, the same as you would in JavaScript without type annotations. _Narrowing_ occurs when TypeScript can deduce a more specific type for a value based on the structure of the code.

```TypeScript
function printId(id: number | string) {
	if (typeof id === "string") {
		console.log(id.toUpperCase());
	} else {
		console.log(id);
	}
}
```

# Type Aliases
---
To avoid using object types and union types by writing them directly in type annotations we can use type aliases.

```TypeScript
type Point = {
	x: number,
	y: number
};

funtion printPoint(pt: Point): void {
	console.log(`x --> ${pt.x}`);
	console.log(`y --> ${pt.y}`);
}
```

We can also give a type alias a union.
```TypeScript
type ID = number | string;
```

## Interfaces
---
An _interface declaration_ is another way to name an object type:

```TypeScript
interface Point {
	x: number;
	y: number;
}
function printCoord(pt: Point) {
	console.log("The coordinate's x value is " + pt.x);
	console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 100, y: 100 });
```


> Difference between Type and Interface

- Extending and interface Vs. type
```TypeScript
// Interfacce
interface Animal {
  name: string;
}  
interface Bear extends Animal {
  honey: boolean;
}  
const bear = getBear();
bear.name;
bear.honey;	

// Type
type Animal = {
  name: string;
}  
type Bear = Animal & { 
  honey: boolean;
}  
const bear = getBear();
bear.name;
bear.honey;
```

- Adding new fields to interface vs. type
```TypeScript
//Interface
interface Window {
  title: string;
}  
interface Window {
  ts: TypeScriptAPI;
}  
const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});

//Type
type Window = {
  title: string;
}  
type Window = {
  ts: TypeScriptAPI;
}  
 // Error: Duplicate identifier 'Window'.
```

## Literal Types
---
In addition to the general types `string` and `number`, we can refer to _specific_ strings and numbers in type positions.
```TypeScript
function printText(s: string, alignment: "left" | "right" | "center") {
	// ...
}
printText("Hello, world", "left");
printText("G'day, mate", "centre"); // Gives an error
```
