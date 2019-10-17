# JavaScript: Best Practice - Book Notes
Published by [SitePoint](https://www.sitepoint.com/) | Get full version of this book [here](https://www.sitepoint.com/premium/books/javascript-best-practice)

Notes by [Martin Suja](https://github.com/Mart17)

___

# Chapter 1: The Anatomy of a Modern JavaScript Application

## ES6 (ES2015)
Changes added:

* Two additional ways to declare variables:
  * `let` - limits the scope of variable to the block
  * `const` - variable which value cannot be changed once it has
  been declared
* Arrow function:
  * `const add = (param1, param2) => param1 + param2;`
  * inherits the value of `this` from the context in which they are defined
* [Class](https://www.sitepoint.com/object-oriented-javascript-deep-dive-es6-classes/) - syntax for defining the state and behavior of objects
* [Promise](https://www.sitepoint.com/overview-javascript-promises/) - represents values that don’t exist at the moment of the computation but that may be
available later (asynchronous calls)

## Modules
* Create separate files with the functionality you want, and export just certain parts to make them available to your application
  ```javascript
  // lib/math.js
  export const pi = 3.141593;
  // app.js
  import pi from "lib/math";
  console.log("Value of π is " + pi)
  ```

## Package Management
* Easy to find and install third-party libraries
* Use [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/lang/en/)

## Build Tools
* [Webpack](https://webpack.js.org/) is a module bundler to combine files together into one or more files
* Some browsers have only partial or no
support for modern javascript. [Babel](https://babeljs.io/) is a compiler that translates your code into compatible code for most browsers

## Application Architecture
* Old-style web applications were usually done by sending multiple pages from a web server, and when a
lot of dynamism was needed, content was loaded via Ajax by replacing chunks of HTML according to user actions.
* [SPA (Single Page Application)](https://en.wikipedia.org/wiki/Single-page_application) - the UI is rendered
entirely client-side (no reloading), but it makes the initial load slow for the client. The only thing that changes is the data inside the application (remote API via Ajax)
* [Isomorphic JS](https://en.wikipedia.org/wiki/Isomorphic_JavaScript) - most of the code
can be executed both on the server and the client, SPA is downloaded in the background

# Chapter 2: Clean Code with ES6 Default Parameters & Property Shorthands

## ES6 Default Parameters
* Initialize functions with default values that are used when an argument is either omitted or `undefined`
* `function multiply (a, b = 2) { ...`
* `function foo (num = 1, multi = multiply(num)) { ...`
* ```javascript
  function createElement (tag = 'div', {
    content = 'Very default',
    classNames = ['module-text', 'special']
  } ...
  ```

## ES6 Property Shorthands
* It’s common to prepare some variables and add them to said object:
  ```javascript
  const a = 'foo', b = 42, c = function () {};
  ```
  Previously we would use constants:
  ```javascript
  const alphabet = {
    a: a,
    b: b,
    c: c
  };
  ```
  Now with the new shorthand:
  ```javascript
  const alphabet = { a, b, c };
  ```
* Instead of this:
  ```javascript
  // data is an object with properties
  const target = data.target;
  const veryLongProperty = data.veryLongProperty;
  useData({ target: target, property: veryLongProperty })
  ```
  you can just do this:
  ```javascript
  const { target, veryLongProperty: property } = data;
  useData({ target, property });
  ```
* Property shorthands can also be applied to method
definitions inside an object:
  ```javascript
  const module = {
    bar (value) {...}
  }
  ```

# Chapter 3: JavaScript Performance Optimization Tips: An Overview
* Mobile - Testing in Chrome DevTools’ device mode isn’t a valid substitute to testing on a real device
* Even if you are testing on real mobile device don't use high-end device, for performance testing use rather something low-end
* Measure performance with the [RAIL model](https://developers.google.com/web/fundamentals/performance/rail)
* Load less JavaScript and load smarter
* Before you dive into optimizing your code, consider what you’re building. Does your code need to do thousands
of operations per second? Do you absolutely need to use a JS framework?
* Avoid using JS animation frameworks for everything. Use it only if you can't implement the animation using regular CSS transitions and animations
* Try shipping JS smarter. Ship what you need, when you need it
  * Webpack - [code splitting](https://webpack.js.org/guides/code-splitting/) &  [dynamic imports](https://webpack.js.org/guides/code-splitting/#dynamic-imports)
  * You can have one bundle with packages to patch up missing features in older browsers and another without them, so you save almost 100 kilobytes to your JS bundle

# Chapter 4: JavaScript Design Patterns: The Singleton
* Singleton pattern restricts the instantiation of a class to one object. A singleton should be immutable by the consuming code, and there should be no danger of instantiating more than one of them
  ```javascript
  class UserStore {
    constructor() {
      // here we check whether or not we’ve already instantiated a UserStore
      // if we have, we won’t create a new one
      if (! UserStore.instance) {
        this._data = [];
        UserStore.instance = this;
      }

      return UserStore.instance;
    }

    add(item) {
      this._data.push(item);
    }

    get(id) {
      return this._data.find(d => d.id === id);
    }
  }

  const instance = new UserStore();
  // result of using Object.freeze is that its methods cannot be changed, nor can new methods or properties be added to it
  Object.freeze(instance);

  // we’re taking advantage of ES6 modules, so we know exactly where UserStore is used
  export default instance;
  ```

# Chapter 5: Object Creation: Patterns and Best Practices
* The old ways of creating JavaScript objects are now considered to be not the best solution. There're problems with repetition, performance and used memory
* Using ES6 class syntax you can create JavaScript objects in a standard, fast, simple and clean way
  ```javascript
  class Thing {
    constructor() {
      this.x = 42;
    }

    g() {}
  }

  const o = new Thing();
  ```

# Chapter 6: Best Practices for Using Modern JavaScript Syntax
* Use `const` for simple number or string variables to initialize and never alter, or for named functions and classes that you expect to define once and then leave closed for modification. Otherwise, use `let` for most variable
declarations — especially those you want to be bounded by the scope in which they were defined
* Modern JavaScript split out the behavior of the traditional
function into arrow functions and classes. This allows programmers to choose whether they would prefer to follow a more functional programming paradigm or use a more [object-oriented](https://www.sitepoint.com/object-oriented-javascript-deep-dive-es6-classes/) approach:
  * A `class` needs to be declared in the script before it is instantiated with a `new` keyword - Prototypal inheritance using the `function` keyword works in JavaScript even if it’s defined later in the script
  * Arrow functions encapsulate several qualities that can make calling them more convenient, and leave out other behavior that isn’t as useful when calling a function. For example, an arrow function inherits both `this` and `arguments` from the contexts in which it’s called. That’s great for situations like event handling. Traditional functions have forced programmers to bind a function to an existing `this` by using `.bind(this)`

# Chapter 7: Flow Control in Modern JS: Callbacks to Promises to Async/Await

## Promises
* A series of two or more asynchronous calls can be completed in series by nesting callback functions, but that can introduce [callback hell](http://callbackhell.com/)
* [Promises](https://www.sitepoint.com/overview-javascript-promises/) provide a clearer syntax. Asynchronous callback-based functions
must return a Promise object that promises to run one of two functions at some point in the future:
  * `resolve` is run when processing successfully completes
  * `reject` is run when a failure occurs (optional)
  *  
  ```javascript
  function asyncDBconnect(param) {
    // function immediately returns a new Promise
    return new Promise((resolve, reject) => {

      // it runs either resolve() or reject() once a connection is established or fails
      db.connect(param, (err, connection) => {
        if (err) reject(err);
        else resolve(connection);
      });
    });
  }
  ```
* Anything that returns a Promise can start a series of asynchronous function call defined in `.then()` methods:
  ```javascript
  asyncDBconnect('http://localhost:1234')
    .then(asyncGetSession)
    .then(asyncGetUser)
    .then(result => {
      console.log('complete');
      // result passed to next .then()
      return result;
    })
    .catch(err => {
      // called on any reject
      console.log('error', err);
    });
  ```
* ES2018 introduces a `.finally()` method, which runs any final logic regardless of the outcome:
  ```javascript
  .then(doSomething2)
  .catch(err => {
      console.log(err);
  })
  .finally(() => { ... })
  ```
*  Promise `.then()` methods run asynchronous functions one after the other. If the order doesn’t matter it’s faster to launch all asynchronous functions at the same time with `Promise.all()`:
  ```javascript
  // accepts an array of functions and returns another Promise
  Promise.all([ async1, async2, async3 ])
    .then(values => {
    // array of resolved values
    console.log(values);
  })
  ```
*  `Promise.all()` terminates immediately if any one of the asynchronous functions calls reject
* `Promise.race()` is similar to `Promise.all()`, except that it will resolve or reject as soon as the first Promise resolves or rejects

## Async/Await
* `async` and `await` make using Premises without using `.then()` cleaner
  ```javascript
  // the outer function must be preceded by an async statement
  async function connect() {
    try {
      // calls to asynchronous functions must be preceded by await
      const connection = await asyncDBconnect('http://localhost:1234'),
      log = await asyncLogAccess(connection);
      return log;
    }

    catch (e) {
      console.log('error', err);
      return null;
    }
  }

  // run connect (self-executing async function)
  (async () => { await connect(); })();
  ```
* `async` functions will silently exit if you omit a `try` / `catch` around any `await`
which fails. If you have a long set of asynchronous await commands, you may need multiple `try` / `catch` blocks

# Chapter 8: JavaScript’s New Private Class Fields, and How to Use Them

* A class is a template which defines how objects of that type behave
* A `constructor` method is run when an object of this type is created, and it typically defines initial properties:
  ```javascript
  class Animal {
    constructor(name = 'anonymous') {
      this.name = name;
    }
    // ...
  }

  // Create new object from this class
  const rex = new Animal('Rex');
  ```
* Setters are methods used to define values only, Getters are
 methods used to return a value only:
  ```javascript
  class Dog extends Animal {
    // constructor(name) { ...

    // setter
    set eats(food) {
      this.food = food;
    }

    // getter
    get dinner() {
      return `${this.name} eats ${this.food || 'nothing'} for dinner.`;
    }
  }

  const rex = new Animal('Rex');
  // call Setter
  rex.eats = 'anything';
  // call Getter
  console.log(rex.dinner);
  ```
* It’s often practical to use one class as the base for another. `super` refers to the parent class and is usually called in the `constructor`:
  ```javascript
  class Dog extends Animal {
    constructor(name) {
      // super used to call the Animal constructor
      super(name);
    }
    // ...
  }
  ```
* Defining a method with the `static` keyword allows it to be called on a class without creating an object instance by adding properties to the class definition:
  ```javascript
  class Dog extends Animal {
    //  ...

    // return number of dog objects
    static get COUNT() {
      return Dog.count;
    }
  }

  // static property added after class is defined
  Dog.count = 0;

  // = Dogs defined: 0
  console.log(`Dogs defined: ${Dog.COUNT}`);

  const don = new Dog('Don');
  // = Dogs defined: 1
  console.log(`Dogs defined: ${Dog.COUNT}`);
  ```
* In [ESnext](https://en.wikipedia.org/wiki/ECMAScript#ES.Next), private class fields are defined using a hash `#` prefix:
  ```javascript
  class MyClass {
    // public
    a = 1;
    // private
    #b = 2;
    // private and static
    static #c = 3;

    //...
  }
  ```
