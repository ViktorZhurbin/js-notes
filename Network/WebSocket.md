# WebSocket
https://javascript.info/websocket

`WebSocket` is a modern way to have persistent browser-server connections.
- WebSockets don’t have cross-origin limitations.
- They are well-supported in browsers.
- Can send/receive strings and binary data.

The `WebSocket` protocol is a specification that provides a way to exchange data between browser and server via a persistent connection. The data can be passed in both directions as “packets”, without breaking the connection and additional HTTP-requests.

`WebSocket` is especially great for services that require continuous data exchange, e.g. online games, real-time trading systems and so on.

### A simple example
To open a websocket connection, we need to create new WebSocket using the special protocol ws in the url:

```js
let socket = new WebSocket("ws://javascript.info");
```

There’s also encrypted `wss://` protocol. It’s like HTTPS for websockets. Always prefer `wss`

Once the socket is created, we should listen to events on it. There are totally 4 events:
- **`open`** – connection established,
- **`message`** – data received,
- **`error`** – websocket error,
- **`close`** – connection closed.

…And if we’d like to send something, then `socket.send(data)` will do that.

There’s a small nodejs server `server.js` running for demo purposes. It responds with “Hello from server, John”, then waits 5 seconds and closes the connection.

So you’ll see events `open` → `message` → `close`:

```js
let socket = new WebSocket("wss://javascript.info/article/websocket/demo/hello");

socket.onopen = function(e) {
  alert("[open] Connection established");
  alert("Sending to server");
  socket.send("My name is John");
};

socket.onmessage = function(event) {
  alert(`[message] Data received from server: ${event.data}`);
};

socket.onclose = function(event) {
  if (event.wasClean) {
    alert(`[close] Connection closed cleanly, code=${event.code} reason=${event.reason}`);
  } else {
    // e.g. server process killed or network down
    // event.code is usually 1006 in this case
    alert('[close] Connection died');
  }
};

socket.onerror = function(error) {
  alert(`[error] ${error.message}`);
};
```