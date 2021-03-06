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
`==` and `!=` : check for value (in)equality<br/>
```
console.log(undefined == null); // true
```
```
console.log('packt' == true); // false
// First, convert the boolean value to number, packt == 1. Next, convert the string value to number. Since the string consists of
// alphabetical characters, it returns NaN, so NaN == 1, which is false
```
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
  - +0, -0 or NaN yields `false`
  - positive or negative numbers yields `true`
- if `val` is string type
  - empty string yields `false`
  - any other non-empty string yields `true` (length >= 1)
- if `val` is objects or arrays (arrays are technically objects in JavaScript)
  - `{}`, `[]` and any other objects or arrays yields `true`
- if `val` is `null`/ `undefined`
  - yields `false`

```
function testTruthy(val) {
  return val ? console.log('true') : console.log('false');
}

testTruthy(true); // true
testTruthy(false); // false
testTruthy(new Boolean(false)); // true (object is always true)

testTruthy(''); // false
testTruthy('Packt'); // true
testTruthy(new String('')); // true (object is always true)

testTruthy(1); // true
testTruthy(-1); // true
testTruthy(NaN); // false
testTruthy(new Number(NaN)); // true (object is always true)

testTruthy({}); // true (object is always true)
var obj = { name: 'John' };
testTruthy(obj); // true
testTruthy(obj.name); // true
testTruthy(obj.age); // false (age property does not exist)
```
#### Logical Operators && and ||
```
const userName = 'Max';
const altName = '';
console.log(userName === 'Max'); // generates and prints a boolean => true
console.log(userName); // wasn't touched, still is a string => 'Max'
 
console.log(userName || null); // userName is truthy and therefore returned by || => 'Max'
console.log(altName || 'Max'); // altName is falsy (empty string), hence 'Max' is returned => 'Max'
console.log(altName || ''); // both altName and '' are falsy but if the first operand is falsy, the second one is always returned => ''
console.log(altName || null || 'Anna'); // altName and null are falsy, 'Anna' is returned => 'Anna'
 
console.log(userName && 'Anna'); // userName is truthy, hence second (!) value is returned => 'Anna'
console.log(altName && 'Anna'); // altName is falsy, hence first value is returned => ''
console.log(userName && ''); // userName is truthy, hence second value is returned => ''
```
`||` can be used in to assign default/ fallback values to variables
```
const enteredValue = ''; // let's assume this is set based on some input provided by the user, therefore it might be an empty string
const userName = enteredValue || 'PLACEHOLDER'; // will assign 'PLACEHOLDER' if enteredValue is an empty string
```

### Statements & Expressions
[MDN - Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions)<br>
[Stack Overflow discussion: difference between expressions and statements](https://stackoverflow.com/questions/12703214/javascript-difference-between-a-statement-and-an-expression)
>An expression is any valid unit of code that resolves to a value.
Basically expressions can be used on the right side of an equal sign; statement (e.g. if statement) cannot.

### ES6 Related
#### var VS let & const
[Article from Free Code Camp - difference among var, let, const](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/#:~:text=var%20variables%20can%20be%20updated,const%20variables%20are%20not%20initialized.)

#### Strict mode
[MDN - Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode#Changes_in_strict_mode)
