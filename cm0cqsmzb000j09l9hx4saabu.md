---
title: "Understanding Event Propagation in JavaScript"
seoTitle: "JavaScript Event Propagation Explained"
seoDescription: "Learn about event propagation in JavaScript, discovering how event bubbling and event capturing work and how to control them"
datePublished: Tue Aug 27 2024 18:10:10 GMT+0000 (Coordinated Universal Time)
cuid: cm0cqsmzb000j09l9hx4saabu
slug: understanding-event-propagation-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1724781943058/6b8d143f-829f-4555-a4cd-929805711d6c.png
tags: webdesign, javascript, angularjs, web-development, flutter, vuejs, reactjs, nextjs, reacthooks, event-propagation, event-handling, eventbubbling, event-capturing, keyboard-events-in-javascript, event-capturing-and-event-bubbling-in-javascript

---

---

In JavaScript, events like clicks don't just stay where they happen. They can move through different parts of your webpage, which is known as **event propagation**. Let's explore what this means, how it works, and how you can control it using event bubbling and event capturing.

## What is Event Propagation?

Event propagation describes how events move through the DOM (Document Object Model) when they are triggered. There are two main ways this can happen:

### 1\. Event Bubbling

* **Direction:** Bottom to Top
    
* **Explanation:** The event starts at the element where it was triggered and then moves up to its parent elements.
    
* **Example:** If you click on a button inside a `div`, the event first triggers on the button, then on the `div`, and finally on the `body`.
    

### 2\. Event Capturing

* **Direction:** Top to Bottom
    
* **Explanation:** The event starts from the root of the DOM (like the `body` or `html` tag) and travels down to the target element.
    
* **Example:** The event first triggers on the `body`, then the `div`, and finally on the button.
    

### Default Behavior in Browsers

In most browsers, **event bubbling** is the default behavior, meaning events move from the target element up to its parents. However, there are cases where you might want to use **event capturing** instead. You can control which one is used by specifying `true` or `false` when you add an event listener:

* `false` (default): Uses event bubbling (Bottom to Top).
    
* `true`: Uses event capturing (Top to Bottom).
    

### Controlling Event Propagation

You can control how events propagate using two key methods:

* `e.stopPropagation()`: Stops the event from moving to other elements.
    
* `e.preventDefault()`: Stops the browser's default action, like following a link or submitting a form.
    

### Example 1: Preventing Event Bubbling

Here's how you can stop event bubbling:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Propagation Example</title>
</head>
<body>
    <ul>
        <li id="man">Man</li>
        <li id="woman">Woman</li>
        <li id="google"><a href="https://www.google.com">Google</a></li>
    </ul>

    <script>
        document.getElementById('man').addEventListener('click', (e) => {
            e.stopPropagation(); // Stops the event from bubbling up
            alert('Man was clicked');
        }, false); // false indicates event bubbling (default)
    </script>
</body>
</html>
```

In this example, when you click on "Man," an alert shows up, and the event stops there. It doesn't trigger any event listeners on parent elements like `ul` or `body`.

### Example 2: Using Event Capturing

Now, let’s see how event capturing works by setting the third argument to `true`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Propagation Example</title>
</head>
<body>
    <ul>
        <li id="dog">Dog</li>
        <li id="cat">Cat</li>
        <li id="lion">Lion</li>
    </ul>

    <script>
        // Event listener on the 'ul' element using capturing (top to bottom)
        document.querySelector('ul').addEventListener('click', (e) => {
            alert('Clicked on the UL element');
          //e.stopPropagation(); // Stops further event capturing
            console.log('UL element was clicked');
        },true); // 'true' enables capturing (top to bottom)

        // Event listener on the 'dog' element using bubbling (default, bottom to top)
        document.getElementById('dog').addEventListener('click', (e) => {
            alert('Dog was clicked');
            console.log('Dog element was clicked');
           // e.stopPropagation(); // Stops further event bubbling
        }); // 'false' enables bubbling (bottom to top)

    </script>
</body>
</html>
```

In this example:

* Clicking on "Dog" first triggers the `ul` event listener (because `true` is set, enabling event capturing), showing the alert "UL was clicked during capturing phase."
    
* After that, the event triggers the "Dog" event listener, showing the alert "Dog was clicked."
    

### Example 3: Preventing Default Browser Behavior

Here’s how you can prevent a link from navigating away:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prevent Default Behavior</title>
</head>
<body>
    <ul>
        <li id="google"><a href="https://www.google.com">Google</a></li>
    </ul>

    <script>
        document.getElementById('google').addEventListener('click', function(e) {
            e.preventDefault(); // Stops the browser from navigating to the URL
            alert('Google link clicked');
            e.stopPropagation(); // Stops the event from bubbling up
        });
    </script>
</body>
</html>
```

When you click on the "Google" link, instead of navigating to Google, it shows an alert. This is done using `e.preventDefault()`. We also use `e.stopPropagation()` to stop the event from affecting other elements.

### Example 4: Removing List Items Dynamically

Here's an example of how to remove items from a list when they are clicked:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Remove List Items</title>
</head>
<body>
    <ul>
        <li id="dog">Dog</li>
        <li id="cat">Cat</li>
        <li id="lion">Lion</li>
        <li id="goat">Goat</li>
        <li id="buffalo">Buffalo</li>
        <li id="man">Man</li>
        <li id="woman">Woman</li>
        <li id="boy">Boy</li>
        <li id="girl">Girl</li>
        <li id="guardian">Guardian</li>
        <li id="google"><a href="https://www.google.com">Google</a></li>
    </ul>

    <script>
        const ul = document.querySelector('ul');
        ul.addEventListener('click', function(e){
            console.log(e.target.tagName);
            if(e.target.tagName == 'LI'){
                e.target.remove(); // Removes the clicked list item
            }
        });
    </script>
</body>
</html>
```

In this example, when you click on any item in the list, that item is removed from the page.

### Conclusion

Understanding event propagation helps you manage how events behave in your web applications. Whether you want to stop an event from going up the DOM or prevent the browser's default actions, using methods like `e.stopPropagation()` and `e.preventDefault()` will give you greater control over your events.