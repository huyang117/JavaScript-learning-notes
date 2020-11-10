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

### '`this`' keyword
```
const movie = {
  info: {
    title: 'little women',
  },
  getFormattedTitle() {
    console.log(this); // to check what 'this' refers to
    return this.info.title.toUpperCase();
  }
};

console.log(movie.getFormattedTitle()); // "LITTLE WOMEN"
// in this case, 'this' refers to the movie object
```
However, if we use object destructuring
```
const movie = {
  info: {
    title: 'little women',
  },
  getFormattedTitle() {
    // console.log(this);
    return this.info.title.toUpperCase();
  }
};

const { getFormattedTitle } = movie;

console.log(getFormattedTitle()); // "TypeError: Cannot read property 'title' of undefined
// because in this case, 'this' refers to the window object
// side note, if we specify 'use strict', then console.log(this) will log 'undefined' instead of the window object
```
In order to specify which object the `this` keyword should refer to, we can use `bind`.
```
const movie = {
  info: {
    title: 'little women',
  },
  getFormattedTitle() {
    // console.log(this);
    return this.info.title.toUpperCase();
  }
};

let { getFormattedTitle } = movie;

getFormattedTitle = getFormattedTitle.bind(movie); // so that 'this' inside getFormattedTitle will refer to the movie object

console.log(getFormattedTitle()); // "LITTLE WOMEN"
```

#### `call()` and `apply()`
`bind()` is useful for occasions where you want to pre-configure a function for the future execution.<br />
`bind()` prepares a function for future execution. `bind()` returns a new function object.

```
const movie = {
  info: {
    title: 'little women',
  },
  getFormattedTitle() { return this.info.title.toUpperCase(); }
};

let { getFormattedTitle } = movie;
getFormattedTitle = getFormattedTitle.bind(movie); // assign a new function object to getFormattedTitle
console.log(getFormattedTitle()); // "LITTLE WOMEN"
```

In the code example above, We can use `call()` instead.<br />
`call()` executes the function right away with what `this` refers to being overrided.<br />
So the code above can be changed to:

```
let { getFormattedTitle } = movie;
console.log(getFormattedTitle.call(movie)); // "LITTLE WOMEN
```

The `call` in the code above can be changed to `apply()`, i.e.

```
let { getFormattedTitle } = movie;
console.log(getFormattedTitle.apply(movie)); // "LITTLE WOMEN"
```

`apply()` is similar to `call()`. The first parameter is what `this` binds to. But the remaining parameters are passed in different ways.
- For `call()`, other parameters are passed in and separated by comma, e.g. `getFormattedTitle.call(movie, paramA, paramB, paramC)`
- For `apply()`, other parameters are passed in as an array, e.g. `getFormattedTitle.apply(movie, [paramA, paramB, paramC])`

```
console.log(Math.max.call(null, 1, 2, 3, 4)); // 4
console.log(Math.max.apply(null, [1, 2, 3, 4])); // 4
```
- [MDN - `bind`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- [MDN - `call`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
- [MDN - `apply`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

#### '`this`' in functions bound to event listener 
The browser binds `this` on event listeners to the DOM element that triggers the event.
```
const filterMovie = function() { console.log(this); } // normal function declared with 'function' keyword instead of arrow function

const filterButton = document.getElementById('search-btn');
filterButton.addEventListener('click', filterMovie); // 'this' refers to the filterButton element
```

#### '`this`' and arrow function
```
const filterMovie = () => { console.log(this); }

const filterButton = document.getElementById('search-btn');
filterButton.addEventListener('click', filterMovie); // 'this' refers to the global window object
```
In arrow functions, `this` is not overwritten. In the code above, `this` refers to the same thing as it would refer to outside of the function. Below is an example where the arrow function shines regarding the reference of `this`:
```
const members = {
  teamName: 'Mocking Bird',
  people: ['Ben', 'Henry'],
  getTeamMembers() {
    this.people.forEach(person => {
      console.log(`${person} - ${this.teamName}`); 
    })
  }
};

members.getTeamMembers();

// result is
// "Ben - Mocking Bird"
// "Henry - Mocking Bird"
// the arrow function does not change the binding of 'this', 
// the 'this' in forEach function refers to the same thing as the 'this' in getTeamMembers() does
```
However, if we change the arrow function passed to `forEach` to a normal function declared with `function` keyword:
```
const members = {
  teamName: 'Mocking Bird',
  people: ['Ben', 'Henry'],
  getTeamMembers() {
    this.people.forEach(function(person) {
      // console.log(this); // 'this' refers to the global window object 
      console.log(`${person} - ${this.teamName}`);
    })
  }
};

members.getTeamMembers();

// result is
// "Ben - undefined"
// "Henry - undefined"
// the 'this' in the callback anonymous function refers to different things than the 'this' in getTeamMembers()
```

