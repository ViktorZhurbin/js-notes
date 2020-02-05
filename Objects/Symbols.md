# Symbol
A “symbol” represents a **unique identifier**.

A value of this type can be created using `Symbol()`:
```js
// id is a new symbol
let id = Symbol();
```

Upon creation, we can give symbol a **description (also called a symbol name)**, mostly useful for debugging purposes:
```js
// id is a symbol with the description "id"
let id = Symbol("id");
```

Symbols are guaranteed to be unique. Even if we create many symbols with the same description, they are different values. The description is just a label that doesn’t affect anything.
```js
let id1 = Symbol("id");
let id2 = Symbol("id");

id1 == id2; // false
```

<div style="border: 3px #f5f2f0 solid;
    padding: 20px;
    border-radius: 10px;
    margin-bottom: 20px;
    ">
<b>Symbols don’t auto-convert to a string</b>

```js
let id = Symbol("id");
alert(id); // TypeError: Cannot convert a Symbol value to a string
```

If we really want to show a symbol, we need to explicitly call `.toString()` on it, like here:

```js
let id = Symbol("tag");
alert(id.toString()); // Symbol(tag), now it works
```

Or get `symbol.description` property to show the description only:

```js
let id = Symbol("tag");
alert(id.description); // tag
```
</div>

### “Hidden” properties
Symbols allow us to create “hidden” properties of an object, that no other part of code can accidentally access or overwrite.

For instance, if we’re working with user objects, that belong to a third-party code, and we’d like to add identifiers to them:
```js
let user = { // belongs to another code
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // we can access the data using the symbol as the key
```

And if some other library adds their own id of type `Symbol` there will be no conflict, since Symbols are unique:
```js
// ...
let id = Symbol("id");

user[id] = "Their id value";
```

<div style="background: #fff3d4;
    border-color: #f6b73c;
    padding-left: 25px;
    border-left-width: 5px;
    border-left-style: solid;
    margin-bottom: 20px;
    padding: 10px;">

**Note:**
Symbols are skipped by `for…in`, `Object.keys()`, but are copied by `Object.assign`
</div>

## Global symbols
#### Symbol.for
We can create symbols in the **global symbol registry** and access them later. It guarantees that repeated accesses by the same name return exactly the same symbol.

In order to read (create if absent) a symbol from the registry, use `Symbol.for(key)`.

That call checks the global registry, and if there’s a symbol described as `key`, then returns it, otherwise creates a new symbol `Symbol(key)` and stores it in the registry by the given `key`:
```js
// read from the global registry
let id = Symbol.for("id"); // if the symbol did not exist, it is created

// read it again (maybe from another part of the code)
let idAgain = Symbol.for("id");

// the same symbol
alert( id === idAgain ); // true
```
#### Symbol.keyFor
`Symbol.keyFor(sym)` checks global symbol registry and returns symbol description:
```js
// get symbol by name
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// get name by symbol
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```

## System symbols
There exist many “system” symbols that JavaScript uses internally, and we can use them to fine-tune various aspects of our objects.

They are listed in the specification in the [Well-known symbols](https://tc39.es/ecma262/#sec-well-known-symbols) table:
```js
Symbol.hasInstance
Symbol.isConcatSpreadable
Symbol.iterator
Symbol.toPrimitive
// …and so on.
```
