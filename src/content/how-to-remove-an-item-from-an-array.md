---
layout: post
title: How to Remove an Item from an Array
image: img/code-2.jpg
author: Don
date: 2019-02-05T07:03:47.149Z
draft: false
tags: ["JavaScript"]
---

We know we can use Lodash's <a href="https://lodash.com/docs/4.17.10#omit" target="_blank">_.omit</a> on an object to return a new object with some
keys removed.

```js
const myObject = {
    foo: 'bar',
    baz: 'quux',
    thud: 'grunt',
};

// We want a new object without the `foo` key/value pair
// The following returns 
// {
//    baz: 'quux',
//    thud: 'grunt',
// }
const myObjectWithoutFoo = _.omit(myObject, 'foo');
```
But what if we have an array and we just want to remove a specific value from the array? 

---

## Array.prototype.filter

Suppose now we have the following:

```js
const myArray = ['foo', 'bar', 'baz'];
```

To remove a specific value from the array, we can use JavaScript's
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter" target="_blank">Array.prototype.filter</a> function.

```js
const myArray = ['foo', 'bar', 'baz'];

// returns ['bar', 'baz']
const myArrayWithoutFoo = myArray.filter(val => val !== 'foo');
```



