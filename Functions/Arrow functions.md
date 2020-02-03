# Arrow functions

### No `this`.
If `this` is accessed, it is taken from the outside.



<div style="border: 3px #f5f2f0 solid; padding: 20px; border-radius: 10px">
<b>Arrow functions VS bind</b>

There’s a subtle difference between an arrow function => and a regular function called with `.bind(this)`:

- `.bind(this)` creates a “bound version” of the function.
- The arrow `=>` doesn’t create any binding. The function simply doesn’t have `this`. The lookup of `this` is made exactly the same way as a regular variable search: in the outer lexical environment.
</div>

### No `arguments` variable
Arrow functions also have no `arguments` variable.

### No `super`

### Can’t be called with `new`