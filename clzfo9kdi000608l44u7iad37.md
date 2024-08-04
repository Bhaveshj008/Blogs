---
title: "Today’s JavaScript Discovery: slice vs. splice - What’s the Difference?"
seoTitle: "JavaScript: Slice vs. Splice Differences"
seoDescription: "Learn JavaScript's `slice` (non-destructive) vs. `splice` (destructive) for array operations. Essential for your coding toolkit!"
datePublished: Sun Aug 04 2024 14:42:57 GMT+0000 (Coordinated Universal Time)
cuid: clzfo9kdi000608l44u7iad37
slug: todays-javascript-discovery-slice-vs-splice-whats-the-difference
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722782461870/574bc4f0-c694-4d9b-b9aa-a50a0d6add38.jpeg
tags: javascript, angularjs, web-development, react-native, vuejs, webdev, reactjs, javascript-framework, javascript-library, web3, web-1, slice-vs-splice

---

---

Hey folks,

I had a bit of a "Eureka!" moment today while working with JavaScript arrays. If you’ve ever used `slice` and `splice`, you might have wondered what exactly sets them apart. Well, I dug into it and thought I’d share what I found.

Let’s dive right in. Here’s a quick snippet of code I was experimenting with:

```javascript
let arr = [32, 43, 54, 56, 34, 12, 54, 76];
console.log(typeof(arr)); // object

console.log("A  ", arr);

// slice creates a new array by copying elements from the start index up to, but not including, the end index. It does not modify the original array.
console.log("using slice ", arr.slice(1, 4)); // [43, 54, 56]
console.log("B  ", arr); // [32, 43, 54, 56, 34, 12, 54, 76]

// splice takes the first parameter as the starting index and the second parameter as the count of elements to remove. It returns the removed elements.
// Any additional parameters (from the third parameter onwards) are optional and are added to the array starting from the position where the elements were removed.
console.log("using splice ", arr.splice(1, 4, 9999, 6666)); // [43, 54, 56, 34]
console.log("C  ", arr); // [32, 9999, 6666, 12, 54, 76]
```

### The `slice` Method

The `slice` method is your go-to when you need to extract a portion of an array without modifying the original. It returns a new array containing the selected elements. For example:

```javascript
arr.slice(1, 4);
```

This will give you a new array `[43, 54, 56]`, leaving the original array untouched. So if you need a snapshot of a part of your array, `slice` is your friend.

### The `splice` Method

On the other hand, `splice` is a bit more dramatic. It modifies the original array by removing or adding elements. Here’s what happened when I used `splice`:

```javascript
arr.splice(1, 4, 9999, 6666);
```

This line removed four elements starting from index 1 and then inserted `9999` and `6666` in their place. The result was that `arr` changed to `[32, 9999, 6666, 12, 54, 76]`, and the removed elements were `[43, 54, 56, 34]`.

### Key Takeaways

* `slice`: Non-destructive, returns a new array.
    
* `splice`: Destructive, modifies the original array and returns the removed elements.
    

So there you have it! If you’re ever unsure whether to use `slice` or `splice`, just remember what you need: a new array or modifications to the existing one. Happy coding!

Catch you later with more discoveries!

---