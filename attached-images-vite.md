---
name: Attached images and Vite builds
description: Why uploaded attachment URLs that work in development may disappear from production builds.
---

Do not rely on a bare `/attached_assets/...` URL for a user-uploaded image: Vite can serve it in development, but it does not automatically copy that folder into production output. Import the image from application source so Vite emits it as a hashed production asset, then verify both the dev page and build output.

**Why:** Luke's uploaded photo loaded directly from `/attached_assets/...` in preview but was absent from the generated `.output/public` until Vite imported it.

**How to apply:** For a user-supplied image in `attached_assets`, make it an import dependency in the UI data module and confirm the generated production asset exists after `bun run build`.