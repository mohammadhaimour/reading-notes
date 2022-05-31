## Classes:

1- Classes are a template for creating objects. They encapsulate data with code to work on that data. Classes in JS are built on prototypes but also have some syntax and semantics that are not shared with ES5 class-like semantics.

2- Defining classes
Classes are in fact "special functions", and just as you can define function expressions and function declarations, the class syntax has two components: class expressions and class declarations.

3-Class declarations:
 ```js
 class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
 ```

 4-Hoisting:

- An important difference between function declarations and class declarations is that while functions can be called in code that appears before they are defined, classes must be defined before they can be constructed. 
```js
const p = new Rectangle(); // ReferenceError

class Rectangle {}
```


5-Class expressions:

- A class expression is another way to define a class. Class expressions can be named or unnamed. The name given to a named class expression is local to the class's body. However, it can be accessed via the name property.
```js
// unnamed
let Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle"

// named
let Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle2"
```

6- Class body and method definitions:

The body of a class is the part that is in curly brackets {}. This is where you define class members, such as methods or constructor.

- Strict mode:

  -The body of a class is executed in strict mode, i.e., code written here is subject to stricter syntax for increased performance, some otherwise silent errors will be thrown, and certain keywords are reserved for future versions of ECMAScript.

- Constructor:
 
  -The constructor method is a special method for creating and initializing an object created with a class. There can only be one special method with the name "constructor" in a class. A SyntaxError will be thrown if the class contains more than one occurrence of a constructor method.
- Prototype methods:

```js
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // Getter
  get area() {
    return this.calcArea();
  }
  // Method
  calcArea() {
    return this.height * this.width;
  }
}

const square = new Rectangle(10, 10);

console.log(square.area); // 100
```
- Generator methods:

    ```js
    class Polygon {
  constructor(...sides) {
    this.sides = sides;
  }
  // Method
  *getSides() {
    for(const side of this.sides){
      yield side;
     }
  }
        }

    const pentagon = new Polygon(1,2,3,4,5);

  console.log([...pentagon.getSides()]); // [1,2,3,4,5]
    
    ```
 ---
 ## Routing:

 1- Routing refers to how an application’s endpoints (URIs) respond to client requests. 
 ```js
 const express = require('express')
const app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})
 ```

 2-Route methods:

A route method is derived from one of the HTTP methods, and is attached to an instance of the express class.
```js
// GET method route
app.get('/', (req, res) => {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', (req, res) => {
  res.send('POST request to the homepage')
})
```

3-Route paths:

  ex:

- This route path will match requests to the root route, /.
```js
app.get('/', (req, res) => {
  res.send('root')
})
```


- This route path will match requests to /about.
```js
app.get('/about', (req, res) => {
  res.send('about')
})
```

4-Route parameters:

Route parameters are named URL segments that are used to capture the values specified at their position in the URL. The captured values are populated in the req.params object, with the name of the route parameter specified in the path as their respective keys.
```js
app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params)
})
```
5-Route handlers:

You can provide multiple callback functions that behave like middleware to handle a request. The only exception is that these callbacks might invoke next('route') to bypass the remaining route callbacks. You can use this mechanism to impose pre-conditions on a route, then pass control to subsequent routes if there’s no reason to proceed with the current route.

- A single callback function can handle a route. For example:
```js
app.get('/example/a', (req, res) => {
  res.send('Hello from A!')
})
```
- More than one callback function can handle a route (make sure you specify the next object). For example:

```js
app.get('/example/b', (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from B!')
})
```

6-Response methods:

The methods on the response object (res) in the following table can send a response to the client, and terminate the request-response cycle. If none of these methods are called from a route handler, the client request will be left hanging.

- res.download() :  Prompt a file to be downloaded.
- res.end() : End the response process.
- res.json() :	Send a JSON response.
- res.jsonp()	Send a JSON response with JSONP support.
- res.redirect()	Redirect a request.
- res.render()	Render a view template.
- res.send()	Send a response of various types.
- res.sendFile()	Send a file as an octet stream.
- res.sendStatus()	Set the response status code and send its - - string representation as the response body.

7-app.route()  :

You can create chainable route handlers for a route path by using app.route(). Because the path is specified at a single location, creating modular routes is helpful, as is reducing redundancy and typos. For more information about routes, see: Router() documentation.

Here is an example of chained route handlers that are defined by using app.route().

```js
app.route('/book')
  .get((req, res) => {
    res.send('Get a random book')
  })
  .post((req, res) => {
    res.send('Add a book')
  })
  .put((req, res) => {
    res.send('Update the book')
  })
```


8-express.Router:

Use the express.Router class to create modular, mountable route handlers. A Router instance is a complete middleware and routing system; for this reason, it is often referred to as a “mini-app”.

The following example creates a router as a module, loads a middleware function in it, defines some routes, and mounts the router module on a path in the main app.

Create a router file named birds.js in the app directory, with the following content:

```js
const express = require('express')
const router = express.Router()

// middleware that is specific to this router
router.use((req, res, next) => {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', (req, res) => {
  res.send('Birds home page')
})
// define the about route
router.get('/about', (req, res) => {
  res.send('About birds')
})

module.exports = router
```

---
