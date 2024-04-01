---
title: JavaScript
date: 2023-02-06 11:28:14
categories:
  - Develop
  - Basic
tags: 
  - Frontend
  - Node
  - Backend
  - Javascript
---

## 1. Use JS in HTML

### 1.1 Use  '<script>'

<script> JS </script>

### 1.2 with external reference(path)

<script src="myScript.js"></script>

### 1.3 with URL

<script src="https://www.w3schools.com/js/myScript.js"></script>

## 2. How to output

- Writing into an HTML element, using `innerHTML`.
- Writing into the HTML output using `document.write()`.
- Writing into an alert box, using `window.alert()`.
- Writing into the browser console, using `console.log()`.

## 3. Key words

| Keyword  | Description                                                  |
| :------- | :----------------------------------------------------------- |
| var      | Declares a variable                                          |
| let      | Declares a block variable                                    |
| const    | Declares a block constant                                    |
| if       | Marks a block of statements to be executed on a condition    |
| switch   | Marks a block of statements to be executed in different cases |
| for      | Marks a block of statements to be executed in a loop         |
| function | Declares a function                                          |
| return   | Exits a function                                             |
| try      | Implements error handling to a block of statements           |

### 3.1  When to Use var, let, or const?

1. Always declare variables

2. Always use `const` if the value should not be changed

3. Always use `const` if the type should not be changed (Arrays and Objects)

4. Only use `let` if you can't use `const`

5. Only use `var` if you MUST support old browsers.

Note: A variable declared with `let` or `const` cannot  be re-declared.

### 3.2 Let

- Variables declared with `let` have **Block Scope**

  ```js
  Variables declared inside a { } block cannot be accessed from outside the block:
  
  {
   let x = 2;
  }
  // x can NOT be used here
  ```

- Variables declared with `let` must be **Declared** before use

- Variables declared with `let` cannot be **Redeclared** in the same scope

### 3.3  Const

#### How to use

`const` variables must be assigned a value when they are declared

Correct

```js
const PI = 3.14159265359;
```

Incorrect

```js
const PI;
PI = 3.14159265359;
```



#### When to use JavaScript const?

**Always declare a variable with `const` when you know that the value should not be changed.**

Use `const` when you declare:

- A new Array
- A new Object
- A new Function
- A new RegExp



#### Constant Objects and Arrays

The keyword `const` is a little misleading.

It does not define a constant value. It defines a constant reference to a value.

Because of this you can NOT:

- Reassign a constant value
- Reassign a constant array
- Reassign a constant object

- But you CAN:

- Change the elements of constant array
- Change the properties of constant object

Correct

```js
// You can create a constant array:
const cars = ["Saab", "Volvo", "BMW"];

// You can change an element:
cars[0] = "Toyota";

// You can add an element:
cars.push("Audi");
```

```js
// You can create a const object:
const car = {type:"Fiat", model:"500", color:"white"};

// You can change a property:
car.color = "red";

// You can add a property:
car.owner = "Johnson";
```

Incorrect

```js
// You can create a constant array:
const cars = ["Saab", "Volvo", "BMW"];

// You can change an element:
cars[0] = "Toyota";

// You can add an element:
cars.push("Audi");
```

## 4. Operators

### 4.1 Arithmetic Operators

| Operator | Description                  |
| :------- | :--------------------------- |
| +        | Addition                     |
| -        | Subtraction                  |
| *        | Multiplication               |
| **       | Exponentiation               |
| /        | Division                     |
| %        | Modulus (Division Remainder) |
| ++       | Increment                    |
| --       | Decrement                    |

### 4.2 Assignment Operators

| Operator | Example | Same As    |
| :------- | :------ | :--------- |
| =        | x = y   | x = y      |
| +=       | x += y  | x = x + y  |
| -=       | x -= y  | x = x - y  |
| *=       | x *= y  | x = x * y  |
| /=       | x /= y  | x = x / y  |
| %=       | x %= y  | x = x % y  |
| **=      | x **= y | x = x ** y |

### 4.3 Comparison Operators

| Operator | Description                       |
| :------- | :-------------------------------- |
| ==       | equal to                          |
| ===      | equal value and equal type        |
| !=       | not equal                         |
| !==      | not equal value or not equal type |
| >        | greater than                      |
| <        | less than                         |
| >=       | greater than or equal to          |
| <=       | less than or equal to             |
| ?        | ternary operator                  |

### 4.4 Logical Operators

| Operator | Description |
| :------- | :---------- |
| &&       | logical and |
| \|\|     | logical or  |
| !        | logical not |

### 4.5 Type Operators

| Operator   | Description                                                |
| :--------- | :--------------------------------------------------------- |
| typeof     | Returns the type of a variable                             |
| instanceof | Returns true if an object is an instance of an object type |

## 5.  Data Types

### JavaScript has 8 Datatypes

1. String
2. Number
3. Bigint
4. Boolean
5. Undefined
6. Null
7. Symbol
8. Object

### The Object Datatype

The object data type can contain:

1. An object  ( `dict` in Python)
2. An array
3. A date

## 6. Functions

```js
function name(parameter1, parameter2, parameter3) {
  // code to be executed
}

let result = name(p1, p2, p3);
```

## 7. Object

### 7.1 Create an object

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
};
```

### 7.2 Accessing Object Properties

```js
person.lastName;

person["lastName"];
```

### 7.3 Object Methods

```js
const person = {
  firstName: "John",
  lastName : "Doe",
  id       : 5566,
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
};

name = person.fullName();
//name = person.fullName; !! it will return the function definition NOT the return value
```

## 8. Events

### HTML Events

```html
<element event='some JavaScript'>
```

| Event       | Description                                        |
| :---------- | :------------------------------------------------- |
| onchange    | An HTML element has been changed                   |
| onclick     | The user clicks an HTML element                    |
| onmouseover | The user moves the mouse over an HTML element      |
| onmouseout  | The user moves the mouse away from an HTML element |
| onkeydown   | The user pushes a keyboard key                     |
| onload      | The browser has finished loading the page          |

```html
<button onclick="document.getElementById('demo').innerHTML = Date()">The time is?</button>

<button onclick="this.innerHTML = Date()">The time is?</button>

<button onclick="displayDate()">The time is?</button>
```

```html
<!DOCTYPE html>
<html>
<body>
<h1>JavaScript HTML Events</h1>
<h2>The onclick Attribute</h2>

<button onclick="document.getElementById('demo').innerHTML=Date()">The time is?</button>

<p id="demo"></p>

</body>
</html>
```

## 9. Strings

### 9.1 escape sequences

| Code | Result               |
| :--- | :------------------- |
| \b   | Backspace            |
| \f   | Form Feed            |
| \n   | New Line             |
| \r   | Carriage Return      |
| \t   | Horizontal Tabulator |
| \v   | Vertical Tabulator   |

### 9.2 [Methods](https://www.w3schools.com/js/js_string_methods.asp)

```
String length
String charAt()
String charCodeAt()
String at()
String [ ]
String slice()
String substring()
String substr()
See Also:
String toUpperCase()
String toLowerCase()
String concat()
String trim()
String trimStart()
String trimEnd()
String padStart()
String padEnd()
String repeat()
String replace()
String replaceAll()
String split()
```

#### 9.2.1 length

```js
let text = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
let length = text.length;
```

#### 9.2.2 Extracting String Characters

##### charAt()

```js
let text = "HELLO WORLD";
let char = text.charAt(0); //returns H
```

##### charCodeAt()

```js
let text = "HELLO WORLD";
let char = text.charCodeAt(0); //returns 72
```

##### at()

The `at()` method is a new addition to JavaScript.

It allows the use of negative indexes while `charAt()` do not.

```js
const name = "W3Schools";
let letter = name.at(2);
```

**Now you can use `myString.at(-2)` instead of `charAt(myString.length-2)`.**(Python list)

##### Property Access [ ]

Property access might be a little **unpredictable:**

- It makes strings look like arrays (but they are not)
- If no character is found, [ ] returns undefined, while charAt() returns an empty string.
- It is read only. str[0] = "A" gives no error (but does not work!)

```js
const name = "W3Schools";
let letter = name[2];
```

```js
let text = "HELLO WORLD";
text[0] = "A";    // Gives no error, but does not work

text.at(0) = "A"  // Gives error

text.charAt(0) = "A" // Gives error
```

#### 9.2.3 Extracting String Parts

There are 3 methods for extracting a part of a string:

- `slice(start, end)`
- `substring(start, end)`
- `substr(start, length)`

##### slice

[start, end)  (it's left-closed right-opened)

```js
//Slice out a portion of a string from position 7 to position 13:
let text = "Apple, Banana, Kiwi";
let part = text.slice(7, 13);  //Banana

//If you omit the second parameter, the method will slice out the rest of the string:
let text = "Apple, Banana, Kiwi";
let part = text.slice(7);

//If a parameter is negative, the position is counted from the end of the string:
let text = "Apple, Banana, Kiwi";
let part = text.slice(-12);   //Banana, Kiwi

//This example slices out a portion of a string from position -12 to position -6:
let text = "Apple, Banana, Kiwi";
let part = text.slice(-12, -6);
```

##### substring

`substring()` is similar to `slice()`.

The difference is that start and end values less than 0 are treated as 0 in `substring()`.

```JS
let str = "Apple, Banana, Kiwi";
let part = str.substring(7, 13);
```

##### substr

`substr()` is similar to `slice()`.

The difference is that the second parameter specifies the **length** of the extracted part.

```JS
let str = "Apple, Banana, Kiwi";
let part = str.substr(7, 6);

//If you omit the second parameter, substr() will slice out the rest of the string.
let str = "Apple, Banana, Kiwi";
let part = str.substr(7);

//If the first parameter is negative, the position counts from the end of the string.
let str = "Apple, Banana, Kiwi";
```

#### 9.2.4 concat

`concat()` joins two or more strings

```JS
text = "Hello" + " " + "World!";
text = "Hello".concat(" ", "World!");
```

#### 9.2.5 trim

The `trim()` method removes whitespace from both sides of a string

```js
let text1 = "      Hello World!      ";
let text2 = text1.trim();
```

##### trimStart

The `trimStart()` method works like `trim()`, but removes whitespace only from the start of a string

```js
let text1 = "     Hello World!     ";
let text2 = text1.trimStart();
```

##### trimEnd

The `trimEnd()` method works like `trim()`, but removes whitespace only from the end of a string

```js
let text1 = "     Hello World!     ";
let text2 = text1.trimEnd();
```

### 9.3 [String Search](https://www.w3schools.com/js/js_string_search.asp)

```
String indexOf()
String lastIndexOf()
String search()
See Also:
Basic String Methods
String Templates
String match()
String matchAll()
String includes()
String startsWith()
String endsWith()
```

#### indexOf

The `indexOf()` method returns the **index** (position) of the **first** occurrence of a string in a string, or it returns -1 if the string is not found

```js
let text = "Please locate where 'locate' occurs!";
let index = text.indexOf("locate");            //7
```

#### lastIndexOf

```js
let text = "Please locate where 'locate' occurs!";
let index = text.lastIndexOf("locate");        //21
```

+ Both `indexOf()`, and `lastIndexOf()` return -1 if the text is not found
+ Both methods accept a second parameter as the starting position for the search

#### search

The `search()` method searches a string for a string (or a regular expression) and returns the position of the match

```js
let text = "Please locate where 'locate' occurs!";
text.search("locate");					//7
text.search(/locate/);					//7
```

- The `search()` method cannot take a second start position argument.
- The `indexOf()` method cannot take powerful search values (regular expressions).

### 9.4 Template Strings

```js
let text = `Hello World!`;
```

#### Interpolation

```js
let firstName = "John";
let lastName = "Doe";

let text = `Welcome ${firstName}, ${lastName}!`;
```

## 10. Numbers

JavaScript strings can have numeric content

```js
{
    let x = 100;         // x is a number
	let y = "100";       // y is a string
	var z =  (x == y);   // z is true
	var z =  (x === y);  // z is false
}
{
    let x = "100";
    let y = "10";
    let z = x / y;       // this will work
}
{
    let x = "100";
	let y = "10";
	let z = x - y;		// this will work
}
{
    let x = "100";
	let y = "10";
	let z = x + y;		// this will NOT work
}
```

#### NaN - Not a Number

`NaN` is a JavaScript reserved word indicating that a number is not a legal number.

Trying to do arithmetic with a non-numeric string will result in `NaN` (Not a Number)

```js
let x = 100 / "Apple";
isNaN(x);
```

#### Infinity

`Infinity` (or `-Infinity`) is the value JavaScript will return if you calculate a number outside the largest possible number.

```js
let x =  2 / 0;
let y = -2 / 0;
```

### 10.1 Methods

| Method          | Description                                        |
| :-------------- | :------------------------------------------------- |
| toString()      | Returns a number as a string                       |
| toExponential() | Returns a number written in exponential notation   |
| toFixed()       | Returns a number written with a number of decimals |
| toPrecision()   | Returns a number written with a specified length   |
| ValueOf()       | Returns a number as a number                       |

**Converting Variables to Numbers**

| Method       | Description                                             |
| :----------- | :------------------------------------------------------ |
| Number()     | Returns a number converted from its argument.           |
| parseFloat() | Parses its argument and returns a floating point number |
| parseInt()   | Parses its argument and returns a whole number          |

### 10.2 Number Properties

| Property          | Description                                           |
| :---------------- | :---------------------------------------------------- |
| EPSILON           | The difference between 1 and the smallest number > 1. |
| MAX_VALUE         | The largest number possible in JavaScript             |
| MIN_VALUE         | The smallest number possible in JavaScript            |
| MAX_SAFE_INTEGER  | The maximum safe integer (253 - 1)                    |
| MIN_SAFE_INTEGER  | The minimum safe integer -(253 - 1)                   |
| POSITIVE_INFINITY | Infinity (returned on overflow)                       |
| NEGATIVE_INFINITY | Negative infinity (returned on overflow)              |
| NaN               | A "Not-a-Number" value                                |

**Number Properties Cannot be Used on Variables**

Number properties belong to the JavaScript **Number Object**.

These properties can only be accessed as `Number.MAX_VALUE`.

Using x.MAX_VALUE, where x is a variable or a value, will return `undefined`:

## 11. Array

Create Access Chang toString Accessfullstring  Methods

```js
const cars = ["Saab", "Volvo", "BMW"];

cars[0]= "Saab";
cars[1]= "Volvo";
cars[2]= "BMW";

cars[0] = "Opel";

const fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo").innerHTML = fruits.toString(); //Banana,Orange,Apple,Mango

const cars = ["Saab", "Volvo", "BMW"];
document.getElementById("demo").innerHTML = cars; //Saab,Volvo,BMW

cars.length   // Returns the number of elements
cars.sort()   // Sorts the array

const fruits = ["Banana", "Orange", "Apple", "Mango"];
let fLen = fruits.length;
```

 looping

```js
let text = "<ul>";
for (let i = 0; i < fLen; i++) {
  text += "<li>" + fruits[i] + "</li>";
}
text += "</ul>";
const fruits = ["Banana", "Orange", "Apple", "Mango"];

let text = "<ul>";
fruits.forEach(myFunction);
text += "</ul>";
function myFunction(value) {
  text += "<li>" + value + "</li>";
}
```

 Adding (push)

```js
const fruits = ["Banana", "Orange", "Apple"];
fruits.push("Lemon");  // Adds a new element (Lemon) to fruits
```

**WARNING !**

Adding elements with high indexes can create undefined "holes" in an array

### Methods

```
Basic Array Methods
Array length
Array toString()
Array at()
Array join()
Array pop()
Array push()
See Also:
Search Methods
Sort Methods
Iteration Methods
Array shift()
Array unshift()
Array delete()
Array concat()
Array copyWithin()
Array flat()
Array splice()
Array toSpliced()
Array slice()
```

### Array Search

```
Array indexOf()
Array lastIndexOf()
Array includes()
See Also:
Basic Methods
Sort Methods
Iteration Methods	Array find()
Array findIndex()
Array findLast()
Array findLastIndex()
```

*array*.indexOf(*item*, *start*)

| *item*  | Required. The item to search for.                            |
| ------- | ------------------------------------------------------------ |
| *start* | Optional. Where to start the search. Negative values will start at the given position counting from the end, and search to the end. |

`Array.indexOf()` returns -1 if the item is not found.

If the item is present more than once, it returns the position of the **first occurrence**.

*array*.lastIndexOf(*item*, *start*)

| *item*  | Required. The item to search for                             |
| ------- | ------------------------------------------------------------ |
| *start* | Optional. Where to start the search. Negative values will start at the given position counting from the end, and search to the beginning |

includes

 `Array.includes()` to arrays. This allows us to **check** if an element is present in an array (including NaN, unlike indexOf).

### Sorting Arrays

```
Alpabetic Sort
Array sort()
Array reverse()
Array toSorted()
Array toReversed()

Numeric Sort
Random Sort
Math.min()
Math.max()
Home made Min()
Home made Max()
```

The `sort()` method sorts an array alphabetically

 `toSorted()` method is a safe way to sort an array **without altering the original array**.

The difference between `toSorted()` and `sort()` is that the first method creates a new array, keeping the original array unchanged, while the last method alters the original array.

By default, the `sort()` function sorts values as **strings**.

If numbers are sorted as strings, "25" is bigger than "100", because "2" is bigger than "1".

Because of this, the `sort()` method will produce incorrect result when sorting numbers.

Provide a **compare function** to sort numbers:

```js
const points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return a - b});
```

Sorting an Array in Random Order:

```js
const points = [40, 100, 1, 5, 25, 10];
points.sort(function(){return 0.5 - Math.random()});
```

### Max/Min value of array

#### Using Math.min() on an Array

```js
function myArrayMin(arr) {
  return Math.min.apply(null, arr);
}
```

#### Using Math.max() on an Array 

```js
function myArrayMax(arr) {
  return Math.max.apply(null, arr);
}
```

### Iteration

```
Array forEach
Array map()
Array flatMap()
Array filter()
Array reduce()
Array reduceRigth()
See Also:
Basic Array Methods
Array Search Methods
Array Sort Methods	Array every()
Array some()
Array from()
Array keys()
Array entries()
Array with()
Array Spread (...)
```

#### map

The `map()` method **creates a new array** by performing a function on each array element.

The `map()` method does not execute the function for array elements without values.

The `map()` method does not change the original array.

```js
const numbers1 = [45, 4, 9, 16, 25];
const numbers2 = numbers1.map(myFunction);

function myFunction(value, index, array) {
  return value * 2;
}
/*or function myFunction(value) {
  return value * 2;
}*/
```

### filter

The `filter()` method creates a new array with array elements that pass a test.

```js
const numbers = [45, 4, 9, 16, 25];
const over18 = numbers.filter(myFunction);

function myFunction(value, index, array) {
  return value > 18;
}

/*or function myFunction(value) {
  return value > 18;
}*/
```

#### reduce

The `reduce()` method runs a function on each array element to produce (reduce it to) a single value.

The `reduce()` method works from left-to-right in the array. See also `reduceRight()`.

The `reduce()` method does not reduce the original array.

```js
const numbers = [45, 4, 9, 16, 25];
let sum = numbers.reduce(myFunction);

function myFunction(total, value, index, array) {
  return total + value;
}
/*or function myFunction(total, value) {
  return total + value;
}*/
```

## 12. if else switch statement

- Use `if` to specify a block of code to be executed, if a specified condition is true
- Use `else` to specify a block of code to be executed, if the same condition is false
- Use `else if` to specify a new condition to test, if the first condition is false
- Use `switch` to specify many alternative blocks of code to be executed
- Same as C  Java Cpp

Switch

```js
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

Same as C

## 13. Loop

- `for` - loops through a block of code a number of times
- `for/in` - loops through the properties of an object
- `for/of` - loops through the values of an iterable object
- `while` - loops through a block of code while a specified condition is true
- `do/while` - also loops through a block of code while a specified condition is true

### For loop (like C)

```js
for (expression 1; expression 2; expression 3) {
  // code block to be executed
}

for (let i = 0; i < 5; i++) {
  text += "The number is " + i + "<br>";
}
```

### For in (like Python)

```js
for (key in object) {
  // code block to be executed
}

const person = {fname:"John", lname:"Doe", age:25};
let text = "";
for (let x in person) {
  text += person[x];
}
```

```js
for (variable in array) {
  code
}

const numbers = [45, 4, 9, 16, 25];
let txt = "";
for (let x in numbers) {
  txt += numbers[x];
}
```

### Array.forEach()

The `forEach()` method calls a function (a callback function) once for each array element.

```js
const numbers = [45, 4, 9, 16, 25];

let txt = "";
numbers.forEach(myFunction);

function myFunction(value, index, array) {
  txt += value;
}
```

### For of

The JavaScript `for of` statement loops through the values of an iterable object.

It lets you loop over iterable data structures such as Arrays, Strings, Maps, NodeLists, and more:

```js
for (variable of iterable) {
  // code block to be executed
}

const cars = ["BMW", "Volvo", "Mini"];
let text = "";
for (let x of cars) {
  text += x;
}

let language = "JavaScript";
let text = "";
for (let x of language) {
text += x;
}
```

### While loop

```js
while (condition) {
  // code block to be executed
}
```

```js
do {
  // code block to be executed
}
while (condition);
```

## 14.  HTML DOM

- JavaScript can change all the HTML elements in the page
- JavaScript can change all the HTML attributes in the page
- JavaScript can change all the CSS styles in the page
- JavaScript can remove existing HTML elements and attributes
- JavaScript can add new HTML elements and attributes
- JavaScript can react to all existing HTML events in the page
- JavaScript can create new HTML events in the page

