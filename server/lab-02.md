# Lab: Handle Connection events

> Time: 10 minutes

## Instructions

1. Update `listen` function on `app-server.ts` file.

```ts
public listen() {
    this.server.listen(this.port, () => {
        console.log(`Running server on port ${this.port}`);
    });
}
```

2. Add `connect` *event* handler. This will be fired upon a _connection_ from client.

```ts
public listen() {
    this.server.listen(this.port, () => {
        console.log(`Running server on port ${this.port}`);
    });

    this.io.on('connect', (socket: SocketIO.Socket) => {
        console.log('Client connected');
    });
}
```

3. Add `disconnect` *event* handler. This will be fired upon _disconnection_.
```ts
}

public listen() {
    this.server.listen(this.port, () => {
        console.log(`Running server on port ${this.port}`);
    });

    this.io.on('connect', (socket: SocketIO.Socket) => {
        console.log('Client connected');

        socket.on('disconnect', () => {
            console.log('Client disconnected');
        });
    });
}
```

## Next Lab
Configure `Socket.IO` instance to listen and send messages on next lab: [Listen and Send messages](lab-03.md)
