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
	3000, // server port
	null, // default: new nodelib.JsonHandler(false, fales) arg1-compress, arg2-stream
	new nodelib.JsonRouter(path.join(__dirname, 'routes')), // route of the server (You should create a folder named routes, and create logic handlers in it.)
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
	new nodelib.JsonHandler(false), // handler (Could be JsonHandler, HandlerJson, HandlerBuffer, HandlerProtobuf)
	new nodelib.Router(methods, path.join(__dirname, 'routes')), // route of the server ("methods" is a key-value object, like {"User.login":10, "User.logout":11, ...}, the value is a protocol like the protobuf's protocol. You should create a folder named routes, and create logic handlers in it.)
	null // secret
);
```

#### PROTOCOLS:
```
0 :connect, clinet should send "uint32 for _uid" and "string for _key".
protocol<0 means ERROR:
-1:"_uid" param not found.
-2:route handler not found.
-3:process in queue (check this method's logic that somewhere take long time).
-4:"_key" expired or "_sign" error or timeout.
```

```
// Logic code file
const server = require('serverc');
server.broadcast(some message...);
```