
## JavaScript Function Concepts and Questions

1. [What are Arrow functions in JavaScript and how it is different from regular functtions.](#Q1)




###  Q1. What are Arrow functions in JavaScript and how it is different from normal functtions.

An arrow function is a compact and alternate way of writing function expression.

How it differs from regular functions:
- Arrow functions don't have their own bindings to `this` and `super`.
- We can not use arrow function as `constructor`.
- we use `call`,`apply`, `bind` to establish scopes, but for arrow functions we can not do that.
- This are best used as non method functions.

```js

  // Anonymous function
  function (a, b) {
    return a * b;
  }

  (a, b) => {
    return a * b;
  }

  // Named function

  function multiply(a, b) {
    return a * b;
  }

  let multiply = (a, b) => {
    return a * b;
  }

```


