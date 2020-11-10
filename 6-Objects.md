## Objects

### Properties

#### Add, modify and delete properties
```
const person = {
  name: "max",
  age: 31,
  greet: () => console.log("hello"),
};

person.isAdmin = true; // add property
person.age = 38; // modify property
delete person.age; // delete property
console.log(person.age); // undefined
```

#### Property Types
- Use square brackets to access keys that cannot be accessed using dot notation
```
const person = {
  "user-id": "max@gmail.com",
};

console.log(person['user-id']); // "max@gmail.com"
```
```
const person = {
  "user-id": "max@gmail.com",
};

const userId = 'user-id';
console.log(person.userId); // undefined, because there is no property named "userId" in person
console.log(person[userId]); // "max@gmail.com"
```

- Number can be used as keys (only zero or positive numbers; negative numbers cannot be used as keys)
```
const person = {
  1.5: "hey",
};

console.log(person[1.5]); // "hey"
```

#### Spread operator and objects
Recap: The spread operator `...` does a shallow copy only. It copies the top level key-value pairs. Any nested reference values are kept. 
```
const person = {
  name: 'max',
  hobbies: ['eating', 'playing'],
}

const copyPerson = {...person}; // The hobbies array in person and copy person point to the same object. Same reference.

copyPerson.name = 'alice';
copyPerson.hobbies.push('sleeping');

console.log(person.name); // "max"
console.log(copyPerson.name); // "alice"

console.log(person.hobbies); // ["eating", "playing", "sleeping"]
console.log(copyPerson.hobbies); // ["eating", "playing", "sleeping"]
```
To copy the nested reference values:
```
const person = {
  name: 'max',
  hobbies: ['eating', 'playing'],
}

const copyPerson = {...person, hobbies: [...person.hobbies]};

copyPerson.name = 'alice';
copyPerson.hobbies.push('sleeping');

console.log(person.name); // "max"
console.log(copyPerson.name); // "alice"

console.log(person.hobbies); // ["eating", "playing"]
console.log(copyPerson.hobbies); // ["eating", "playing", "sleeping"]
```
Another way to copy an object is to use `Object.assign()` - [MDN Object.assign()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

#### Object destructuring
```
const person = {
  name: 'max',
  hobbies: ['eating', 'playing'],
}

const { name } = person;
console.log(name); // "max"
```
Assign a new name to the extracted property using `:`
```
const person = {
  username: 'max',
  hobbies: ['eating', 'playing'],
}

const { username: personName } = person; // rename the property name
console.log(username); // error
console.log(personName); // "max"
```

#### Check for property existence
- use `in`
```
const person = {
  username: 'max',
  hobbies: ['eating', 'playing'],
}

console.log('username' in person); // true
console.log('age' in person); // false
```
- check whether [object].[property] is `undefined`
```
const person = {
  username: 'max',
  hobbies: ['eating', 'playing'],
}

const { username, age } = person;

if (username) {
  console.log(`username = ${username}`);
} else {
  console.log(`username is undefined`);
}

if (age) { // undefined will be coerced to false
  console.log(`age = ${age}`)
} else {
  console.log(`age is undefined`);
}

// "username = max"
// "age is undefined"
```
