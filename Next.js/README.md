### **Next.js: 20 Theoretical & Conceptual Questions**

**1. Q: What is Next.js and how does it differ from a standard React app (like one from Create React App)?**
*   **A:** Next.js is a popular **React framework** for building production-ready applications. Unlike a standard React app (CRA) which is a client-side library, Next.js provides a structured environment with features like server-side rendering, static site generation, file-based routing, and API endpoints out of the box. It solves many common problems you'd otherwise have to configure yourself.

**2. Q: What is Server-Side Rendering (SSR)? What are its main benefits?**
*   **A:** Server-Side Rendering is a rendering strategy where the server generates the full HTML for a page in response to a browser request. The server fetches data, renders the React components into an HTML string, and sends it to the client. Its main benefits are:
    *   **Better SEO:** Search engine crawlers can see the fully rendered HTML content, improving indexability.
    *   **Faster First Contentful Paint (FCP):** Users see the content of the page immediately, without waiting for a JavaScript bundle to load and execute.

**3. Q: What is Static Site Generation (SSG)? What are its main benefits?**
*   **A:** Static Site Generation is a rendering strategy where the HTML for all pages is generated at **build time**. The pre-built HTML, CSS, and JS files are then hosted on a CDN. Its main benefits are:
    *   **Extremely Fast Performance:** Pages are served instantly from a CDN, leading to the best possible performance.
    *   **High Security & Reliability:** With no server-side processes or database connections per request, the attack surface is minimal.

**4. Q: When would you choose SSR vs. SSG vs. Client-Side Rendering (CSR)?**
*   **A:**
    *   **SSG:** Best for content that is the same for all users and doesn't change often. Examples: a blog, marketing website, documentation pages.
    *   **SSR:** Best for pages that need to be SEO-friendly but display dynamic, user-specific, or frequently updated data. Examples: an e-commerce product details page with live pricing, a social media feed.
    *   **CSR:** Best for pages that are behind a login and don't need SEO, or for highly interactive applications. Example: a user dashboard, a complex web application like Figma.

**5. Q: What is Incremental Static Regeneration (ISR)?**
*   **A:** ISR is a hybrid rendering strategy that combines the benefits of SSG with dynamic data. It allows you to re-generate static pages *after* build time at a specified interval. When a user requests a page after its revalidation time has passed, they get the stale (cached) page, and Next.js triggers a regeneration in the background. The next user will get the freshly generated page.

**6. Q: Explain file-based routing in the Next.js Pages Router.**
*   **A:** In the Pages Router, every `.js`, `.jsx`, `.ts`, or `.tsx` file inside the `pages` directory automatically becomes a route. The file path maps directly to the URL path.
    *   `pages/index.js` -> `/`
    *   `pages/about.js` -> `/about`
    *   `pages/posts/first.js` -> `/posts/first`

**7. Q: How do you create a dynamic route in the Pages Router?**
*   **A:** You create a dynamic route by naming the file with square brackets. For example, the file `pages/posts/[slug].js` would match routes like `/posts/my-first-post` or `/posts/another-post`. The value of the dynamic segment (e.g., 'my-first-post') is passed as a query parameter to the page component.

**8. Q: What is the difference between `getStaticProps` and `getServerSideProps`?**
*   **A:** Both are data-fetching functions in the Pages Router.
    *   `getStaticProps`: Runs at **build time** on the server. It's used to fetch data for a page that will be statically generated (SSG).
    *   `getServerSideProps`: Runs on **every request** on the server. It's used to fetch data for a page that will be server-side rendered (SSR). The page will not be rendered until this function completes.

**9. Q: What is `getStaticPaths` and when is it required?**
*   **A:** `getStaticPaths` is a function used in **dynamic pages** that use `getStaticProps`. It is required to tell Next.js which dynamic paths to pre-render at build time. It must return an object with a `paths` array (listing the dynamic segments to build) and a `fallback` option.

**10. Q: What is the `_app.js` file used for?**
*   **A:** The `_app.js` (or `_app.tsx`) file is a custom App component that acts as a wrapper around all your pages. It is the ideal place to put shared layouts, global CSS files, inject global state (like with Context providers), or persist state between page navigations.

**11. Q: How is the `_document.js` file different from `_app.js`?**
*   **A:** `_document.js` is a custom Document component that allows you to augment the `<html>` and `<body>` tags of your application. It is rendered only on the **server**, so it's a good place for server-side only logic like setting the `lang` attribute on `<html>` or adding custom fonts. It should not contain any application logic, unlike `_app.js`.

**12. Q: What are API Routes in Next.js?**
*   **A:** Any file inside the `pages/api` directory is mapped to the `/api/*` endpoint and is treated as a serverless function. This allows you to build a full-stack application by creating a backend API directly within your Next.js project without needing a separate server.

**13. Q: How does the Next.js `<Image>` component optimize images?**
*   **A:** The `<Image>` component provides automatic image optimization. It serves images in modern formats like WebP, resizes them for different device viewports, and lazy-loads them by default to improve performance and Core Web Vitals.

**14. Q: What is the difference between `next/link` and a regular `<a>` tag?**
*   **A:** The `<Link>` component from `next/link` enables client-side navigation between pages, which is much faster than the browser's default full-page reload triggered by an `<a>` tag. It pre-fetches the code for the linked page in the background, making the transition feel instantaneous.

**15. Q: What is Next.js Middleware?**
*   **A:** Middleware allows you to run code on the server *before* a request is completed. It runs on a Vercel Edge Function, which is very fast. Common use cases include authentication, A/B testing, redirects, and modifying request/response headers.

**16. Q: What is the Next.js App Router?**
*   **A:** The App Router is a new routing and rendering paradigm introduced in Next.js 13. It is built on top of React Server Components and uses a directory named `app` instead of `pages`. It enables features like nested layouts, server components, and more granular data fetching.

**17. Q: Explain Server Components vs. Client Components in the App Router.**
*   **A:**
    *   **Server Components:** The default in the App Router. They run **only on the server**. They cannot use state or effects (`useState`, `useEffect`) and have direct access to the backend (e.g., filesystem, database). They are great for fetching data and improving performance by sending less JavaScript to the client.
    *   **Client Components:** You opt into these by adding the `"use client"` directive at the top of a file. They are rendered on the server for the initial page load and then "hydrated" to become interactive on the client. They are required for using hooks, event listeners, and any browser-only APIs.

**18. Q: What is the purpose of the `layout.js` file in the App Router?**
*   **A:** A `layout.js` file defines a UI that is shared across multiple pages. A layout wraps a `page.js` file or child layouts. A key feature is that layouts preserve state and do not re-render during navigation between child pages.

**19. Q: How does Next.js handle code splitting?**
*   **A:** Next.js has automatic code splitting built-in. Each page in the `pages` directory is split into its own JavaScript bundle. This means the browser only downloads the code necessary for the initial page, improving load times. It also supports dynamic imports (`import()`) for component-level code splitting.

**20. Q: What are Route Handlers in the App Router?**
*   **A:** Route Handlers are the equivalent of API Routes in the App Router. By creating a `route.js` file, you can define server-side endpoints that handle HTTP requests (e.g., `GET`, `POST`) using standard Web APIs like `Request` and `Response`.