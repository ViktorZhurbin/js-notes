# Partial function application

### With context
```js
function mul(a, b) {
  return a * b;
}

let double = mul.bind(null, 2);

alert( double(3) ); // = mul(2, 3) = 6
alert( double(4) ); // = mul(2, 4) = 8
alert( double(5) ); // = mul(2, 5) = 10
```
The call to `mul.bind(null, 2)` creates a new function double that passes calls to `mul`, fixing `null` as the context and `2` as the first argument. Further arguments are passed “as is”.

That’s called *partial function application* – we create a new function by fixing some parameters of the existing one.

The benefit is that we can create an independent function with a readable name (`double`, `triple`). We can use it and not provide the first argument every time as it’s fixed with `bind`.

In other cases, partial application is useful when we have a very generic function and want a less universal variant of it for convenience.

For instance, we have a function `send(from, to, text)`. Then, inside a `user` object we may want to use a partial variant of it: `sendTo(to, text)` that sends from the current user.

### Without context
What if we’d like to fix some arguments, but not the context this? For example, for an object method.

The native bind does not allow that. We can’t just omit the context and jump to arguments.

Fortunately, a function partial for binding only arguments can be easily implemented.

Like this:
```js
function partial(func, ...argsBound) {
  return function(...args) { // (*)
    return func.call(this, ...argsBound, ...args);
  }
}

// Usage:
let user = {
  firstName: "John",
  say(time, phrase) {
    alert(`[${time}] ${this.firstName}: ${phrase}!`);
  }
};

// add a partial method with fixed time
user.sayNow = partial(
    user.say,
    new Date().getHours() + ':' + new Date().getMinutes()
);

user.sayNow("Hello");
// Something like:
// [10:00] John: Hello!
```
The result of `partial(func[, arg1, arg2...])` call is a wrapper `(*)` that calls `func` with:

- Same `this` as it gets (for `user.sayNow` call it’s `user`)
- Then gives it `...argsBound` – arguments from the partial call (`"10:00"`)
- Then gives it `...args` – arguments given to the wrapper (`"Hello"`)
