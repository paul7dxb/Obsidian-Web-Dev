- This will be the route componene that NextJS will render
- Useful for base layout wrapper

```JSX
import Layout from '@/components/layout/Layout'
import '@/styles/globals.css'

export default function App({ Component, pageProps }) {
  return (
  <Layout>
    <Component {...pageProps} />
  </Layout>)
```