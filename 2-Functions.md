## Functions
### Function Declaration and Function Expression 
```
// Function statement/ declaration

function multiply(a, b) { 
  return a * b;
}
```
```
// Function Expression (on the right side of the '=')

const multiply = function() {
  return a * b;
}
```

### Default Arguments
```
const printParam = (paramA = 'temperature', paramB) => {
  console.log(`paramA = ${paramA}; paramB = ${paramB}`);
}

printParam(undefined, 'time'); // "paramA = temperature; paramB = time"

printParam(null, 'time'); // "paramA = null; paramB = time"

printParam('humidity'); // "paramA = humidity; paramB = undefined"
```
```
// when assigning a default value, can use parameters that came before that parameter
// e.g. use paramA to decide the default value of paramB

const printParam = (paramA, paramB = paramA === undefined ? 'area' : 'humidity') => {
  console.log(`paramA = ${paramA}; paramB = ${paramB}`);
}

printParam(undefined); // "paramA = undefined; paramB = area"

printParam(null); // "paramA = null; paramB = humidity"
```

### Rest Operator
```
// The rest operator ... takes all the arguments the function gets and merges them into an array
const sumUp = (...numbers) => {
  let sum = 0;
  for (const num of numbers) { // numbers is the array containing all the arguments passed in
    sum += num;
  }
  console.log(sum);
}

sumUp(1,2,3,4,5,6,7); // 28
sumUp(1,2,3,4,5,6,7,8,9,10); // 55
```
Rest parameter must be last formal parameter; but can have parameters in front of rest parameter
```
// The first two parameters will be assigned to a and b; paramaters thereafter will be merged together

const sumUp = (a, b, ...numbers) => {
  let sum = 0;
  for (const num of numbers) { // numbers is the array containing all the arguments passed in
    sum += num;
  }
  console.log(sum);
}

sumUp(1,2,3,4,5,6,7); // 25
sumUp(1,2,3,4,5,6,7,8,9,10); // 52
```
Alternative to using the rest operator before ES6: `arguments` variable" (it is recommended to use the rest operator)
```
// arguments is a built-in keyword. It can be used inside of functions, but only inside of the functions that use the function keyword

const sumUp = function() {
  let sum = 0;
  for (const num of arguments) {
    sum += num;
  }
  console.log(sum);
}

sumUp(1,2,3,4,5,6,7); // 28
sumUp(1,2,3,4,5,6,7,8,9,10); // 55
```

### Functions inside of functions
```
const sumUp = (...numbers) => {

  // validateNumber is only accessible within the sumUp function
  const validateNumber = () => {}
  
  validateNumber();
}

// cannot access validateNumber() outside of sumUp
```

### Callback functions
Pass `functionA` to `functionB` as a parameter such that `functionA` is executed at certain point within `functionB`. In this case, `functionA` is the callback function and `functionB` is the higher order function.<br />
Callback function is used in functions such as `addEventListener` and `setTimeout`.<br />
`addEventListener('click', func)` means to execute `func` when there is an click event.<br />
`setTimeout(func, 3000)` means to execute `func` after 3 seconds (3000 milliseconds).
```
// In this example, alertNoEmpty is the callback function;
// it will be called by the checkInput function when NO empty string is passed as argument

const checkInput = (alertNoEmpty, ...strings) => {
  let hasEmptyString = false;
  for (const str of strings) {
    if (!str) {
      hasEmptyString = true;
      break;
    }
  }
  if (!hasEmptyString) {
    alertNoEmpty();
  }
}

checkInput(() => alert('No empty string is detected'), 'a', 'b', 'c'); // will see alert
checkInput(() => alert('No empty string is detected'), 'a', 'b', ''); // will not see alert
```
