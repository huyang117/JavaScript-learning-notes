# JavaScript-learning-notes
## Basics
### Numbers and Strings
##### Converting Data Types
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
##### Increment and Decrement Operators
a++ and ++a both increase the value of a by 1, but there is a difference in the return values. ++a returns the increased/edited value; a++ returns the value before it was changed.
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
