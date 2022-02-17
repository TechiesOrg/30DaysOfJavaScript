---
layout: post
title: Load WebAssembly Modules in JavaScript
subtitle: How Load WebAssembly Modules in JavaScript
categories: javascript
tags: [javascript , node]
---


You can use the Fetch API to fetch .wasm file. The returned  `Promise`  instance of  `fetch`  is passed into  `WebAssembly.instantiateStreaming`. For example:

```js
WebAssembly.instantiateStreaming(fetch('program.wasm'), importObj)
           .then(prog => {
               console.log(prog.instance.exports.add(1, 2)); 
           });
```

`WebAssembly.instantiateStreaming`  would take out the  `ArrayBuffer`  instance from the  `Promise`  object and instantiate the module. The following code has the same effect as the above.

```js
fetch('program.wasm')
    .then(response => response.arrayBuffer())
    .then(wasm => WebAssembly.instantiate(wasm, importObj))
    .then(prog => {
        console.log(prog.instance.exports.add(1, 2)); 
    });
```

That's to say, what we want is the  `ArrayBuffer`containing your WebAssembly module binary so you can use  `XMLHttpRequest`  even through it's older than Fetch API.

```js
const request = new XMLHttpRequest();
request.responseType = 'arraybuffer';
request.onload = function() {
    const wasm = request.response;
    WebAssembly.instantiate(wasm, importObj)
               .then(prog => {
                   console.log(prog.instance.exports.add(1, 2)); 
               });
};
request.open('GET', 'program.wasm');
request.send();
```

`WebAssembly.instantiate`  accepts  `ArrayBuffer`  or  `TypedArray`  and returns  `Promise`. After the success of the asynchronous operation, the promise’s value is an object containing two properties  `module`  and  `instance`. The  `module`  property is an instance of  `WebAssembly.Module`. It contains stateless WebAssembly code that has already been compiled by the browser. The  `instance`  property is an instance of  `WebAssembly.Instance`. It contains all the exported WebAssembly functions that allow calling into WebAssembly code from JavaScript.

If only the instance of  `WebAssembly.Module`  is required, you may use  `WebAssembly.compileStreaming`. It accepts the returned  `Promise`  of  `fetch`  and returns  `Promise`. After completing the operation, the promise's value is an instance of  `Module`.

```js
WebAssembly.compileStreaming(fetch('program.wasm'))
       .then(module => new WebAssembly.Instance(module, importObj))
       .then(instance => {   
           console.log(instance.exports.add(1, 2)); 
       });
```

As shown in the above, you can take the  `Module`  object as the argument to constructing the  `Instance`  object. In fact,  `WebAssembly.compileStreaming`  will take out the  `ArrayBuffer`  and use  `WebAssembly.compile`  to compile it to a  `WebAssembly.Module`  instance. The following code has the same effect as the above.

```js
fetch('program.wasm')
    .then(response => response.arrayBuffer())
    .then(wasm => WebAssembly.compile(wasm))
    .then(module => new WebAssembly.Instance(module, importObj))
    .then(instance => {   
        console.log(instance.exports.add(1, 2)); 
    });
```

You can use a  `Module`  instance to construct a  `WebAssembly.Instance`  instance. If you have  `ArrayBuffer`, you can construct a  `WebAssembly.Module`  object.

```js
const module = new WebAssembly.Module(wasm);
```

Using  `new`  to construct  `WebAssembly.Instance`  or  `WebAssembly.Module`  is a blocking operation.  `WebAssembly.compile()`  and  `WebAssembly.instantiate()`  are asynchronous operations and return  `Promose`.

You can use  `WebAssembly.validate()`  to validate a given typed array of WebAssembly binary code.
