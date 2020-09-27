# JavaScript-learning-notes
## Basics
### Numbers and Strings
#### Converting Data Types
```
const b = '5';
const a = 3;
console.log(a + b); // 35
console.log(a + parseInt(b)); // 8, the + operator supports strings (for string concatenation)
console.log(a + +b); // 8, the + operator in front of b converts it to number

console.log(a * b); // 15 (number, not string)
console.log(a - b); // -2
console.log(a / b); // 0.6
```
#### Increment and Decrement Operators
a++ and ++a both increase the value of a by 1, but there is a difference in the **return values**. ++a returns the increased/edited value; a++ returns the value **before** it was changed.
```
let a = 3;
const b = a++;
console.log(a); // 4
console.log(b); // 3
```
```
let a = 3;
const b = ++a;
console.log(a); // 4
console.log(b); // 4
```
```
let a = 3;
alert(a++); // alert 3
```
```
let a = 3;
alert(++a); // alert 4
```
#### null, undefined, NaN
six primitive data types in JavaScript: [tutorial link](https://www.javascripttutorial.net/javascript-data-types/#null)

1. undefined: default value of uninitialized variables.
2. null: never a default value; you can set something to null (e.g. to reset/ clear a variable). In JavaScript, the data type of null is an object.
3. NaN: result of invalid calculations. it is not a type. It is of type number.
```
console.log(typeof undefined); // "undefined"
console.log(typeof null); // "object"
console.log(typeof NaN); // "number"
```

