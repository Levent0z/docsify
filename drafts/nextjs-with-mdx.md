# NextJS with MDX

## 1. blog-starter-app
>Blog.  A statically generated blog example using Next.js and Markdown.

[GitHub](https://github.com/vercel/next.js/tree/canary/examples/blog-starter)

**Get started:**  `yarn create next-app --example blog-starter blog-starter-app`

**package.json**
```json
  "dependencies": {
    "classnames": "^2.3.1",
    "date-fns": "^2.28.0",
    "gray-matter": "^4.0.3",
    "next": "latest",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "remark": "^14.0.2",
    "remark-html": "^15.0.1",
    "typescript": "^4.7.4"
  },
  "devDependencies": {
    "@types/node": "^18.0.3",
    "@types/react": "^18.0.15",
    "@types/react-dom": "^18.0.6",
    "autoprefixer": "^10.4.7",
    "postcss": "^8.4.14",
    "tailwindcss": "^3.1.4"
  }
```

## 2. PressBlog

By Elijah Agbonze

[Live Example](https://pressblog.vercel.app/)   
[GitHub](https://github.com/Elijah-trillionz/pressblog-mdx-nextjs)

**package.json**
```json
  "dependencies": {
    "@mdx-js/loader": "^2.0.0-rc.2",
    "@mdx-js/react": "^2.0.0-rc.2",
    "@reach/disclosure": "^0.16.2",
    "@reach/tooltip": "^0.16.2",
    "@stefanprobst/rehype-shiki": "^2.2.0",
    "gray-matter": "^4.0.3",
    "next": "12.0.7",
    "react": "17.0.2",
    "react-dom": "17.0.2",
    "rehype-highlight": "^5.0.2",
    "rehype-shiki": "^0.0.9",
    "remark-frontmatter": "^4.0.1",
    "shiki": "^0.14.0"
  },
  "devDependencies": {
    "eslint": "8.4.1",
    "eslint-config-next": "12.0.7"
  }
```


## 3. Portfolio-with-blog

By Lee Rob

Get Started: `git clone https://github.com/leerob/leerob.io.git`

Uses
- [next-mdx-remote](https://github.com/hashicorp/next-mdx-remote), supports frontmatter
- 

**package.json**
```json
 "dependencies": {
    "@next/font": "13.0.2",
    "@prisma/client": "^4.5.0",
    "@sanity/image-url": "^1.0.1",
    "@sanity/webhook": "^2.0.0",
    "@tailwindcss/typography": "0.5.7",
    "@vercel/analytics": "^0.1.3",
    "classnames": "^2.3.2",
    "date-fns": "2.29.3",
    "googleapis": "48.0.0",
    "motion": "^10.14.3",
    "next": "13.0.2",
    "next-auth": "4.15.1",
    "next-mdx-remote": "^4.1.0",
    "next-sanity": "^1.0.6",
    "next-themes": "^0.2.1",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "sanity": "dev-preview",
    "sanity-plugin-markdown": "^3.0.0-v3-studio.0",
    "styled-components": "^5.3.6",
    "swr": "1.3.0",
    "tailwindcss": "3.2.1",
    "use-delayed-render": "^0.0.7"
  },
  "devDependencies": {
    "@types/react": "^18.0.24",
    "autoprefixer": "10.4.13",
    "eslint": "8.26.0",
    "eslint-config-next": "13.0.2",
    "globby": "13.1.2",
    "postcss": "^8.4.18",
    "prettier": "2.7.1",
    "prisma": "4.5.0",
    "reading-time": "^1.5.0",
    "rehype": "12.0.1",
    "rehype-autolink-headings": "6.1.1",
    "rehype-code-titles": "1.1.0",
    "rehype-prism-plus": "^1.5.0",
    "rehype-slug": "5.1.0",
    "remark-gfm": "^3.0.1",
    "rss": "1.2.2",
    "typescript": "^4.8.4"
  },
  ```

  - `pages/*.tsx`
  - `pages/blog/[slug].tsx`
  - `components/*.tsx`
  - `layouts/*.tsx`

## 4. Next JS MDX Blog Starter

By John Polacek

[GitHub](https://github.com/johnpolacek/nextjs-mdx-blog-starter)

- Theme UI
- Gray Matter

**package.json**
```json
"dependencies": {
    "@emotion/react": "^11.7.1",
    "@emotion/styled": "^11.10.5",
    "@mdx-js/loader": "^1.6.22",
    "@mdx-js/runtime": "^1.6.22",
    "@next/mdx": "^12.0.8",
    "disqus-react": "^1.1.2",
    "gray-matter": "^4.0.2",
    "next": "^12.0.8",
    "prism-react-renderer": "^1.1.1",
    "prop-types": "^15.8.1",
    "react": "^17.0.1",
    "react-dom": "^17.0.1",
    "react-ga": "^3.3.0",
    "theme-ui": "^0.13.1"
  },
  "devDependencies": {
    "onchange": "^7.1.0",
    "prettier": "^2.5.1"
  },
```

**next.config.js**
```js
const withMDX = require("@next/mdx")({
  extension: /\.mdx?$/,
})
```

- `pages/*.js`
- `pages/[slug].js`
- `pages/blog/[page].js`
- `src/layout/*.js`
- `src/mdx/**/*.mdx`
- `src/ui/*.js`
- `src/views/*.js`



