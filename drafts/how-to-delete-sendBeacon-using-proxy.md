# How to delete sendBeacon using Proxy

`window.navigator.sendBeacon` cannot be deleted, however it can be overwritten. Here's an example of doing in in Puppetteer. This allows testing the case where sendBeacon isn't supported.

```javascript
// Puppetteer Test Code

const page = await browser.newPage();
page.setDefaultTimeout(60000);
page.evaluateOnNewDocument(() => {
    // We need to delete sendBeacon to test the fallback behavior (to fetch).
    // sendBeacon can't be deleted. Deleting navigator wholesale causes other issues
    // We define a proxy without sendBeacon.
    const nav = window.navigator;
    delete window.navigator; // this is required to reset the field
    window.navigator = new Proxy(nav, {
        get(target, property) {
            if (property === 'sendBeacon') {
                return undefined;
            }
            return target[property];
        },
    });
});
```
