# HTML DOM

## Finding elements
```javascript
let el = document.getElementById('element-id');
el = document.querySelector('#element-id');    // Same as above. Use the # CSS selector for IDs.

const divs = document.getElementsByTagName('div'); // Returns an HTMLCollection
let elArray = document.getElementsByClassName('class-name'); // Returns an HTMLCollection
elArray = document.querySelectorAll('.class-name'); // Returns a NodeList. Use the . CSS selector for classes.
```

## Navigating Node Relationships
```javascript
// These are properties
el.parentNode
el.children   // Returns an HTMLCollection
el.childNodes // Returns a NodeList

// Navigating all node types
el.firstChild // Could return a text node, for example
el.lastChild
el.nextSibling
el.previousSibling

// Navigating elements only
el.firstElementChild
el.lastElementChild
el.nextElementSibling
el.previousElementSibling
```

### Differences berween HTMLCollection and NodeList.
- They are both *like* arrays, but they don't have array methods like `pop`, `push`, etc. `NodeList` does have a `forEach` method.
- `HTMLCollection` only contains elements (a subset of nodes). `NodeList` contains all types of nodes.
- `HTMLCollection` is a "live" collection, that gets updated if the DOM changes. `NodeList` is a static collection.

## Modifying an element
```javascript
element.innerHTML = ''; // The string can be some new HTML
element.id = 'unique-id';
element.style.color = 'red';    // Style fields are camel-cased versions of CSS properties
element.classList.add('class-name');
element.setAttribute('attribute-name', value);
element.setAttribute('stand-alone-attribute', '');
element.removeAttribute('attribute-name');

element.builtInProperty = value; // This only works for certain properties (not all attributes)
```

## Adding and Deleting elements
```javascript
// Always create on the document
const div = document.createElement('div');
const textNode = document.createTextNode("Some text");
div.appendChild(textNode);

const p1 = document.createElement('p');
p1.innerHTML = 'P1';
const p2 = document.createElement('p');
p1.innerHTML = 'P2';
div.appendChild(p1);
div.replaceChild(p2, p1);   // (new, old)
div.removeChild(p2);
// or
p2.remove();

// Make it part of the DOM by appending to an element
// already on the DOM or to the document directly
// NOTE: Only one element on document allowed.
document.appendChild(div);

// There's also these methods:
div.insertBefore()
div.insertAdjacentText()
div.insertAdjacentElement()
div.insertAdjacentHTML()
```

## Other properties of nodes/elements
```javascript
// Assuming empty document
const div = document.createElement('div');
document.appendChild(div);
div.nodeName            // 'DIV'
div.nodeValue           // null - always null for elements
div.childElementCount   // 0
div.hasChildNodes()     // false
div.childNodes.length   // 0
```

## Event Handling
`Bubbling`: Event is handled by the inner element first, moves to the ancestors
`Capturing`: Event is handled by the element fist before moving to descendants

```javascript
function someFunction(event) { 
    event.preventDefault(); // Only if you want to prevent default behavior
}
// useCapture is optional. If true, use capturing, otherwise use bubbling.
element.addEventListener('click', someFunction, useCapture);
element.removeEventListener('click', someFunction, useCapture);
```

An event handler for a specific element can be specified as an attribute on an element using the **on** prefix, such as `onclick`. The value of the attribute is actual JavaScript, with `this` being the element. See forms section for an example. [List of event attributes](https://www.w3schools.com/tags/ref_eventattributes.asp).

## Forms
```html
<form action="/endpoint" method="post">
	<fieldset>
		<legend>Applicant</legend>
		<label for="name">Name</label>
		<input type="text" name="name" required>
		<label for="age">Age</label>
		<input type="number" name="age" min="13" max="120">
	</fieldset>
	<fieldset>
		<legend>Loan</legend>
		<label for="amount">Amount</label>
		<input id="loan-amount" type="number" name="amount" min="50000" max="1000000" required>
		<label for="term">Term</label>
		<select name="term">
			<option value="15">15 Years</option>
			<option value="20">20 Years</option>
			<option value="30">30 Years</option>
		</select>
	</fieldset>
	<input type="submit" value="Submit" onclick="console.log('submit')">
</form>
```

[See this code at codepen.io](https://codepen.io/levent0z/pen/PoEvmvq)

[More form elements at w3schools.com](https://www.w3schools.com/html/html_form_elements.asp)


```javascript
const input = document.getElementById('loan-amount');
if (!input.checkValidity()) {
    input.validationMessage     // string
    input.validity.rangeUnderflow  // boolean
    input.validity.rangeOverflow   // boolean
    input.validity.valueMissing    // boolean
}
```