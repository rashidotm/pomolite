# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PomoLite is a lite personal pomodoro timer with three selectable stages: Focus, Short Break, and Long Break. It is a static single-page application hosted on Firebase Hosting.

## Tech Stack

- **Frontend**: Vanilla HTML, CSS, and JavaScript (no framework, no build tools)
- **Hosting**: Firebase Hosting (project ID: `pomolite001`)
- **Firebase SDK**: v12.8.0 compat APIs loaded via CDN (`/__/firebase/` auto-configured paths)
- **Architecture**: Single-page app — all routes rewrite to `/index.html` via `firebase.json`

## Development

```bash
# Start local dev server (requires Firebase CLI installed globally)
firebase emulators:start --only hosting

# Local server runs at http://127.0.0.1:5002
```

```bash
# Deploy to production
firebase deploy --only hosting
```

There is no package.json, no bundler, and no test framework. All application code lives in `public/index.html` (inline styles and scripts) or additional files under `public/`.

## Architecture

- `public/` — the hosting root; everything here is deployed as-is
- `public/index.html` — the single entry point for the SPA
- Firebase SDK scripts are loaded from the hosting reserved `/__/firebase/` namespace (auto-configured by Firebase Hosting, works in both emulator and production)
- `firebase.json` — hosting config with SPA rewrite rule
- `.firebaserc` — maps `default` project alias to `pomolite001`
- `CHANGELOG.md` — version history; update this when making changes and bump the version in `public/index.html`

## Current State

The pomodoro timer is fully functional and live at https://pomolite001.web.app. Features include:

- Three stages (Focus, Short Break, Long Break) with auto-advance cycle
- Configurable durations and background colors per stage
- Audio alerts via Web Audio API (with iOS/macOS Safari fix)
- User settings persisted in localStorage
- Reset settings button to restore defaults
- Version number displayed in the controls card
