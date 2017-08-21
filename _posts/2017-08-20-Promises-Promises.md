---
layout: post
title: "Promises, promises"
date: 2017-08-20 T19:00:00Z
---

I've been stretching my learning muscles again and getting back into JavaScript. By far the most frustrating thing I have found to date is the unpredictability of async functions but using the 'Promises' toolbox I have been able to overcome my nightmares and have a ton of fun instead.

JavaScript is single-threaded, meaning it can only handle one bit of script at a time. To overcome this and give our code the power to multi-task, we can use event listeners and callbacks.

Promises are like event listeners only instead of being able to listen out for things that could happen multiple times, they do  a better job of handling async success/failure.

A promise can be in one of four states:
- Pending - hasn't fulfilled or rejected yet
- Fulfilled - the promised action succeeded
- Rejected - the promised action failed
- Settled - the promise has fulfilled or rejected

Here's an example of setting up a Promise using ES6 syntax:
```javascript
var promise = new Promise( (resolve, reject) => {
  // do a thing, which can be async, then...
  if (/* promise is fulfilled */){
    resolve("Promise fulfilled!");
  } else {
    reject(Error("Promise rejected :("));
  }
})
```
Did you see that the reject statement uses an ```Error()``` function? That's custom rather than requirement but it can be really useful for debugging because it captures the stack trace if the promise is rejected.

That promise pattern is only half complete though! This is how to use it:
```javascript
promise.then((result) => {
  console.log(result);  // "Promise fulfilled!"
}, (err) => { console.log(err); }) // "Promise rejected :("
```
Look at that ```.then()``` function! It takes two arguments, although these are optional. They are both callbacks, one for success, one for failure.

What's more, and this is really cool, the 'then's can be chained together to queue up and run async functions one after another. This uses some transformation magic but once understood it can be powerful.

After you use a ```.then()``` and return a value, the next ```.then()``` in the chain is called with that venue. What's more, if the thing to be returned is promise-like, the function will wait until the promise is settled before continuing.

```javascript
let studentPromise

function getStudent(name) {
  studentPromise = studentPromise || getJSON('studentRegister.json');

  return studentPromise.then((studentRegister) => {
    return getJSON(studentRegister.students[name]);
  })
}

// and to use it with a queue of then()s:
getStudent('Chris').then((student) => {
  console.log(student); // { name: 'Chris', studying: 'JavaScript' }
  return getStudent('Dave');
}).then((student) => {
  console.log(student); // { name: 'Dave', studying: 'Ruby' }
}).catch(function(error) {
  console.log("Failed!", error);
})
```
I've cheekily added a ```.catch()``` to the above but I'm sure you'll forgive me when I explain that it's just like another ```.then()``` except a bit neater. There are some great examples of how this (and everything else I've talked about) can be used to handle errors in a try / catch flow here in the [Google Web Fundamentals](https://developers.google.com/web/fundamentals/getting-started/primers/promises) docs.

So there you have it, a neat way of handling async functions and potential errors! That's why promises in JavaScript are a welcome addition.



NB: I'm really bad at semi-colons in ES6 so have largely put them everywhere... I read that they can be omitted in certain situations because of [Automatic Semi-Colon Insertion (ASI)](https://www.ecma-international.org/ecma-262/5.1/#sec-7.9).
