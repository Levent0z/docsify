# CSS - Draft

## Selectors

| Selector              | Example    | description                                                        |
| --------------------- | ---------- | ------------------------------------------------------------------ |
| *                     | *          | Selects all elements                                               |
| element               | p          | Selects all `<p>` elements                                         |
| #id                   | #firstname | Selects the element with id="firstname"                            |
| .class                | .intro     | Selects all elements with class="intro"                            |
| element.class         | p.intro    | Selects only `<p>` elements with class="intro"                     |
| element, element, ... | div, p     | Selects all `<div>` and all `<p>` elements                         |
| parent > child        | div > p    | Selects the `<p>` elements that are direct children of the `<div>` |
| ancestor descendant   | div p      | Selects all `<p>` elements under a `div` element                   |

## Pseudo-classes

- `:active`, : commonly used on `<a>` and `<button>`
- `:link`, `:visited`, `:hover`, 

## The Box model

- `Content` - The content of the box, where text and images appear
- `Padding` - Clears an area around the content. The padding is transparent
- `Border` - A border that goes around the padding and content
- `Margin` - Clears an area outside the border. The margin is transparent

When you set the `width` and `height` properties of an element with CSS, you just set them for the content area. To calculate the full size of an element, you must also add padding, borders and margins.

An `outline` is a line that is drawn around elements, OUTSIDE the borders, to make the element "stand out". Unlike border, the outline is drawn outside the element's border, and may overlap other content. Also, the outline is NOT a part of the element's dimensions.

By default in the CSS box model, the width and height you assign to an element is applied only to the element's content box. The `box-sizing` property can be used to adjust this behavior:
- `content-box`: default CSS behavior. May be desirable when `position` is `relative` or `absolute`.
- `border-box`: account sfor border ad padding in the element's provided width and height. This is the default for `<table>`, `<select>`, `<button>` elements and the `<input>` element whose type is `radio`, `checkbox`, `reset`, `button`, `submit`, `color` or `search`.


## Sizing

- The effects of `width` and `height` are controlled by `box-sizing`.
- `min-width`, `max-width` override `width`. Similarly `min-height`, `max-height` override `height`. 

## Positioning

### Position

- The `position` property can take many values. (TBD)

### Stacking

When the `z-index` property is not specified on any element, elements are stacked in the following order (from bottom to top):

1. The background and borders of the root element
2. Descendant **non-positioned** blocks, in order of appearance in the HTML
3. Descendant **positioned** elements, in order of appearance in the HTML
   
`z-index` allows to reorder elements.

## Variables

Define variables with double-dashes:
```css
:root {
    --blue: #0000FF;
    --white: #FFFFFF;
}
div {
    color: var(--blue);
}
```

- The function `var(--name, fallbackvalue)` accepts an optional fallback vale.
- Redefined variables can override global variables locally.

Dealing with variables in JavaScript:
```javascript
const div = document.querySelector('#id');
const st = getComputedStyle(div);
const color = st.getPropertyValue('--blue');
div.style.setProperty('--blue', 'lightblue');
```

## Media Queries

Can check for:
- width and height of the viewport/device
- orientation (landscape/portrait)
- resolution

Syntax:
```css
@media not|only all|print|screen|speech and (expressions) {
  CSS-Code;
}
```

The `<link>` element has a `media` property.


## Flex

### Basic Responsive Two-Column Layout
[Reference](https://www.w3schools.com/css/tryit.asp?filename=trycss_mediaqueries_website)

HTML
```html
<div class="navbar">
    <a href="#">One</a>
    <a href="#">Two</a>
</div>
<div class="row">
    <div class="left-column">
    </div>
    <div class="right-column">
    </div>
</div>
```

CSS
```css
* {
  box-sizing: border-box;
}

.navbar {
  display: flex;
}
.row {  
  display: flex;
  flex-wrap: wrap;
}
.left-column {
  flex: 30%;  
}
.right-column {
  flex: 70%;  
}

@media screen and (max-width: 700px) {
  .row, .navbar {   
    flex-direction: column;
  }
}
```

## Responsive Design

Add the following to let the width and zoom be proper for the device 
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Often this one is required:
```css
* {
  box-sizing: border-box;
}
```

If creating rules for columns whose % widths add up to 100% and using `float: left`, this must be cleared with the row:

```css
.row::after {
  content: "";
  clear: both;
  display: table;
}
```


For an `<img>` or `<video>`, if the `width` property is set to a **percentage** and the `height` property is set to **auto**, the element will be responsive and scale up and down. Use `max-width` to only allow scale-down.

