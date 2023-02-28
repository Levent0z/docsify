# Theming

https://vscodethemes.com/


## Shiki

Usage:
```javascript
import shiki, { IShikiTheme } from 'shiki';
import withShiki from '@stefanprobst/rehype-shiki';
import { getTheme } from 'shiki-themes';

getTheme('dark_plus') // installed as part of shiki-themes
await shiki.loadTheme('../../node_modules/shiki-themes/data/vscode/dark_plus.json') // better
'dark-plus' // built-in as part of shiki
```

List:
- node_modules/shikit/themes/*.json
- node_modules/shiki-themes/data/material/*.json
- node_modules/shiki-themes/data/nice/*.json
- node_modules/shiki-themes/data/vscode/*.json
- node_modules/shiki-themes/dist/types.d.ts
- https://github.com/shikijs/shiki/blob/main/docs/themes.md#all-themes
- https://github.com/ayu-theme/vscode-ayu/blob/master/ayu-dark.json 


## HighlightJS

Usage:
```javascript
import rehypeHighlight from 'rehype-highlight'; 
import 'highlight.js/styles/vs2015.css';
```
Demo:
- https://highlightjs.org/static/demo/ 

List:

Reference:
- https://unifiedjs.com/explore/package/rehype-highlight

