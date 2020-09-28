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
`a++` and `++a` both increase the value of a by 1, but there is a difference in the **return values**. `++a` returns the increased/edited value; `a++` returns the value **before** it was changed.
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
Six primitive data types in JavaScript: [tutorial link](https://www.javascripttutorial.net/javascript-data-types/#null)

1. `undefined`: default value of uninitialized variables.
2. `null`: never a default value; you can set something to null (e.g. to reset/ clear a variable). In JavaScript, the data type of null is an object.
3. `NaN`: result of invalid calculations. it is not a type. It is of type number.
```
console.log(typeof undefined); // "undefined"
console.log(typeof null); // "object"
console.log(typeof NaN); // "number"
```
#### Boolean Operators
`==` and `!=` : check for value (in)equality
`===` and `!==` : check for value AND type (in)equality
#### Operator Precedence
Can refer to this article: [MDN - Operator Precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
>the unique exponentiation operator has right-associativity, whereas other arithmetic operators have left-associativity. It is interesting to note that, the order of evaluation is always left-to-right irregardless of associativity.
```
2 ** 3 ** 2 // result 512, equal to 2 ** (3 ** 2)
```
#### Coercion
Coerce in JavaScript means to interpret the non-boolean value passed to if statement as a boolean. For example,
```
let val = 'Max';
if (val) { 
  // ... do something
}
```
- if `val` is number type
  - 0 yields `false`
  - positive or negative numbers yields `true`
- if `val` is string type
  - empty string yields `false`
  - any other non-empty string yields `true`
- if `val` is objects or arrays (arrays are technically objects in JavaScript)
  - `{}`, `[]` and any other objects or arrays yields `true`
- if `val` is `null`/ `undefined`/ `NaN`
  - yields `false`


