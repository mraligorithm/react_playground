# Arrow Function

## Syntax

Instead of the function keyword, arrow function uses an arrow (=>) made up of an equal sign and a greater-than character (not to be confused with the greater-than-or-equal operator, which is written >=).

```
// ES5 Regular function
let add = function(a, b) { 
  return a + b;
};

// ES6 Arrow function
let add = (a, b) => { return a + b };
```

It is important to note that arrow functions, introduced in ES6 in 2015, are anonymous, which means that they are not named. The example above shows the anonymous arrow function with two arguments a and b that returns a + b.

## One argument
If we have only one argument, then parentheses around parameters can be omitted, making that even shorter.

```
// ES5 Regular function
let double = function(n) { return n * 2 }  
alert( double(3) ); // 6

// ES6 Arrow function
let double = n => n * 2; 
alert( double(3) ); // 6
```

## No arguments
If you have no arguments, here’s how you can go about it.

```
// ES5 Regular function
function sayHi() {
  return alert("Hello!");
}
sayHi();

// ES6 Arrow function
let sayHi = () => alert("Hello!");
sayHi();

//Or

// ES6 Arrow function
let sayHi = _ => alert("Hello!");
sayHi();
```

## Multiline arrow functions

Sometimes we need something a little bit more complex, like multiple expressions or statements. It is also possible, but we should enclose them in curly braces. Then use a normal return within them.

```
const power = (base, exponent) => {      // the curly brace opens a 
  let result = 1;                           //multiline function
  for (let count = 0; count < exponent; count++) {
    result *= base;                  
  }.                                // if we use curly braces, then
  return result;                     // we need an explicit "return"
};
```

```
let sum = (a, b) => {  // the curly brace opens a multiline function
  let result = a + b;  // if we use curly braces, then we need an 
  return result;          //explicit "return"
}
alert(sum(5, 7));    //12
```

-----

## “this” binding

When discussing the arrow functions it is important to mention that unlike regular functions, arrow functions do not have their own this. Arrow functions don’t redefine the value of this within their function body. This makes it a lot easier to predict their behavior when passed as callbacks, and prevents bugs caused by use of this within callbacks.

In classic function expressions, the this keyword is bound to different values based on the context in which it is called. With arrow functions, however, this is lexically bound. It means that it uses this from the code that contains the arrow function, in other words, this means the same thing within the function body as it does outside of it.

For example, look at the setTimeout function below:

```
// ES5
let obj = {
  id: 42,
  counter: function counter() {
    setTimeout(function() {
      console.log(this.id);
    }.bind(this), 1000);
  }
};
```

In the ES5 example, .bind(this) is required to help pass the this context into the function. Otherwise, by default this would be undefined.

```
// ES6
let obj = {
  id: 42,
  counter: function counter() {
    setTimeout(() => {
      console.log(this.id);
    }, 1000);
  }
};
```
ES6 arrow functions can’t be bound to a this keyword, so it will lexically go up a scope, and use the value of this in the scope in which it was defined.


## Argument binding

Unlike regular functions arrow functions do not have an arguments binding. However, they have access to the arguments object of the closest non-arrow parent function. Named and rest parameters are heavily relied upon to capture the arguments passed to arrow functions.

The arguments is a reference of the name in the enclosing scope, for example:

```
function show() {
    return x => x + arguments[0];
}
let display = show(10, 20);
let result = display(5);
console.log(result); // 15
```

The arrow function inside the showMe() function references the arguments object. However, this arguments object belongs to the show() function, not the arrow function.

## Using “new” keyword

Regular functions created using function declarations or expressions are constructible and callable. Since regular functions are constructible, they can be called using the new keyword.

For example, the Car() function creates instances of a car:
```
function Car(color) {
  this.color = color;
}
const blueCar = new Car('blue');
blueCar instanceof Car; // => true
```

Car is a regular function, and when invoked with new keyword, it creates new instances of Car type.

Not having this naturally means another limitation for arrow functions: the arrow functions are only callable and not constructible, i.e arrow functions can never be used as constructor functions. Hence, they can’t be called with new keyword.

If you try to invoke an arrow function prefixed with new keyword, JavaScrip throws an error:

```
const Car = (color) => {
  this.color = color;
};
const blueCar = new Car('blue');  //TypeError: Car is not a       
                                    //constructor
```

Invoking new Car('blue'), where Car is an arrow function, throws TypeError: Car is not a constructor.

## Duplicate named parameters

Regular function can have duplicate named parameters:


`function add(a, a){}`

However, it isn’t possible when using strict mode:

```
'use strict';
function add(a, a){}
// SyntaxError: duplicate formal argument a
```

Arrow functions can never have duplicate named parameters, whether in strict or non-strict mode.
```
(a, a) => {}
// SyntaxError: duplicate argument names not allowed in this context
```

# Conclusion
You got familiar with two different styles for declaring functions: function expressions and arrow functions. Understanding the differences between regular and arrow functions helps choose the right syntax for specific needs.

Arrow functions excel when a simple change or operation needs to be used repeatedly. But they’re certainly used to write long, full functions too!

Arrow functions:
* Do not have this
* Do not have arguments
* Can’t be called with new

That’s because they are meant for short pieces of code that do not have their own “context”, but rather work in the current one. And they really shine in that use case.

Resources:

* 📖 https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions
* 📖 https://developer.mozilla.org/en-US/docs/Glossary/IIFE
* 📖 https://www.w3schools.com/js/js_functions.asp
* 📖 https://www.w3schools.com/js/js_arrow_function.asp
* 📖 https://stackoverflow.com/questions/34361379/are-arrow-functions-and-functions-equivalent-interchangeable
* 📖 https://www.freecodecamp.org/news/when-and-why-you-should-use-es6-arrow-functions-and-when-you-shouldnt-3d851d7f0b26/
* 📖 https://eloquentjavascript.net/
* 📖 https://www.javascripttutorial.net/es6/javascript-arrow-function/
* 📖 https://javascript.info/arrow-functions-basics