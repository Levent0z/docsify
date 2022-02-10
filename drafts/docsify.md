# Build a Blog or Documentation Hub with Docsify

- [Home](https://docsify.js.org/#/)
- [Helpers](https://docsify.js.org/#/helpers) - Extensions to Markdown
- [Curated List](https://github.com/docsifyjs/awesome-docsify) - Includes plugins
- [Writing a plugin](https://docsify.js.org/#/write-a-plugin)

## Getting Started

```sh
# Git init
npm init
npm i docsify-cli -g
docsify init ./docs
docsify serve ./docs
# open ./docs/index.html
```

## Folder structure

```yaml
docs                  # Optional parent
    README.md         # Main page, maps to /#/
    _sidebar.md       # Default sidebar
    favicon.ico       # Favorite icon
    index.html        # Base template
    .nojekyll         # Empty file to disable jekyll
    somefolder
        README.md     # Optional, maps to /#/somefolder/
        _sidebar.md   # Optional, see "Nested Sidebars" in docs
```

## Add Search

Include the following in `index.html`:

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

## Embed Video

```
[<description>](assets/<file_name> ':include :type=video controls height=400px width=100%')
```

## Publishing

- Using [GitHub Pages](https://pages.github.com/).
- [Configuring a publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

## Notes

> If you look into the browser's local storage (using Chrome: developer tools > application tab > local storage) you can see the content of Docsify's search index under the docsify.search.index key.

> Sidebar seems buggy: when expanding a top-level item, it shows incorrect children.
> To fix, remove [subMaxLevel](https://docsify.js.org/#/configuration?id=submaxlevel) from the configuration.
