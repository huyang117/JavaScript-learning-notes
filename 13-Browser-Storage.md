## Browser Storage

- Browser side: store temporary, "convenience" data
- Server side: store essential and persistent data

Three major browser storage types

| localStorage, sessionStorage                  | Cookies                                        | IndexedDB                                     |
|:----------------------------------------------|:-----------------------------------------------|:----------------------------------------------|
| Simple key-value pairs, can be used to save the sessionID, some analytics key that is needed to be send to the analytics server | Simple key-value pairs with some config options (e.g. set expiration time) | Relatively sophisticated, client-side database |
| Manage user preferences or basic user data    | Manage user preferences or basic user data     | Manage complex data for the web app           |
| Can be cleared by the user and via JavaScript | Can be cleared by the user and via JavaScript  | Can be cleared by the user and via JavaScript |
| Easy to use, quite versatile, bad for complex data in rich web app (e.g. data in Google Sheet) | Usually sent to server with outgoing requests and (unlike localStorage and sessionStorage) can also be read by the server, bad for complex data | Great for complex (non-critical) data, good performance |

### localStorage VS sessionStorage

[MDN - localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

[MDN - sessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage)

In the key-value pair, both key and value should be in string format. Object cannot be stored as value properly but JSON data can, e.g.
```
const userId = "user123";
const user = {
  name: "max",
  age: 30,
  hobbies: ["reading", "sleeping"],
};

sessionStorage.setItem("userId", userId);
localStorage.setItem("user", JSON.stringify(user));

// localStorage.setItem("user", user); // this will be stored as "user"(key):"[object Object]"(value)
```


- sessionStorage lives as long as the page is open in the browser; reloading will not cause it to disappear; if that tab or the entire browser is closed, sessionStorage is cleared
- localStorage will not be cleared when the tab or the browser is closed. localStorage will only be cleared when the user manually clears it or the browser clears it because it is running out of space 
