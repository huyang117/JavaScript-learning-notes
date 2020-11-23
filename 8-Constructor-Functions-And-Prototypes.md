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

#### `__proto__` and `prototype` (both are property)

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
In the code above, `Person.prototype` defines what will be assigned as a prototype to any object that is created based on the `Person` constructor function. Therefore, any object created based on `Person` receives the default prototype with the `printAge` function added.

Another way (rarely used) to create a new object (continue with the code above) using `__proto__`:
```
const p = new Person();
const p2 = new p.__proto__.constructor(); // don't forget the new keyword
console.log('p2', p2); // get a new Person object
```

The `prototype` property exists on everything that is a constructor function. It defines what will be assigned as a prototype to any object that is created based on the this constructor function. Objects created using object literal`{}` do not have the `prototype` property. 
```
const book = {
  price: 23,
};

console.dir(book);
// Object
// price: 23
// __proto__: Object
```

#### Side note about static method
In the example used in "`__proto__` and `prototype` (both are property)" section, `Person.prototype.printAge` defines a method available to every instance created based on `Person` constructor function. In constrast, `Person.[function_name]` defines function that is only available to the constructor function object itself.
```
function Person() {
  this.age = 30;
  this.name = 'max';
  this.print = function() {
    console.log(`Hi I am ${this.name}, I am ${this.age} years old`);
  }
}

Person.staticMethod = function() {
  console.log('This method is not available on the instances created based on Person');
}

const person = new Person(); 
person.staticMethod(); // Uncaught TypeError: person.staticMethod is not a function

Person.staticMethod(); // "This method is not available on the instances created based on Person" 
```

#### `Object`
The default prototype object that all objects can come back to is `Object.prototype` (not `Object` but `Object.prototype`).

Any object created using the object literal notation or based on constructor functions by default always use the `Object` constructor function, and will therefore use `Object.prototype` as its fallback value.

So the prototype chain ends at `Object.prototype`.

```
console.log(Object.prototype.__proto__); // null
```