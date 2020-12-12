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
