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
support for modern javascript. [Babel](https://babeljs.io/) is a compiler that translates your code into compatible code for
most browsers

...
