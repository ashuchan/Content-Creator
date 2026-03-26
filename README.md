# Likhavat — Hindi Film Script Writer

A browser-based Hindi/Hinglish screenplay generator powered by Claude.

## Architecture

```
/
├── frontend/        Static HTML+JS (served on :3000)
│   └── index.html
├── server/          Node/Express SSE proxy (runs on :3001)
│   ├── index.js
│   └── package.json
├── package.json     Root — concurrently dev runner
└── README.md
```

The frontend never touches the Anthropic API directly. All calls go through the Express proxy (`POST /api/generate`) which streams tokens back as Server-Sent Events.

## Setup

### 1. Install dependencies

```bash
npm run setup
```

This installs root dev-deps (concurrently) and server deps in one shot.

### 2. Configure your API key

```bash
cp server/.env.example server/.env
# Edit server/.env and paste your Anthropic API key
```

### 3. Start dev servers

```bash
npm run dev
```

Opens:
- `http://localhost:3000` — the app
- `http://localhost:3001/health` — server health check

## Features

- **Hinglish/Hindi/English** output via language mix slider
- **Structured Bollywood beats** — opening, inciting incident, interval, climax, resolution
- **Streaming render** — script lines appear as tokens arrive, replaced with formatted layout on completion
- **Scene navigator** — right panel tracks scenes as they are generated
- **PDF export** — print-optimised layout via `window.print()`
- **Agla Scene** — appends the next beat without resetting the page

## Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start both servers concurrently |
| `npm run server` | Start API proxy only |
| `npm run frontend` | Start static file server only |
| `npm run setup` | Install all dependencies |
