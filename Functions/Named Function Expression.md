
# Named Function Expression
Let’s take an ordinary Function Expression:
```js
let sayHi = function(who) {
  alert(`Hello, ${who}`);
};
```
And add a name to it:
```js
let sayHi = function func(who) {
  alert(`Hello, ${who}`);
};

sayHi("John"); // Hello, John
```
The function is still available as `sayHi()`:

Adding the name `func` after function did not make it a Function Declaration. This is a *Named Function Expression*.

There are two benefits in it: **we can call `func` inside the current function** and **it's not available from outside**. The specification guarantees that it will always reference the current function.

```js
let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest");
  }
};

let welcome = sayHi;
sayHi = null;

welcome(); // Hello, Guest (nested call works)
```