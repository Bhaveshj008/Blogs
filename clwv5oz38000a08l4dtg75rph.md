---
title: "Important Terminologies in JavaScript"
seoTitle: "Key JavaScript Terms Explained"
seoDescription: "Key JavaScript terminologies explained: function statements, expressions, anonymous functions, first-class functions, callbacks, and more"
datePublished: Fri May 31 2024 20:48:15 GMT+0000 (Coordinated Universal Time)
cuid: clwv5oz38000a08l4dtg75rph
slug: important-terminologies-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1717188268231/8f41938a-4098-4080-ab28-2595e94f2a49.jpeg
tags: javascript, web-development, webdev, reactjs, functional-programming, function-expressions, anonymous-function, callback-functions, first-class-functions, function-declaration, named-function-expression, javascript-terminologies

---

## 1\. Function Statement

A function statement is a simple way of creating a function:

```javascript
function a() {
  console.log("a called");
}
```

This simple way of creating a function is known as a function statement.

## 2\. Function Expression

A function expression is when a function acts like a value of a variable:

```javascript
var b = function() {
  console.log("b called");
};
```

## 3\. Difference Between Function Statement and Function Expression

The major difference between these two is hoisting:

```javascript
a(); // Output: "a called"
b(); // Output: TypeError

function a() {
  console.log("a called");
}

var b = function() {
  console.log("b called");
};
```

In this code, during the hoisting phase (the memory allocation phase), `a` is assigned its function definition. But in the case of a function expression, `b` is treated like any other variable and is assigned `undefined` initially. Until the code hits `b = function()`, `b` remains undefined. Therefore, calling `b()` before its definition results in an error. This is the major difference between a function statement and a function expression.

## 4\. Function Declaration

A function declaration is nothing but a function statement. Function declaration and function statement are the same things:

```javascript
function a() {
  console.log("a called");
}
```

## 5\. Anonymous Function

An anonymous function is a function without a name:

```javascript
function() {
  // Code
}
```

Anonymous functions do not have their own identity. Creating an anonymous function like this will give you a syntax error:

```javascript
function() {
  // Code
}
```

Because an anonymous function looks like a function statement but has no name, according to the ECMAScript specification, functions should always have a name. Therefore, `function () {}` is invalid syntax. Anonymous functions are used where functions are used as values:

```javascript
var b = function() {
  console.log("b called");
};
```

## 6\. Named Function Expression

A named function expression is like a function expression but with a name:

```javascript
var b = function xyz() {
  console.log("b called");
};
```

If you call `b()`, it works, but calling `xyz()` will give an error. `xyz` is not defined in the outer scope; it is only available inside the function itself:

```javascript
var b = function xyz() {
  console.log(xyz);
};

b(); // Prints the function definition
xyz(); // ReferenceError: xyz is not defined
```

## 7\. Difference Between Parameters and Arguments

Parameters are the names listed in the function definition, while arguments are the values passed to the function when it is invoked:

```javascript
function a(param1, param2) {
  console.log("hello");
}

a(1, 2); // 1 and 2 are the arguments
```

## 8\. First-Class Functions

The ability to use a function as a value is known as a first-class function. The ability of a function to be used as a value and passed as an argument to another function, or returned from a function, is known as a first-class function. This ability is known as a first-class function. For example:

```javascript
var b = function(x) {
  console.log(x);
};

b(function() {
  console.log("Anonymous function");
});

function xyz() {
  console.log("Named function");
}

b(xyz);

var c = function() {
  return function() {
    console.log("Returned anonymous function");
  };
};

console.log(c()());
```

First-class functions allow us to treat functions like any other value, also referred to as "first-line citizens."

## 9\. Callback Functions

Callback functions are first-class citizens in JavaScript. This means you can take a function and pass it into another function, and when you do so, the function you pass into another function is known as a callback function. Callback functions are very powerful in JavaScript. They give us access to the asynchronous world in a synchronous single-threaded language. Due to callbacks, we can do asynchronous things in JavaScript:

```javascript
function x(callback) {
  console.log("x");
  callback();
}

x(function y() {
  console.log("y");
});
```

If you call a function and pass a function into another function, the passed function is the callback function. This function is known as a callback function because it is called back later in the code. You give the responsibility of this function to another function. For example:

```javascript
setTimeout(function() {
  console.log("timer");
}, 5000);

function x(y) {
  console.log("x");
  y();
}

x(function y() {
  console.log("y");
});
```

JavaScript has just one call stack, also known as the main thread. Everything executed inside your page is executed through the call stack only. If any operation blocks the call stack, it is known as blocking the main thread. For example, if your function `x()` had a very heavy operation that takes around 20 to 30 seconds to complete, by that time, because JavaScript has only one call stack, it won't be able to execute any other function inside the code. That means everything will be blocked on the code. This is why we should never block our main thread. We should always try to use asynchronous operations for tasks that take time, just like using `setTimeout`:

```javascript
setTimeout(function() {
  console.log("timer");
}, 5000);

function x(y) {
  console.log("x");
  y();
}

x(function y() {
  console.log("y");
});
```

Using web APIs, `setTimeout`, and callback functions, we can achieve asynchronous operations in JavaScript.

---

We know how to use these concepts practically, but we often don't know the terminologies. If an interviewer asks what a function expression is, we might get stuck because we don't know the term. A function expression is when a function acts like a value of a variable:

```javascript
javascriptCopy codevar b = function() {
  console.log("b called");
};
```

However, we use this type of syntax many times in JavaScript coding without knowing what it's called.