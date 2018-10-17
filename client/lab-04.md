# Lab: Handle Connection events

> Time: 5 minutes

## Instructions

1. Update `socket.service.ts` file.

```ts
public onEvent(event: string): Observable<any> {
    return new Observable<string>(observer => {
        this.socket.on(event, () => observer.next());
    });
}

public stop(): void {
    this.socket.disconnect();
    console.log('stop listening.');
}
```

2. Update `ngOnInit` function into `messages.component.ts`. Add `connect` and `disconnect` events.

```ts
ngOnInit() {
    this.socketService.onMessage().subscribe((message: Message) => {
      console.log('received message', message);
      this.messages.push(message);
      if(message.content === 'finished') {
          console.log('Finishing communication');
          this.socketService.stop();
      }
    });

    this.socketService.onEvent('connect').subscribe(() => {
      console.log('connected');
    });

    this.socketService.onEvent('disconnect').subscribe(() => {
      console.log('disconnected');
    });
}
```

## Next Lab

You can receive/listen for incoming messages and now you can [Send messages from client](lab-05.md)
