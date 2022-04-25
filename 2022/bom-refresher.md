# Browser Object Model

## Fetch API

### HTTP GET:
```javascript
// Using promises
fetch(url)
//.then(resp => resp.json()) // alternative
.then(resp => resp.text())
.then(text => console.log(text))
.catch(err => console.error(err));

// Using async/await
async function example() {
    try {
        const resp = await fetch(url);
        // const json = await resp.json(); // alternative
        const text = await resp.text(); 
        console.log(text);
    } catch (err) {
        console.error(err);
    }
}
```

### HTTP POST 

Sending JSON data:
```javascript
await fetch(url, {
    method: 'POST'
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(data),
});
```

Sending a file:
```javascript
// <input type="file">
const input = document.querySelector('input[type="file"]');

// Alternatively: <input type="file" multiple>
// const input = document.querySelector('input[type="file"][multiple]');

const formData = new FormData();
Array.from(input.files).forEach((v, i) => formData.append(`file_${i}`, input.files[i]);
await fetch(url, {
  method: 'POST',
  body: formData
});
```

[More on Mozilla](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

## History

```javascript
history.back();
history.forward();
history.go(-1); // Go back
history.go(1); // Go forward

// pushState/replaceState:
// Arg #1 is custom serializable object that represents state
// Arg #2 is not typically used
// Arg #3 is the URL to be shown in the address bar, but won't actually navigate there
history.pushState(someStateObj, '', optionalUrl);
history.replaceState(someOtherStateObj, '', optionalUrl);

window.onpopstate = (event) => { 
    // The state is of the top of the stack (not of the one that was popped)
    console.log(event.state); 
};
history.back();
```

[More on Mozilla](https://developer.mozilla.org/en-US/docs/Web/API/History_API/Working_with_the_History_API)

## Storage

Use `localStorage` for persistent store, `sessionStorage` for temporary store. They share the same API.

```javascript
let text;

localStorage.setItem('key', 'stringValue');
text = localStorage.getItem('key');
console.log(localStorage.length, localStorage.key(0));  // 1 'stringValue'
localStorage.removeItem('key');
localStorage.clear();

sessionStorage.setItem('key', 'stringValue');
text = sessionStorage.getItem('key');
sessionStorage.removeItem('key');
sessionStorage.clear();
```

## Workers

1. Use `onmessage` of `Worker` on the UI thread:

```javascript
let w;
function startWorker() {
    if(!w) {
        w = new Worker("worker.js");
        w.onmessage = (event) => console.log(event.data);
    }
}
function stopWorker() { 
    if (w) {
        w.terminate();
        w = undefined;
    }
}
```

2. Use `postMessage` on the worker file worker.js:
```javascript
let i = 0;
setInterval(() => postMessage(i++), 500);
```

## Geolocation

```javascript
navigator.geolocation.getCurrentPosition((gp) => {
    // Available properties:
    gp.timestamp;
    gp.coords.accuracy;
    gp.coords.latitude;
    gp.coords.longitude;
    gp.coords.altitude;
    gp.coords.altitudeAccuracy;
    gp.coords.heading;
    gp.coords.speed;
});
```
