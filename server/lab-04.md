
# Lab: Server side client

> Time: 10 minutes

## Instructions

1. Install `socket.io-client`
```
npm install socket.io-client --save
```

2. Define `app-client.js` file

```js
const io = require('socket.io-client');

const socket = io.connect(
  'http://localhost:3000',
  {
    reconnect: true
  }
);

socket.on('connect', () => {
  console.log('Connected to the server');
  socket.on('message', message => {
    console.log('Received message: ' + JSON.stringify(message));
  });
});

socket.emit('message', {
  from: 'client',
  content: 'hello world'
});
```

3. Run Application client

```console
node server/app-client.js
```