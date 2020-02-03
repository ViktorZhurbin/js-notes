# Ordinary Functions

The following code shows three ways of doing (roughly) the same thing: creating an ordinary function.
```js

// Function declaration (a statement)
function ordinary1(a, b, c) {
  // ···
}

// const plus anonymous function expression
const ordinary2 = function (a, b, c) {
  // ···
};

// const plus named function expression
const ordinary3 = function myName(a, b, c) {
  // `myName` is only accessible in here
};
```

In case of object methods, an ordinary function is initialized with its own `this=undefined`, which shadows `this` of the object:
```js
const person = {
    name: 'Jill',
    ordinaryFunc: function () {
        return this.name
    },
    arrowFunc: () => this.name;
}

person.ordinaryFunc(); // TypeError: Cannot read property 'name' of undefined
person.arrowFunc(); // 'Jill'
```

### The Special Variable `arguments`

### Function Expression VS Function Declaration

A Function Expression is created when the execution reaches it and is usable only from that moment.

A Function Declaration can be called earlier than it is defined (hoisted). When JavaScript prepares to run the script, it first looks for global Function Declarations in it and creates the functions. And after all Function Declarations are processed, the code is executed. So it has access to these functions.

For example, this works:
```js
sayHi("John"); // Hello, John

function sayHi(name) {
  alert( `Hello, ${name}` );
}
```
This doesn't:
```js
sayHi("John"); // error!

let sayHi = function(name) {  // (*) no magic any more
  alert( `Hello, ${name}` );
};
```