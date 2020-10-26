## Working with DOM

### Side Note
Difference between `console.log` and `console.dir`: <br />
[StackOverflow anwser](https://stackoverflow.com/questions/11954152/whats-the-difference-between-console-dir-and-console-log) <br />
[Pass `document.body` to console.log and console.dir in Chrome](https://stackoverflow.com/questions/11954152/whats-the-difference-between-console-dir-and-console-log/19269945#19269945)

### Nodes & Elements
Nodes
- The objects that make up the DOM
- HTML tags are just "element nodes" (or "elements)
- Text create "text nodes"
- Attributes create "attribute nodes"

Elements
- One type of nodes (nodes that are created off of HTML tags)
- There are special properties and methods to interact with the elements
- Available methods and properties depend on the kind of element
- Can be selected in various ways
- Can be created/ removed via JavaScript

### Node query methods
`document.body` => Selects the `<body>` element node.<br />

`document.head` => Selects the `<head>` element node.<br />

`document.documentElement` => Selects the `<html>` element node.<br />

`document.querySelector(<CSS selector>)` takes any CSS selector (e.g. '#some-id', '.some-class' or 'div p.some-class') and returns the first matching element in the DOM. Returns null if no matching element could be found.<br />

`document.getElementById(<ID>)` takes an ID (without #, just the id name) and returns the element that has this id. Since the same ID shouldn't occur more than once on your page, it'll always return exactly that one element. Returns null if no element with the specified ID could be found.<br />

`document.querySelectorAll(<CSS selector>)` takes any CSS selector (e.g. '#some-id', '.some-class' or 'div p.some-class') and returns all matching elements in the DOM as a static (non-live) NodeList. Returns and empty NodeList if no matching element could be found.<br />

`document.getElementsByClassName(<CSS CLASS>)` takes a CSS class g (e.g. 'some-class') and returns a live HTMLCollection of matched elements in your DOM. Returns an empty HTMLCollection if not matching elements were found.<br />

`document.getElementsByTagName(<HTML TAG>)` takes an HTML tag (e.g. 'p') and returns a live HTMLCollection of matched elements in your DOM. Returns an empty HTMLCollection if not matching elements were found.
