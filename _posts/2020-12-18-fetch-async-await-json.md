---
layout: post
title: "Use JavaScript Fetch with async/await: Get JSON Data"
subtitle:
categories: javascript
tags: [javascript]
---


The  [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)  is the default tool to make network in web applications. While  `fetch()`  is generally easy to use, there some nuances to be aware of.

In this post, you’ll find the common scenarios of how to use  `fetch()`  with  `async/await`  syntax. You’ll understand how to fetch data, handle fetch errors, cancel a fetch request, and more.


## Intro to  _fetch()_

The Fetch API accesses resources across the network. You can make HTTP requests (using  `GET`,  `POST`  and other methods), download, and upload files.

To start a request, call the special function  `fetch()`:

```javascript
const response = await fetch(resource[, options]);
```

which accepts 2 arguments:

-   `resource`: the URL string, or a  [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request)  object
-   `options`: the configuration object with properties like  `method`,  `headers`,  `body`,  `credentials`,  [and more](https://javascript.info/fetch-api).

`fetch()`  starts a request and returns a promise. When the request completes, the promise is resolved with the  [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)  object. If the request fails due to some network problems, the promise is rejected.

`async/await`  syntax fits great with  `fetch()`  because it simplifies the work with promises.

For example, let’s make a request to fetch some movies:

```javascript
async function fetchMovies() {
  const response = await fetch('/movies');
  // waits until the request completes...
  console.log(response);
}
```

`fetchMovies()`  is an asynchronous function since it’s marked with the  `async`  keyword.

`await fetch('/movies')`  starts an HTTP request to  `'/movies'`  URL. Because the  `await`  keyword is present, the asynchronous function is paused until the request completes.

When the request completes,  `response`  is assigned with the response object of the request. Let’s see in the next section how to extract useful data, like JSON or plain text, from the response.

## Fetching JSON

The  `response`  object, returned by the  `await fetch()`, is a generic placeholder for multiple data formats.

For example, you can extract the JSON object from a fetch response:

```javascript
async function fetchMoviesJSON() {
  const response = await fetch('/movies');
  const movies = await response.json();  return movies;
}

fetchMoviesJSON().then(movies => {
  movies; // fetched movies
});
```

`response.json()`  is a method on the Response object that lets you extract a JSON object from the response. The method returns a promise, so you have to wait for the JSON:  `await response.json()`.

The  [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)  object offers a lot of useful methods (all returning promises):

-   `response.json()`  returns a promise resolved to a JSON object
-   `response.text()`  returns a promise resolved to raw text
-   `response.formData()`  returns a promise resolved to  [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)
-   `response.blob()`  returns a promise resolved to a  [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)  (a file-like object of raw data)
-   `response.arrayBuffer()()`  returns a promise resolved to an  [ArryBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)  (raw generic binary data)

## Handling fetch errors

When I was familiarizing with  `fetch()`, I was surprised that  `fetch()`  doesn’t throw an error when the server returns a bad HTTP status, e.g. client (`400–499`) or server errors (`500–599`).

For example, let’s access a non-existing page  `'/oops'`  on the server. As expected, such request ends in a  `404`  response status:

```javascript
async function fetchMovies404() {
  const response = await fetch('/oops');
  
  response.ok;     // => false
  response.status; // => 404

  const text = await response.text();
  return text;
}

fetchMovies404().then(text => {
  text; // => 'Page not found'
});
```

When fetching the URL  `'/oops'`  the server responds with status  `404`  and text  `'Page not found'`. Surprisingly,  `fetch()`  doesn’t throw an error for a missing URL, but considers this as a  _completed_  HTTP request.

`fetch()`  rejects only if a request cannot be made or a response cannot be retrieved. It might happen because of network problems: no internet connection, host not found, the server is not responding.

Fortunately,  `response.ok`  property lets you separate good from bad HTTP response statuses. The property is set to  `true`  only if the response has status  `200-299`.

In the above example, the  `response.ok`  property is  `false`  because the response has the status  `404`.

If you’d like to throw an error on a  _bad HTTP status_  (outside of the range  `200-299`), check the value of  `response.ok`  property and throw an error manually:

```javascript
async function fetchMoviesBadStatus() {
  const response = await fetch('/oops');

  if (!response.ok) {    const message = `An error has occured: ${response.status}`;    throw new Error(message);  }
  const movies = await response.json();
  return movies;
}

fetchMoviesBadStatus().catch(error => {
  error.message; // 'An error has occurred: 404'
});
```

## Canceling a fetch request

Unfortunately,  `fetch()`  API alone doesn’t allow to cancel a fetch request once started. To cancel a fetch request you need an additional tool  [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController).

Connecting  `fetch()`  and  `AbortController`  requires 3 steps:

```javascript
// Step 1: instantiate the abort controller
const controller = new AbortController();

// Step 2: make the fetch() aware of controller.signal
fetch(..., { signal: controller.signal });

// Step 3: call to cancel the request
controller.abort();
```

A) Before starting the request, create an abort controller instance:  `controller = new AbortController()`.

B) When starting the request properly, use the options argument of  `fetch(url, { signal: controller.signal })`  and set  `signal`  property to be  `controller.signal`.

C) Finally, if you need to cancel the request, just call  `controller.abort()`  method.

For example, let’s implement 2 buttons that control a fetch request. Clicking the button  _Fetch movies_  starts a  `fetch()`  request, while clicking  _Cancel fetch_  aborts the request in progress:

```javascript
let controller = null;

fetchMoviesButton.addEventListener('click', async () => {
  controller = new AbortController();  try {
    const response = await fetch('/movies', { 
      signal: controller.signal     });
  } catch (error) {
    console.log('Fetch error: ', error);
  }
  controller = null;
});

cancelFetchButton.addEventListener('click', () => {
  if (controller) {
    controller.abort();  }
});
```

Open  [the demo](https://codesandbox.io/s/cancel-fetch-request-ggieh?file=/src/index.html). Click  _Fetch movies_  to start the request, then right away click  _Cancel fetch_  to cancel it. This makes the active request cancel:  `await fetch()`  gets rejected by throwing an abort error. The  `catch`  block then catches the abort error.

The abort controller instances aren’t reusable. Each time you start a  `fetch()`  request, you have to create a new abort controller instance for each request.


## Parallel fetch requests

To perform parallel fetch requests use the  [Promise.all()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)  helper function.

Let’s start 2 parallel requests to fetch movies and categories:

```javascript
async function fetchMoviesAndCategories() {
  const [moviesResponse, categoriesResponse] = await Promise.all([    fetch('/movies'),    fetch('/categories')  ]);
  const movies = await moviesResponse.json();
  const categories = await categoriesResponse.json();

  return [movies, categories];
}

fetchMoviesAndCategories().then(([movies, categories]) => {
  movies;     // fetched movies
  categories; // fetched categories
}).catch(error => {
  // /movies or /categories request failed
});
```

`await Promise.all([...])`  starts fetch requests in parallel, and waits until all of them are resolved.

If any request fails, then the whole parallel promise gets rejected right away with the failed request error.

In case if you want all parallel requests to complete, despite any of them fail, consider using  [Promise.allSettled()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled).

##  Summary

Calling  `fetch()`  starts a request and returns a promise. When the request completes, the promise resolves to the response object. From the response object you can extract data in the format you need: JSON, raw text, Blob.

Because  `fetch()`  returns a promise, you can simplify the code by using the  `async/await`  syntax:  `response = await fetch()`.

You’ve found out how to use  `fetch()`  accompanied with  `async/await`  to fetch JSON data, handle fetching errors, cancel a request, perform parallel requests.

