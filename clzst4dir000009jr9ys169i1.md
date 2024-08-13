---
title: "Today, I Deepened My Understanding of the fetch Function"
seoTitle: "How Fetch works"
seoDescription: "Deep dive into the `fetch` function: understanding data handling, web environment requests, and promise fulfillment in web development"
datePublished: Tue Aug 13 2024 19:19:53 GMT+0000 (Coordinated Universal Time)
cuid: clzst4dir000009jr9ys169i1
slug: today-i-deepened-my-understanding-of-the-fetch-function
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1723576497753/2aa6e6bb-15f3-421e-8e45-733db1c1499d.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723576750261/1772afeb-cb6a-4655-82db-5b264d810c52.jpeg
tags: programming-blogs, javascript, asynchronous, web-development, nodejs, promises, coding, frontend-development, fetch, web-api, fetch-api, asynchronous-programming, programming-concepts, codingtutorial

---

---

Hey folks! Today, I delved into something that's been a part of my coding life for a while, but I never really stopped to appreciate its inner workings—the `fetch` function. It's a crucial tool, especially in web development, where we're constantly dealing with API requests and handling data. So, I thought, why not take a closer look and share what I learned?

---

## How `Fetch` Works

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1723576526393/282b0025-475a-40ef-ab89-1cbbd84ae01c.png align="center")

The working mechanism of the `fetch` function has been divided into two parts. One part handles the browser or Node.js API request, and the other is responsible for reserving the data space in variables and memory.

## Part 1: Data Handling

The first part is the data handling, though the actual name "Data" can be anything else. There are two arrays associated with it:

1. **onFulfilled\[\]**: This array handles the resolution of the promise or `resolve()`.
    
2. **onRejection\[\]**: This array handles the rejection of the promise or `reject()`.
    

Both `onFulfilled[]` and `onRejection[]` are arrays, but we are not allowed to push values into these arrays. These are not within our range, and we cannot access them. These are private fields, and even the `Data:__` is also a private field.

## Part 2: Web Browser/Node.js Handling

The second part is handled by the Web Browser or Node.js environment, which manages our browser-based API or Node API. From this part, the network request is thrown. We are not able to send the network request directly; some middle resource is mandatory to send the network request. Here, the network resource is provided by the browser or the Node.js environment.

Once the network request is made, the request either goes to the network or not. If the network request reaches the network and we receive any response, even a 404 error (Not Found), the response goes to the `onFulfilled[]` array or `resolve()`.

For example, if we get a 404 error, it means the request went to the network; otherwise, we wouldn't receive the 404 error. If the request is stuck and cannot reach the network, the rejection will be thrown and passed to the `onRejection[]` array or `reject()`.

## Final Step: Data Fulfillment

Then next, `Data:__` is reserved in the memory. The value of `Data:__` is initially empty or undefined. The request is fulfilled or rejected, then there is a function in the `onFulfilled[]` or `onRejection[]`, and this function is responsible to fulfill the `Data:__`. Once the data is fulfilled, the `response` variable we created will be available in the global memory. So this is the responsibility of the data to fulfill the response.

---