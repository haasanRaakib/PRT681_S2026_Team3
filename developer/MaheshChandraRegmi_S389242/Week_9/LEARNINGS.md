# Week 9 — Frontend fundamentals + Next.js

Week 7 I got a React page working against `TasksApi` with Vite, but I was leaning on what I already knew. This week I went back over the frontend basics underneath it, then rebuilt the same tasks UI in Next.js to see what the framework actually adds.

## Frontend refreshers

- semantic HTML — `form`, `button type="submit"`, real `label`s — instead of div soup
- flexbox vs grid: flex for one axis, grid for the two-axis layout of the tasks table
- plain JS before React: DOM selection, events, `fetch` with `async`/`await`
- component thinking: props flow down, events flow up, and state lives at the highest common parent

## Next.js (App Router)

- file-based routing: a folder is a URL segment, `page.tsx` is the page
- server components by default — data fetching happens on the server, no `useEffect` dance
- `'use client'` only where I need interactivity (the add-task form, the delete buttons)
- `layout.tsx` for the shared shell, plus the loading/error file conventions
- route handlers as a small backend-for-frontend
- deployed the demo to Vercel to see the difference from `npm run dev`

## Things I sat with

**Server components changed where fetch lives.** The Week 7 React app fetched in `useEffect`, showed a spinner, then rendered. The Next.js version fetches in the component and arrives already rendered — less client code, no loading flash.

**Vite SPA vs Next.js is a trade-off, not an upgrade.** My `TasksWeb` talks to a separate ASP.NET API and that's fine. Next.js wins when I want rendering, routing, and API in one deployable thing.
