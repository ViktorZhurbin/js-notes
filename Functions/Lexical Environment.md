# Closure & Lexical Environment
>A closure is a function that remembers its outer variables and can access them.

### Variables
In JavaScript, every running function, code block `{...}`, and the script as a whole have an internal (hidden) associated object known as the *Lexical Environment*.

>Lexical Environment is a specification object: it only exists “theoretically” in the language specification to describe how things work. We can’t get this object in our code and manipulate it directly.

Lexical Environment consists of two parts:

- Special internal **object that stores all local variables** as its properties (and some other information like the value of `this`), called *Environment Record*.
<sub>A “variable” is just a property of the Environment Record.</sub>
<br />

- **Reference to the outer lexical environment**, the one associated with the outer code.
<sub>Global Lexical Environment has no outer reference, so it equals `null`. </sub>
<br />

### Function Declarations
A function is also a value, like a variable.

**The difference is that a Function Declaration is instantly fully initialized.**
We can use a function, declared as Function Declaration, even before the declaration itself.

This does not apply to Function Expression and Arrow Function since they are assigned to variables.

### Inner and outer Lexical Environment
When a function runs, at the beginning of the call, a new Lexical Environment is created automatically to store local variables and parameters of the call.

During the function call we have **two Lexical Environments**: the **inner** one and the **outer** (global) one. The inner Lexical Environment has a reference to the outer one.

**When the code wants to access a variable – the inner Lexical Environment is searched first, then the outer one, then the more outer one and so on until the global one.**

### Returning a function
Let’s return to the makeCounter example.

```js
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
```

At the beginning of each `makeCounter()` call, a new Lexical Environment object is created, to store variables for this `makeCounter` run.

So we have two nested Lexical Environments:
- LexicalEnvironment of `makeCounter()` call
    <sub>outer reference = global LexicalEnvironment below</sub>
    ```js
    {
        count: 0
    }
    ```
    <br/>
- global LexicalEnvironment:
    <sub>outer reference is `null`</sub>
    ```js
    {
        makeCounter: function
        counter: undefined
    }
    ```

During the execution of `makeCounter()`, a tiny nested function is created of only one line: `return count++`.

All functions have the hidden property named `[[Environment]]`, that keeps the reference to the Lexical Environment where the function was created. So **all functions remember the Lexical Environment in which they were made.**

The `[[Environment]]` reference is set once and forever at function creation time.

So, `counter.[[Environment]]` has the reference to `{ count: 0 }` Lexical Environment. Later, when `counter()` is called, a new Lexical Environment is created for the call, and its outer Lexical Environment reference is taken from `counter.[[Environment]]`.

If we call `counter()`, we initialize it with `[[Environment]]` in which `count = 0`. First, it looks for `count` in its own LE, doesn't find it and looks in the `[[Environment]]`.

**A variable is updated in the Lexical Environment where it lives.**

So `count` is updated in the `[[Environment]]`. If we call `counter()` multiple times, the count variable will be increased to 2, 3 and so on, at the same place.
