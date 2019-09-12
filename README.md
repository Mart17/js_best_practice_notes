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
* ```javascript
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

# Chapter3: JavaScript Performance Optimization Tips: An Overview
* Mobile - Testing in Chrome DevTools’ device mode isn’t a valid substitute to testing on a real device
* Even if you are testing on real mobile device don't use high-end device, for performance testing use rather something low-end
* Measure performance with the [RAIL model](https://developers.google.com/web/fundamentals/performance/rail)
* Load less JavaScript and load smarter
* Before you dive into optimizing your code, consider what you’re building. Does your code need to do thousands
of operations per second? Do you absolutely need to use a JS framework?
* Avoid using JS animation frameworks for everything. Use it only if you can't implement the animation using regular CSS transitions and animations
* Try shipping JS smarter. Ship what you need, when you need it
  * Webpack - [code splitting](https://webpack.js.org/guides/code-splitting/) &  [dynamic imports](https://webpack.js.org/guides/code-splitting/#dynamic-imports)

# ...
