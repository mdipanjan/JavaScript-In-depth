
## JavaScript Function Concepts and Questions

1. [What are Arrow functions in JavaScript and how it is different from regular functtions.](#Q1)
1. [What is a pure function and side effect.](#Q2)
1. [What are Higher-Order functions.](#Q3)
1. [What is a first class function.](#Q4)
1. [What is a first order function.](#Q5)
1. [What is an IIFE or Immediately Invoked Function Expression.](#Q6)
1. [What is call/apply/bind.](#Q7)
1. [What is closure in JavaScript](#Q8)
1. [What is currying function.](#Q9)
1. [Pollyfills for in built functions](#Q10)
1. [some, find, includes and other in built Javascript methods](#Q11)
1. [Split, Replace, Splice, Slice](#Q12)
1. [What is an Eval Function](#Q13)





###  Q1. 
### What are Arrow functions in JavaScript and how it is different from normal functions.

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

<!-- ###  Q2. What is a pure function and side effect. -->

### Q3. 
### What are Higher-Order functions.

A `Higher-order` function is noting but a regular function which can take a function as an argument or can return a function as a value.

Here's an simple example of `Higher-order` function:

```js
  
  // print function takes a function as an argument
  function print(helper){
    helper();
  }

  // We're invoking the print function by passing a function as an argument
  print(function(){
    console.log('Print value here...')
  })
  
  //Here printName returns a function as a value;
  function printName(name) {
    return function() {
      console.log(`Hello ${name}..`);
    }
  }
  let result = printName('John Doe');
  result();


```
So lets understand how `Higher-order` function with this example.

We've an array of numbers

```js
  let data = [10,20,4,8];
```
and we need to multiply the values by 2 and return the new array, 
so we can do it like this.

```js
  function multiply(data, num) {

    let final = [];
    for(let item of data) {
      final.push(item * num)
    }
    return final
  }
  multiply(data, 2);
  // [20,40,8,16]
```
Now if we want to divide elements by 2, we can just make a new function which will divide numbers by 2,

```js

  function divide(data, num) {

    let final = [];
    for(let item of data) {
      final.push(item / num)
    }
    return final
  }
  divide(data, 2);
  // [5,10,2,4]
```
So we're dupliacting the logic, we can do it like this

```js
  function operate(data, operation, num){

    let final = [];

    if(operation === 'multi') {
      for(let item of data) {
        final.push(item * num)
      }
    }else if(operation === 'divi') {
      for(let item of data) {
        final.push(item / num)
      }
    }
    return final;
  }
  operate(data, 'multi', 2);
  // [20,40,8,16] 
  operate(data, 'divi', 2);
  // [5,10,2,4]
 
```
Now our problem is solved, but we'retaking more parameters and if we want to do addition, deletion we need to make some more `if` `else` conditions. Which will make our code covoluted. So now we can use the power of `Higher-order` function here.

```js

  //We're creating pure functions here
  // function to multiply values
  function multiply(item, num) {
    return item * num;
  }
  // function to divide values
  function divide(item, num) {
    return item / num;
  }

```
Now we change the operate function to a `Higher-order` function here,

```js
  function operate(data, operation, num) {

    let final = [];

    for(let item of data) {
      final.push(operation(item, num));
    } 
    return final;
  }
  operate(data, multiply, 2);
  // [20, 40, 8, 16]
  operate(data, divide, 2);
  // [5, 10, 2, 4]
```
So now we're having similar structure like before, and passing data as the first parameter and then the function as second parameter and the number.
If we had to do add or decrement we can do it easily and we can just introduce seperate pure functions for those. 


**Built-In Higher-order functions in JavaScript:**

Many of the popular array methods are Higher-order functions basically. `map`, `reduce`, `filter` these are HoF. They take a function as an argument and operate on the array elements.

```js
  let data = [10,20,30,40];

  let final = data.map(function(item){
    return item * 2;
  })
  // [20,40,60,80]
```


