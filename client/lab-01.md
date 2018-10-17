# Lab: Adding List of Messages

> Time: 15 minutes

You'll need to have `starter` project up and running.

## Instructions

1. Define a model for incoming messages. Create `shared/model/message.ts` file.
```ts
export interface Message {
    date: string;
    from: string;
    content: string;
}
```

2. Define an array for `Message` objects into `messages.component.ts` file.
```ts
export class MessagesComponent implements OnInit {
  messages: Message[] = [
    {
      date: '2018-10-18T09:53:00',
      from: 'juan',
      content: 'hello'
    },
    {
      date: '2018-10-18T15:59:00',
      from: 'maria',
      content: 'hey, how are you?'
    }
  ];
}
```

3. Define a list for incoming messages. Update `messages.component.html` file.
```html
<mat-list class="chat-list">
  <mat-list-item *ngFor="let message of messages">
      <h4 mat-line>{{message.from}} - {{message.content}}</h4>
      <p mat-line> {{message.date | date:'M/d/yy, h:mm:ss a'}} </p>
  </mat-list-item>
</mat-list>
```

4. Import/Export `MatListModule` into `material.module.ts`
```ts
import { MatListModule } from '@angular/material/list';
...
imports: [
    MatListModule
  ],
  exports: [
    MatListModule
  ],
...
```

## Next Lab
The app needs to have a layer for server communication. [Define WebSocket service](lab-02.md)