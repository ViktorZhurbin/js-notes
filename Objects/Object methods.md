# Object methods
A function that is the property of an object is called its method.
```js
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
  alert("Hello!");
};

// sayHi is now a method of the object user.
user.sayHi(); // Hello!
```

### Method shorthand
There exists a shorter syntax for methods in an object literal:
```js
// these objects do (roughly) the same
// There are subtle differences related to object inheritance

user = {
  sayHi: function() {
    alert("Hello");
  }
};

user = {
  sayHi() {
    alert("Hello");
  }
};
```

### “this” in methods
To access the object, a method can use the `this` keyword.

The value of `this` is the object “before dot”, the one used to call the method:
```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // "this" is the "current object"
    alert(this.name);
  }

};

// this = user
user.sayHi(); // John
```

### “this” is not bound
The value of `this` is evaluated during the run-time, depending on the context.

The rule is simple: if `obj.method()` is called, then `this` = `obj` during the call of `method`:
```js
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// use the same function in two objects
user.method = sayHi;
admin.method = sayHi;

// these calls have different this
// "this" inside the function is the object "before the dot"
user.method(); // John  (this == user)
admin.method(); // Admin  (this == admin)

admin['f'](); // Admin (dot or square brackets access the method – doesn't matter)
```
