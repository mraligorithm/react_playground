# Let and Const

The JavaScript let and const keywords are quite similar, in that they create block-level scope. However, they do differ a bit in the way that they behave. For example, the JavaScript let keyword is similar to the var keyword in that assignments can be changed. On the other hand, the JavaScript const keyword differs in that assignments can not be changed. So, once you declare a variable using the const keyword, you cannot re-assign a value to that variable. This does not mean that the variable is immutable. If you assign an object to a variable using the const keyword, you can mutate that object. You just can’t re-assign that variable with a new value. Let’s take a look at some examples.

For testing go to https://jsbin.com/?js,console

```
var i = 100;

{
    let i = 50;

    console.log('(A) i = ' + i); //50
}

console.log('(B) i = ' + i); //100

```