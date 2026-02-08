# IDEAS.md

Future feature ideas for PomoLite. This document captures potential enhancements organized by category.

---

## 1. Keyboard & Accessibility

### Keyboard Shortcuts
**Summary:** Control the timer without touching the mouse.

**Description:** Add keyboard shortcuts for common actions — spacebar to start/pause, R to reset, 1/2/3 to switch stages, S to open settings. Display a help tooltip (?) showing available shortcuts.

**Implementation:** Add a `keydown` event listener on `document`. Map keys to existing button click handlers. Store shortcut preferences in localStorage for customization.

**Complexity:** Low
**Priority:** High

---

### Screen Reader Support
**Summary:** Make the timer fully accessible to visually impaired users.

**Description:** Add ARIA labels, live regions for timer updates, and ensure all interactive elements are keyboard-focusable. Announce stage changes and timer completion.

**Implementation:** Add `aria-label`, `aria-live="polite"` for timer display, `role="timer"`, and ensure proper focus management. Test with NVDA/VoiceOver.

**Complexity:** Medium
**Priority:** Medium

---

## 2. Notifications & Alerts

### Browser Notifications
**Summary:** Alert users even when the tab is in the background.

**Description:** Request notification permission and send a system notification when a stage completes. Include the next stage name and a "Start" action button.

**Implementation:** Use the Notifications API. Request permission on first timer start. Fall back to audio-only if denied.

**Complexity:** Low
**Priority:** High

---

### Custom Alert Sounds
**Summary:** Let users choose their preferred notification sound.

**Description:** Offer a selection of built-in sounds (chime, bell, gong, gentle beep) and allow users to upload their own audio file. Preview sounds in settings.

**Implementation:** Store sound preference in localStorage. For custom sounds, use FileReader to convert to base64 and store. Add a sound picker dropdown in settings.

**Complexity:** Medium
**Priority:** Medium

---

### Vibration Support
**Summary:** Haptic feedback for mobile devices.

**Description:** Trigger a short vibration pattern when a stage completes on supported devices.

**Implementation:** Use `navigator.vibrate([200, 100, 200])`. Feature-detect and only show option on supporting devices.

**Complexity:** Low
**Priority:** Low

---

## 3. Visual Enhancements

### Progress Ring
**Summary:** Circular progress indicator around the timer.

**Description:** Display an SVG ring that depletes as time passes, providing a visual sense of progress. Color matches the current stage.

**Implementation:** Use an SVG circle with `stroke-dasharray` and `stroke-dashoffset` animated via CSS or JS. Update offset each second based on remaining/total time.

**Complexity:** Medium
**Priority:** High

---

### Smooth Animations
**Summary:** Polish transitions between states.

**Description:** Add CSS transitions for stage changes (background color fade), button hover effects, settings panel slide-in, and timer digit changes.

**Implementation:** Use CSS `transition` properties. Consider `requestAnimationFrame` for timer digit flip animations.

**Complexity:** Low
**Priority:** Medium

---

### Theme Presets
**Summary:** One-click color schemes.

**Description:** Offer curated theme presets (e.g., "Ocean," "Forest," "Sunset," "Midnight") that set all three stage colors at once. Keep custom color option.

**Implementation:** Store theme presets as objects with focus/shortBreak/longBreak colors. Add a theme dropdown that applies all three colors.

**Complexity:** Low
**Priority:** Medium

---

### Dark Mode
**Summary:** Reduce eye strain in low-light environments.

**Description:** Add a dark mode toggle that adjusts card backgrounds, text colors, and UI elements for dark environments. Respect system preference via `prefers-color-scheme`.

**Implementation:** Use CSS custom properties for colors. Add a toggle that sets a `data-theme="dark"` attribute on `<html>`. Store preference in localStorage.

**Complexity:** Low
**Priority:** Medium

---

## 4. PWA & Offline

### Service Worker & Offline Support
**Summary:** Make PomoLite work without internet.

**Description:** Cache all assets so the app works offline. Show an "offline" indicator when disconnected but continue functioning normally.

**Implementation:** Create a service worker that caches `index.html` and any static assets on install. Use cache-first strategy. Register SW in main script.

**Complexity:** Medium
**Priority:** High

---

### Add to Home Screen (A2HS)
**Summary:** Installable as a standalone app.

**Description:** Add a web app manifest with icons, theme color, and display mode. Users can install PomoLite to their home screen for an app-like experience.

**Implementation:** Create `manifest.json` with required fields. Add `<link rel="manifest">`. Design app icons in required sizes (192x192, 512x512).

**Complexity:** Medium
**Priority:** High

---

## 5. Distraction-Free Mode

### Fullscreen Mode
**Summary:** Immersive, distraction-free timer view.

**Description:** A button or keyboard shortcut (F) to enter fullscreen mode with just the timer display. Minimal UI, maximum focus.

**Implementation:** Use the Fullscreen API (`element.requestFullscreen()`). Create a simplified fullscreen layout. Handle `fullscreenchange` event.

**Complexity:** Low
**Priority:** Medium

---

### Auto-Hide UI
**Summary:** Controls fade away during active sessions.

**Description:** After starting the timer, fade out control buttons and settings after a few seconds of inactivity. Show them again on mouse movement or touch.

**Implementation:** Use `setTimeout` to add a `.hidden` class after 3 seconds of no interaction. Listen for `mousemove`/`touchstart` to reset.

**Complexity:** Low
**Priority:** Low

---

## 6. Ambient Audio

### Background Sounds
**Summary:** Optional ambient audio during focus sessions.

**Description:** Offer ambient soundscapes (white noise, rain, coffee shop, nature) to help users concentrate. Volume control and toggle in settings.

**Implementation:** Use HTML5 `<audio>` with loop. Host small audio files or use royalty-free CDN sources. Store volume/selection preference.

**Complexity:** Medium
**Priority:** Medium

---

### Binaural Beats
**Summary:** Focus-enhancing audio frequencies.

**Description:** Generate binaural beats using Web Audio API for enhanced concentration (alpha/beta waves). Offer frequency presets.

**Implementation:** Use two `OscillatorNode` instances with slightly different frequencies. Require headphones warning.

**Complexity:** Medium
**Priority:** Low

---

## 7. Tracking & Stats

### Daily Session Counter
**Summary:** Track completed pomodoros today.

**Description:** Display a simple counter showing how many focus sessions were completed today. Reset at midnight.

**Implementation:** Store `{ date: "YYYY-MM-DD", count: N }` in localStorage. Increment on focus stage completion. Check date on load.

**Complexity:** Low
**Priority:** High

---

### Daily Goal
**Summary:** Set and track a target number of pomodoros.

**Description:** Let users set a daily goal (e.g., 8 pomodoros). Show progress toward the goal with a visual indicator and celebration when reached.

**Implementation:** Add goal setting in preferences. Compare completed count to goal. Trigger confetti or animation on goal completion.

**Complexity:** Low
**Priority:** Medium

---

### Session History
**Summary:** Log of past sessions with timestamps.

**Description:** Record each completed session with start time, duration, and stage type. Display a simple log view, filterable by day.

**Implementation:** Store session array in localStorage (with size limit). Add a history panel/modal. Consider IndexedDB for larger storage.

**Complexity:** Medium
**Priority:** Medium

---

### Streak Tracking
**Summary:** Gamify consistency with streak counts.

**Description:** Track consecutive days with at least one completed pomodoro. Display current streak and best streak.

**Implementation:** Store last active date and streak count. On session completion, check if consecutive day and update streak.

**Complexity:** Low
**Priority:** Medium

---

### Weekly/Monthly Charts
**Summary:** Visualize productivity over time.

**Description:** Simple bar charts showing pomodoros completed per day over the last week or month.

**Implementation:** Use CSS-only bar charts or a lightweight library. Aggregate session history data by day.

**Complexity:** Medium
**Priority:** Low

---

## 8. Task Management

### Mini Task List
**Summary:** Track what you're working on.

**Description:** A simple task input where users can note their current focus task. Optionally link tasks to completed sessions.

**Implementation:** Add a text input above/below the timer. Store current task in localStorage. Optionally log tasks with session history.

**Complexity:** Low
**Priority:** Medium

---

### Session Notes
**Summary:** Quick notes for each pomodoro.

**Description:** After completing a focus session, optionally prompt for a brief note about what was accomplished. Store with session history.

**Implementation:** Show a small modal/input on focus completion. Store note with session record. Make it skippable.

**Complexity:** Low
**Priority:** Low

---

## 9. Wellness Features

### Break Activity Suggestions
**Summary:** Ideas for what to do during breaks.

**Description:** Display random suggestions during breaks: "Stretch your legs," "Look out the window," "Get some water." Customizable list.

**Implementation:** Array of suggestions, randomly selected on break start. Allow users to add/remove suggestions in settings.

**Complexity:** Low
**Priority:** Medium

---

### Eye Strain Reminder (20-20-20)
**Summary:** Protect eye health with periodic reminders.

**Description:** Every 20 minutes, remind users to look at something 20 feet away for 20 seconds. Subtle notification that doesn't interrupt flow.

**Implementation:** Track cumulative focus time. Trigger gentle reminder at 20-minute intervals. Allow dismissal or disable.

**Complexity:** Low
**Priority:** Low

---

### Breathing Exercise
**Summary:** Guided breathing during breaks.

**Description:** Optional guided breathing animation during breaks (4-7-8 technique or box breathing) to help users actually relax.

**Implementation:** CSS animation with inhale/hold/exhale phases. Text prompts or expanding/contracting circle visual.

**Complexity:** Medium
**Priority:** Low

---

### Standing/Movement Reminder
**Summary:** Prompt to move during long breaks.

**Description:** During long breaks, suggest standing up and moving around with an optional movement timer.

**Implementation:** Display suggestion text on long break start. Optional countdown for movement duration.

**Complexity:** Low
**Priority:** Low

---

## 10. Sharing & Social

### Shareable Timer Links
**Summary:** Share timer settings via URL.

**Description:** Encode current settings (durations, colors) in URL parameters so users can share their setup with others.

**Implementation:** Serialize settings to URL query params. On load, parse params and apply settings. Add "Copy Link" button.

**Complexity:** Low
**Priority:** Low

---

### Embeddable Widget
**Summary:** Embed PomoLite in other sites.

**Description:** Provide an iframe embed code for blogs, Notion, or other sites. Compact widget mode with minimal UI.

**Implementation:** Create a `?embed=true` mode with stripped-down UI. Generate embed code snippet. Handle cross-origin considerations.

**Complexity:** Medium
**Priority:** Low

---

### Cloud Sync
**Summary:** Sync settings and history across devices.

**Description:** Optional sign-in (Firebase Auth) to sync settings and session history to the cloud. Access your data from any device.

**Implementation:** Add Firebase Auth (Google sign-in). Store user data in Firestore. Merge local and cloud data on sign-in.

**Complexity:** High
**Priority:** Low

---

## 11. Customization

### Custom Cycle Length
**Summary:** Configure how many pomodoros before long break.

**Description:** Let users change the default 4 pomodoros before long break cycle. Some prefer 3, others prefer 5.

**Implementation:** Add cycle length setting. Track completed focus sessions in current cycle. Reset count after long break.

**Complexity:** Low
**Priority:** Medium

---

### Timer Display Format
**Summary:** Choose how time is displayed.

**Description:** Options for MM:SS, M:SS (no leading zero), or countdown with total time (5:00 / 25:00).

**Implementation:** Add display format preference. Adjust timer rendering logic accordingly.

**Complexity:** Low
**Priority:** Low

---

### Font Customization
**Summary:** Choose timer font style.

**Description:** Offer a few font options for the timer display (monospace, sans-serif, retro digital).

**Implementation:** Include a few Google Fonts or system font stacks. Add font picker in settings.

**Complexity:** Low
**Priority:** Low

---

### Timer Size
**Summary:** Adjust timer display size.

**Description:** Let users scale the timer larger or smaller to fit their preference or screen size.

**Implementation:** Add a size slider or S/M/L options. Apply CSS `font-size` scale to timer container.

**Complexity:** Low
**Priority:** Low

---

## Summary Table

| Category | Feature | Complexity | Priority |
|----------|---------|------------|----------|
| Keyboard & Accessibility | Keyboard Shortcuts | Low | High |
| Keyboard & Accessibility | Screen Reader Support | Medium | Medium |
| Notifications & Alerts | Browser Notifications | Low | High |
| Notifications & Alerts | Custom Alert Sounds | Medium | Medium |
| Notifications & Alerts | Vibration Support | Low | Low |
| Visual Enhancements | Progress Ring | Medium | High |
| Visual Enhancements | Smooth Animations | Low | Medium |
| Visual Enhancements | Theme Presets | Low | Medium |
| Visual Enhancements | Dark Mode | Low | Medium |
| PWA & Offline | Service Worker | Medium | High |
| PWA & Offline | Add to Home Screen | Medium | High |
| Distraction-Free | Fullscreen Mode | Low | Medium |
| Distraction-Free | Auto-Hide UI | Low | Low |
| Ambient Audio | Background Sounds | Medium | Medium |
| Ambient Audio | Binaural Beats | Medium | Low |
| Tracking & Stats | Daily Session Counter | Low | High |
| Tracking & Stats | Daily Goal | Low | Medium |
| Tracking & Stats | Session History | Medium | Medium |
| Tracking & Stats | Streak Tracking | Low | Medium |
| Tracking & Stats | Weekly/Monthly Charts | Medium | Low |
| Task Management | Mini Task List | Low | Medium |
| Task Management | Session Notes | Low | Low |
| Wellness | Break Activity Suggestions | Low | Medium |
| Wellness | Eye Strain Reminder | Low | Low |
| Wellness | Breathing Exercise | Medium | Low |
| Wellness | Standing Reminder | Low | Low |
| Sharing & Social | Shareable Timer Links | Low | Low |
| Sharing & Social | Embeddable Widget | Medium | Low |
| Sharing & Social | Cloud Sync | High | Low |
| Customization | Custom Cycle Length | Low | Medium |
| Customization | Timer Display Format | Low | Low |
| Customization | Font Customization | Low | Low |
| Customization | Timer Size | Low | Low |

---

*Last updated: February 2026*
