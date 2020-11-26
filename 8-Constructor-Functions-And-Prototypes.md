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
Code Example
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

- Every object has `__proto__` property that points at the prototype object.
- Another way (rarely used) to create a new object (continue with the code above) using `__proto__`:
```
const p = new Person();
const p2 = new p.__proto__.constructor(); // don't forget the new keyword
console.log('p2', p2); // get a new Person object
```
- In the code example above, `Person.prototype` defines what will be assigned as a prototype to any object that is created based on the `Person` constructor function. Therefore, any object created based on `Person` receives the default prototype with the `printAge` function added.

- The `prototype` property exists on everything that is a constructor function. It defines what will be assigned as a prototype to any object that is created based on the this constructor function. Objects created using object literal`{}` do not have the `prototype` property: 
```
const book = {
  price: 23,
};

console.dir(book);
// Object
// price: 23
// __proto__: Object
```

To summarize the difference between `someObj.__proto__` vs `SomeFunction.prototype`:

`__prototype` points at the prototype object of `someObj`; `prototype` points at the prototype object that will be assigned as prototype to objects created based on `SomeFunction`.

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

[MDN - Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)

The default prototype object that all objects can come back to is `Object.prototype` (not `Object` but `Object.prototype`).

Any object created using the object literal notation or based on constructor functions by default always use the `Object` constructor function, and will therefore use `Object.prototype` as its fallback value.

So the prototype chain ends at `Object.prototype`.

```
console.log(Object.prototype.__proto__); // null
```

#### class VS constructor function - How field/ property is added
```
class Human extends Species {
  name = 'max'; // the name property will be added after super() is called

  constructor() {
    super();
    this.age = 30;
  }
}
```
Adding a field `name` is translated to a property assignment that works in the same way as it would work if you would add it in the constructor method. So the code above is equivalent to the code below, which is clearer that all properties are added after the `super()` call. 
```
class Human extends Species {
  constructor() {
    super();
    this.age = 30;
    this.name = 'max'; // the name property will be added after super() is called
  }
}
```

#### class VS constructor function - How method is added
Unlike fields being added as properties, extra prototypes can be added by JavaScript when we add method in class. For example:
```
class Species {
  printSpecies() {
    console.log('printing...');
  }
}

class Human extends Species {
  name = 'max';

  constructor() {
    super();
    this.age = 30;
  }

  printAge() {
    console.log(`age = ${this.age}`);
  }
}

const human = new Human();
console.log(human);
``` 
The `printAge()` appears under `Human.__proto__` (in other words, `printAge()` is not part of object itself); and `printSpecies()` appears under `Species.__proto__`.

By adding method to a prototype, JavaScript makes it that all the `Human` object we create share the same prototype object. For example, we can add these code and the comparison will yield `true`. (For methods defined in this way, `bind` is needed sometimes to specify what `this` keyword points at.)
```
const human2 = new Human();
console.log(human.__proto__ === human2.__proto__); // true, which means that they are exactly the same object in memory
```
In this way, less objects are created and hence less performance impact. 

The equivalent code in constructor functions is:
```
function Human() {
  this.age = 30;
  this.name= 'max';
}

Human.prototype.printAge = function() {
  console.log(`age = ${this.age}`);
}
```

However, if in class `Human`, `printAge` is defined with the constructor method, i.e. `super(); this.age = 30; this.printAge = n() {}`, or defined outside of the constructor method but as a field, i.e. `printAge = function() {}` or use arrow function, then `printAge` will not be part of the prototype but will instead be created for every instance based on `Human`. (which means creating more objects and hence more performance impact, probably just a little bit more only).

To summarize:

| Method Shorthand | Property Function | Property Arrow Function |
|------------------|-------------------|-------------------------|
|`class Person {`<br />`greet() {}`<br />`}`|`class Person {`<br />`greet = function() {}`<br />`constructor(){`<br />`this.greet2 = function(){}`<br />`}`<br />`}`|`class Person {`<br />`greet = () => {}`<br />`constructor(){`<br />`this.greet2 = () => {}`<br />`}`<br />`}`|
|Assigned to `Person`'s prototype and hense shared across all instances (NOT re-created per instance)| Assigned to individual instance and hence re-created per object. Need to use `bind` sometimes to specify what `this` points at | Assigned to individual instances and hence re-created per object. `this` always refers to instance |
