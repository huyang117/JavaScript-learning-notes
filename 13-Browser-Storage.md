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

