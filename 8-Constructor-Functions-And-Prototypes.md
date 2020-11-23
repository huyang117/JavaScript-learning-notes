## Constructor Functions and Prototypes

### Constructor function
A way to create blueprint for objects without using `class`
```
function Person() {  // convention is to capitalize the name for constructor functions
  this.age = 30;
  this.name = 'max';
  this.print = function() {
    console.log(`Hi I am ${this.name}, I am ${this.age} years old`);
  }
}

const person = new Person(); 
person.print(); // "Hi I am max, I am 30 years old"
```
In the code above, if we call `const person = Person();` without the `new` keyword, `person` would be `undefined` because `function Person()` does not return anything.

`class` is more like a syntactical sugar for the constructor function (i.e. an easier way of writing blueprint definitions). Constructor function can be confusing since it has the form of `function` but behaves a bit differently from the normal functions.

Behind the scenes, `class` does more than setting up the constructor function.

### Prototypes
>JavaScript is a prototype-based language which uses prototypical inheritance.

[MDN - Object Prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)

If JavaScript tries to access a certain property or method and does not find it on an object, it automatically looks at the prototype object and looks for the property there. If it does not find it there, it looks at the prototype of the prototype and so on (walking up the chain of prototypes). If in the end it did not find that property or method anywhere, it would return `undefined` for the property or throw an error for the method.

Every object has `__proto__` property that points at the prototype object.
```
function Person() {
  this.age = 30;
  this.name = 'max';
  this.print = function() {
    console.log(`Hi I am ${this.name}, I am ${this.age} years old`);
  }
}

Person.prototype.printAge = function() { 
  console.log(this.age);
} // so when we create an object based on Person, we have the printAge method available

const person = new Person();
console.log(person.__proto__ === Person.prototype); // true
person.printAge(); // 30
```
Another way (rarely used) to create a new object (continue with the code above):
```
const p = new Person();
const p2 = new p.__proto__.constructor(); // don't forget the new keyword
console.log('p2', p2); // get a new Person object
```
Objects created using object literal`{}` do not have the `prototype` property.
```
const book = {
  price: 23,
};

console.dir(book);
// Object
// price: 23
// __proto__: Object
```
