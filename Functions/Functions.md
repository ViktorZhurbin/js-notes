### Never add a newline between return and the value

For a long expression in return, it might be tempting to put it on a separate line, like this:
```js
return
    (some + long + expression + or + whatever * f(a) + f(b))
 ```
That doesn’t work, because JavaScript assumes a semicolon after return. That’ll work the same as:
```js
return; // note ;
    (some + long + expression + or + whatever * f(a) + f(b))
 ```
So, it effectively becomes an empty return.

If we want the returned expression to wrap across multiple lines, we should start it at the same line as return. Or at least put the opening *parentheses* there as follows:

```js
return (
    some + long + expression
    + or +
    whatever * f(a) + f(b)
)
```

And it will work just as we expect it to.

---
### Prefixes

It is a widespread practice to start a function with a *verbal prefix* which vaguely describes the action. There must be an agreement within the team on the meaning of the prefixes.

For instance, functions that start with `show` usually show something.

Function starting with…

- `get…` – return a value,
- `calc…` – calculate something,
- `create…` – create something,
- `check…` – check something and return a boolean, etc.

---
### One function – one action
**Functions == Comments**

Functions should be short and do exactly one thing suggested by its name, no more.

A small function is not only easier to test and debug – it's easier to understand what it does by just reading the name.

### Function Expression vs Function Declaration
A Function Expression is created when the execution reaches it and is usable only from that moment.
A Function Declaration can be called earlier than it is defined. When JavaScript prepares to run the script, it first looks for global Function Declarations in it and creates the functions. And after all Function Declarations are processed, the code is executed. So it has access to these functions.

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