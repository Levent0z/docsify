# Build a Blog or Documentation Hub with Docsify

https://docsify.js.org/#/

```bash
# Git init
npm init
npm i docsify-cli -g
docsify init ./docs
docsify serve ./docs
```

Open ./docs/index.html


Plugins:
https://github.com/mrpotatoes/docsify-toc


Side Panel --> _sidebar.md
Main Panel --> README.md


## Add Search

Include the following in `index.html`:
```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```
Note:
> If you look into the browser's local storage (using Chrome: developer tools > application tab > local storage) you can see the content of Docsify's search index under the docsify.search.index key.



> Sidebar seems buggy: when expanding a top-level item, it shows incorrect children.
> To fix, remove [subMaxLevel](https://docsify.js.org/#/configuration?id=submaxlevel) from the configuration.