## Object-oriented Programming
 
### Classes & Instances

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


