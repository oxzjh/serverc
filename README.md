# server

Ease to create nodejs server, include http,https,tcp,udp,websocket,security websocket.

#### Http:
```
// npm install serverc
// index.js

require('compilec');

const path = require('path');
const nodelib = require('nodelibc');
const server = require('serverc');

server.runHTTP(
	3000,
	new nodelib.Router(path.join(__dirname, 'routes')), // route of the server (You should create a folder named routes, and create logic handlers in it.)
	null, // secret
	null, // domain (Could be '*' when you are testing.)
	false, // sign (Check sign or not)
	300000 // timeout (Compare server timestamp with client timestamp, if more then this value will return directly.)
);
```

#### Websocket:
```
// npm install ws
// index.js

require('compilec');

const path = require('path');
const nodelib = require('nodelibc');
const server = require('serverc');

server.runServerWS(
	3000,
	new nodelib.JsonHandler(false), // handler (Could be JsonHandler, ProtobufHandler, BufferHandler, JsonHandler argument 1 means compress or not)
	new nodelib.Router(path.join(__dirname, 'routes')), // route of the server (You should create a folder named routes, and create logic handlers in it.)
	null // secret
);
```

```
// Logic code file
const server = require('serverc');
server.broadcast('some message...');
```