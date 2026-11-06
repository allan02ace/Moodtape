# Moodtape

Single-page app. The user describes a mood, the AI returns 15 songs, each with a short "why it fits" note and a Spotify search link.

## Files
- `index.html` – the whole front end (HTML, CSS, JS). Hosted on GitHub Pages.
- `manifest.webmanifest` – PWA manifest (name, colors, icons).
- `icon.svg` – logo. Used in the header, as the favicon, and in the manifest.
- `icon-192.png`, `icon-512.png` – manifest icons.
- `apple-touch-icon.png` (180px) – iOS home screen icon.
- `favicon-32.png` – fallback favicon.
- `worker.js` – Cloudflare Worker that calls Gemini. The API key lives here as the secret `GEMINI_API_KEY`.

## How it works
1. The page sends `{ prompt }` to `WORKER_URL`.
2. The Worker calls Gemini and returns `{ text }`.
3. `text` is JSON: `{"title": "...", "songs": [{"title": "...", "artist": "...", "why": "..."}]}`.

## Features
- Mood box with quick-idea chips
- OPM only switch (Filipino artists only)
- Remix keeps the OPM setting
- Copy track list

## Rules
- Keep all icon files and `manifest.webmanifest` in the same folder as `index.html`. Links are relative.
- Logo background is `#f9d3ba`. Keep `theme-color` and the manifest in sync with it.
- Keep the UI minimal. No eyebrow labels, no long instructions, no filler copy.
- Never put API keys in `index.html` or the repo.
- Never output song lyrics. Titles and artists only.
- Set `ALLOWED_ORIGIN` on the Worker to the GitHub Pages domain.
