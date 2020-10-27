## Arrays and Iterables

### Some concepts

#### Iterables
Definition: An iterable is an object where you can use the `for-of` loop.<br />
Example: Array, NodeList, String, Map, Set

#### Array-like Object
Definition: Objects that have a `length` property and use indexes to access items.<br />
Example: NodeList, String

### Array

#### Create an array
Method 1: most common way
```
const arr = [1, 2, 3];
```

Method 2: use `Array.from()`, which is useful in converting iterables and array-like objects into arrays. <br />
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
hobbies.push('jogging');
console.log(hobbies); // ["reading", "swimming", "jogging"]
```
- `unshift` adds new element at the **beginning** of an array
```
const hobbies = ['reading', 'swimming'];
hobbies.unshift('jogging');
console.log(hobbies); // ["jogging", "reading", "swimming"]
```
