---
title: "JavaScript Essentials: Understanding Scope, Lexical Environment, and Hoisting"
seoTitle: "JavaScript Basics: Scope, Lexical, Hoisting"
seoDescription: "Master JavaScript Scope, Lexical Environment, and Hoisting: Key concepts for writing predictable and bug-free code"
datePublished: Mon May 27 2024 19:29:53 GMT+0000 (Coordinated Universal Time)
cuid: clwpd4sfg000008mig7zh7jef
slug: javascript-essentials-understanding-scope-lexical-environment-and-hoisting
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716837913690/e6b4c3b2-8bcf-4f94-8340-ff3212fb9a55.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1716838149909/186256b6-62a4-434a-9369-d12af05d53ce.jpeg
tags: javascript, localhost, functional-programming, blockchain, hoisting, scope, lexical-environment, temporal-dead-zone, tdz, local-scope, scope-chain, javascript-hoisting, global-scope, block-scope, function-scope

---

Unveiling JavaScript Scope, Lexical Environment, and Hoisting: Demystifying Key Concepts

### Scope: Where Variables and Functions Live

Scope determines where you can access a specific variable or function in your code. It is directly dependent on the lexical environment.

### Types of Scope

1. **Global Scope**:
    
    * Variables declared outside any function are in the global scope.
        
    * Accessible from anywhere in the code.
        
    
    ```javascript
    var globalVar = "I'm global";
    
    function foo() {
        console.log(globalVar); // Accessible here
    }
    
    foo();
    console.log(globalVar); // Accessible here too
    ```
    
2. **Local/Function Scope**:
    
    * Variables declared within a function are in the local scope.
        
    * Accessible only within that function.
        
    
    ```javascript
    function bar() {
        var localVar = "I'm local";
        console.log(localVar); // Accessible here
    }
    
    bar();
    console.log(localVar); // ReferenceError: localVar is not defined
    ```
    
3. **Block Scope**:
    
    * Variables declared with `let` or `const` within a block (`{}`) are in the block scope.
        
    * Accessible only within that block.
        
    
    ```javascript
    if (true) {
        let blockVar = "I'm block scoped";
        console.log(blockVar); // Accessible here
    }
    
    console.log(blockVar); // ReferenceError: blockVar is not defined
    ```
    

### What is a Lexical Environment?

A lexical environment is created whenever an execution context is established. It includes the local memory and the lexical environment of its lexical parent. Lexical here means the order or hierarchy in which code is written. For instance:

```javascript
function a() {
    c();
    function c() {
        console.log(b);
    }
}
var b = 10;
a();
```

In this example:

* `c()` is lexically inside `a()`, meaning it is physically within the `a()` function.
    
* `a()` is lexically inside the global scope.
    

### Call Stack and Lexical Environment

Let's create a call stack for the above code:

1. **Global Execution Context**: Created first, with `b` being assigned a value of `10`.
    
2. **Function** `a()` Execution Context: Created when `a()` is called.
    
3. **Function** `c()` Execution Context: Created when `c()` is called within `a()`.
    

Each execution context has its lexical environment, which contains its local variables and a reference to its lexical parent's environment.

### Scope Chain

The scope chain is the chain of all lexical environments and their parent references. This allows functions to access variables from their lexical parents.

### Hoisting: `var`, `let`, and `const`

#### `var`

Variables declared with `var` are hoisted to the top of their scope and are attached to the global object if declared globally.

#### `let` and `const`

Variables declared with `let` and `const` are also hoisted but to a separate memory space than the global object. They are not accessible until they have been initialized, resulting in a concept called the Temporal Dead Zone (TDZ).

### Temporal Dead Zone (TDZ)

The TDZ is the time between the hoisting of a `let` or `const` variable and its initialization. During this time, accessing the variable will result in a Reference Error.

Example:

```javascript
console.log(a); // Uncaught ReferenceError: Cannot access 'a' before initialization
let a = 5;
```

In this example, `a` is in the TDZ until it is initialized with the value `5`.

Understanding these concepts is crucial for writing predictable and bug-free JavaScript code. It helps you grasp how variables are stored, accessed, and manipulated in different scopes and contexts within your program.