Let's explore the `buffer`, `bufferTime`, and `bufferWhen` operators in RxJS with in-depth explanations and examples.

1. `buffer` Operator:
   - The `buffer` operator is used to group emitted values from an observable into arrays, based on the emissions of another "notifier" observable.
   - When the "notifier" observable emits a value, the `buffer` operator collects all the values emitted by the source observable since the last "notifier" emission and emits them as an array.
   - The notifier observable controls when the buffer is flushed and a new buffer is started.
   - The buffer array is emitted downstream only when the notifier observable emits a value.

Example of `buffer` operator:

```typescript
import { interval, fromEvent } from 'rxjs';
import { buffer } from 'rxjs/operators';

const sourceObservable = interval(1000); // Emit values every second
const notifierObservable = fromEvent(document, 'click'); // Emit values when the document is clicked

sourceObservable.pipe(buffer(notifierObservable)).subscribe((bufferedValues) => {
  console.log('Buffered Values:', bufferedValues);
});
```

Output:

```
Buffered Values: [0, 1, 2, 3, 4]
Buffered Values: [5, 6, 7, 8]
Buffered Values: [9, 10, 11, 12, 13]
```

In this example, the `sourceObservable` emits values `0` to `13` every second. The `notifierObservable` emits values whenever the document is clicked. The `buffer` operator groups the emitted values from `sourceObservable` into arrays and emits each array when a click event occurs (when the `notifierObservable` emits). The emitted arrays contain the values that were emitted by the `sourceObservable` since the last click event.

2. `bufferTime` Operator:
   - The `bufferTime` operator is used to group emitted values from an observable into arrays periodically, based on a time interval.
   - The `bufferTime` operator collects all the values emitted by the source observable within the specified time interval and emits them as an array.
   - The buffer array is emitted downstream every time the specified time interval elapses, regardless of the number of values emitted within that interval.

Example of `bufferTime` operator:

```typescript
import { interval } from 'rxjs';
import { bufferTime } from 'rxjs/operators';

const sourceObservable = interval(1000); // Emit values every second

sourceObservable.pipe(bufferTime(3000)).subscribe((bufferedValues) => {
  console.log('Buffered Values:', bufferedValues);
});
```

Output:

```
Buffered Values: [0, 1, 2]
Buffered Values: [3, 4, 5]
Buffered Values: [6, 7, 8]
Buffered Values: [9, 10, 11]
...
```

In this example, the `sourceObservable` emits values every second. The `bufferTime` operator collects all the values emitted by the `sourceObservable` within every 3-second interval and emits them as arrays downstream.

3. `bufferWhen` Operator:
   - The `bufferWhen` operator is used to group emitted values from an observable into arrays based on a "closing selector" function.
   - The "closing selector" function takes no arguments and returns an observable.
   - When the returned observable from the "closing selector" function emits a value, the `bufferWhen` operator collects all the values emitted by the source observable since the last "closing selector" emission and emits them as an array.
   - The buffer array is emitted downstream only when the "closing selector" observable emits a value.

Example of `bufferWhen` operator:

```typescript
import { interval, timer } from 'rxjs';
import { bufferWhen } from 'rxjs/operators';

const sourceObservable = interval(1000); // Emit values every second

sourceObservable.pipe(bufferWhen(() => timer(3000))).subscribe((bufferedValues) => {
  console.log('Buffered Values:', bufferedValues);
});
```

Output:

```
Buffered Values: [0, 1, 2]
Buffered Values: [3, 4, 5]
Buffered Values: [6, 7, 8]
Buffered Values: [9, 10, 11]
...
```

In this example, the `sourceObservable` emits values every second. The `bufferWhen` operator uses the `timer` function to create a "closing selector" observable that emits a value after 3 seconds. The `bufferWhen` operator collects all the values emitted by the `sourceObservable` since the last "closing selector" emission and emits them as arrays downstream.

In summary, `buffer`, `bufferTime`, and `bufferWhen` are powerful operators in RxJS to group emitted values from observables into arrays based on various criteria like the emission of another observable, time intervals, or custom conditions.