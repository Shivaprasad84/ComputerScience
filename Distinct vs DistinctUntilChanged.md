Sure! Let's explore the `distinct` and `distinctUntilChanged` operators in RxJS with in-depth explanations and examples.

1. `distinct` Operator:
   - The `distinct` operator filters out duplicate values emitted by an observable, ensuring that only unique values are passed downstream.
   - When a new value is emitted, `distinct` checks if it is different from the previous values emitted so far. If it's a new value, it passes it to the subscriber; otherwise, it ignores the duplicate value.
   - The `distinct` operator uses strict equality (`===`) to compare emitted values for uniqueness.

Example of `distinct` operator:

```typescript
import { of } from 'rxjs';
import { distinct } from 'rxjs/operators';

const sourceObservable = of(1, 2, 2, 3, 1, 4, 4, 5);

sourceObservable.pipe(distinct()).subscribe((value) => console.log(value));
```

Output:

```
1
2
3
4
5
```

In this example, the `distinct` operator filters out the duplicate values (2 and 4) emitted by the source observable `sourceObservable`, and only unique values (1, 2, 3, 4, and 5) are passed downstream.

2. `distinctUntilChanged` Operator:
   - The `distinctUntilChanged` operator filters out consecutive duplicate values emitted by an observable, passing only the values that are different from their immediate previous value.
   - When a new value is emitted, `distinctUntilChanged` checks if it is different from the last emitted value. If it's a new value, it passes it to the subscriber; otherwise, it ignores the consecutive duplicate value.
   - The `distinctUntilChanged` operator uses strict equality (`===`) to compare emitted values for uniqueness.

Example of `distinctUntilChanged` operator:

```typescript
import { of } from 'rxjs';
import { distinctUntilChanged } from 'rxjs/operators';

const sourceObservable = of(1, 2, 2, 3, 1, 4, 4, 5);

sourceObservable.pipe(distinctUntilChanged()).subscribe((value) => console.log(value));
```

Output:

```
1
2
3
1
4
5
```

In this example, the `distinctUntilChanged` operator filters out consecutive duplicate values (2, 4) emitted by the source observable `sourceObservable`, and only distinct values (1, 2, 3, 1, 4, and 5) are passed downstream.

Note: In both examples, we used the `of` function to create a simple cold observable that emits a sequence of values. However, you can use `distinct` and `distinctUntilChanged` with any observable to filter out duplicate or consecutive duplicate values emitted by the observable.