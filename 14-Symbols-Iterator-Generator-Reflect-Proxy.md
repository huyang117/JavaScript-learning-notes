## Meta-Programming

Topics that might be more interesting to library authors.

### Symbol

[MDN - Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)

- Primitive values
- Can be used ad keys in objects (i.e. object property identifiers)
- Built-in and creatable by developers
- **Guarantee uniqueness**

```
const symbolId = Symbol();
const person = {
  [symbolId]: '1',
  name: 'max',
  age: 49,
};
console.log(person[Symbol()]); // undefined
console.log(person[symbolId]); // 1
console.log(Symbol() === symbolId); // false
console.log(Symbol() === Symbol()); // false
```

#### Symbol.toStringTag

```
const person = {
  name: 'max',
  age: 49,
  [Symbol.toStringTag]: 'Custom User', // without this property, it will log [object Object] instead
};

console.log(person.toString()); // [object Custom User]
```

#### Iterator & Generator

Example of Iterator (an iterator is basically an object which has a `next()` method)

```
const company = {
  currEmployeeIndex: 0,
  employees: ["Amy", "Max", "Lidia"],
  next() {
    let value, done;

    if (this.currEmployeeIndex >= this.employees.length) {
      value = this.currEmployeeIndex;
      done = true;
    } else {
      value = this.employees[this.currEmployeeIndex];
      done = false;
      this.currEmployeeIndex++;
    }
    return { value, done };
  },
};

let emp = company.next();
while (!emp.done) {
  console.log(emp);
  emp = company.next();
}
```
The `company` object in the code above is iterable because it has this `next()` method

#### Symbol.iterator

[MDN - Symbol.iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/iterator)

Refactor the code for the `company` object, using `Symbol.iterator`:

```
const company = {
  currEmployeeIndex: 0,
  employees: ["Amy", "Max", "Lidia"],
  [Symbol.iterator]: function* () {
    while(this.currEmployeeIndex < this.employees.length) {
      yield this.employees[this.currEmployeeIndex];
      this.currEmployeeIndex++;
    }
  },
};

console.log([...company]); // ["Amy", "Max", "Lidia"]
```

`function*` defines a generator function. 

[MDN - Iterators and generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)

[MDN - function*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)

[MDN - Generator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)


### Reflect API

Useful for meta work on objects, e.g. delete property, define property, change prototype of a certain object, etc.

```
const course = {
  title: "JS",
};

Reflect.setPrototypeOf(course, {
  toString() {
    return this.title;
  },
});

console.log(course.toString()); // JS
```

[MDN - Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)

[MDN - Compaing Reflect and Object methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect/Comparing_Reflect_and_Object_methods)


### Proxy API

[MDN - Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

```
const meetingHandler = {
  get(object, propertyName) {
    if (propertyName === 'password') {
      return 'PLEASE ASK ADMIN FOR PASSWORD';
    }
    return object[propertyName] || 'NOT FOUND';
  }
};

const meeting = {
  title: "JS",
  password: "1234",
};

const pMeeting = new Proxy(meeting, meetingHandler);

console.log(pMeeting.title);    // JS
console.log(pMeeting.password); // PLEASE ASK ADMIN FOR PASSWORD
console.log(pMeeting.length);   // NOT FOUND
```
