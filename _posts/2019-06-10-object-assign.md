---
layout: post
title: Object.assign()
subtitle: Learn how to use Object.assign() in JavaScript
tags: [javascript]
---

In this article, we will teach you how to use the JavaScript  `Object.assign()`  method which is available in modern JS starting with ES6+.

The  `Object.assign()`  only performs a shallow clone, not a deep clone.

This is the syntax of the  `Object.assign()`  method:

```js
Object.assign(target, ...sources)
```

The  `Object.assign()`  method works by copying all enumerable and own properties from the  `source`  objects to the  `target`  object and returns the  `target`  object.

The  `Object.assign()`  methods calls the getters on the source objects and setters on the target. It assigns properties only, not copying or defining new properties.

## Using JavaScript  `Object.assign()`  to clone an object

The example below makes use of the  `Object.assign()`  method to  clone an object.

```js
let comp = {
    bg: 'black'
};

let clonedComp = Object.assign({}, comp);
console.log(clonedComp);
```

The output in the browser's console will be:

```
{ bg: 'black' }
```

## Using JavaScript  `Object.assign()`  to merge objects

The  `Object.assign()`  can be used to merge source objects into a target object which has properties consisting of all the properties of the source objects. For example:

```js
let A = {
    height: 10,
    width: 20
};

let B = {
    color: 'Red',
    borderStyle: 'solid'
};

let AB = Object.assign({}, A, B);

console.log(AB);

``` 

The output will be:

`{
    height: 10,
    width: 20,
    color: 'Red',
    borderStyle: 'solid'
}` 


If the source object contains the same property as the target, the property of the later object overwrites the earlier one.

## Summary

The `Object.assign()`  method assigns enumerable and own properties from a source object to a target object.
