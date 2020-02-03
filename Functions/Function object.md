# Function object, NFE
In JavaScript, functions are objects.

### The “name” property
Function’s name is accessible as the “name” property:
```js
function sayHiFD() {
  alert("Hi");
}

alert(sayHiFD.name); // sayHi

// OR

let sayHiFE = function() {
  alert("Hi");
};

alert(sayHiFE.name); // sayHi
```

Object methods have names too:
```js
let user = {
  sayHi() {},
  sayBye: function() {}
}

alert(user.sayHi.name); // sayHi
alert(user.sayBye.name); // sayBye
  ```

### The “length” property
Property “length” that returns the number of function parameters, for instance:
```js
function f1(a) {}
function f2(a, b) {}
function many(a, b, ...more) {}

alert(f1.length); // 1
alert(f2.length); // 2
alert(many.length); // 2, rest parameters are not counted
```

### Custom properties
We can also add properties of our own.
```js
function sayHi() {
  alert("Hi");
  sayHi.counter++;
}
sayHi.counter = 0; // initial value

sayHi(); // Hi
sayHi(); // Hi

alert( `Called ${sayHi.counter} times` ); // Called 2 times
```
