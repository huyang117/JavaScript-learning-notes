## Functions - Advanced Concepts

### Pure Functions & Side Effects

Pure function: for the same input, always produce the same output. And it does not trigger any side effect (which means that it does not change anything outside of the function). 

Examples of impure functions:

```
const impureFunc = num => {
  return num + Math.random();
} // result changes everytime because the random number introduced
```

```
let result = 0;

const sideEffectFunc1 = (num1, num2) => {
  const sum = num1 + num2;
  result = sum; // changed a variable that is defined outside of the function; this is a side-effect
  return sum;
}
```

```
const hobbies = ['reading', 'sudoku'];

const sideEffectFunc2 = arr => {
  arr.push('NEW_HOBBY'); // introduced side-effect by changing the original array
  console.log(arr);
}

sideEffectFunc2(hobbies);
```
