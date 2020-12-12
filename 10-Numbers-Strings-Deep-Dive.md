## Numbers & Strings - Deep Dive

### Numbers in JavaScript

- In JavaScript, every number is a floating point number. There is no integer type for numbers.
- Number are stored as 64 bit floating points.
```
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
console.log(Math.pow(2,53) - 1); // 9007199254740991

console.log(Number.MAX_VALUE); // 1.7976931348623157e+308

console.log(Number.MIN_SAFE_INTEGER); // -9007199254740991
```

#### Floating point (im)precision

Example of rounding errors in JavaScript

```
console.log(0.2 + 0.4); // 0.6000000000000001
console.log(0.2 + 0.4 === 0.6); // false
```
[Article about the rounding errors and why they occur](https://modernweb.com/what-every-javascript-developer-should-know-about-floating-points/)

[MDN - Numbers and dates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Numbers_and_dates)

To put it simply, there are certain fractions where there is no perfect solution in the binary system 
```
console.log(0.2.toString(2)); // "0.001100110011001100110011001100110011001100110011001101" 
```

#### The `BigInt` type

Perfect type for working with big integers.

[MDN- BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)


### Strings in JavaScript

#### Tagged templates

[MDN - Tagged templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates)

Simple example:
```
const prodDescription = (strings, name, price) => {
  console.log(strings); // ["the ", " should be ", "", raw: Array(3)]
  const priceCategory = price > 50 ? 'expensive' : 'not expensive';
  return `${strings[0]}${name}${strings[1]}${priceCategory}`;
}

const n = 'book';
const p = 30;
const p2 = 60;

console.log(prodDescription`This ${n} is ${p}`); // This book is not expensive
console.log(prodDescription`This ${n} is ${p2}`); // This book is expensive
```


