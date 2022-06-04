# Chrome API

```typescript
chrome.storage.sync.get(string | string[], function(items) { } );

chrome.storage.sync.set(object, function() {} );

close();

opt: {
	type: "basic",
	title: "string",
	message: "string",
	iconUrl: "filename"
}
// Notifications may only work on Windows or Chrome OS
chrome.notifications.create('reset'. opt, function() {});


chrome.storage.onChanged.addListener(function(chabges) {
	changes.variableName.newValue
});

chrome.browserAction.setBadgeText({"text": "string" });


menuItem = {
	id: "string",
	title: "string",
	contexts: [ "well-known-string"], // "selection"
}

chrome.contextMenus.create(menuItem)
chrome.contextMenus.onClicked.addListener(function(clickData) {
	clickData.menuItemId
	clickData.selectionText
});

chrome.tabs.query({active: true, currentWindow: true}, function(tabs) {
	chrome.pageAction.show(tabs[0].id);
});

//content scripts are attached to a page URL, but can't utilize Chrome APIs - must use messaging API

chrome.runtime.sendMessage(anyobject)

// request is the object sent in sendMessage
chrome.runtime.onMessage.addListener(function(request, sender, sendResponse) {

});

chrome.tabs.sendMessage(tabs[0].id, anyObjectToSend)


chrome.runtime.on

```

Idea: add CSS automatically to the first item through content_script CSS

## Manifest.json

Replace upper-case values as needed

```json
{
    "manifest_version": 2,
    "version": "1.0.0",
    "description": "DESCRIPTION",
    "name": "PROJECT_NAME",
    "browser_action": {
        "default_title": "TITLE",
        "default_icon": "assets/ICON-48.png",
        "default_popup": "POPUP.html"
    },
    "omnibox": {
        "keyword": "KEYWORD"
    },
    "permissions": [
        "cookies",
        "contextMenus",
        "storage"
        "tabs",
        "https://URL/"
    ],
    "background": {
        "scripts": [
            "UTILITY.js",
            "background.js"
        ],
        "persistent": true
    },
    "content_scripts": [
        {
            "all_frames": false,
            "run_at": "document_start",
            "matches": [
                "https://URL*"
            ],
            "js": [
                "resources/js/INJECTED.js"
            ],
            "css": [
                "resources/css/INJECTED.css"
            ]
        }
    ],
    "icons": {
        "16": "assets/ICON-16.png",
        "32": "assets/ICON-32.png",
        "48": "assets/ICON-48.png",
        "64": "assets/ICON-64.png",
        "96": "assets/ICON-96.png",
        "128": "assets/ICON-128.png"
    },
    "options_page": "options.html",
    "content_security_policy": "script-src 'self' 'unsafe-eval' https://www.googletagmanager.com https://www.google-analytics.com; object-src 'self'",

}
```
