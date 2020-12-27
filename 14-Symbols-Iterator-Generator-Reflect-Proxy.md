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

Example of Iterator (an iterator is basically an object which has a `next` method)

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



