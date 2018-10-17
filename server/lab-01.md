# Lab: Adding WebSocket support 

> Time: 10 minutes

You'll need to have `starter` project up and running.

## Instructions

Use a separate command line interface to run all commands.

1. Install `Socket.IO`.

```console
npm install socket.io --save
npm install @types/socket.io --save-dev
```

1. Import `createServer` function, `Server` and `Socket.IO` into `app-server.ts` file.

```ts
import { createServer, Server } from 'http';
import * as socketIo from 'socket.io';
```

1. Add `io` and `server` attributes into `app-server.ts` file.

```ts
private io: SocketIO.Server;
private server: Server;
```

1. Create `Server` instance on `constructor`.
```ts
this.server = createServer(this.app);
```

1. Create `Socket.IO` instance on `constructor` using `Server` object.
```ts
this.io = socketIo(this.server);
```

## Next Lab
Configure `Socket.IO` instance to handle connection events on next lab: [Listen Connection events](lab-02.md)