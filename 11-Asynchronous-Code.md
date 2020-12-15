## Asynchronous Code

- Synchronous code execution: JavaScript is single-threaded. It means that JavaScript execute tasks in sequence and can only execute **one** task at a time.
- Tasks that take longer time can be offloaded to the browser to achieve asynchronous code execution (e.g. When we use `addEventListener`, we hand this task off to the browser and then the code after the `addEventListener` line will not be blocked but executed right away. The browser will invoke the event listener callback function when the event occurs.)
- The browser uses multiple threads.

### The event loop

[MDN - Concurrency and the event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

[Medium article - JavaScript Event Loop Explained](https://medium.com/front-end-weekly/javascript-event-loop-explained-4cd26af121d4)

### Promise

[MDN - Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

#### Wrap the `setTimeout` API with promise logic:
```
const delay = time => new Promise(resolve => setTimeout(resolve, time));

// delay(2000).then(() => {  }); // add more code in the curly bracket
```

#### Three promise states 

- PENDING: Promise is doing work, neither `then()` nor `catch()` executes at this moment
- RESOLVED: Promise is resolved => `then()` executes
- REJECTED: Promise was rejected => `catch()` executes

When you have another `then()` block after a `catch()` or `then()` block, the promise re-enters PENDING mode 

`then()` and `catch()` always return a new promise - either not resolving to anything or resolving to what you return inside of `then()`. 

Only if there are no more `then()` blocks left, it enters a new, final mode: SETTLED.

Once SETTLED, you can use a special block - `finally()` - to do final cleanup work. `finally()` is reached no matter if you resolved or rejected before.


#### `finally` block (not a must-have)
```
somePromiseCreatingCode()
    .then(firstResult => {
        return 'done with first promise';
    })
    .catch(err => {
        // would handle any errors thrown before
        // implicitly returns a new promise - just like then()
    })
    .finally(() => {
        // the promise is settled now - finally() will NOT return a new promise!
        // you can do final cleanup work here
    });
```

#### async/ await

[MDN - async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)

#### Other useful resources

[MDN - `Promise.all()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

[MDN - `Promise.race()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)

[MDN - `Promise.allSettled()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled)
