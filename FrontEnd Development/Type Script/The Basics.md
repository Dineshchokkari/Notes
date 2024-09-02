
Let's start with an example:

```JavaScript

message.toLowerCase();

// Calling the Function
message();
```

The potential problems with the above code assuming we don't know the value of message:
- Is `message` callable?
- Does it have a property called `toLowerCase` on it?
- If it does, is `toLowerCase` even callable?
- If both of these values are callable, what do they return.

Let's define `message` as:
```JavaScript
const message = 'Hello World';
```

Then we get `hello world` on running the first line of the code. But we get something like `TypeError: message is not function` executing the second line.

>`TypeScript` can  catch bugs when we make mistakes in our code. That’s great, but TypeScript can _also_ prevent us from making those mistakes in the first place.


# tsc, the TypeScript compiler
---
> To install TypeScript

```node
npm install -g typescript
```

create a simple `ts` file and call it `hello.ts`

```TypeScript
console.log('Hello World');
```

It looks similar to a plain JavaScript file. If we compile a typescript file using `tsc` command, it generates use `js` file of the same name if there are no errors.

Let's rewrite the `hello.ts` to

```TypeScript
function greet(person, date) {

console.log(`Hello ${person}, today is ${date}!`);

}

greet("Brendan");
```

If we run it again using the `tsc` command we'll get `Expected 2 arguments, but got 1.`


# TypeScript to JavaScript
---

```TypeScript
function greet(person: string, date: Date): void {

console.log(`Hello ${person}, today is ${date}!`);

}

greet("Brendan", new Date());
```

```JavaScript
function greet(person, date) {

console.log("Hello ".concat(person, ", today is ").concat(date, "}!"));

}

greet("Brendan", new Date());
```

Notice that
- 1. Our `person` and `date` parameters no longer have type annotations.
2. Our “template string” - that string that used back ticks (the `` ` `` character) - was converted to plain strings with concatenations.

`tsc` strip out or transform any TypeScript-specific code so that you can run it. TypeScript has the ability to rewrite code from newer versions of ECMAScript to older ones such as ECMAScript 3 or ECMAScript 5 (a.k.a. ES3 and ES5). This process of moving from a newer or “higher” version of ECMAScript down to an older or “lower” one is sometimes called _downleveling_.