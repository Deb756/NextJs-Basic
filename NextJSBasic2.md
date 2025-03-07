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
