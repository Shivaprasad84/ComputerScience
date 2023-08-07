The main difference between a normal `Subject` and a `BehaviorSubject` lies in their behavior when a new subscriber subscribes to them:

1. Subject:
   - A `Subject` is a basic type of subject in RxJS.
   - When a new subscriber subscribes to a `Subject`, it will not receive any past values that were previously emitted by the `Subject`. It starts receiving values emitted after the subscription.
   - A `Subject` doesn't have any initial value, and it does not remember or buffer any past values.

2. BehaviorSubject:
   - A `BehaviorSubject` is a specific type of subject in RxJS.
   - When a new subscriber subscribes to a `BehaviorSubject`, it immediately receives the "current value" of the subject (the last value that was emitted).
   - A `BehaviorSubject` requires an initial value when it's created. This initial value will be emitted to any new subscriber before it starts receiving new values.
   - Unlike a regular `Subject`, a `BehaviorSubject` remembers the last emitted value and replays it to new subscribers upon subscription.

Regarding whether you can turn a normal `Subject` into a `BehaviorSubject`, the answer is no. Once you create a `Subject`, its behavior is fixed, and you cannot change it to behave like a `BehaviorSubject` retrospectively. If you need a `BehaviorSubject` with initial value emission, you should create it as a `BehaviorSubject` from the beginning and provide the initial value during its creation.

Here's how you create a `BehaviorSubject`:

```typescript
import { BehaviorSubject } from 'rxjs';

// Create a BehaviorSubject with an initial value of 0
const behaviorSubject = new BehaviorSubject<number>(0);

// Subscribers will immediately receive the initial value (0) upon subscription
behaviorSubject.subscribe((value) => {
  console.log('Subscriber 1:', value);
});

// Later, when you update the BehaviorSubject with a new value (e.g., 10),
// all subscribers will receive the new value.
behaviorSubject.next(10);

// Output:
// Subscriber 1: 0
// Subscriber 1: 10
```

In contrast, if you use a regular `Subject`, the subscriber will only receive the value emitted after its subscription:

```typescript
import { Subject } from 'rxjs';

const subject = new Subject<number>();

subject.subscribe((value) => {
  console.log('Subscriber 1:', value);
});

subject.next(5);

// Output:
// Subscriber 1: 5
```

As you can see, a `Subject` doesn't emit any previous values to new subscribers. If you need that behavior, you should use a `BehaviorSubject`.