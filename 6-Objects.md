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
