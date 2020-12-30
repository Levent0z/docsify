# Chrome API

```JavaScript
chrome.storage.sync.get(string | strin[], function(items) { } );

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

content scripts are attached to a page URL, but can't utilize Chrome APIs - must use messaging API

chrome.runtime.sendMessage(anyobject)

// request is the object sent in sendMessage
chrome.runtime.onMessage.addListener(function(request, sender, sendResponse) {

});

chrome.tabs.sendMessage(tabs[0].id, anyObjectToSend)


chrome.runtime.on

```

Idea: add CSS automatically to the first item through content_script CSS


