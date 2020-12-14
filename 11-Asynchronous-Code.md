## Asynchronous Code

- Synchronous code execution: JavaScript is single-threaded. It means that JavaScript execute tasks in sequence and can only execute **one** task at a time.
- Tasks that take longer time can be offloaded to the browser to achieve asynchronous code execution (e.g. When we use `addEventListener`, we hand this task off to the browser and then the code after the `addEventListener` line will not be blocked but executed right away. The browser will invoke the event listener callback function when the event occurs.)
- The browser uses multiple threads.

### The event loop

[MDN - Concurrency and the event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

[Medium article - JavaScript Event Loop Explained](https://medium.com/front-end-weekly/javascript-event-loop-explained-4cd26af121d4)
