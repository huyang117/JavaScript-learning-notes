## Work with Http requests

### Background

- [Academind - how the web works](https://academind.com/learn/web-dev/how-the-web-works/)
- [MDN - Http request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [MDN - HTTP messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)
- [MDN - HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [MDN - HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)

### JSON data

JSON stands for JavaScript Object Notation.

Example (the whole JSON "object" is wrapped in double quotes itself because JSON data in the end is just a string): 
```
{
    "name": "Max",
    "age": 30,
    "hobbies": [
        { "id": "h1", "title": "Sports" },
        { "id": "h2", "title": "Cooking" }
    ],
    "isInstructor": true
}
```

JSON data supports objects (`{}`), arrays (`[]`), strings (MUST use double-quotes), numbers (NO quotes) and booleans (also NO quotes).

All object keys (e.g. `"name"`) HAVE to be wrapped by double quotes. No quotes or single quotes are NOT allowed.

Use `JSON.stringify()` to convert JavaScript object to JSON data:
```
const person = { // this is NOT JSON - it's a normal ("raw") JavaScript object!
    name: 'Max',
    age: 30,
    hobbies: [
        { id: 'h1', title: 'Sports' },
        { id: 'h2', title: 'Cooking' }
    ],
    isInstructor: true
};
 
const jsonData = JSON.stringify(person); // convert raw JS data to JSON data string
console.log(jsonData); // a string with machine-readable JSON data in it
console.log(typeof jsonData); // string
```
`JSON.stringify()` can be applied on strings, arrays, numbers and booleans as well:
```
const jsonNumber = JSON.stringify(2); // "2"
const jsonText = JSON.stringify('Hi there! I use single quotes in raw JS'); // ""Hi there! ...""
const jsonArray = JSON.stringify([1, 2, 3]); // "[1,2,3]"
const jsonBoolean = JSON.stringify(true); // "true"
```

Use `JSON.parse()` to convert JSON data to JavaScript object:
```
const parsedData = JSON.parse(jsonData); // yields a "raw" JS object/ array etc.
```


