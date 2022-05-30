## Node.js :

1-  Is an open-source, cross-platform runtime environment that allows developers to create all kinds of server-side tools and applications in JavaScript.

2-  Node has a number of benefits:
 - Great performance! Node was designed to optimize throughput and scalability in web applications and is a good solution for many common web-development problems.

- ode is written in "plain old JavaScript", which means that less time is spent dealing with "context shift" between languages when you're writing both client-side and server-side code.

- JavaScript is a relatively new programming language and benefits from improvements in language design when compared to other traditional web-server languages 

- The node package manager (NPM) provides access to hundreds of thousands of reusable packages. It also has best-in-class dependency resolution and can also be used to automate most of the build toolchain.

- Node.js is portable. It is available on Microsoft Windows, macOS, Linux, Solaris, FreeBSD, OpenBSD, WebOS, and NonStop OS. Furthermore, it is well-supported by many web hosting providers, that often provide specific infrastructure and documentation for hosting Node sites.

- It has a very active third party ecosystem and developer community, with lots of people who are willing to help.

3 -You can use Node.js to create a simple web server using the Node HTTP package :

- Create a file called  for Ex:"hello.js" and paste the following code into it:
```js

// Load HTTP module
const http = require("http");

const hostname = "127.0.0.1";
const port = 8000;

// Create HTTP server
const server = http.createServer(function(req, res) {

   // Set the response HTTP header with HTTP status and Content type
   res.writeHead(200, {'Content-Type': 'text/plain'});

   // Send the response body "Hello World"
   res.end('Hello World\n');
});

// Prints a log once the server starts listening
server.listen(port, hostname, function() {
   console.log(`Server running at http://${hostname}:${port}/`);
})
```

- To run your server Go back to the terminal and type the following command:
```js
node hello.js
```

- Finally, navigate to http://localhost:8000 in your web browser; you should see the text "Hello World" in the upper left of an otherwise empty web page.
---
## Express :
1- Express is the most popular Node web framework, and is the underlying library for a number of other popular Node web frameworks

2-  It provides mechanisms to:
 - Write handlers for requests with different HTTP verbs at different URL paths (routes).
 
 - Integrate with "view" rendering engines in order to generate responses by inserting data into templates.

- Set common web application settings like the port to use for connecting, and the location of templates that are used for rendering the response.

3- Where did Node and Express come from?

- Node was initially released, for Linux only, in 2009. The NPM package manager was released in 2010, and native Windows support was added in 2012. Delve into Wikipedia if you want to know more.

- Express was initially released in November 2010 and is currently on version 4.17.3 of the API (with 5.0 in "beta"). You can check out the changelog for information about changes in the current release, and GitHub for more detailed historical release notes.

4- To use Express:
 - . 
 ```js
  const express = require('express');
const app = express();
const port = 3000;

app.get('/', function(req, res) {
  res.send('Hello World!')
});

app.listen(port, function() {
  console.log(`Example app listening on port ${port}!`)
});
```
- Importing and creating modules :
```js 
const express = require('express');
const app = express();

```

- Exporting a methods form object :
```js 
exports.method-name_one = function();
exports.method-name_two = function();
```




- Export a complete object :
```js
module.exports = {
method-name_one: function(),
method-name_two: function();
}
```

- Use express router :
```js
// wiki.js - Wiki route module

const express = require('express');
const router = express.Router();

// Home page route
router.get('/', function(req, res) {
res.send('Wiki home page');
});

// About page route
router.get('/about', function(req, res) {
res.send('About this wiki');
});

module.exports = router;

and you can access it:
const wiki = require('./wiki.js');
// ...
app.use('/wiki', wiki);
```

5-Using middleware :

Middleware is used extensively in Express apps, for tasks from serving static files to error handling, to compressing HTTP responses. Whereas route functions end the HTTP request-response cycle by returning some response to the HTTP client, middleware functions typically perform some operation on the request or response and then call the next function in the "stack", which might be more middleware or a route handler. The order in which middleware is called is up to the app developer.

- 
 ```js
 const express = require('express');
const app = express();

// An example middleware function
let a_middleware_function = function(req, res, next) {
  // ... perform some operations
  next(); // Call next() so Express will call the next middleware function in the chain.
}

// Function added with use() for all routes and verbs
app.use(a_middleware_function);

// Function added with use() for a specific route
app.use('/someroute', a_middleware_function);

// A middleware function added for a specific HTTP verb and route
app.get('/', a_middleware_function);

app.listen(3000);
 ```
-
```js
app.use(express.static('public'));

```

---
## Handiling errors:
- Errors are handled by one or more special middleware functions that have four arguments, instead of the usual three: (err, req, res, next). For example:
```js
app.use(function(err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```
---
## Using database:

- Express apps can use any database mechanism supported by Node . There are many options, including PostgreSQL, MySQL, Redis, SQLite, MongoDB, etc.
 
 1- 
 ```js
 $ npm install mongodb
 ```
 2-
 ```js
 //this works with older versions of mongodb version ~ 2.2.33
const MongoClient = require('mongodb').MongoClient;

MongoClient.connect('mongodb://localhost:27017/animals', function(err, db) {
  if (err) throw err;

  db.collection('mammals').find().toArray(function (err, result) {
    if (err) throw err;

    console.log(result);
  });
});

//for mongodb version 3.0 and up
const MongoClient = require('mongodb').MongoClient;
MongoClient.connect('mongodb://localhost:27017/animals', function(err, client){
   if(err) throw err;

   let db = client.db('animals');
   db.collection('mammals').find().toArray(function(err, result){
     if(err) throw err;
     console.log(result);
     client.close();
   });
});
 ```
 ---
 
