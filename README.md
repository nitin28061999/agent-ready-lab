# Agent Ready Lab

A production-oriented, local-first readiness report for code repositories. It checks whether a coding agent or a new contributor can understand the project, set it up, and get a useful signal from its workflows.

## Run locally

Requirements: Node.js 20 or newer and npm.

```powershell
npm ci
npm run build
npx wrangler pages dev dist
```

Open the local URL Wrangler prints. The app has no runtime server, account, API key, database, or third-party JavaScript dependency.

## Deploy free on Cloudflare Pages

Cloudflare Pages offers a free tier. This project uses Direct Upload, so it can deploy without a GitHub repository. A Cloudflare account is required for the hosted site.

For the first deployment, authenticate and create the Pages project:

```powershell
npx wrangler login
npx wrangler pages project create agent-ready-lab --production-branch main
npm run deploy
```

The site will be served at `https://agent-ready-lab.pages.dev` if that name is available. If it is already taken, Cloudflare will ask for another unique project name; update the project name in `package.json` and repeat the project creation step. Later deployments use `npm run deploy`.

Cloudflare documents the [Direct Upload workflow](https://developers.cloudflare.com/pages/get-started/direct-upload/) and [free plan limits](https://developers.cloudflare.com/pages/platform/limits/). Their current free Pages tier allows 500 builds per month; this project uploads prebuilt static files directly.

## Privacy and security

- Repository selection and analysis run entirely in the browser. Only filenames are inspected; file contents are not read or uploaded.
- The app makes no runtime network requests. Hosting serves static files; no project data is sent to Cloudflare by the app.
- `_headers` configures a restrictive Content Security Policy and common browser security headers.
- Generated output and local credentials are excluded from Git.
- The scanner skips common generated and dependency directories when counting and matching files.

This is a structured readiness checklist, not a security audit. Its filename-based signals can produce false positives and do not measure code quality or test effectiveness.

## Checks in this version

- Agent instructions such as `AGENTS.md`
- Project overview in a README
- Dependency setup and lockfiles
- Test and CI workflow structure
- Example environment configuration
- `.gitignore`
- Recognizable project entry points

## Why this project

Agent-assisted development is becoming a mainstream workflow. Gartner's November 2026 software engineering trends announcement calls out agent harnesses grounded in organizational knowledge and governance, and predicts a move toward eval-driven development. A repository readiness report is a concrete, approachable project at that intersection.

Sources: [Gartner: strategic technology trends in software engineering for 2026](https://www.gartner.com/en/newsroom/press-releases/2026-11-18-gartner-identifies-the-top-strategic-technology-trends-in-software-engineering-for-2026-and-beyond), [Anthropic: 2026 agentic coding trends report](https://resources.anthropic.com/2026-agentic-coding-trends-report).
