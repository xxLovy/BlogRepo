---
title: TypeScript
date: 2024-04-18 10:44:00
tags:
---

## Begin

### Compile Typescript to Javascript

```shell
tsc test.ts
```

Even if there are any error in the `.ts` file, a javascript file will still be generated. with `--noEmitOnError` option, the `.js` file will not be generated.

```
tsc --noEmitOnError test.ts
```

### Explicit Types

use `:` to write explicit type annotations 

```ts
function greet(person: string, date: Date) {
  console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}
```

### Erased Types When Compile

Most TypeScript-specific code gets erased away after comliling.

**test.ts**

```ts
function greet(person: string, date: Date) {
    console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}

greet("Maddison", new Date());
```

**compile**

```
tsc test.ts
```

**test.js**

```js
function greet(person, date) {
    console.log("Hello ".concat(person, ", today is ").concat(date.toDateString(), "!"));
}
greet("Maddison", new Date());
```

### Strictness

#### `noImplicitAny`

Recall that in some places, TypeScript doesn’t try to infer types for us and instead falls back to the most lenient type: `any`. This isn’t the worst thing that can happen - after all, falling back to `any` is just the plain JavaScript experience anyway.

However, using `any` often defeats the purpose of using TypeScript in the first place. The more typed your program is, the more validation and tooling you’ll get, meaning you’ll run into fewer bugs as you code. Turning on the [`noImplicitAny`](https://www.typescriptlang.org/tsconfig#noImplicitAny) flag will issue an error on any variables whose type is implicitly inferred as `any`.

#### `strictNullChecks`

By default, values like `null` and `undefined` are assignable to any other type. This can make writing some code easier, but forgetting to handle `null` and `undefined` is the cause of countless bugs in the world - some consider it a [billion dollar mistake](https://www.youtube.com/watch?v=ybrQvs4x0Ps)! The [`strictNullChecks`](https://www.typescriptlang.org/tsconfig#strictNullChecks) flag makes handling `null` and `undefined` more explicit, and *spares* us from worrying about whether we *forgot* to handle `null` and `undefined`.

## Types

### Common types in ts

The primitives: `string`, `number`, and `boolean`

Arrays: Array<number> number[]

any: for skipping type-check(use `noImplicitAny` to avoid this)

### Type Annotations

Explicit type:

```ts
let myName: string = "Alice";
```

Implicit type:

```ts
// No type annotation needed -- 'myName' inferred as type 'string'
let myName = "Alice";
```

### Functions

#### Parameter Type Annotations

```ts
// Parameter type annotation
function greet(name: string) {
  console.log("Hello, " + name.toUpperCase() + "!!");
}
```

The arguments will be checked

```ts
// Would be a runtime error if executed!
greet(42);
```

*Argument of type 'number' is not assignable to parameter of type 'string'.*

#### Return Type Annotations

You usually don’t need a return type annotation because TypeScript will infer the function’s return type based on its `return` statements.

```ts
function getFavoriteNumber(): number {
  return 26;
}
```

#### Functions Which Return Promises

```ts
async function getFavoriteNumber(): Promise<number> {
  return 26;
}
```

#### Anonymous Functions

Even though the parameter `s` didn’t have a type annotation, TypeScript used the types of the `forEach` function, along with the inferred type of the array, to determine the type `s` will have.

Similar to the inference rules, you don’t need to explicitly learn how this happens.

```ts
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

### Object Types

```ts
// The parameter's type annotation is an object type
function printCoord(pt: { x: number, y: number, z?: number}) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 3, y: 7 });
```

+ z is optional

+ `pt: { x: number; y: number; z?: number}` and `pt: { x: number, y: number, z?: number}` are equivalent.

### Union Types

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

*Argument of type '{ myID: number; }' is not assignable to parameter of type 'string | number'.*

```ts
function printId(id: number | string) {
  console.log(id.toUpperCase());
}
```

*Property 'toUpperCase' does not exist on type 'string | number'.*
*Property 'toUpperCase' does not exist on type 'number'.*

solution:

add a if statement to check the type of `id`

```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    // In this branch, id is of type 'string'
    console.log(id.toUpperCase());
  } else {
    // Here, id is of type 'number'
    console.log(id);
  }
}
```

### Type Aliases

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

### Interfaces

```ts
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

### Differences Between Type Aliases and Interfaces

#### Extending

**interface**

```ts
interface Animal {
  name: string;
}

interface Bear extends Animal {
  honey: boolean;
}

const bear = getBear();
bear.name;
bear.honey;
```

**type**

```ts
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

#### Adding new fields

**interface**

```ts
interface Window {
  title: string;
}

interface Window {
  ts: TypeScriptAPI;
}

const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});
```

**type**

**A type cannot be changed after being created**

### Type Assertions

TypeScript only allows type assertions which convert to a *more specific* or *less specific* version of a type. This rule prevents “impossible” coercions like:

```ts
const x = "hello" as number;
```

*Conversion of type 'string' to type 'number' may be a mistake because neither type sufficiently overlaps with the other. If this was intentional, convert the expression to 'unknown' first.Conversion of type 'string' to type 'number' may be a mistake because neither type sufficiently overlaps with the other. If this was intentional, convert the expression to 'unknown' first.*

Sometimes this rule can be too conservative and will disallow more complex coercions that might be valid. If this happens, you can use two assertions, first to `any` (or `unknown`, which we’ll introduce later), then to the desired type:

```ts
const a = expr as any as T;
```

### Literal Types

```ts
const x = "hello"
```

is equivalent to

```ts
let x: "hello" = "hello";
// OK
x = "hello";
// ...
x = "howdy";
```

*Type '"howdy"' is not assignable to type '"hello"'.*

By combining literal types and union types:

```ts
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");
printText("G'day, mate", "centre"); // typo
```

*Argument of type '"centre"' is not assignable to parameter of type '"left" | "right" | "center"'.*

```ts
interface Options {
  width: number;
}
function configure(x: Options | "auto") {
  // ...
}
configure({ width: 100 });
configure("auto");
configure("automatic");
```

*Argument of type '"automatic"' is not assignable to parameter of type 'Options | "auto"'.*

```ts
declare function handleRequest(url: string, method: "GET" | "POST"): void;
 
const req = { url: "https://example.com", method: "GET" };
handleRequest(req.url, req.method);
```

*Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.*

In the above example `req.method` is inferred to be `string`, not `"GET"`. Because code can be evaluated between the creation of `req` and the call of `handleRequest` which could assign a new string like `"GUESS"` to `req.method`, TypeScript considers this code to have an error.

```ts
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method);
```

The `as const` suffix acts like `const` but for the type system, ensuring that all properties are assigned the literal type instead of a more general version like `string` or `number`.

### null/undefined

#### `strictNullChecks` on

1. With [`strictNullChecks`](https://www.typescriptlang.org/tsconfig#strictNullChecks) *on*, when a value is `null` or `undefined`, you will need to test for those values before using methods or properties on that value.

   ```ts
   function doSomething(x: string | null) {
     if (x === null) {
       // do nothing
     } else {
       console.log("Hello, " + x.toUpperCase());
     }
   }
   ```

2. Non-null Assertion Operator (Postfix `!`): TypeScript also has a special syntax for removing `null` and `undefined` from a type without doing any explicit checking. Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`

   ```ts
   function liveDangerously(x?: number | null) {
     // No error
     console.log(x!.toFixed());
   }
   ```

## Narrowing

### typeof narrowing

```ts
function padLeft(padding: number | string, input: string): string {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
  }
  return padding + input;
}
```

### Truthiness narrowing

```ts
function getUsersOnlineMessage(numUsersOnline: number) {
  if (numUsersOnline) {
    return `There are ${numUsersOnline} online now!`;
  }
  return "Nobody's here. :(";
}
```

In JavaScript, constructs like `if` first “coerce” their conditions to `boolean`s to make sense of them, and then choose their branches depending on whether the result is `true` or `false`. Values like

- `0`
- `NaN`
- `""` (the empty string)
- `0n` (the `bigint` version of zero)
- `null`
- `undefined`

### Equality narrowing

```ts
function example(x: string | number, y: string | boolean) {
  if (x === y) {
    // We can now call any 'string' method on 'x' or 'y'.
    x.toUpperCase();
    y.toLowerCase(); 
  } else {
    console.log(x);       
    console.log(y);
  }
}
```

### The `in` operator narrowing

```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };
type Human = { swim?: () => void; fly?: () => void };
 
function move(animal: Fish | Bird | Human) {
  if ("swim" in animal) {
    animal;     
// (parameter) animal: Fish | Human
  } else {
    animal;      
// (parameter) animal: Bird | Human
  }
```

### `instanceof` narrowing

```ts
function logValue(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString());           
// (parameter) x: Date
  } else {
    console.log(x.toUpperCase());              
// (parameter) x: string
  }
}
```

#### Assignments

```ts
let x = Math.random() < 0.5 ? 10 : "hello world!";
// let x: string | number
x = 1;
console.log(x);         
// let x: number
x = "goodbye!";
console.log(x);         
//let x: string

// Error
x = true;
```

*Type 'boolean' is not assignable to type 'string | number'.*

### Control flow analysis

Control flow will narrow down the type

```ts
function example() {
  let x: string | number | boolean;
  x = Math.random() < 0.5;
  console.log(x);         
// let x: boolean
  if (Math.random() < 0.5) {
    x = "hello";
    console.log(x);           
// let x: string
  } else {
    x = 100;
    console.log(x);        
// let x: number
  }
  return x;      
// let x: string | number
}
```

### Never Type

When narrowing, you can reduce the options of a union to a point where you have removed all possibilities and have nothing left. In those cases, TypeScript will use a `never` type to represent a state which shouldn’t exist.

## Functions

### Function Type Expressions

```ts
function greeter(fn: (a: string) => void) {
  fn("Hello, World");
}
 
function printToConsole(s: string) {
  console.log(s);
}
 
greeter(printToConsole);
```

or like this

```ts
type GreetFunction = (a: string) => void;
function greeter(fn: GreetFunction) {
  // ...
}
```

### Call Signatures

If we want to describe something callable with properties, we can write a *call signature* in an object type:

```ts
type DescribableFunction = {
  description: string;
  (someArg: number): boolean; // function signature
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}
 
function myFunc(someArg: number) {
  return someArg > 3;
}
myFunc.description = "default description";
 
doSomething(myFunc);
```

This code defines a type alias called `DescribableFunction`, which describes a function type with specific properties: `description` as a string and a **function signature** that accepts a `number` argument and returns a `boolean`.

Then, a function named `doSomething` is defined. It takes a parameter `fn` of type `DescribableFunction`. Inside `doSomething`, it prints the `fn.description` string, then calls `fn(6)` and prints its return value.

Next, a function named `myFunc` is defined. It accepts a `number` argument and returns a `boolean`. This function also has a `description` property with a value of `"default description"`.

Finally, `doSomething(myFunc)` is called, passing `myFunc` as an argument. Since `myFunc` conforms to the `DescribableFunction` type, it can be passed as an argument to `doSomething`. Inside `doSomething`, it prints the value of `myFunc.description`, then calls `myFunc(6)` and prints its return value.

### Construct Signatures

JavaScript functions can also be invoked with the `new` operator. TypeScript refers to these as *constructors* because they usually create a new object. You can write a *construct signature* by adding the `new` keyword in front of a call signature

```ts
type SomeConstructor = {
  new (s: string): SomeObject;
};
function fn(ctor: SomeConstructor) {
  return new ctor("hello");
}


interface CallOrConstruct {
  (n?: number): string;
  new (s: string): Date;
}
```

### Generic Functions

Code below

```ts
function firstElement(arr: any[]) {
  return arr[0];
}
```

can be implemented as

```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}
```

with the use of `generic (<Type>)`  to avoid the use of `any`

so to test the function above:

```ts
function firstElement<Type>(arr: Type[]): Type | undefined {
  return arr[0];
}

// s is of type 'string'
const s = firstElement(["a", "b", "c"]);
// n is of type 'number'
const n = firstElement([1, 2, 3]);
// u is of type undefined
const u = firstElement([]);
```

#### 2 types generic

```ts
function map<Input, Output>(arr: Input[], func: (arg: Input) => Output): Output[] {
    return arr.map(func);
}

// Parameter 'n' is of type 'string'
// 'parsed' is of type 'number[]'
const parsed = map(["1", "2", "3"], (n) => parseInt(n));
```

#### Constraints

We need a function that returns the longer of two values. To do this, we need a `length` property that’s a number. We *constrain* the type parameter to that type by writing an `extends` clause

```ts
function longest<Type extends { length: number }>(a: Type, b: Type) {
  if (a.length >= b.length) {
    return a;
  } else {
    return b;
  }
}
 
// longerArray is of type 'number[]'
const longerArray = longest([1, 2], [1, 2, 3]);
// longerString is of type 'alice' | 'bob'
const longerString = longest("alice", "bob");
// Error! Numbers don't have a 'length' property
const notOK = longest(10, 100);
```

*Argument of type 'number' is not assignable to parameter of type '{ length: number; }'.*

#### Good Generic Function

**Rule1**: When possible, use the type parameter itself rather than constraining it

```ts
function firstElement1<Type>(arr: Type[]) {
  return arr[0];
}
 
function firstElement2<Type extends any[]>(arr: Type) {
  return arr[0];
}
 
// a: number (good)
const a = firstElement1([1, 2, 3]);
// b: any (bad)
const b = firstElement2([1, 2, 3]);
```

**Rule2**: Always use as few type parameters as possible

```ts
function filter1<Type>(arr: Type[], func: (arg: Type) => boolean): Type[] {
  return arr.filter(func);
}
 
function filter2<Type, Func extends (arg: Type) => boolean>(
  arr: Type[],
  func: Func
): Type[] {
  return arr.filter(func);
}
```

**Rule3**: If a type parameter only appears in one location, strongly reconsider if you actually need it

Sometimes we forget that a function might not need to be generic:

```ts
function greet<Str extends string>(s: Str) {
  console.log("Hello, " + s);
}
 
greet("world");Try
```

We could just as easily have written a simpler version:

```ts
function greet(s: string) {
  console.log("Hello, " + s);
}Try
```

### Optional Parameters

use `?`

```ts
function f(x?: number) {
  // ...
}
f(); // OK
f(10); // OK
```

use default value

```ts
function f(x = 10) {
  // ...
}

// All OK
f();
f(10);
f(undefined);
```

**Rule4**: When writing a function type for a callback, *never* write an optional parameter unless you intend to *call* the function without passing that argument

### Function Overloads

```ts
// overload signature
function makeDate(timestamp: number): Date;
function makeDate(m: number, d: number, y: number): Date;
// implementation signature
function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
  if (d !== undefined && y !== undefined) {
    return new Date(y, mOrTimestamp, d);
  } else {
    return new Date(mOrTimestamp);
  }
}
const d1 = makeDate(12345678);
const d2 = makeDate(5, 5, 5);

// Error
const d3 = makeDate(1, 3);
```

*No overload expects 2 arguments, but overloads do exist that expect either 1 or 3 arguments.*

In this example, we wrote two overloads: one accepting one argument, and another accepting three arguments. These first two signatures are called the *overload signatures*.

Then, we wrote a function implementation with a compatible signature. Functions have an *implementation* signature, but this signature can’t be called directly. Even though we wrote a function with two optional parameters after the required one, it can’t be called with two parameters!

#### Good Overloads Function

**Rule1**: Always prefer parameters with union types instead of overloads when possible

```ts
function len(s: string): number;
function len(arr: any[]): number;
function len(x: any) {
  return x.length;
}

len(""); // OK
len([0]); // OK
len(Math.random() > 0.5 ? "hello" : [0]);
/**
No overload matches this call.
  Overload 1 of 2, '(s: string): number', gave the following error.
    Argument of type 'number[] | "hello"' is not assignable to parameter of type 'string'.
      Type 'number[]' is not assignable to type 'string'.
  Overload 2 of 2, '(arr: any[]): number', gave the following error.
    Argument of type 'number[] | "hello"' is not assignable to parameter of type 'any[]'.
      Type 'string' is not assignable to type 'any[]'.
*/
```

so the implementation signature should be

```ts
function len(x: any[] | string) {
  return x.length;
}
```

### Rest Parameters and Arguments

```ts
function multiply(n: number, ...m: number[]) {
  return m.map((x) => n * x);
}
// 'a' gets value [10, 20, 30, 40]
const a = multiply(10, 1, 2, 3, 4);
```

### Parameter Destructuring

```ts
function sum({ a, b, c }: { a: number; b: number; c: number }) {
  console.log(a + b + c);
}
```

or

```ts
type ABC = { a: number; b: number; c: number };
function sum({ a, b, c }: ABC) {
  console.log(a + b + c);
}
```

## Objects

### Optional Properties

To handle `undefined` situation, we can use `xPos=0 yPos=0` to destruct props

```ts
interface PaintOptions {
  shape: Shape;
  xPos?: number;
  yPos?: number;
}
 
function paintShape({ shape, xPos = 0, yPos = 0 }: PaintOptions) {
  console.log("x coordinate at", xPos);
  console.log("y coordinate at", yPos);
}
 
const shape = getShape();
paintShape({ shape });
paintShape({ shape, xPos: 100 });
paintShape({ shape, yPos: 100 });
paintShape({ shape, xPos: 100, yPos: 100 });
```

### readonly

```ts
interface SomeType {
  readonly prop: string;
}
```

Using the `readonly` modifier doesn’t necessarily imply that a value is totally immutable - or in other words, that its internal contents can’t be changed. It just means the property itself can’t be re-written to.

```ts
interface Home {
  readonly resident: { name: string; age: number };
}
 
function visitForBirthday(home: Home) {
  // We can read and update properties from 'home.resident'.
  console.log(`Happy birthday ${home.resident.name}!`);
  home.resident.age++;
}
 
function evict(home: Home) {
  // But we can't write to the 'resident' property itself on a 'Home'.
  home.resident = {
    name: "Victor the Evictor",
    age: 42,
  };
}
```

*Cannot assign to 'resident' because it is a read-only property.*

### Extending Types

```ts
interface BasicAddress {
  name?: string;
  street: string;
  city: string;
  country: string;
  postalCode: string;
}
interface AddressWithUnit {
  name?: string;
  unit: string;
  street: string;
  city: string;
  country: string;
  postalCode: string;
}
```

as

```ts
interface BasicAddress {
  name?: string;
  street: string;
  city: string;
  country: string;
  postalCode: string;
}
 
interface AddressWithUnit extends BasicAddress {
  unit: string;
}
```

```ts
interface Colorful {
  color: string;
}
 
interface Circle {
  radius: number;
}
 
interface ColorfulCircle extends Colorful, Circle {}
 
const cc: ColorfulCircle = {
  color: "red",
  radius: 42,
};
```

### Generic Object Types

```ts
interface Box<Type> {
  contents: Type;
}
let box: Box<string>;
```

## React & TS

A button with props

```tsx
import React, { JSXElementConstructor, useState } from 'react'

interface buttonProps {
    backgroundColor: "red" | "green" | "blue",
    fontSize: number,
    radius: boolean,
    padding: [number, number, number, number]
}

function Button({ backgroundColor = 'blue', fontSize = 5, radius = true, padding = [0, 0, 0, 0] }: buttonProps) {
    const [count, setCount] = useState(0)
    return (
        <button className={`bg-${backgroundColor}-500 text-white ${radius ? "rounded" : "rounded-none"} pt-${padding[0]} pb-${padding[1]} pl-${padding[2]} pr-${padding[3]}`} onClick={() => { setCount(count + 1) }}>
            Clicked {count} times!
        </button>
    )
}

export default Button
```

interface can't do everything

interface can only specify a object

```ts
interface Color {
    color: "red" | "green" | "blue"
}
const color: Color["color"] = "red"
```

while type allies can do this

```ts
type color = "red" | "green" | "blue"
const color: color = "red"
```

So make `type allies` default
