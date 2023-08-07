## Switch map

```typescript
this.cc.get<string>('continent')?.valueChanges.pipe(takeUntil(this.destroyed$), switchMap((value: string) => {
  return this.http.get(`${this.baseUrl}/continents?continent=${value}`);
})).subscribe((countries) => {
  this.co = countries;
  this.selectedCountry = this.co[0];
});
```

In switch map if the inner subscription takes too long and the outer subscription emits a new value the inner one will be cancelled

`switchMap` is an RxJS operator that transforms each value emitted by the source observable into an inner observable. It switches to the latest inner observable and unsubscribes from the previous inner observable whenever a new value is emitted by the source observable. This means that only the emissions from the latest inner observable are forwarded to the output observable.

The syntax of `switchMap` is as follows:

```typescript
sourceObservable.pipe(
  switchMap((value: any) => innerObservable)
);
```

Here's an in-depth explanation of `switchMap` with an example:

Consider the following scenario: You have an input field that emits a stream of search queries, and you want to make an HTTP request to fetch search results for each query. However, you want to cancel previous HTTP requests when a new search query is entered to avoid outdated results.

```typescript
import { fromEvent } from 'rxjs';
import { switchMap, debounceTime, distinctUntilChanged } from 'rxjs/operators';

// Simulate an input field that emits search queries
const inputElement = document.getElementById('searchInput');
const searchQueriesObservable = fromEvent(inputElement, 'input').pipe(
  debounceTime(500), // Wait for 500ms between user input
  distinctUntilChanged() // Emit only distinct search queries
);

// Simulate a function that fetches search results from an API based on the query
const fetchSearchResults = (query: string) => {
  // Simulate an asynchronous HTTP request
  return fetch(`https://api.example.com/search?q=${query}`)
    .then((response) => response.json())
    .then((data) => data.results);
};

// Use switchMap to fetch search results for each query
searchQueriesObservable
  .pipe(
    switchMap((query: string) => fetchSearchResults(query))
  )
  .subscribe((searchResults) => console.log(searchResults));
```

In this example, we have an observable `searchQueriesObservable` that emits search queries from an input field. We use `fromEvent` to create an observable that listens to the `'input'` event on the input field.

The `debounceTime` operator is used to introduce a 500ms delay between user inputs to avoid making multiple HTTP requests in quick succession.

The `distinctUntilChanged` operator ensures that only distinct search queries are emitted, preventing redundant HTTP requests for the same search query.

The `switchMap` operator is then used to transform each emitted search query into an inner observable (`fetchSearchResults(query)`). Whenever a new search query is emitted, `switchMap` unsubscribes from the previous inner observable and subscribes to the latest inner observable (i.e., the inner observable corresponding to the latest search query). This effectively cancels any ongoing HTTP requests from previous search queries.

As a result, the output shows the search results for the latest search query, and outdated search results from previous queries are not emitted.

In summary, `switchMap` is a powerful operator to handle scenarios where you want to switch to a new inner observable whenever a new value is emitted from the source observable. It's commonly used for scenarios like type-ahead search, autocomplete suggestions, and any situation where you need to cancel previous operations when new ones are initiated.