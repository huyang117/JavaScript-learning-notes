## Object-oriented Programming
 
### Classes & Instances

[MDN - Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

#### Class declarations
```
class Product { // convention of class name: capitalize the first letter
  title = 'DEFAULT TITLE'; // define a field
  imageURL;
  price;
  description;
}

console.log(new Product());
```
`title`, `imageURL`, `price`, `description` are fields defined in the class; and will be the properties of the object created from the `Product` class. In this case, every instance created will have a `title` property with value = 'DEFAULT TITLE', while the other three properties will be `undefined` when the object is created.
<br />

Use `constructor` method:
```
class Product { // convention: capitalize the first letter
  constructor(title, imageURL, price, description) {
    this.title = title; // assign a value to a property
    this.imageURL = imageURL;
    this.price = price;
    this.description = description;
  }
}

console.log(new Product('A Mirror', '#', 20.5, 'A make-up mirror with light'));
/* the new instance created has the following properties:
{
  description: "A make-up mirror with light",
  imageURL: "#",
  price: 20.5,
  title: "A Mirror"
} */
```

#### Static properties, fields, methods
| Static Field/ Property/ Method                            | Instance Field/ Property/ Method                                           |
|:----------------------------------------------------------|:---------------------------------------------------------------------------|
| Defined with `static` keyword                             | Defined without `static` keyword                                           |
| Only accessible on the class and not on instance          | Only accessible on instance created based on the class using `new` keyword |
| Typically used in helper class, global configuration etc. | Typically used for core, re-useable logic                                  |

#### Inheritance
[MDN - inheritance](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)

#### Private fields, properties, methods
[MDN - private class fields](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)<br />
[MDN - private fields declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#:~:text=Private%20field%20declarations,-Using%20private%20fields&text=By%20defining%20things%20which%20are,front%20in%20a%20field%20declaration.)

