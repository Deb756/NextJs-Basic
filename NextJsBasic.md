# What is NextJs ?

> its a framework for building fast and search engine friendly application.

> its basically build on the top of React framework which is basically used for frontend.

> React is simply a library for buiding interactive UIs

> NextJs is a comprehensive frame work which consist libraries + tools + conventions

> it consist of

## 1. Compiler

> it simply used to transform and minify the javascript code.

## 2. CLI (Command Line Interface)

> its used to build and start the Nextjs App

## 3. Node.js Runtime

> its simply used to excute the javascript codes.

# What is file based routing in NextJS?

File-based routing in Next.js is a system where the file structure inside the pages/ directory automatically defines the application's routes. Instead of manually setting up routes like in React Router, Next.js generates them based on the file and folder names.

🔹 How It Works:
Basic Page Routing

Any .js, .jsx, or .tsx file inside the pages/ directory becomes a route.

```bash
/pages
  ├── index.js      →  '/'  (Homepage)
  ├── about.js      →  '/about'
  ├── contact.js    →  '/contact'
```

index.js corresponds to the root / route.<br>
about.js corresponds to /about.<br>
contact.js corresponds to /contact.

## 1. Dynamic Routing

You can create dynamic routes using square brackets [ ].
Example:

```bash
/pages
  ├── blog
  │   ├── [id].js   → '/blog/:id' (Dynamic route for blog posts)
```

A request to /blog/123 will be handled by pages/blog/[id].js.

## 2.Nested Routing

You can organize files into folders to create nested routes.
Example:

```bash
/pages
  ├── products
  │   ├── index.js  → '/products'
  │   ├── details.js → '/products/details'
```

index.js inside products/ maps to /products.<br>
details.js inside products/ maps to /products/details.

## 3. Catch-All Routes ([...param].js)

Captures multiple segments in a URL.
Example:

```bash
/pages
  ├── blog
  │   ├── [...slug].js → '/blog/*'
```

/blog/my-first-post <br>
/blog/2024/march/new-post

## 4. API Routes (pages/api/)

Files inside pages/api/ become API endpoints.
Example:

```bash
/pages
  ├── api
  │   ├── hello.js  → API endpoint at `/api/hello`
```

pages/api/hello.js handles GET requests at /api/hello.

## 🔥 Advantages of File-Based Routing:

- ✅ No need for external routing libraries (like React Router).
- ✅ Automatic code splitting (each page is loaded only when needed).
- ✅ SEO-friendly (static and dynamic pages are pre-rendered).
- ✅ Easier navigation with the <Link> component (next/link).

Would you like a practical example of dynamic routing? 🚀

# What is Js Runtime ?

> There ar two ways that we can execute JS codes i.e

- web server (by Clientside)
- Node.js runtime (by serverside)

> - Here by NextJs we can do fullstack devolopement faster
> - Here in this we can write Frontend and Backend within the same NextJs program
> - Here the <b>Frontend</b> will be exected in web browser and <b>Backend</b> will be executed by the Node.js Runtime

# What is Serverside Rendering (SSR) in Next.js App ?

> - its also known as <b> Dynamic Rendering (SSR)</b>
> - In this for every request of client it generates a html page
>   and it can very for request to request like for POST , GET , UPDATE , DELETE etc

> - To use SSR for a page we need to <b> export </b> an <b> aysnc </b> function called <b> getServerSideProps </b>. Int this the <b> Async Function </b> is called each time a request is made for the page .

# Syntax :-

```js
export default function Page({ data }) {
  return <>YOU CAN DISPLAY YOUR DATA ACCORDINGLY</>;
}
export async function getServerSideProps() {
  // Your code
  const data = [];

  // Passing data to the Page using props
  return {
    props: { data },
  };
}
```

# What is Staticside Generation (SSG)

> - it is a feature that prerenders all the pages of your website as a static HTML files during the build process
> - Means the content is created beforehead the client interact to the server . which result in _Faster Loading , improved SEO (search engine optimisation) performance_ . Esssentially it creates a compleat website by using set of static files which is ready to deployed on a server
> - To fetch this data on pre-render, Next.js allows you to export an async function called getStaticProps from the same file. This function gets called at build time and lets you pass fetched data to the page's props on pre-render.

# Syntax : -

```js
export default function Blog({ posts }) {
  // Render posts...
}

// This function gets called at build time
export async function getStaticProps() {
  // Call an external API endpoint to get posts
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  // By returning { props: { posts } }, the Blog component
  // will receive `posts` as a prop at build time
  return {
    props: {
      posts,
    },
  };
}
```

# Why Next.js Can Be Full-Stack?

- Next.js is primarily a frontend framework built on React, but it includes backend features like:
- ✅ API Routes – You can create backend APIs within Next.js (like a mini backend).
- ✅ Server-Side Rendering (SSR) & Static Site Generation (SSG) – Improves SEO and performance.
- ✅ Database Integration – You can connect to databases (MongoDB, PostgreSQL, MySQL) using ORM tools like Prisma.
- ✅ Authentication & Middleware – Supports authentication (e.g., NextAuth.js) and middleware for backend logic.

# 🚀 CSR vs SSR Comparison

| Client Side Rendering(CSR)                            | Server side Rendering(SSR)                                |
| ----------------------------------------------------- | --------------------------------------------------------- |
| Fster Load                                            | Slow due to Server Processing                             |
| Its not SEO friendly                                  | Its SEO froendly                                          |
| Here all the files (related or irrrected are renderd) | Here only specific are rendered as per the Client request |
| It fetches data on clientside                         | It featches data on server side                           |
| Its less secured                                      | Its highly secured                                        |

# Steps to create Next.js project

1.

```js
npx create-next-app
-------------------@latest
-------------------@13.4
```

2.

```js
cd next-app-name
```

3.

```js
npm run dev
```

# Poject Structure of Next.js

```ruby
my-nextjs-app/
│── public/                # Static assets (images, favicons, etc.)
│── src/                   # Source files (optional but recommended for better structure)
│   ├── app/               # App Router (for Next.js 13+ with the new app directory structure)
│   │   ├── layout.tsx     # Root layout for the app
│   │   ├── page.tsx       # Main page (Home)
│   │   ├── about/         # Example route (pages are inside folders)
│   │   │   ├── page.tsx   # About page
│   │   │   ├── layout.tsx # Optional layout for this route
│   │   ├── api/           # API routes (server-side functions)
│   │   │   ├── hello/route.ts # Example API route (GET /api/hello)
│   ├── components/        # Reusable components
│   │   ├── Header.tsx     # Example header component
│   │   ├── Footer.tsx     # Example footer component
│   ├── styles/            # Global and module styles
│   │   ├── globals.css    # Global CSS file
│   │   ├── Home.module.css # CSS Modules (scoped styles)
│   ├── lib/               # Utility functions, database connections, etc.
│   │   ├── db.ts          # Example database connection
│   ├── hooks/             # Custom React hooks
│   ├── context/           # React context providers
│   ├── store/             # State management (Redux, Zustand, etc.)
│   ├── middleware.ts      # Middleware (authentication, logging, etc.)
│── .env.local             # Environment variables (API keys, DB credentials)
│── .gitignore             # Files to be ignored by Git
│── package.json           # Project dependencies and scripts
│── tsconfig.json          # TypeScript configuration (if using TypeScript)
│── next.config.js         # Next.js configuration file
│── README.md              # Project documentation

```
# Adding Tailwind 4.0 config 

 ``` npm install -D tailwindcss``` <br>
 use ``` npx tailwindcss-cli@latest init``` to create the tailwind.config.js file. Updated with verion v4.0.