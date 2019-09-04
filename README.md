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
  ```
  const add = (param1, param2) => param1 + param2;
  ```
  * inherits the value of `this` from the context in which they are defined
* [Class](https://www.sitepoint.com/object-oriented-javascript-deep-dive-es6-classes/) - syntax for defining the state and behavior of objects
* [Promise](https://www.sitepoint.com/overview-javascript-promises/) - represents values that don’t exist at the moment of the computation but that may be
available later (asynchronous calls)

...
