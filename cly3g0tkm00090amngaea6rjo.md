---
title: "Asynchronous JavaScript and Event Loops: Unleashing the Superpowers of Browsers"
seoTitle: "JavaScript Asynchronous Event Loops Explained"
seoDescription: "Learn how asynchronous JavaScript and event loops unlock the superpowers of modern web browsers for efficient, responsive applications"
datePublished: Mon Jul 01 2024 20:39:16 GMT+0000 (Coordinated Universal Time)
cuid: cly3g0tkm00090amngaea6rjo
slug: asynchronous-javascript-and-event-loops-unleashing-the-superpowers-of-browsers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719866007988/9990f567-887d-4566-afe8-e5ddc6019020.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1719866321259/c7ea1ddd-4f96-41a0-9dd3-9dee61af1a85.jpeg
tags: javascript, browsers, web-development, promises, windows, reactjs, webapi, callback, event-loop, chrome-cj73auo4o0012c3wted1yb7a1, settimeout, callstack, callback-hell, event-listeners-in-javascript, starvation

---

---

## **Introduction to Browser Capabilities**

Browser is one of the most remarkable creations in the history of mankind. Browsers have the JS engine inside them and they also have the local storage to store some data. They have a timer as well which you can access a timer inside the browser. And by the browser, you can connect to a server using a URL like https:// and you can fetch some data from there and then you can show the data in the UI. And browsers also have access to other superpowers like Bluetooth access and geolocation access. That is why browsers are considered one of the most remarkable creations in the history of mankind.

---

## **Accessing Browser Superpowers in JavaScript**

![browser](https://cdn.hashnode.com/res/hashnode/image/upload/v1719864050903/b6edb8ba-6d41-48df-b869-2e6b2ee82fc5.png align="center")

Now the question arises, How do we access these superpowers of the browser inside the JavaScript code? The JS engine needs to have a way to access these superpowers. Therefore, to achieve this, there is a way in which we can establish a connection. The JS engine needs to have a way to access these superpowers of the browser. Therefore to achieve this there is something known as Web APIs.

### Some of the Web APIs are:

* `setTimeout`
    
* `DOM APIs`
    
* `fetch`
    
* `localStorage`
    
* `console`
    
* `location`
    

![web api's](https://cdn.hashnode.com/res/hashnode/image/upload/v1719864192426/1972a5dd-9812-4a9f-bde2-c7ddf10866ec.png align="center")

`setTimeout` is not a part of JavaScript. And even DOM APIs like `document.getElementById` are not a part of JavaScript. All of these things are basically the superpowers of the browser. And the browser is providing us access to these superpowers inside the JS call stack or JavaScript engine.

Suppose you need to access a timer inside the browser. The browser is giving you access to `setTimeout`. If you need to access the DOM tree (HTML script), the browser gives you access to the DOM tree through the DOM APIs. If you need to access the server, there is something known as `fetch` which allows you to make a connection to the external server which is incredibly powerful. All of these capabilities are provided by the browser. We get access to these superpowers inside the call stack because of the global object (window).

---

## **Understanding the Global Object (Window)**

### What is the global object?

The global object is window. In the case of browsers, the browser is giving the JS engine the facility to use all the superpowers through the keyword known as window. Suppose you want to use the superpowers of a timer inside the JS code. You will use `window.setTimeout()`. If you write `window.setTimeout()` inside your JS code it will give you access to the timer. The same applies to all Web APIs.

But if you write code, you don’t write `window.setTimeout()` you only write `setTimeout()`. Why? Because window is the global object and all the Web APIs are present in the global object or at the global scope. Therefore you can access them without the keyword window. Whether you write `window.setTimeout()` or just `setTimeout()`, it is the same thing. The browser wraps up all the Web APIs into the global object (window) and is providing you access to these superpowers to the JS call stack or JavaScript engine.

---

## **Example of Asynchronous Code Execution**

```javascript
console.log("start");
setTimeout(function cb() {
    console.log("callback");
}, 5000);
console.log("end");
```

In this example, the first line `console.log("start")` calls the console API which internally modifies or logs something inside the console. These APIs are provided through the window to your code which is executed inside the global execution context.

Next, setTimeout is called. What does `setTimeout` do? `setTimeout` calls the Web API `setTimeout()` which gives access to the timer feature of the browser. This is one of the superpowers of the browser. It takes a callback function and a delay and registers a callback `cb()`. The 5000 ms timer starts and the JS code moves to the next line without waiting.

The next line calls the console API and logs “end” to the console. Meanwhile, the timer is still counting down the 5000 ms. Once all the code is executed and the global execution context is popped off the stack, the timer is still running. When the timer expires, the callback function `cb()` needs to be executed. Since all the code in JavaScript is executed inside the call stack, the callback function must be placed inside the call stack.

### Here the Event loop and the Callback queue comes into the Picture.

![event loop callback queue](https://cdn.hashnode.com/res/hashnode/image/upload/v1719864235522/16b1aeb0-886a-41ac-8699-80bee31c4220.png align="center")

As soon as the timer expires, the callback function is put inside the callback queue. The event loop checks this queue and pushes the function into the call stack. The call stack then quickly executes whatever comes inside it. The event loop acts as a gatekeeper checking the callback queue and pushing any waiting functions inside the call stack. As soon as the 5000 milliseconds expire, the callback function `cb()` is pushed inside the callback queue. The event loop then checks the queue and pushes the function inside the call stack for execution.

---

## **Example of Event Listener Registration**

```javascript
console.log("start");
document.getElementById("btn").addEventListener("click", function cb() {
    console.log("callback");
});
console.log("end");
```

In this example, just like in the previous example, the global execution context is created. The first line calls the console API and logs “start” inside the console. The code then moves to the next line: `document.getElementById("btn").addEventListener`.

### What is addEventListener?

It is another superpower provided by the browser to the JS engine through the window object in the form of the Web API, specifically the DOM API. When you use something like `document.`, you are calling the DOM API to fetch something from the DOM which is the Document Object Model (the HTML script). The DOM API accesses the HTML to find the element with the ID `btn` and returns it. If you add `.addEventListener` it registers a callback on the `click` event. This callback is `cb()` and the event is `click`. This process is known as registering a callback.

In the Web API environment, whenever you see addEventListener, it registers a callback function and attaches an event to it. The code then moves on to the next line, which is `console.log("end")`. This calls the console API and logs “end” inside the console. When there is nothing left to execute, the global execution context is popped off the stack. However, the event handler remains in the Web API environment until it is explicitly removed or the browser is closed. This registered callback method stays there, waiting for a user to click the button. When the user clicks the button, the callback method is pushed into the callback queue, waiting for its turn to be executed.

---

## **Event Loop and Callback Queue Interaction**

![interaction event loop and callback](https://cdn.hashnode.com/res/hashnode/image/upload/v1719864449272/641a0b13-8f59-4af6-8346-5c8941dc7b54.png align="center")

The event loop continuously monitors the call stack and the callback queue. If the call stack is empty and there is a callback function waiting in the callback queue, the event loop pushes the function into the call stack for execution. Once the function is picked from the callback queue by the event loop, it is removed from the queue.

---

## **Why Do We Need a Callback Queue?**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719864569932/f0fc03ec-f34b-46be-b47f-a5a147e759be.png align="center")

You might wonder why we need a callback queue and why we can't directly pick the callback from the Web API environment and push it into the call stack. The reason is that, in a real-world application, there are many event listeners and other things happening inside the browser. For example, if a user clicks a button 7-8 times in quick succession, the callback function is pushed into the callback queue 7-8 times. The event loop will continuously check if the call stack is empty and then push the functions from the callback queue into the call stack one by one.

---

## **Handling Promises and the Microtask Queue**

### The fetch API works differently from other APIs.

Consider the following code:

```javascript
console.log("start");
setTimeout(function cbt() {
    console.log("cb settimeout");
}, 5000);
fetch("https://api.netflix.com").then(function cbf() {
    console.log("cb Netflix");
});
// millions of lines
console.log("end");
```

Fetch makes a network call and returns a promise. You pass a callback function that executes once the promise is resolved. As in the previous examples, the global execution context is created and pushed inside the call stack and the code starts executing line by line. The first line logs “start” to the console. The `setTimeout` registers a callback function `cbt()` in the Web API environment and the 5000 ms timer starts. The JS engine then moves to the next line.

The `fetch` function registers a callback function `cbf()` in the Web API environment. Now, there are two functions in the Web API environment: `cbf()` and `cbt()`. The `cbt()` function waits for the timer to expire while `cbf()` waits for data from the Netflix server. When the `fetch` function receives data, the callback function `cbf()` is ready to execute.

Suppose the Netflix server responds within 50 ms. The callback function `cbf()` is now ready to execute. Does it go to the callback queue? No, it doesn't.

### Here comes the confusing part: The Microtask Queue.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719864607164/7d8165bf-98cf-49d7-9178-b3bb9acee7b2.png align="center")

The microtask queue is similar to the callback queue but has higher priority. Callback functions from promises and network calls go to the microtask queue. The event loop checks if the call stack is empty and then pushes functions from the microtask queue into the call stack.

Suppose the Netflix server responds within 50 ms, but the timer still has 4950 ms remaining. The `cbf()` function is pushed into the microtask queue, which has higher priority than the callback queue. The event loop first checks the call stack and finds millions of lines of code still executing. It takes some time to execute, but the callback function `cbf()` is already waiting in the microtask queue.

---

## **Event Loop Behavior**

When the main thread is busy running millions of lines of code, the event loop continuously checks whether the call stack is empty. If it is empty, the event loop schedules both tasks: those in the microtask queue and those in the callback queue.

Suppose the billions of lines of code finish executing and we reach `console.log("end")`. The console logs “end” first. Once there is nothing else to execute, the global execution context is popped off the stack. The event loop then checks the call stack and the microtask queue, giving higher priority to the microtask queue. It takes the `cbf()` function from the microtask queue, pushes it inside the call stack, and the function logs “cb Netflix” to the console. The function then finishes executing and is removed from the call stack. The event loop then gives a chance to the callback queue, where `cbt()` is waiting. The event loop schedules the `cbt()` function, pushes it into the call stack, and it logs “cb settimeout” to the console. The whole code finishes executing.

---

## **Importance of the Microtask Queue**

What can come inside the microtask queue? All the callback functions which come through promises go inside the microtask queue. There is also something known as a mutation observer, which checks for mutations in the DOM tree and executes callback functions accordingly. Both promises and mutation observers go inside the microtask queue. However, callback functions from `setTimeout` and DOM APIs like event listeners go inside the callback queue, also known as the task queue.

---

## **Prioritization of Microtasks and Callback Queues**

### What is Starvation ?  

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719864730470/73ade1e8-9d6e-48d6-ae57-278b2fed3365.png align="center")

One more important thing to note: Suppose there are three microtasks pending inside the microtask queue, and we have one task in the callback queue. So the event loop will only give the opportunity to the callback queue task once all the tasks from the microtask queue are completed. One more important point is: Just because the event loop will give the first priority to the microtask queue, suppose if the microtask creates a new microtask in itself and the new microtask creates another one and so on, then the task over in the callback queue will never get a chance to execute. Right? Because the microtask has more priority, that means there is a possibility that the task waiting in the callback queue does not get a chance to get executed for a long time. And in this case, this is known as starvation, the starvation of the callback queue or the task inside the callback queue. This is the possibility. This was what happened....