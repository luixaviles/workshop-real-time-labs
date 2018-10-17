# Lab: Define WebSocket service

> Time: 10 minutes

## Instructions

1. Install `socket.io-client`
```console
npm install @types/socket.io-client --save-dev
```

1. Generate a `socket` service.
```console
ng generate service shared/socket
```

2. Import `socketIo` and create an instance on `constructor`
```ts
import * as socketIo from 'socket.io-client';
```

```ts
constructor() {
    this.socket = socketIo('http://localhost:3000');
}
```

3. Define `sendMessage` function to allow send messages from client application.
```ts
public sendMessage(message: Message): void {
    this.socket.emit('message', message);
  }
```

4. Define `onMessage` function to listen incoming messages
```ts
public onMessage(): Observable<Message> {
    return new Observable<Message>(observer => {
      this.socket.on('message', (data: Message) => observer.next(data));
    });
}
```

## Next Lab
Message component now can inject the service and [Subscribe to Message updates](lab-03.md)