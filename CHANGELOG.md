# Changelog

## 1.2.3 — 2026-02-05

- Restrict Tab navigation to duration inputs only (remove buttons and color pickers from tab order)

## 1.2.2 — 2026-02-05

- Add meta description tag for SEO

## 1.2.1 — 2026-02-05

- Add inline SVG favicon (tomato icon)

## 1.2.0 — 2026-02-05

- Add reset settings icon button to clear localStorage and restore defaults

## 1.1.0 — 2026-02-05

- Persist user settings (durations and colors) in localStorage across page reloads

## 1.0.2 — 2026-02-05

- Swap default colors: Short Break is now blue, Long Break is now green

## 1.0.1 — 2026-02-05

- Fix: Stop auto-starting timer on page load; wait for user to press Start

## 1.0.0 — 2026-02-05

- Initial release
- 3 stages: Focus, Short Break, Long Break
- Auto-advance cycle (Long Break every 4th focus session)
- Configurable durations and background colors per stage
- Audio alerts via Web Audio API (3-beep notification)
- Tab-safe timer using Date.now()
- Fix: Sound playback on iOS and macOS Safari
