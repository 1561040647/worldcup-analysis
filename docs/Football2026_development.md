Football-2026 — Chrome Extension Development & Packaging

This document explains how to load, develop, debug and pack the Chrome MV3 extension in `Football-2026`.

Prerequisites: Node.js (16+), npm/yarn (optional), Chrome.

1) Load unpacked extension (development)

- Open Chrome → `chrome://extensions/` → enable Developer mode → "Load unpacked" → select the `Football-2026` folder.
- The extension icon should appear in the toolbar.

2) Build / asset generation

- If you modify icons or use generator scripts, run:

```bash
node Football-2026/generate-icons.js
```

(Install Node if required.)

3) Debugging

- Open `chrome://extensions/`, find the extension card, click "background page" → Inspect to open DevTools for the service worker/background.
- On the target website (e.g. zq.titan007.com) open DevTools Console to inspect content-script logs and interactions.
- For Manifest V3, service worker logs are ephemeral; use the Inspect view each time or use `chrome://serviceworker-internals` for longer tracing.

4) Pack extension for distribution

- In Chrome extensions page, click "Pack extension", choose the `Football-2026` folder and optionally provide a private key to produce a `.crx`.

5) Notes on MV3

- Background scripts run as service workers; avoid long-running operations in background.
- Use message passing and alarms for background tasks.

6) Local testing checklist

- Ensure `manifest.json` version is updated if required.
- Check `content-extractor.js` and `collector.js` are correctly mapping DOM selectors for the target site.
- If AI integration is used, confirm API endpoints / keys are configured in the Settings UI of the extension.

If you'd like, I can add a small `dev/` folder with recommended Node scripts and a short checklist for QA before publishing.
