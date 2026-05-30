---
name: planelet-creator
description: Create local SuperPlane Planelet plugin projects that developers can run with npm run dev. Use when your AI agent needs to create an npm-based local Planelet server from the planelet-sdk-ts documentation at https://github.com/EvanZhouDev/planelet-sdk-ts, generate a manifest/action starter from the SDK docs and examples, or make a plugin that SuperPlane can reach from Docker through host.docker.internal.
---

# Planelet Creator

## Overview

Create a local npm/TypeScript Planelet project by reading the Planelet SDK documentation first.

Planelet SDK source: https://github.com/EvanZhouDev/planelet-sdk-ts

The output must be a small local server with `npm run dev` as the main command.

## Workflow

1. Read the documentation first.
   - Open or fetch https://github.com/EvanZhouDev/planelet-sdk-ts and read its README, examples, package docs, and SDK source types before scaffolding.
   - Search the target workspace for existing Planelet conventions only after reading the SDK documentation.
   - If the target repo already has Planelet conventions, follow those conventions over generic assumptions.

2. Pick the target folder.
   - Use the folder requested by the user.
   - If no folder is specified, create a short slug folder in the current workspace.
   - Avoid overwriting non-empty folders unless the user explicitly asks for replacement.

3. Create the local Planelet from the docs.
   - Use npm scripts.
   - Use TypeScript unless the user explicitly asks for JavaScript.
   - Use `planelet-sdk-ts` when the docs show it as the intended path.
   - Include a `dev` script that starts the local server with `npm run dev`.
   - Include a simple starter action unless the user requested a specific integration.

4. Verify the local project.
   - Run `npm install` from the generated folder unless dependencies are already installed.
   - Run the available npm validation command, such as `npm run check`, `npm run typecheck`, or the documented equivalent.
   - Start it with `npm run dev` when the user wants a running local server, then report `http://127.0.0.1:<port>/manifest` and `http://host.docker.internal:<port>` for SuperPlane-in-Docker.

## Generated Project Shape

A typical docs-following local project should include:

- `package.json` with `dev`, `check`, `typecheck`, `smoke`, `build`, and `start` scripts.
- `src/plugin.ts` defining the Planelet plugin and actions.
- `src/server.ts` serving the plugin locally with Node.
- `src/smoke.ts` or tests validating `/manifest` and at least one action.
- `.env.example`, `.gitignore`, `tsconfig.json`, and a short project README.

The exact files and commands should follow the documentation read in step 1. The local server should default to a reasonable port such as `3000`, configurable with `PORT`.

```bash
npm install
npm run check
npm run dev
```

## Local Planelet Rules

- Use npm scripts in the generated project.
- Keep the server local and simple; do not scaffold a Next.js or Vercel app unless the user explicitly asks.
- Use `host.docker.internal:<port>` as the SuperPlane URL when SuperPlane runs in Docker.
