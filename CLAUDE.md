# PORTAL — project context

Single self-contained `index.html` — a mobile-first showcase app (gyro-anchored raymarched Apollonian fractal + generative audio). Part of the single-prompt AI showcase series (siblings: `~/projects/flux`, `~/projects/echo`).

## Invariants

- ONE file, zero dependencies, no build step. Everything inline.
- Public repo `trusch/portal`, deployed via GitHub Pages from `main` root. Pushing to `main` is allowed for this repo.
- The JS `mapJS()` MUST stay mathematically identical to the shader `map()` — it is used for spawn search and glide collision.
- Audio changes must keep the mobile unlock dance (suspended AudioContext + gesture-end resume kicks) and the iPad audio-session promotion (audioSession.type='playback' + silent <audio> keepalive) intact.

## Verification

- Syntax: `awk '/<script>/{f=1;next}/<\/script>/{f=0}f' index.html > /tmp/p.js && node --check /tmp/p.js`
- Render: headless chromium with `--use-angle=swiftshader --enable-unsafe-swiftshader --virtual-time-budget=4000 --screenshot=...`, auto-call `open()` via injected setTimeout in a /tmp copy (never commit test harnesses).
- SwiftShader runs this at a few fps — black/short screenshots usually mean too few frames, not a broken app. Probe with readPixels when in doubt.
