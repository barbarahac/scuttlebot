# Scuttlebot

A bot-server for the phoenix network. Provides an RPC server for operating it locally or remotely. Can be `require()`ed to create your own bots.

Usage:

```
./scuttlebot serve --port 2000 --ssbport 2001
```

API:

```js
var sbot = require('scuttlebot')
var ssbapi = require('secure-scuttlebutt/api')

// with the default api:
var server = sbot.serve(2000, __dirname) // port, (optional) directory to put data
var client = sbot.connect(2000, 'localhost') // port, (optional) hostname
client.whoami(function(err, prof) {
  // ...
})

// with a custom API:
var server = sbot.serve(2000, __dirname, function(backend) {
  // return your muxrpc server
  return ssbapi.server(backend.ssb, backend.feed)
})
var client = sbot.connect(2000, 'localhost', ssbapi.client())
var feedstream = client.createFeedStream()
// ...