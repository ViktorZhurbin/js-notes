# Arrow functions

```js
x => { return x * x }  // statement block
// Need to return a value explicitly

x => x * x  // expression, equivalent to previous line
// Expression is always implicitly returned
```

Two main benefits:
1. Shorter syntax
2. Lexical `this` (i.e. it's picked up from surroundings)

No need `bind()` or `that = this`, anymore (:+1:).

The following variables are all lexical inside arrow functions:
```js
arguments
super
this
new.target
```

### No `this`.
Arrow functions don't shadow `this`, like ordinary functions do. If `this` is accessed, it is taken from the outside — just like a variable is looked up in outer sopes.

<div style="border: 3px #f5f2f0 solid; padding: 20px; border-radius: 10px">
<b>Arrow functions VS bind</b>

There’s a subtle difference between an arrow function => and a regular function called with `.bind(this)`:

- `.bind(this)` creates a “bound version” of the function.
- The arrow `=>` doesn’t create any binding. The function simply doesn’t have `this`. The lookup of `this` is made exactly the same way as a regular variable search: in the outer lexical environment.
</div>
<br />

### Compared to "traditional" functions
An arrow function is different from a normal function in only two ways:

- The following constructs are lexical: `arguments, super, this, new.target`
- Normal functions support `new` via the internal method `[[Construct]]` and the property `prototype`. Arrow functions have neither, which is why `new (() => {})` throws an error.

Apart from that, there are no observable differences between an arrow function and a normal function.

---
In JavaScript, traditional functions can be used as:
- Non-method functions
- Methods
- Constructors

These roles clash:
- Due to roles 2 and 3, functions always have their own `this`.
- But that prevents you from accessing the th`is of, e.g., a surrounding method from inside a callback (role 1).

### Syntax pitfalls
If body of an arrow function is an expression, you don’t need braces:
```js
asyncFunc.then(x => console.log(x));
```

However, statements have to be put in braces:
```js
asyncFunc.catch(x => { throw x });
```

