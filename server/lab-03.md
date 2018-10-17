# Lab: Listen and Send messages

> Time: 15 minutes

## Instructions

1. Define a custom model to send/receive messages. Create a `message.ts` file.

```ts
export interface Message {
    date: string;
    from: string;
    content: string;
}
```

2. Import `Message` model on `app-server.ts` file.

```ts
import { Message } from './message';
```

3. Register a new handler for a `message` event on `app-server.ts` file. The `Socket.IO` instance is ready to listen.
```ts
this.io.on('connect', (socket: SocketIO.Socket) => {
    console.log('Client connected');

    socket.on('message', (m: Message) => {
        console.log('Message received: ' + JSON.stringify(m));
    });

    socket.on('disconnect', (reason: any) => {
        console.log('Client disconnected', reason);
        clearInterval(interval);
    });
});
```

4. Create a `message-generator.ts` file
```ts
import { Message } from './message';

export class MessageGenerator {

    WORDS: string[] = [
        'lorem', 'ipsum', 'dolor', 'sit', 'amet', 'consectetur',
		'eleifend', 'blandit', 'nunc', 'ornare', 'odio', 'ut', 'finished'
    ];

    public generateMessage(): Message {
        return {
            date: new Date().toISOString(),
            from: 'server',
            content: this.getRandomContent()
        };
    }

    private getRandomContent(): string {
        const position = Math.floor(Math.random() * this.WORDS.length);
        return this.WORDS[position];
    }
}
```

5. Create a `MessageGenerator` object and send a random message through existing `socket` every second. Update `listen` function on `app-server.ts` file as follows. Don't forget to import `MessageGenerator` first.
```ts
this.io.on('connect', (socket: SocketIO.Socket) => {
    const generator = new MessageGenerator();
    console.log('Client connected');

    socket.on('message', (m: Message) => {
        console.log('Message received: ' + JSON.stringify(m));
    });

    let interval = setInterval(() => {
        const message = generator.generateMessage();
        console.log('sending message: ' + JSON.stringify(message));
        this.io.emit('message', message);
    }, 1000);

    socket.on('disconnect', (reason: any) => {
        console.log('Client disconnected', reason);
        clearInterval(interval);
    });
});
```

## Next Lab

Create a [Server side client](lab-04.md)
