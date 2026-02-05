# PomoLite

A lightweight pomodoro timer. Single HTML file, no dependencies.

## Features

- **3 stages**: Focus, Short Break, Long Break
- **Auto-advance**: Focus → Short Break (or Long Break every 4th) → Focus, auto-starts next stage
- **Configurable durations**: edit minutes directly on each stage button
- **Custom background colors**: pick a color per stage
- **Audio alerts**: 3-beep notification via Web Audio API when a stage completes
- **Tab-safe**: timer stays accurate when the browser tab is backgrounded

## Development

```bash
firebase emulators:start --only hosting
```

Open http://127.0.0.1:5002

## Deploy

```bash
firebase deploy --only hosting
```

## Tech

- Vanilla HTML/CSS/JS — no frameworks, no build tools
- Firebase Hosting (project: `pomolite001`)
- Live site: https://pomolite001.web.app
