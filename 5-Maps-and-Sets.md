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
