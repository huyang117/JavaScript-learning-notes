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


### Factory Functions

Factory function: function that produces another function.

```
function createTaxCalculatorWithRate(rate) {
  function calculateTaxWithAmount(amount) {
    return rate * amount;
  }
  // the inner function is returned from the outer function before being executed
  return calculateTaxWithAmount;
}

// taxCalculator1 holds reference to the inner function 'calculateTaxWithAmount' with 'rate' = 0.19
const taxCalculator1 = createTaxCalculatorWithRate(0.19); 

// taxCalculator2 holds reference to the inner function 'calculateTaxWithAmount' with 'rate' = 0.25
const taxCalculator2 = createTaxCalculatorWithRate(0.25); 

// pass the amount argument to taxCalculator1 and taxCalculator2, 'rate' has been pre-configured.
console.log(taxCalculator1(100)); // 19
console.log(taxCalculator2(200)); // 50
```
Factory function is convenient when you have a function that is called multiple times in different places and can be pre-configured in a certain way. 

In the example above, the tax rate is pre-configured; and `taxCalculator1` & `taxCalculator2` created with the rate can be called multiple times with different amount.


### Closure

An important rule: every function in JavaScript is a closure.

Useful resources: 

[MDN - Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

[MDN - IIFE (Immediately Invoked Function Expression) ](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)


### Recursion

Example of a basic recursive function: 

```
function powerOf(x, n) {
  // specify the exit condition(s)
  if (n === 0) return 1; 
  if (n === 1) return x; 
  return x * powerOf(x, n-1);
}
```

Example of where recursive function shines:

```
const myself = {
  name: 'max',
  friends: [
    {
      name: 'mary',
      friends: [
        {
          name: 'clare',
          friends: [],
        },
        {
          name: 'loki',
          friends: [
            {
              name: 'xavi',
              friends: [
                {
                  name: 'amy'
                },
              ]
            },
          ]
        }
      ],
    },
    {
      name: 'penny',
      friends: [
        {
          name: 'berne',
        }
      ]
    }
  ],
}

const friendsList = [];

function getFriends(person) {
  if (!person.friends) return;
  
  for (let friend of person.friends) {
    friendsList.push(friend.name);
    getFriends(friend);
  }
}

getFriends(myself);

console.log(friendsList); // ["mary", "clare", "loki", "xavi", "amy", "penny", "berne"]
```
The function part can be changed to this (to avoid using `friendsList` as global variable): 
```
// const friendsList = [];

function getFriends(person) {
  const friendsList = [];
  if (!person.friends) return [];
  
  for (let friend of person.friends) {
    friendsList.push(friend.name);
    friendsList.push(...getFriends(friend));
  }
  return friendsList;
}

console.log(getFriends(myself)); // ["mary", "clare", "loki", "xavi", "amy", "penny", "berne"]
```
