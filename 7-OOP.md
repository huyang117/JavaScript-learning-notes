## Object-oriented Programming
 
### Classes & Instances

[MDN - Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

#### Class declarations
```
class Product { // convention of class name: capitalize the first letter
  title = 'DEFAULT TITLE'; // define a field
  imageURL;
  price;
  description;
}

console.log(new Product());
```
`title`, `imageURL`, `price`, `description` are fields defined in the class; and will be the properties of the object created from the `Product` class. In this case, every instance created will have a `title` property with value = 'DEFAULT TITLE', while the other three properties will be `undefined` when the object is created.
<br />

Use `constructor` method:
```
class Product { // convention: capitalize the first letter
  constructor(title, imageURL, price, description) {
    this.title = title; // assign a value to a property
    this.imageURL = imageURL;
    this.price = price;
    this.description = description;
  }
}

console.log(new Product('A Mirror', '#', 20.5, 'A make-up mirror with light'));
/* the new instance created has the following properties:
{
  description: "A make-up mirror with light",
  imageURL: "#",
  price: 20.5,
  title: "A Mirror"
} */
```

#### Static properties, fields, methods
| Static Field/ Property/ Method                            | Instance Field/ Property/ Method                                           |
|:----------------------------------------------------------|:---------------------------------------------------------------------------|
| Defined with `static` keyword                             | Defined without `static` keyword                                           |
| Only accessible on the class and not on instance          | Only accessible on instance created based on the class using `new` keyword |
| Typically used in helper class, global configuration etc. | Typically used for core, re-useable logic                                  |

#### Inheritance
[MDN - inheritance](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)

#### Private fields, properties, methods
[MDN - private class fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)<br />
[MDN - private fields declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#:~:text=Private%20field%20declarations,-Using%20private%20fields&text=By%20defining%20things%20which%20are,front%20in%20a%20field%20declaration.)

#### `instanceof` operator
Use `instanceof` to check whether an object is created based on a certain class.
```
class Human {
  species = 'human';
}

const h = new Human();

console.log(typeof h); // "object"
console.log(h instanceof Human); // true
```

#### Object descriptors
`Object.getOwnPropertyDescriptors()` return a new object of property descriptors. It shows the configuration about the properties that can be changed.
```
const person = {
  name: 'max',
  printName() {
    console.log(this.name);
  }
}

person.printName();

console.log(Object.getOwnPropertyDescriptors(person));

// result on JS Bin:
// "max"
// [object Object] {
//   name: [object Object] {
//     configurable: true,
//     enumerable: true,
//     value: "max",
//     writable: true
//   },
//   printName: [object Object] {
//     configurable: true,
//     enumerable: true,
//     value: function printName() {
//       window.runnerWindow.proxyConsole.log(this.name);
//     },
//     writable: true
//   }
// }
```
As shown above, there are 4 configuration items: `configurable`(whether can be deleted), `enumerable`(whether can appear in for-in loop), `value` and `writable`(whether can be set to other values). `Object.defineProperty()` can be used to change the configuration item.<br />
For example, with the `person` object created above, we can set the `writable` to `false` for the `name` property to lock it down:
```
Object.defineProperty(person, 'name', {
  configurable: true,
  enumerable: true,
  value: person.name,
  writable: false,
});

person.name = 'brie';

console.log(person.name); // still "max"; changes are not accepted and no error is thrown
```
We can still use `delete person.name` to delete the `name` property. But If we set `configurable` to be `false` in the code above, then `delete person.name` will return `false` and the `name` property will still be there.<br />
To elaborate what `enumerable` means: 
```
for (const key in person) {
  console.log(key);
}
// the properties that are picked up by the for-in loop
// "name"
// "printName"
```
If we only want to iterate through properties that are not functions, we can do:
```
Object.defineProperty(person, 'printName', {
  configurable: true,
  enumerable: false,
  value: person.greet,
  writable: false,
});
```
Then, if we run the `for-in` loop again afterwards, only `name` will be logged and `printName` will be skipped.
