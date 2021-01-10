## Potential security holes (focus on client side)

Resource: [Security of JavaScript Applications](https://dhtmlx.medium.com/security-of-javascript-applications-1c95cd2ce533)

### Security details in the code

- The JavaScript code running on the page can be read by anyone visiting the page.
- Should not expose security-relevant details in the client side JavaScript code, e.g. database access credentials.


### Cross-Site Scripting Attacks (XSS)

- Cross-Site Scripting Attack is a attack pattern where malicious JS code gets injected and executed.
- Injected code can do anything your code could do as well.
- Attacker gets full behind-the-scenes control.
- Use `element.innerHTML` to store user inputs can introduce potential attacks, compared to `element.textContent`.

There are packages that help to protect against cross-site scripting attack. One example is [`sanitize-html`](https://www.npmjs.com/package/sanitize-html).


### Cross-Site Request Forgery (CSRF)

Typical scenario for this attack: people trick you into clicking on a link that leads to a prepared page where they abuse your local cookies to send a request another normal page.

- More of a server-side issue.
- Attack pattern that depends on injected content.
- Requests to malicious servers are made with user's cookies.
- Actions can be executed without the user knowing.


### Cross-Origin Resource Sharing (CORS)

[MDN - CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

Idea of CORS: by default, request from the browser side application can only be made to a backend that runs on the same server, so that the HTML page and the script that executes there are served by the same server that you are trying to send requests to.

- Not an attack pattern but a security concept.
- Requests are only allowed from the same origin (domain).
- Controlled via server-side response headers and browser.



