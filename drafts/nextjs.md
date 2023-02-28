# NextJS

- Put assets in `public` folder.
- Put pages in `pages` folder.
- Use square brackets in file names for dynamic routing.


## next.config.[m]js

```js
/**
 * @type {import('next').NextConfig}
 */
module.exports = {
  reactStrictMode: true,
  images: {
    domains: [
      'i.scdn.co', // Spotify Album Art
      'pbs.twimg.com', // Twitter Profile Picture
    ]
  },
  experimental: {
    fontLoaders: [
      { loader: '@next/font/google', options: { subsets: ['latin'] } }
    ]
  },
  async headers() {
    return [
      {
        source: '/(.*)',
        headers: securityHeaders    // Refer to prortfolio-with-blog for actual values
      }
    ];
  }
};
```

Note: config can be passed into `withMDX()` from `@next/mdx` before exporting.


## _app.tsx
```tsx
import type { AppProps } from 'next/app'
import Head from 'next/head'
import '../styles/main.css'

export default function App({ Component, pageProps }: AppProps) {
  return (
    <>
      <Head>
      </Head>
      <Component {...pageProps} />
    </>
  )
}
```

## _document.tsx
```tsx
import { Html, Head, Main, NextScript } from 'next/document'

export default function Document() {
 
  return (
    <Html lang="en">
      <Head>
      </Head>
      <body>
        <Main />
        <NextScript />
      </body>
    </Html>
  )
}
```

## Routing
```jsx
import { useRouter } from 'next/router'
const query = useRouter().query
```

## Server-side Initialization

```js
// This function gets called at build time
export async function getStaticPaths() {

  const id = 'id'

  // Get the paths we want to pre-render based on posts
  const paths = [{
    params: { id }
  }]

  // We'll pre-render only these paths at build time.
  // { fallback: false } means other routes should 404.
  return { paths, fallback: false }
}

// This also gets called at build time
export async function getStaticProps({ params }) {
  // params contains the post `id`.
  const field = 'value';

  // Pass post data to the page via props
  return { props: { field } }
}

export default Post
```


## Reference

- [SWR](https://swr.vercel.app/) - React Hooks for Data Fetching
- [Tailwind Intellisense VSCode Extension](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
- [Explaning Next MDX Theme UI](https://notebook.lachlanjc.com/2019-09-06_explaining_next_mdx_theme_ui)
- [Create NextJS MDX Blog](https://blog.logrocket.com/create-next-js-mdx-blog/)
- [Theming in NextJS with Styled-Components and Use-Dark-Mode](https://blog.logrocket.com/theming-in-next-js-with-styled-components-and-usedarkmode/)