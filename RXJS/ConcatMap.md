## Concat   map

![[concat-map.png]]

However in concat map, it will wait till the inner subscription is completed, it will not cancel

`concatMap` is an RxJS operator that transforms each value emitted by the source observable into an inner observable and concatenates the emissions of the inner observables in a serialized manner. It subscribes to each inner observable only after the previous inner observable has completed, ensuring that the order of emitted values is preserved.

The syntax of `concatMap` is as follows:

```typescript
sourceObservable.pipe(
  concatMap((value: any) => innerObservable)
);
```

Here's an in-depth explanation of `concatMap` with an example:

Consider the following scenario: You have an observable that emits a stream of user IDs, and you want to make an HTTP request to fetch user details for each user ID. However, you need to ensure that the HTTP requests are made one at a time, and the order of the responses matches the order of the emitted user IDs.

```typescript
import { from, of } from 'rxjs';
import { concatMap, delay } from 'rxjs/operators';

// Simulate an observable that emits user IDs
const userIdsObservable = from([1, 2, 3, 4, 5]);

// Simulate a function that fetches user details from an API based on user ID
const fetchUserDetails = (userId: number) =>
  of({ id: userId, name: `User ${userId}`, email: `user${userId}@example.com` }).pipe(delay(1000));

// Use concatMap to fetch user details for each user ID
userIdsObservable
  .pipe(
    concatMap((userId: number) => fetchUserDetails(userId))
  )
  .subscribe((userDetails) => console.log(userDetails));
```

Output:

```
{ id: 1, name: 'User 1', email: 'user1@example.com' }
{ id: 2, name: 'User 2', email: 'user2@example.com' }
{ id: 3, name: 'User 3', email: 'user3@example.com' }
{ id: 4, name: 'User 4', email: 'user4@example.com' }
{ id: 5, name: 'User 5', email: 'user5@example.com' }
```

In this example, we have an observable `userIdsObservable` that emits user IDs `[1, 2, 3, 4, 5]`. We also have a function `fetchUserDetails` that returns an observable containing user details for a given user ID. We use `of` to create an observable with mock user details and `delay` to simulate an asynchronous HTTP request.

The `concatMap` operator is then used to transform each emitted user ID into an inner observable (`fetchUserDetails(userId)`). `concatMap` subscribes to each inner observable one at a time, waiting for the previous inner observable to complete before subscribing to the next one. This ensures that the HTTP requests are made in a serialized manner, preserving the order of emitted user IDs.

As a result, the output shows the user details for each user ID in the order they were emitted by the source observable.

In summary, `concatMap` is useful when you need to perform asynchronous tasks sequentially, preserving the order of emissions from the source observable. It's commonly used in scenarios where the order of operations is crucial, such as handling HTTP requests that depend on the previous response or any other scenario where you need to maintain the order of operations.

