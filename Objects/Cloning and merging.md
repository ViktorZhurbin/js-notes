# Cloning and merging

Simple cloning:
```js
let user = {
  name: "John",
  age: 30
};

let clone2 = Object.assign({}, user);
// OR
let clone2 = { ...user };
```

Merge several objects into one:
```js
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };
let name = { name: "Pete" };

// copies all properties from permissions1 and permissions2 into user, overwrites the name
Object.assign(user, permissions1, permissions2, name);
// OR
user = { ...permissions1, ...permissions2, ...name };

// now user = { name: "Pete", canView: true, canEdit: true }
```

<div style="background: #fff3d4;
    border-color: #f6b73c;
    padding-left: 25px;
    border-left-width: 5px;
    border-left-style: solid;
    margin-bottom: 20px;
    padding: 10px;">
  <strong>Note:</strong>

  `Object.assign()` and Spread syntax go only one level deep. Therefore, it may be unsuitable for copying multidimensional arrays or nested objects.
</div>
```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = Object.assign({}, user);

clone.sizes == user.sizes // true, sizes is an object so it's copied by reference

clone.sizes.height = 190
user.sizes.height // 190
```

To fix this, we need to use deep cloning algorythm, like `_.cloneDeep(obj)` from lodash.