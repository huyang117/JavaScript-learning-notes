## Object-oriented Programming
 
### Classes & Instances

#### Class declarations
```
class Product { // convention of class name: capitalize the first letter
  title = 'DEFAULT TITLE'; 
  imageURL;
  price;
  description;
}

console.log(new Product());
```
`title`, `imageURL`, `price`, `description` are fields defined in the class; and will be the properties of the object created from the `Product` class. In this case, every `Product` object created will have a `title` property with value = 'DEFAULT TITLE', while the other three properties will be `undefined` when the object is created.

