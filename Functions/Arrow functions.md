# Arrow functions
<div style="border: 3px #f5f2f0 solid; padding: 20px; border-radius: 10px">
In JavaScript, traditional functions can be used as:

- Non-method functions
- Methods
- Constructors

These roles clash:
- Due to roles 2 and 3, functions always have their own `this`.
- But that prevents you from accessing the `this` of, e.g., a surrounding method from inside a callback (role 1).
</div>

## Enters Arrow Function

### Compared to "traditional" functions
An arrow function is different from a normal function in only two ways:

1. The following constructs are lexical: `arguments, super, this, new.target`
2. Normal functions support `new` via the internal method `[[Construct]]` and the property `prototype`. Arrow functions have neither, which is why `new (() => {})` throws an error.

Apart from that, there are no observable differences between an arrow function and a normal function.

### No `this`
Arrow functions don't have their own `this`, like ordinary functions do. If `this` is accessed, it is taken from the outside — just like a variable is looked up in outer sopes.

No need for `bind()` or `that = this`, anymore (:+1:).

<div style="border: 3px #f5f2f0 solid; padding: 20px; border-radius: 10px">
<b>Arrow functions VS bind</b>

There’s a subtle difference between an arrow function `=>` and a regular function called with `.bind(this)`:

- `.bind(this)` creates a “bound version” of the function.
- The arrow `=>` doesn’t create any binding. The function simply doesn’t have `this`. The lookup of `this` is made exactly the same way as a regular variable search: *in the outer lexical environment*.
</div>

### Syntax pitfalls
If body of an arrow function is an expression, you don’t need braces — expression is always implicitly returned:
```js
asyncFunc.then(a => console.log(a));

x => x * x
```

However, statements have to be put in braces:
```js
asyncFunc.catch(x => { throw b });

x => { return x * x }
```
