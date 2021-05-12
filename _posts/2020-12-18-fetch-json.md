---
layout: post
title: Use the JavaScript Fetch API to Get JSON Data
subtitle:
categories: javascript
tags: [javascript]
---


The  [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)  is a newer built-in feature of JavaScript that makes working with requests and responses easier.

```js
// Replace ./data.json with your JSON feed
fetch('./data.json')
  .then((response) => {
    return response.json()
  })
  .then((data) => {
    // Work with JSON data here
    console.log(data)
  })
  .catch((err) => {
    // Do something for an error here
  })
```

Note that with Fetch, even a  `404`  or  `500`  error will not return an error. Only a network error or a request not completing will throw an error.
