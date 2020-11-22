## Constructor Functions

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
In the code above, if we call `const person = Person();` without the `new` keyword, `person` would be `undefined` because `function Person()` does not return anything. <br />
`class` is more like a syntactical sugar for the constructor function (i.e. an easier way of writing blueprint definitions). Constructor function can be confusing since it has the form of `function` but behaves a bit differently from the normal functions.<br />
Behind the scenes, `class` does more than setting up the constructor function.


## Prototypes & Prototypical Inheritance
