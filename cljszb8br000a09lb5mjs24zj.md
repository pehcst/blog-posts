---
title: "Unraveling console.log"
datePublished: Fri Jul 07 2023 19:37:53 GMT+0000 (Coordinated Universal Time)
cuid: cljszb8br000a09lb5mjs24zj
slug: unraveling-consolelog
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688827407644/bf57cfe7-0a20-4a4c-9592-e42897f3f503.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1688827424671/29e0ea17-4e25-4e0a-85a4-5c00a15ca4a0.jpeg
tags: tutorial, javascript, tips, frontend-development

---

Using `console.log()` is a very basic way to diagnose and troubleshoot minor issues in your code.

But did you know that there's more to the console than just a log? In this post, I bring you two additional functionalities to print to the console in JS.

# **.log()**

The `console.log()` method is the simplest and most well-known, which generates a message to your browser's console. The message can be a single string or one or more JavaScript objects.

```javascript
const x = 'Test'
console.log(x)
```

In this example, '*Test*' will be returned in the console, pretty simple, right?

We can also include multiple values in the console. Add a string at the beginning to identify what you're logging.

```javascript
const x = 'Test'
console.log("value", x)
```

But what if we have multiple values to show?

```javascript
const x = 'Test'
const y = 'Super test'
const z = 'Mega test'
```

Would we use console.log 3 times? No! We can include all of them in one and still add a string to identify each of them.

```javascript
const x = 'Test'
const y = 'Super test'
const z = 'Mega test'
console.log('x:', x, 'y:', y, 'z:', z)
```

But that's a lot of work. To make it easier, simply wrap the variables inside curly braces to transform the log into an object.

```javascript
const x = 'Test'
const y = 'Super test'
const z = 'Mega test'
console.log({x, y, z})
```

# Log Variations

There are other variations to improve visibility in the browser console.

```javascript
console.log('Simple console log')
console.info('Information console')
console.debug('Debug console')
console.warn('Warning console')
console.error('Error console')
```

Each of these has a different interaction with the browser, making debugging easier. You can add styles to the logs, for example, where a warning will appear in <mark>yellow</mark> and an error in **red**.

The styles may vary depending on your browser.

# **.assert()**

We can also add conditionals to the browser console. By using `assert()`, we can print the log according to the boolean value of the information.

```javascript
const works = false
console.assert(works, 'This is the reason')
```

If the first argument of assert is false, the message will be printed in the console. But if it returns true, it won't appear.

# **.count()**

Yes, it's possible to create a counter within the console.

```javascript
for (i = 0; i < 10; i++) {
  console.count()
}
```

Each iteration of the loop will print a counter in the console. In this case, you will see the default: 1 up to default: 10. If you execute the loop again, it will continue from where it left off, starting from 11 up to 20.

To reset the counter, you can use the `console.countReset()` after the loop.

# **.Time()**

In addition to counting, we can also time the execution using the `console.time()`. However, it alone can't do much. To demonstrate, let's create a small interval that simulates rendering using `setTimeout()`. Within this time limit, we'll use `console.timeEnd()` to get the final execution time.

```javascript
console.time()
setTimeout(() => {
  console.timeEnd()
}, 2000)
```

By executing this code snippet, you can see that the console will display the time it took to execute the `setTimeout()`.

We can also display the elapsed time using timeLog to label a timer.

```javascript
console.time()
setTimeout(() => {
  console.timeLog()
}, 2000)
```

# **.Table()**

Want to see your log as a table? It's possible with `.table()`. This is one of the uses to improve the visualization of certain objects.

```javascript
let devices = [
  {
    name: 'iPhone',
    brand: 'Apple'
  },
  {
    name: 'Galaxy',
    brand: 'Samsung'
  },
  {
    name: 'Pixel',
    brand: 'Google'
  },
  {
    name: 'Poco',
    brand: 'Huawei'
  }
]
console.table(devices);
```

![](https://images.prismic.io/pehcst/af4e16f5-9c69-402f-856d-5b8254a66b51_log.jpeg?auto=compress,format align="left")

# **.clear()**

Have trouble finding a log due to the multiple renders you're doing on the page? Are you constantly refreshing and getting lost in the browser console?

Simple, add `console.clear()` at the beginning of your code, and every time you render, you'll have a fresh console.

Just don't add it at the end of your code 🤪🤪🤪

Well, that's all! Thank you for reading, and of course, there are many other logs you can use.

Explore the documentation: [**https://developer.mozilla.org/enUS/docs/Web/API/Console**](https://developer.mozilla.org/en-US/docs/Web/API/Console)