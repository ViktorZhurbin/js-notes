### Terminology: parameters vs. arguments

The term parameter and the term argument basically mean the same thing. If you want to, you can make the following distinction:

- **Parameters are part of a function definition**. They are also called *formal parameters* and *formal arguments*.

- **Arguments are part of a function call**. They are also called *actual parameters* and *actual arguments*.


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
