# Lab: Send messages from client

> Time: 5 minutes

## Instructions

1. Import `MatInputModule` on `material.module.ts` file.
```
import { MatInputModule } from '@angular/material/input';
```

2. Add input field message
```html
<mat-form-field>
  <input matInput placeholder="what are you thinking?"
         [(ngModel)]="message" (keyup.enter)="onSendMessage(message)">
  <mat-hint>Send your message</mat-hint>
</mat-form-field>
```

3. Define `message` model and `onSendMessage` function on `message.component.ts` file.
```ts
message: string;

onSendMessage(message: string) {
    this.socketService.sendMessage({
      date: new Date().toISOString(),
      from: 'client',
      content: message
    });
}
```

Is there any way to have the same message back from the server in order to display it as part of the list?