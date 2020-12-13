## Arrays and Iterables

### Some concepts

#### Iterables
Definition: An iterable is an object where you can use the `for-of` loop.

Example: Array, NodeList, String, Map, Set

#### Array-like Object
Definition: Objects that have a `length` property and use indexes to access items.

Example: NodeList, String

### Array

#### Create an array
Method 1: most common way
```
const arr = [1, 2, 3];
```

Method 2: use `Array.from()`, which is useful in converting iterables and array-like objects into arrays. 

`Array.from()` only accepts one argument.
```
const strArr = Array.from('Hi!'); // ["H", "i", "!"], an array of characters in the string
```
```
/* suppose you have the following code within the <body> element in the html code
<ul>
  <li>list item 1</li>
  <li>list item 2</li>
  <li>list item 3</li>
</ul>
*/

const listItems = document.querySelectorAll('li'); // get a NodeList object with length = 3
const listItemsArr = Array.from(listItems); // get an array of 3 <li> elements
```

Method 3: use constructor function
```
const arr1 = new Array(); // create an empty array, []
const arr2 = new Array(1, 2, 3); // create an array containing 3 elements, [1, 2, 3]
const arr3 = new Array(3); // NOT create an array with 3 as the only element; instead, create an array with length = 3 and undefined elements, i.e. [undefined, undefined, undefined]
```

Method 4: similar to Method 3, without the `new` keyword
```
const arr1 = Array(); // []
const arr2 = Array(1, 2, 3); // [1, 2, 3]
const arr3 = Array(3); // [undefined, undefined, undefined]
```

Method 5: use `Array.of()`
```
const arr1 = Array.of(); // create an empty array, []
const arr2 = Array.of(1, 2, 3); // create an array containing 3 elements, [1, 2, 3]
const arr3 = Array.of(3); // create an array with one element, 3; different from how new Array(3) or Array(3) works
```
- Method 3 - 5 are not often used to create arrays.
- It is flexible in terms of what data can be stored in an array, e.g. `Array.of(1, 'hi', [1, 2, 3])` returns an array containing a number, a string and a nested array, `
[1, "hi", [1, 2, 3]]`

#### Add & Remove elements
- `push` adds new element at the **end** of an array
```
const hobbies = ['reading', 'swimming'];
hobbies.push('jogging'); // push returns the new length of the array after the element being added, in this case, 3
console.log(hobbies); // ["reading", "swimming", "jogging"]
```

- `unshift` adds new element at the **beginning** of an array
```
const hobbies = ['reading', 'swimming'];
hobbies.unshift('jogging'); // unshift also returns the new length of the array, in this case, 3
console.log(hobbies); // ["jogging", "reading", "swimming"]
```

- `pop` removes the **last** element
```
const hobbies = ['reading', 'swimming'];
hobbies.pop(); // pop returns the element removed, in this case, "swimming"
console.log(hobbies); // ["reading"]
```

- `shift` removes the **first** element
```
const hobbies = ['reading', 'swimming'];
hobbies.shift(); // shift also returns the element removed, in this case, "reading"
console.log(hobbies); // ["swimming"]
```

- change element at other positions using index
```
const hobbies = ['reading', 'swimming'];
hobbies[1] = 'coding'; // change the second element to coding
console.log(hobbies); // ["reading", "coding"]
```

- rare case of changing element at other index
```
const hobbies = ['reading', 'swimming'];
hobbies[5] = 'coding'; // specify an element out of current index range
console.log(hobbies); // ["reading", "swimming", undefined, undefined, undefined, "coding"], index 2,3,4 will be empty spots
```

#### Array methods
- `splice()`: used to add/ remove/ replace elements in arrays at specific index. `splice()` only applys to arrays, not to iterables or array-like objects.<br /> 
`arr.splice(0)` can be used to clear up an array. `arr.splice(1)` deletes everything up from index 1 (including index 1). `splice()` return an array of removed elements.<br />
[MDN - `splice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

- `slice()`: used toreturn a copy of a portion of an array.<br />
[MDN - `slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

- `concat()`: used to merge two or more arrays or concatenate values into array. Return a new array instead of changing the original array.<br />
[MDN - `concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)

- `indexOf()` and `lastIndexOf()`: to find the index of element.<br />
[MDN - `indexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)<br />
[MDN - `lastIndexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf)

- `find()`: returns the first element in the provided array that fulfills the provided testing function. <br />
[MDN - `find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
```
const arr = [{ name: 'h'}, { name: 'o'}];
const h = arr.find(a => a.name === 'h');
console.log(h); // {name: "h"}, not a copy of the object, but exactly the same reference value
```

- `findIndex()`: returns the **index** of the first element in the provided array that fulfills the provided testing function. <br />
[MDN - `findIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
```
const arr = [{ name: 'h'}, { name: 'o'}];
const hIndex = arr.findIndex(a => a.name === 'h');
console.log(hIndex); // 0
```

- `includes()`: check whether an array includes a certain value; return `true` or `false`.<br /> 
Same result as `[fullArray].indexOf([target]) !== -1`. <br />
[MDN - `includes()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

- `sort()`<br />
[MDN - `sort()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
```
const arr = [9, 4, 11, 7];
console.log(arr.sort((a, b) => a - b)); // pass the sorting logic, in this case, ascending; result is [4, 7, 9, 11]
```

- `reverse()`: reverse an array. <br />
[MDN - `reverse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

- `filter()`: creates a **new array** with all elements that pass the test implemented by the provided function.<br />
[MDN - `filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
```
const arr = [9,4,11,7];
console.log(arr.filter(a => a % 2 === 0)); // [4]
```

- `reduce()`: execute a reducer function and result in a single output value.<br />
[MDN - `reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
```
const arr = [13, 7, 7, 36, 18, 3, 7, 1, 15, 31];

const findMaxAndMin = (...arguments) => {
  // return an array of length 2, 
  // first element is the min value in the array, 
  // second element is the max value in the array
  return arguments.reduce(
    (accumulator, customValue) => {
      accumulator[0] =
        accumulator[0] < customValue ? accumulator[0] : customValue;
      accumulator[1] =
        accumulator[1] > customValue ? accumulator[1] : customValue;
      return accumulator;
    },
    new Array(2)
  );
};

const [min, max] = findMaxAndMin(...arr);
console.log("min", min); // min 1
console.log("max", max); // max 36
```

#### Array and String
- `split()`: split string into an array.<br />
[MDN - `split()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split)
```
const str = 'hey;this;is;daniel';
const arr = str.split(';');
console.log(arr); // ["hey", "this", "is", "daniel"]
```

- `join()`: join elements of an array into a string. The elements are separated by **commas (default)** or a specified separator string.<br />
[MDN - `join()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)
```
const elements = [1, 2, 3];
console.log(elements.join()); // "1,2,3"
```

#### Array Destructuring
```
const elements = [1, 2, 3];
const [a, b, c, d] = elements;
console.log(a, b, c, d); // 1, 2, 3, undefined
```
```
const elements = [1, 2, 3, 4, 5, 6];
const [a, b, c, ...d] = elements;
console.log(a, b, c, d); // 1, 2, 3, [4, 5, 6]
```
[MDN - Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
