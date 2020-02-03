#Callbacks

> **Callback** is a function passed into another function as an argument

So we use function as an argument, kind of saying: *We'll call you back*.

You're likely to havee used callbacks a few times in your life. Check this:

```js
function callback(name) {
  alert('Hello ' + name);
}

function otherFunction(callback) {
  var name = prompt('Please enter your name.');
  callback(name);
}

otherFunction(callback);
```

Above example is a *synchronous* callback, that is executed immediately. Nothing special.

Let's discuss a more interesting kind.

Say, we have two functions. When we call them, they are executed one after another:

```js
const one = () => console.log(1);
const two = () => console.log(2);

one(); // 1
two(); // 2
```

What happens when it takes some time for the first function to execute? Javascript will just wait for it, keeping things synchronous and blocking our next function execution:

```js
const heavyLongComputation = () => {
    // do some heavy computations taking 5 seconds
    console.log(1)
}
const one = () => {
    console.log(0);
    heavyLongComputation();
}
const two = () => console.log(2);

one(); // 0
// then 5 seconds later
// 1
two(); // 2
```

Sometimes we would like to just move on to the next function call and let the first one finish whenever it's done. This is where things start to get asynchronous.

There's a built-in way in JS to delay function execution called `setTimeout`. It takes two arguments: a function (callback), and delay in ms after which that function is scheduled to execute. In this delay window our following function will have time to run.

```js
const one = () => {
    console.log(0);
    setTimeout(heavyLongComputation, 100);
}
const two = () => {
    console.log(2);
}

one(); // 0
two(); // 2
// then roughly 5.1 seconds later
// 1
```

But what if our code needs to use the result of the code that does not resolve immediately, like reading or downloading a file? We need to fetch some data and then want to process that data. Let's write some pseudo-code:
```js
const fetchData = (url) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url); // go get data from this url
    console.log('got the photo!');

    return xhr.response;
}

const data = fetchData('https://someapi.com/getData'); // takes time to load
processData(data); // wouldn't work, we do not have data yet
// some time later
// got the photo!
```

So we need to:
1. know when our request is completed
2. then process the respose

XMLHttpRequest fires `'load'` event when request is completed. So we can add event listener to catch that. Actual response in stored in `xhr.response` property, and we'll grab it from there.

As you already know, event listener's second argument should be a callback that runs when specified event happens. That's the perfect place for our processData function:
```js
const fetchData = (url, callback) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url); // go get data from this url
    let data;
    xhr.addEventListener('load', () => {
        console.log('we got data!');
        data = callback(xhr.response)
    }) // request completed, now we can process data

    return data;
}

const data = fetchData('https://someapi.com/getData', processData); // now it works!
```


Above example is an *asynchronous* callback, that is executed at some point later.



---
##References:

https://developer.mozilla.org/en-US/docs/Glossary/Callback_function
http://javascript.info/callbacks
https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced