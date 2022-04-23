# LWC

[lwv.dev](https://lwc.dev/)

## Getting Started
```sh
npx create-lwc-app my-app
cd my-app
npm run watch
```

## Communication

### Child-to-parent, use a custom event

#### Child component calls

```javascript
this.dispatchEvent(new CustomEvent('myeventname'));
```

#### The parent handles the event:

```xml
<c-child-component onmyeventname={handleEvent}></c-child-component>
```

### Parent-to-child, use `@api`


## Shadow-DOM

To disable Native Shadow, add this to the top of `src/index.js`:
```javascript
import from '@lwc/synthetic-shadow'
```

## Registry

npm.lwcjs.org