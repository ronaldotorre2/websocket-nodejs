# Websocket-example
It is an example of implementing websocket(ws) on both server and client side

## Install
```
$ npm install --save ws express
```

#### client
`websocket client` is a browser supported object.

There are 3 basic must know fucntions:
 - `ws.onopen` : emmited when connected
 - `ws.send` : sending a send event to websocket server
 - `ws.onmessage` : event emmited when receiving message 

([Read More](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications))

```js
<script>
    var ws = new WebSocket('ws://localhost:40510');
    ws.onopen = function () {
        console.log('websocket is connected ...');
        ws.send('connected');
    }
    
    ws.onmessage = function (ev) {
        console.log(ev);
    }
</script>
```

#### server
server code is simple.

```js
var WebSocketServer = require('ws').Server, wss = new WebSocketServer({port: 40510});

wss.on('connection', function (ws) {
  ws.on('message', function (message) {
    console.log('received: %s', message)
  })

  setInterval(
    () => ws.send(`${new Date()}`),
    1000
  )
})

```

## Run

Run server
```
$ npm start
``` 

Open browser
```
http://localhost:3000/
```