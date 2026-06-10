# RJ Content Engine

Gemini-powered personal brand content generator for Rudra Joshi. Research live trends, sharpen angles, and write LinkedIn/X posts in your voice using the PACC intelligence framework.

**Tagline:** Curiosity is the exploit.

## Features

- **Single Post**, **Batch × 3**, **X Thread**, and **Full Week** generation modes
- Live trend research via Google Search grounding
- Platform, pillar, and post-type controls with auto-pick options
- Copy individual posts or all output at once
- Per-post regeneration with a fresh angle

## Project Structure

```
├── index.html          # Main entry
├── css/styles.css      # Wine/copper luxury editorial theme
├── js/
│   ├── app.js          # State, init, UI handlers, modes
│   ├── api.js          # Gemini fetch (proxy or direct)
│   ├── prompts.js      # System prompt + buildPrompt()
│   └── render.js       # Render posts, copy, regenerate
├── api/
│   └── generate.js     # Vercel serverless proxy to Gemini
├── vercel.json
└── README.md
```

## API Key Modes

The app supports two ways to authenticate with Gemini:

### Mode 1 — Client-side key (local / fallback)

1. Get a free key at [Google AI Studio](https://aistudio.google.com/apikey)
2. Paste it in the app and click **Save Key**
3. The key is stored in `localStorage` (`rj_api_key`) and sent directly to Google's API from the browser

Best for: local development, opening `index.html` without a server, or when you prefer your own key.

### Mode 2 — Server proxy (deployed / recommended)

1. Set `GEMINI_API_KEY` in your Vercel project environment variables
2. Deploy to Vercel — the client calls `/api/generate` instead of Google directly
3. Users do **not** need to enter an API key

Best for: production deploys where you don't want users handling keys.

**Priority:** If a user has a saved browser key, the app uses the direct API. Otherwise it uses the server proxy.

## Local Development

### Static only (requires your own API key)

Serve the folder with any static server:

```bash
npx serve .
```

Open the URL, save your Gemini API key in the UI, and generate.

### With serverless proxy (Vercel dev)

```bash
npm i -g vercel
vercel dev
```

Create a `.env.local` file (never commit this):

```
GEMINI_API_KEY=your_key_here
```

## Deploy to Vercel

### Option A — Vercel CLI

```bash
vercel login
vercel
vercel env add GEMINI_API_KEY
vercel --prod
```

### Option B — GitHub integration

1. Push this repo to GitHub
2. Import the repo at [vercel.com/new](https://vercel.com/new)
3. Add environment variable: `GEMINI_API_KEY` = your Gemini API key
4. Deploy — no build command needed (static site + serverless function)

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GEMINI_API_KEY` | For proxy mode | Google Gemini API key (server-side only) |

Never commit `.env` or `.env.local` files.

## Tech Stack

- Vanilla HTML/CSS/JS (ES modules)
- Google Gemini 2.5 Flash with optional Google Search grounding
- Vercel serverless function for API proxy

## License

Private — personal brand tool for Rudra Joshi.
