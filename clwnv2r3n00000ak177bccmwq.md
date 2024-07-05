---
title: "JavaScript Concepts: Hoisting, this Keyword, and Undefined vs. Not Defined"
seoTitle: "Hoisting, this Keyword, and Undefined vs. Not Defined"
seoDescription: "Learn the key JavaScript concepts of hoisting, the this keyword, and the difference between undefined and not defined to enhance your coding skills and writ"
datePublished: Sun May 26 2024 18:16:39 GMT+0000 (Coordinated Universal Time)
cuid: clwnv2r3n00000ak177bccmwq
slug: javascript-concepts-hoisting-this-keyword-and-undefined-vs-not-defined
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716746850131/dee4babd-c207-41e4-b8aa-fa947f4ab8bf.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1716746889796/30e99116-5144-44e6-841f-d384198fee90.jpeg
tags: programming-blogs, js, javascript, frontend, web-development, coding, frontend-development, hoisting, undefined, this-keyword, javascript-concept, not-defined, javascript-best-practices, js-execution-context, undefined-vs-not-defined

---

---

JavaScript is a versatile and powerful language, but it comes with some concepts that can be tricky to understand. In this blog, we’ll explore three important concepts: hoisting, the `this` keyword, and the difference between `undefined` and `not defined`.

## Hoisting in JavaScript

Hoisting is a phenomenon in JavaScript where you can access variables and functions even before you initialize them. This happens because during the compilation phase, the JavaScript engine moves the declarations of variables and functions to the top of their containing scope. However, only the declarations are hoisted, not the initializations.

### Example:

```javascript
console.log(myVar); // Output: undefined
var myVar = 5;
console.log(myVar); // Output: 5

myFunction(); // Output: "Hello, World!"
function myFunction() {
  console.log("Hello, World!");
}
```

In the example above, the variable `myVar` and the function `myFunction` are hoisted. This means you can reference them before their actual declarations in the code.

## The `this` Keyword

The `this` keyword in JavaScript is a bit tricky as its value depends on the context in which it is used. In a global execution context (outside of any function), `this` refers to the global object, which is `window` in the case of browsers.

### Global Context:

```javascript
console.log(this === window); // Output: true
```

### Function Context:

When you create a function, `this` inside the function refers to the object from which the function was called, unless the function is called as a method of an object.

```javascript
function showThis() {
  console.log(this);
}

showThis(); // Output: window (in a browser)

const obj = {
  method: showThis
};

obj.method(); // Output: obj
```

### Important Points:

* At the global level, `this` points to the global object.
    
* Inside a function, `this` can vary depending on how the function is called.
    
* In strict mode, `this` will be `undefined` if the function is called without an object.
    

## Undefined vs. Not Defined

In JavaScript, `undefined` and `not defined` are different concepts.

### `undefined`:

When JavaScript allocates memory for variables and functions, it initializes them with the value `undefined`. This is a placeholder indicating that the variable has been declared but not yet assigned a value.

```javascript
var myVar;
console.log(myVar); // Output: undefined
```

### `not defined`:

A variable is `not defined` when it has not been declared in any scope accessible to the code being executed.

```javascript
console.log(myVar); // Output: Uncaught ReferenceError: myVar is not defined
```

### Key Differences:

* `undefined` means a variable has been declared but has not yet been assigned a value.
    
* `not defined` means the variable has not been declared in the current scope.
    

## Conclusion

Understanding these core JavaScript concepts—hoisting, the `this` keyword, and the difference between `undefined` and `not defined`—is crucial for mastering the language. These principles form the foundation of how JavaScript code is interpreted and executed, enabling you to write more predictable and error-free code.

Happy coding!

---