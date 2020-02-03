# Global object

In a browser it is named `window`, for Node.js it is `global`, for other environments it may have another name.

Recently, `globalThis` was added to the language, as a standardized name for a global object, that should be supported across all environments.

All properties of the global object can be accessed directly:
```js
alert("Hello");
// is the same as
window.alert("Hello");
```

In a browser, global functions and variables declared with `var` (not `let`/`const`!) become the property of the global object:
```js
var gVar = 5;

alert(window.gVar); // 5 (became a property of the global object)
```
This behavior exists for compatibility reasons. Modern scripts use JavaScript modules where such thing doesn’t happen.

If a value is so important that you’d like to make it available globally, write it directly as a property:
```js
// make current user information global, to let all scripts access it
window.currentUser = {
  name: "John"
};

// somewhere else in code
alert(currentUser.name);  // John

// or, if we have a local variable with the name "currentUser"
// get it from window explicitly (safe!)
alert(window.currentUser.name); // John
```

Using global variables is generally discouraged. **There should be as few global variables as possible.**

### Using for polyfills

We use the global object to test for support of modern language features.

For instance, test if a built-in `Promise` object exists (it doesn’t in really old browsers):
```js
if (!window.Promise) {
  alert("Your browser is really old!");
}
```
If there’s none (say, we’re in an old browser), we can create a polyfill:
```js
if (!window.Promise) {
  window.Promise = ... // custom implementation of the modern language feature
}
```