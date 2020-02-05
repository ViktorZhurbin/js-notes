# Objects

```js
const user = {
    age: 25,
    tall: true
 }
 ```

To remove a property, we can use `delete` operator:
```js
delete user.age;
```

### Existence check
Usually we check that property exists by comparing it to `undefned`
```js
let user = {};

user.noSuchProperty === undefined; // true means "no such property"
```

There is also a special operator `in` to check for the existence of a property:
```js
let user = { name: "John", age: 30 };

"age" in user; // true, user.age exists
"blabla" in user; // false, user.blabla doesn't exist
```

<div style="border: 3px #f5f2f0 solid; padding: 20px; border-radius: 10px">

**Using `in` for properties that store `undefined`**

Usually, the `=== undefined` check is just fine. But there’s a special case when it fails, but `in` works correctly.

It’s when an object property exists, but stores `undefined`:
```js
let obj = {
  test: undefined
};

obj.test // it's undefined, so - no such property?
"test" in obj // true, the property does exist!
```

In the code above, the property `obj.test` technically exists. So the `in` operator works right.

Situations like this happen very rarely, because `undefined` is usually not assigned. We mostly use `null` for “unknown” or “empty” values. So the `in` operator is an exotic guest in the code.
</div>
<br />

### Ordered like an object
Are objects ordered? In other words, if we loop over an object, do we get all properties in the same order they were added? Can we rely on this?

The short answer is: “ordered in a special fashion”:
- integer properties are sorted
- others appear after them in creation order.

By *integer properties* we mean a string that can be converted to-and-from an integer without a change.

```js
let codes = {
  "49": "Germany",
  "smth": "smthValue",
  "41": "Switzerland",
  "44": "Great Britain",
  "1": "USA"
};

codes['newItem'] = "itemValue";

for (let code in codes) {
  console.log(code); // 1, 41, 44, 49, smth, newItem
}
```

### Copying by reference
One of the fundamental differences of objects vs primitives is that they are stored and copied “by reference”.

**A variable stores not the object itself, but its “address in memory”, in other words “a reference” to it.**

When an object variable is copied – the reference is copied, the object is not duplicated.

```js
let user = { name: "John" };

let admin = user; // copy the reference
```
Now we have two variables, each one with the reference to the same object. We can use any variable to modify object:
```js
let user = { name: 'John' };
let admin = user;
admin.name = 'Pete'; // changed by the "admin" reference

user.name; // 'Pete', changes are seen from the "user" reference
```

### Comparison by reference
The equality `==` and strict equality `===` operators for objects work exactly the same.

Two objects are equal only if they are the same object.
```js
let a = {};
let b = a; // copy the reference

a == b; // true, both variables reference the same object
a === b; // true
```
And here two independent objects are not equal, even though both are empty:
```js
// two independent objects
let a = {};
let b = {};

a == b; // false
```
