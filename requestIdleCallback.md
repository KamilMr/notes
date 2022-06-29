https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback

## window
- window.requestIdleCallback() method queues a function to be called during a browser's idle periods.
- Functions are generally called in first-in-first-out order
- callbacks which have a timeout specified may be called out-of-order if necessary in order to run them before the timeout elapses
- You can call requestIdleCallback() within an idle callback function to schedule another callback to take place no sooner than the next pass through the event loop.

A timeout option is strongly recommended.

## syntax
```
requestIdleCallback(callback)
requestIdleCallback(callback, options)
```

`callback`
A reference to a function that should be called in the near future, when the event loop is idle. The callback function is passed an IdleDeadline object describing the amount of time available and whether or not the callback has been run because the timeout period expired.

`options`
timeout

`return` is id and can be passed to `window.cancelIdleCallback();`

https://developer.mozilla.org/en-US/docs/Web/API/Background_Tasks_API

Concepts and usage
The main thread of a Web browser is centered around its event loop. This code draws any pending updates to the Document currently being displayed, runs any JavaScript code the page needs to run, accepts events from input devices, and dispatches those events to the elements that should receive them. In addition, the event loop handles interactions with the operating system, updates to the browser's own user interface, and so forth. It's an extremely busy chunk of code, and your main JavaScript code may run right inside this thread along with all of this. Certainly most if not all code that is capable of making changes to the DOM is running in the main thread, since it's common for user interface changes to only be available to the main thread.

Because event handling and screen updates are two of the most obvious ways users notice performance issues, it's important for your code to be a good citizen of the Web and help to prevent stalls in the execution of the event loop. In the past, there's been no way to do this reliably other than by writing code that's as efficient as possible and by offloading as much work as possible to workers. Window.requestIdleCallback() makes it possible to become actively engaged in helping to ensure that the browser's event loop runs smoothly, by allowing the browser to tell your code how much time it can safely use without causing the system to lag. If you stay within the limit given, you can make the user's experience much better.

## When to use it?
- Use idle callbacks for tasks which don't have high priority.
- Idle callbacks should do their best not to overrun the time allotted.
- Avoid making changes to the DOM within your idle callback.
- Avoid tasks whose run time can't be predicted.
- Use timeouts when you need to, but only when you need to.
