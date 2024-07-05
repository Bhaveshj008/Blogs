---
title: "Understanding Closures in JavaScript"
seoTitle: "JavaScript Closures Explained"
seoDescription: "Understanding closures in JavaScript: concept, uses, pitfalls, and examples for mastering asynchronous code and robust applications"
datePublished: Wed May 29 2024 19:30:59 GMT+0000 (Coordinated Universal Time)
cuid: clws81wby000109l5fxkmb5a0
slug: understanding-closures-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1717010898449/51899396-f2c6-48c4-83c2-13a5392e6dbe.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1717011027617/f33e521d-6d24-42d6-990c-d0a7fe05e7d0.jpeg
tags: closure, js, javascript, asynchronous, web-development, react-native, fundamentals, reactjs, javascript-framework, memoization, settimeout, iterator, currying, lexical-scope, next-js-tips

---

---

Closures in JavaScript can seem like a complex concept, but they are fundamental to understanding how the language works. In essence, a closure is a function bundled together with its lexical environment. This means that a function, along with the variables it was declared with, forms a closure. This bundled structure allows the function to access those variables even after it has been executed outside its original scope.

## Uses of Closures

Closures are incredibly powerful and versatile, and they have several practical applications in JavaScript:

* **Module Design Pattern**: Encapsulating private data.
    
* **Currying**: Creating functions with preset arguments.
    
* **Functions like Once**: Ensuring a function is called only once.
    
* **Memoization**: Caching results of expensive function calls.
    
* **Maintaining State in Async World**: Managing state across asynchronous operations.
    
* **SetTimeouts**: Delaying execution of code.
    
* **Iterators**: Generating sequences of values.
    

### Example: `setTimeout` and Closures

Consider the following example to understand how `setTimeout` interacts with closures:

```javascript
function x() {
    var i = 1;
    setTimeout(function() {
        console.log(i);
    }, 3000);
    console.log("Namaste JavaScript");
}
x();
```

In this example, many might think that JavaScript’s `setTimeout` will wait before executing the callback function. However, JavaScript does not wait. It prints "Namaste JavaScript" first, then waits for 3000 milliseconds before printing the value of `i`. The callback function forms a closure, remembering the reference to `i`, and after the timer expires, it logs the value of `i`.

### Common Pitfall

Let’s examine a common mistake when using `setTimeout` inside a loop:

```javascript
function x() {
    for (var i = 1; i <= 5; i++) {
        setTimeout(function() {
            console.log(i);
        }, i * 1000);
    }
    console.log("Namaste JavaScript");
}
x();
```

You might expect this code to print "Namaste JavaScript" followed by 1, 2, 3, 4, 5, each after a second. However, the output is "Namaste JavaScript" followed by 6 five times. Why does this happen?

#### Explanation:

Due to closure, all `setTimeout` callbacks remember the reference to `i`, not its value. By the time the timers expire, the loop has completed, and `i` equals 6. All callbacks then log the final value of `i`.

### Fixing the Issue

To fix this issue, use `let` instead of `var`:

```javascript
function x() {
    for (let i = 1; i <= 5; i++) {
        setTimeout(function() {
            console.log(i);
        }, i * 1000);
    }
    console.log("Namaste JavaScript");
}
x();
```

Here, `let` creates a new block-scoped variable `i` for each iteration, resulting in the desired output: "Namaste JavaScript", then 1, 2, 3, 4, 5 each after a second.

### Achieving the Same Without `let`

If you must use `var`, you can create a new scope using a function:

```javascript
function x() {
    for (var i = 1; i <= 5; i++) {
        (function(i) {
            setTimeout(function() {
                console.log(i);
            }, i * 1000);
        })(i);
    }
    console.log("Namaste JavaScript");
}
x();
```

In this version, the immediately invoked function expression (IIFE) creates a new scope, capturing the value of `i` for each iteration. This ensures each `setTimeout` callback logs the correct value.

### Conclusion

Closures are a powerful feature in JavaScript that allow functions to remember their lexical environment. Understanding closures and how they work with asynchronous code, such as `setTimeout`, is crucial for mastering JavaScript. By leveraging closures, you can write more robust and maintainable code.

---

By understanding and using closures effectively, you can tackle complex programming challenges in JavaScript with confidence and ease. Happy coding!