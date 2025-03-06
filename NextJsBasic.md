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

    and it can very for request to request like for POST , GET , UPDATE , DELETE etc

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
