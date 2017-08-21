---
layout: post
title: "Promises, promises"
date: 2017-08-20 T19:00:00Z
---

JavaScript is single-threaded, meaning it can only handle one bit of script at a time. To overcome this and give our code the power to multi-task, we use event listeners and callbacks.

Promises are like event listeners only instead of being able to listen out for things that could happen multiple times, they do  a better job of handling async success/failure.

A promise can be in one of four states:
- Pending - hasn't fulfilled or rejected yet
- Fulfilled - the promised action succeeded
- Rejected - the promised action failed
- Settled - the promise has fulfilled or rejected

Here's an example of setting up a Promise using ES6 syntax:
```javascript
var Promise = new Promise( (resolve, reject) => {
  // do a thing, which can be async, then...
  if (/* promise is fulfilled */){
    resolve("Promise fulfilled!")
  } else {
    reject(Error("Promise rejected :("))
  }
})
```
Did you see that the reject statement uses an ```Error()``` function? That's custom rather than requirement but it can be really useful for debugging because it captures the stack trace if the promise is rejected. 


References:  
[Google Web Fundamentals](https://developers.google.com/web/fundamentals/getting-started/primers/promises)