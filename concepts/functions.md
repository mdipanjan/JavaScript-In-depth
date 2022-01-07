
## JavaScript Function Concepts and Questions

1. [What are Arrow functions in JavaScript and how it is different from regular functtions.](#Q1)




###  Q1. What are Arrow functions in JavaScript and how it is different from normal functions.

An arrow function is a compact and alternate way of writing function expression.

How it differs from regular functions:
- Arrow functions don't have their own bindings to `this` and `super`.
- We can not use arrow function as `constructor`.
- We use `call`, `apply`, `bind` to establish scopes, but for arrow functions we can not do that.
- We should not use arrow function as method.

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
1. Why we should not use arrow function as method

```js

  /*
    Here printLength1 method uses normal function, 
    so this will have binding with the obj Object.

    For printLength2 this will refer to the global window Object, 
    as arrow functions don't have their own bindingf to this.
  */

  let obj = {
    length: 100,
    printLength1: function() {
      console.log(this);
      // {length: 100, printLength1: ƒ, printLength2: ƒ}
    },
    printLength2: () => {
      console.log(this);
      // window{...}
    }
  }
```
2. Why `call`, `apply`, `bind` are not suitable for arrow functions.

```js
  let obj = {
    length: 10
  }
  // we're setting length to window object
  window.length = 111;

  let multiply = function(a,b) { 
    console.log(this.length * a * b);
  }
  //setting the scope as obj
  multiply.call(obj, 1, 2);
  // 20

  //can not set the scope as obj, so the scope will be window object
  let arrowMultiply = (a,b) => {
    console.log(this.length * a * b)
  }
  arrowMultiply.call(obj, 1, 2);
  // 222

```

