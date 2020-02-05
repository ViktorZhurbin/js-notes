
### Reference Type
There're two operations in `obj.method()` statement:
- First, the dot `.` retrieves the property `obj.method`.
- Then parentheses `()` execute it.

If we put these operations on separate lines, then `this` will be lost for sure:
```js
let user = {
  name: "John",
  hi() { alert(this.name); }
}

let hi = user.hi;
hi(); // Error, because `this` is undefined
user.hi() // John
```
To make `user.hi()` calls work, JavaScript uses a trick – the dot `.` returns not a function, but a value of the special *Reference Type*.
```js
// Reference Type value
(user, "hi", true)
```
The value of Reference Type is a three-value combination `(base, name, strict)`, where:

`base` is the object.
`name` is the property name.
`strict` is true if `use strict` is in effect.

When parentheses `()` are called on the Reference Type, they receive the full information about the object and its method, and can set the right `this` (`=user` in our case).

Reference Type is a special “intermediary” internal type, with the purpose to pass information from dot `.` to calling parentheses `()`.

Any other operation like assignment `hi = user.hi` discards the reference type as a whole, takes the value of `user.hi` (a function) and passes it on. So any further operation “loses” `this`.

So, as the result, the value of `this` is only passed the right way if the function is called directly using a dot `obj.method()` or square brackets `obj['method']()` syntax.