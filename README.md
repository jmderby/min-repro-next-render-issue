## Description

When using Next.js App Router, a specific combination of Server and Client Components with Context Providers and global CSS causes rendering issues. The server appears to hang and fails to re-render beyond the initial render.

The problematic setup involves:

1. A Server Component (`layout.tsx`) that imports global CSS (which is default from the create-next-app cli command) and renders a Client Component (`Providers`).
2. The `Providers` component wraps the children with a Context Provider.
3. A Client Component (`page.tsx`) is rendered as a child of the `Providers` component.

This configuration causes the Next.js server to become unresponsive, preventing subsequent re-renders and updates to the page.

## Steps to Reproduce

1. Run `pnpm i`
2. Run `pnpm dev`
3. Visit localhost:3000, see console logs not display on the client browser console.

Caveat: Issue will reproduce intermittently, to repro successfully, restart the Next.js server.

## Expected vs Actual Behavior

- Expected: App mounts and re-renders allowing the `TestProvider`'s console log to print client-side.
- Actual: Server hangs after initial render, blocking further updates

## Additional Context

This issue seems to be related to the interaction between Server Components, Client Components with Context Providers, and global CSS imports. It persists even when following Next.js best practices for mixing Server and Client Components.

A minimal reproduction repository has been created to demonstrate this issue.

This minimal reproduction was inspired by this Vercel guide of using React Context with Next.js: https://vercel.com/guides/react-context-state-management-nextjs
