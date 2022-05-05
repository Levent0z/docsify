Write a function that takes a non-negative timeout value and 2 callback functions (1 for success case, 2 for error case), and calls that function with the current date-time after the timeout elapses. If the system time has changed such that the new time is earlier than when the function was called, it should call the error callback.

```javascript
function timer(timeout, successCallback, errorCallback) {
    const then = Date.now();
    setTimeout(function () {
        const now = Date.now();;
        if (now < then) {
            errorCallback();
        }
        callback(new Date(now));
    }, timeout);
}
// #1 Use the function such that the time is logged to the console

// #2 convert the function to return a Promise 
function timerAsync(timeout) {
    return new Promise((resolve, reject) => {
        setTimeout(function () {
            resolve(new Date());
        }, timeout);
    })
}

// #2 use it in an example with .then
// #3 use it in an example with async/await
// #4 write this function as a methof in TypeScript class
```
