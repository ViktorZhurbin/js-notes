# Partial function application

**Function Declaration**
```js
function mul(a, b) {
  return a * b;
}

let double = mul.bind(null, 2);
// Same with arrow function
let double = a => mul(a, 2);

alert( double(3) ); // = mul(2, 3) = 6
alert( double(4) ); // = mul(2, 4) = 8
alert( double(5) ); // = mul(2, 5) = 10
```

We created a new function `double` that passes calls to `mul` with a fixed first argument (`2`). The `bind` version also fixes `null` as the context. Further arguments are passed “as is”.

That’s called *partial function application* – we create a new function by fixing some parameters of the existing one.

The benefit is that we can create an independent function with a readable name (`double`, `triple`). We can use it and not provide the first argument every time.

In other cases, partial application is useful when we have a very generic function and want a less universal variant of it for convenience. For instance, we have a function `send(from, to, text)`. Then, inside a `user` object we may want to use a partial variant of it: `sendTo(to, text)` that sends from the current user.
