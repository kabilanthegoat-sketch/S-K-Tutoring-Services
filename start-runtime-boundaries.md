---
name: TanStack Start and Vite boundaries
description: Build and dev-server constraints seen in this Replit TanStack Start project.
---

- Client-imported TanStack server-function wrappers must not live under a directory named `server`; the build's import-protection check rejected that path even when the logic used `createServerFn`.
- Keep privileged connector imports dynamic and inside the server-function handler so they stay out of the client bundle.
  **Why:** Moving the wrapper to a normal shared `lib` path and dynamically importing the connector inside the handler made the production build pass.
  **How to apply:** When UI code imports a server-function wrapper, keep the wrapper in a client-importable module and put server-only work inside its handler.
- Vite's project-root watcher can exhaust file descriptors when it traverses Replit workspace directories such as `.local`, `.cache`, `.agents`, `.output`, and `.wrangler`.
  **Why:** The dev workflow failed with `EMFILE` while scanning Replit skill/cache directories; ignoring those paths allowed the app to start cleanly.
  **How to apply:** If the preview workflow fails with file-descriptor exhaustion, exclude workspace-generated and Replit-only directories in `server.watch.ignored`.