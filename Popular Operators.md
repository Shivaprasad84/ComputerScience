
1. [x] `map`: Transforms each value emitted by the source observable using a projection function.
2. [x] `filter`: Filters the values emitted by the source observable based on a predicate function.
3. [x] `mergeMap` (flatMap): Projects each source value to an inner observable, and then flattens all inner observables into a single output observable.
4. [x] `switchMap`: Projects each source value to an inner observable, and switches to the latest inner observable, unsubscribing from previous inner observables.
5. [x] `combineLatest`: Combines the latest values from multiple observables into an array, emitting a new array whenever any of the source observables emit a value.
6. [x] `zip`: Combines the values from multiple observables in a strict sequence, emitting an array of combined values when all the source observables have emitted a value.
7. [ ] `catchError`: Catches errors thrown by the source observable and replaces them with a fallback observable or a default value.
8. [ ] `retry`: Retries the source observable when it encounters an error, up to a specified number of times.
9. [x] `debounceTime`: Delays emitted values from the source observable, and only emits the latest value after a specified time has passed since the last emission.
10. [x] `distinctUntilChanged`: Filters out consecutive duplicate values emitted by the source observable.
11. [x] `tap` (do): Allows you to perform side effects without modifying the emitted values of the source observable.
12. [x] `share`: Transform hot observables into shared observables to enable multiple subscribers to share the same data stream.
13. [x] `shareReplay`: Transform hot observables into shared observables and cache a specified number of past values for late subscribers.
