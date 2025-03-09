# Data Featching in NextJs

> There are two types of data featching i.e
>
> - <b> Client Side data fetching</b>
> - <b> Server Side data fetching</b>

| <b> ClientSide DF                                               | Serverside DF   |
| --------------------------------------------------------------- | --------------- |
| In this we use <b> useState() and useEffect() for data fetching | Here we can use |
| No SEO                                                          | It supports SEO |
| Less secure                                                     | More Secure     |

# Caching in NextJs

> Caching in Next.js is a technique to store and reuse previously fetched or computed data to improve performance, reduce load times, and minimize unnecessary requests to the server.
>
> - Its simply mean storing data somewhere that is faster to access
> - it stores the data in browser
> - it works in clentside not server side like (Session)

## Next.js provides multiple levels of caching:

### 1️⃣ Static Caching (Pre-rendering)

For Static Site Generation (SSG) – The page is generated at build time and cached on the server/CDN.

📌 How it Works:

Uses fetch with default caching behavior (cache: 'force-cache').
Content is pre-generated and served instantly.
Ideal for SEO-friendly, rarely changing pages.
✅ Example (Static Caching - Default Behavior)

```tsx
export default async function StaticPage() {
  const res = await fetch("https://api.example.com/data");
  const data = await res.json();

  return <p>Data: {data.message}</p>;
}
```

🔹 Default Behavior:

Next.js caches the data at build time.
The same data is served to all users until the next build.

### 2️⃣ Server-Side Caching

For Server-Side Rendering (SSR) – The page is generated on each request, but responses can be cached.

📌 How it Works:

You can configure dynamic caching in API calls using fetch.
Example: Revalidating cached data at specific intervals.
✅ Example (Revalidating Cached Data Every 60 Seconds)

```tsx
export default async function RevalidatedPage() {
  const res = await fetch("https://api.example.com/data", {
    next: { revalidate: 60 }, // Cache expires every 60 seconds
  });
  const data = await res.json();

  return <p>Data: {data.message}</p>;
}
```

🔹 Behavior:

The response is cached for 60 seconds.
After 60 seconds, Next.js fetches fresh data from the API.

# Static and Dynamic rendering in Next.js

1. **Static Rendering**

   > - It only happens in Building time
   > - In this a Html page onlu render once at the time of build of the app and after that if it needed then the NextJs not re-render them because its stored in cache so it simply fetch from that which increase performance of app

2. **Dynamic Rendering**
   > - it happens at the request time
   > - In this For every request freash content are generated

# 🚀 Static vs. Dynamic Rendering in Next.js

Next.js provides two main rendering strategies:
1️⃣ Static Rendering (Pre-rendered at build time)
2️⃣ Dynamic Rendering (Rendered at request time)

These rendering strategies affect performance, SEO, and user experience. Let’s break them down!

1️⃣ Static Rendering (Pre-rendering)
The page is generated at build time and served as a static HTML file.
🚀 Fast & SEO-friendly because content is cached and served instantly.

🔹 Types of Static Rendering

- ✅ Static Site Generation (SSG) – Built Once, Served Fast

Next.js generates the page at build time.
The page is cached and served instantly to all users.
Ideal for SEO-friendly, rarely changing pages.

- ✅ Example: Static Page (Default Behavior)

```tsx
export default async function StaticPage() {
  const res = await fetch("https://api.example.com/data");
  const data = await res.json();

  return <p>Data: {data.message}</p>;
}
```

🔹 Default Behavior:

Next.js caches the response at build time.
The page remains the same for all users until the next build.

- ✅ Example: Using ISR (Incremental Static Regeneration)
  Rebuilds only specific pages instead of the whole app.

```tsx
export async function getStaticProps() {
  const res = await fetch("https://api.example.com/data");
  const data = await res.json();

  return {
    props: { data },
    revalidate: 60, // Revalidates every 60 seconds
  };
}
```

🔹 Behavior:

The page is cached and refreshed every 60 seconds.
Ideal for semi-dynamic data (e.g., news updates, product listings).
🎯 When to Use Static Rendering?

- ✅ SEO is important (e.g., blogs, landing pages).
- ✅ Content does not change frequently.
- ✅ Want super-fast performance with pre-built HTML.

2️⃣ Dynamic Rendering (On-Demand)
The page is generated on each request or client-side, making it always up-to-date.

🔹 Types of Dynamic Rendering

- ✅ Server-Side Rendering (SSR) – Rendered on Each Request
- ✅ Client-Side Rendering (CSR) – Rendered in the Browser

- ✅ Example: Server-Side Rendering (SSR)
  Use SSR for dynamic content that must be fresh on every request.

```tsx
export async function getServerSideProps() {
  const res = await fetch("https://api.example.com/data");
  const data = await res.json();

  return { props: { data } };
}

export default function ServerPage({ data }) {
  return <p>Data: {data.message}</p>;
}
```

🔹 Behavior:

The page fetches fresh data on each request.
Slower than SSG but ensures real-time updates.
🎯 When to Use SSR?

- ✅ Data changes frequently (e.g., stock prices, real-time dashboards).
- ✅ Personalized content (e.g., user-specific data).
- ✅ SEO is important, but content must be fresh.

- ✅ Example: Client-Side Rendering (CSR)
  The page loads first, then fetches data dynamically using JavaScript.

'use client'; // Needed for CSR in Next.js 13+ (App Router)

```tsx
import { useEffect, useState } from "react";

export default function ClientComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("/api/data")
      .then((res) => res.json())
      .then((data) => setData(data));
  }, []);

  if (!data) return <p>Loading...</p>;

  return <p>Data: {data.message}</p>;
}
```

🔹 Behavior:

The page loads first, then fetches data in the background.
Not SEO-friendly (since content is rendered in the browser).
🎯 When to Use CSR?

- ✅ User-specific content (e.g., dashboards, authenticated pages).
- ✅ SEO is not a concern.
- ✅ Fast interactions after the initial load.
