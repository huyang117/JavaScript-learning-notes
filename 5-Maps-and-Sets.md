## Sets and Maps

### Comparison - Arrays, Sets, Maps
| Arrays                              | Sets                              | Maps                                                                    |
|:------------------------------------|:----------------------------------|:------------------------------------------------------------------------|
| Store Data of any kind and length   | Store Data of any kind and length | Store key-value data of any kind and length, any key values are allowed |
| Iterable; special array methods available | Iterable; special set methods available | Iterable; special map methods available                     |
| Order is guranteed                  | Order is not guranteed            | Order is guranteed                                                      |
| Duplicates are allowed              | Duplicates are not allowed        | Duplicate keys are not allowed                                          |
| Zero-based index to access elements | No index-based access             | Key-based access                                                        |

### Set
[MDN - Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
#### Set methods

- `has()`: to check whether an element exists in a set; return `true` or `false`
```
const ids = new Set(['hello', 'from', 'america']);
console.log(ids.has('hello')); // true
```

- `add()` and `delete()` <br />
if you try to add an existing value, it will not be added and no error will be thrown. If you try to delete an item that is not in the set, it will just be ignored and no error will be thrown (can use `has()` to check before adding/ deleting elements).

- `entries()`
```
const ids = new Set(['hello', 'from', 'america']);
for (const entry of ids.entries()) {
  console.log(entry);
}
// ["hello", "hello"]
// ["from", "from"]
// ["america", "america"]
```

- `values()`
```
const ids = new Set(['hello', 'from', 'america']);
for (const value of ids.values()) {
  console.log(value);
}  
// "hello"
// "from"
// "america"
```

### Map
[MDN - Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)

#### Map methods
- create `Map` object from 2-D array
```
const map = new Map([['key1', 'value1'], ['key2', 'value2']]);
console.log(map.get('key1')); // "value1"
console.log(map.size); // 2
```

- add data to a map using `set()`; check key exists or not using `has()`
```
let keyString = 'key String';
let keyObj = {};
let keyFunc = () => {};

let map = new Map();
map.set(keyString, 'value for keyString');
map.set(keyObj, 'value for keyObj');
map.set(keyFunc, 'value for keyFunc');

console.log(map.size); // 3

console.log(map.get('key String')); // "value for keyString"
console.log(map.has('key String')); // true
console.log(map.delete('key String')); // true

console.log(map.get({})); // undefined; has() and delete() will return false
console.log(map.get(() => {})); // undefined; has() and delete() will return false
```

- loop through the entries using `for...of` loop
```
for (const entry of map.entries()) {
  console.log(entry);
}

// also can use array destructuring
for (const [key, value] of map.entries()) {
  console.log(key, value);
}
```

- loop through the keys using `for...of` loop
```
for (const key of map.keys()) {
  console.log(key);
}
```

- loop through the values using `for...of` loop
```
for (const value of map.values()) {
  console.log(value);
}
```

