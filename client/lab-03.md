# Lab: Subscribe to Message updates

> Time: 5 minutes

## Instructions

1. Inject `SocketService` into `message.component.ts` file

```ts
constructor(private socketService: SocketService) { }
```

2. Subscribe to message updates
```ts
ngOnInit() {
    this.socketService.onMessage().subscribe((message: Message) => {
      console.log('received message', message);
      this.messages.push(message);
    });
}
```

## Next Lab
Take control of `connected` and `disconnected` events: [Handle Connection events](lab-04.md)