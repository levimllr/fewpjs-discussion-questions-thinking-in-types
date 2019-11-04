# Discussion Questions: Thinking in Types

## Objectives

- Recall the datatypes in JavaScript
- Identify the types of different data
- Identify the types of input and output of functions and operators

## JS Data Types Review Questions

1. What are the basic data types in JavaScript? Fill in the table of types below with descriptions of the types and the operators that work on them.

[JavaScript data types](https://javascript.info/types) include the following 7:

  1. `number`: represents integers, floating point decimals, `Infinity`, `-Infinity`, and `NaN`
  2. `string`: denoted by double and single quotes and backticks
  3. `boolean`: `true` or `false`
  4. `null`: represents nothing, empty, or value unknown. Usually assigned.
  5. `undefined`: represents value not assigned. Usually _not_ assigned.
  6. `symbol`: used to create unique identifiers for objects
  7. `object`: used to store collections of data

All but `object` are considered primitive data types, meaning they aren't objects and thus they have no methods. The `typeof` operator returns the type of the argument.

2. `Object` is the basic data type that we use to build other, more specialized 'types' of data. Name some of the ways that `Object` is used in JavaScript (e.g. what other types are really `Object` underneath).

`object` can be used to create classes in JavaScript, as well as hashes/dictionaries. Arrays are objects!

## Exercise - Thinking in Types

When writing a function, it's often helpful to start by considering the inputs and the output. In particular, knowing the data type of the inputs and the data type of the outputs lets you know what kinds of operations are allowed on those arguments. They also hint at what the 'right' operations to do are.

For the following functions, fill in the table with the types of the inputs and the types of the outputs.

| Function                                         | types of inputs                  | type of output                |
| ------------------------------------------------ | -------------------------------- | ----------------------------- |
| `function addFive(number) { return number + 5}`  | `number`                                 | `number`                              |
| ------------------------------------------------ | -------------------------------- | ----------------------------- |
| `function sum(A, B) { return A + B }`            |  `number`                                | `number`                              |
| ------------------------------------------------ | -------------------------------- | ----------------------------- |
| `function concat(A, B) { return "" + A + B }`    | `string`                                 | `string`                              |
| ------------------------------------------------ | -------------------------------- | ----------------------------- |
| `document.querySelector`                         | `string`                                 | `object`                              |
| ------------------------------------------------ | -------------------------------- | ----------------------------- |
| `window.fetch`                                   | `object`                                 | `object`                              |

### "Shapes" of `Object`s

Many functions operate on `Object` types that need to have particular keys. In such cases, it's useful to name the 'shapes' of `Object` that functions expect. You might say that a 'Person' is an `Object` that has keys 'name' and 'age'. You might write:

```js
// Person: {
//  name: string,
//  age: number,
// }
```

to represent the 'shape' of a Person.

When you have functions like the following, you can use the shorthand to write the type of the input and output.

```js
function getName(person) {
  return person.name;
}

function getAge(person) {
  return person.age;
}

function makePerson(name, age) {
  return {
    name: name,
    age: age
  };
}

function birthday(person) {
  person.age += 1;
  return person;
}

// Point: {
// x: number
// y: number
// name: string
//}

function getDistance(pointA, pointB) {
  return Math.sqrt((pointA.x - pointB.x) ** 2 + (pointA.y - pointB.y) ** 2);
}
```

Fill in the table using the 'shape' shorthand

| Function      | types of inputs | type of output |
| ------------- | --------------- | -------------- |
| `getName`     | { name: string, age: number }  | string |
| `getAge`      | { name: string, age: number }  | number |
| `makePerson`  | string, number  | { name: string, age: number } |
| `birthday`    | { name: string, age: number } | { name: string, age: number } |
| `getDistance` | { x: number, y: number, name: string }  | number |

### Function Signatures

It's often conventional to write the 'signature' of a function to concisely capture the function's name, the names and types of the arguments, and the type of the return value. For the `getDistance` function above, the signature might be written as:

```js
// getDistance(pointA: Point, pointB: Point): number
```

The `:` is used to indicate that the type is 'about' the preciding name. In `pointA: Point`, `pointA` is a `Point`.

Reading this function signature out loud, you would say

> `getDistance` is a function that takes in Points pointA and pointB and returns a number.

For practice, add the function signature to the functions in the table.

| Function      | types of inputs | type of output | function signature |
| ------------- | --------------- | -------------- | ------------------ |
| `getName`     | { name: string, age: number }  | string | getName(person: Person): string |
| `getAge`      | { name: string, age: number }  | number | getAge(person: Person): number |
| `makePerson`  | string, number  | { name: string, age: number } | makePerson(name: string, age: number): Person
| `birthday`    | { name: string, age: number } | { name: string, age: number } | birthday(person: Person): Person
| `getDistance` | { x: number, y: number, name: string }  | number | getDistance(pointA: Point, pointB: Point): number

### Operators as 'Functions'

You can think of many operators as if they were functions. They take in inputs and evaluate to an output.

For the following operators, fill in the types of the inputs and outputs. Following the example, try to write out a function signature, as if the operator was a function.

| Operator   | types of inputs  | type of output | function signature                        |
| ---------- | ---------------  | -------------- | ------------------------------------------|
| \*         | number, number   | number         | multiply(a: number, b: number): number    |
| + (string) | string, string   | string         | add(a: string, b: string): string         |
| + (number) | number, number   | number         | add(a: number, b: number): number         |
| -          | number, number   | number         | subtract(a: number, b: number): number    |
| ^          | number, number   | number         | bitwiseXor(a: number, b: number): number  |
| \*\*       | number, number   | number         | exponential(a: number, b: number): number |
| \|\|       | boolean, boolean | boolean        | or(a: boolean, b: boolean): boolean       |
| &&         | boolean, boolean | boolean        | and(a: boolean, b: boolean): boolean      |

### Functions that take in functions as arguments

Some functions take in functions as arguments ('callback functions'). If those functions will be called with particular types of arguments, it's helpful to specify the type of function that will be passed in.

> Note: you may see the word `void` meaning 'this function does not return anything'

Fill in the rest of the table.

| Function                       | types of inputs                 | type of output | function signature                                         |
| ------------------------------ | ------------------------------- | -------------- | ---------------------------------------------------------- |
| `EventTarget.addEventListener` | string, handler(e: Event): void | void           | addEventListener(type: string, handler: function): void    |
| `window.setTimeout`            | function, number                | number         | window.setTimeout(function: object, delay: number): number |
| `Array.prototype.map`          | object (function)               | object(array)  | Array.prototype.map(function: object): object (array)      |
| `Array.prototype.find`         | object (function)               | various        | Array.prototype.find(function: object): various            |
| `Array.prototype.filter`       | object (function)               | object(array)  | Array.prototype.filter(function: object): object (array)   |
| `Array.prototype.reduce`       | object (function)               | number         |  Array.prototype.filter(function: object): number          |
