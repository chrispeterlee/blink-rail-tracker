# Blink Rail Tracker — Prototype

Real-time DB train delay tracker. Registers a journey and monitors for payout triggers via the v6.db.transport.rest API (no key required).

## What it does

- Register a journey by train number, stations, date and time
- Quick-fill presets for common ICE routes
- Looks up the live service via DB Navigator data feed
- Tracks departure delay and arrival delay in real time
- Auto-refreshes every 60 seconds
- Triggers payout card (lounge pass or €50 cash) at 60+ min delay

## Deploy to Netlify

### Option A — Netlify UI (easiest)
1. Push this folder to a GitHub repo
2. Go to app.netlify.com → Add new site → Import from Git
3. Select your repo — build settings auto-detected from `netlify.toml`
4. Deploy

### Option B — Netlify CLI
```bash
npm install -g netlify-cli
netlify login
cd blink-rail
netlify deploy --prod
```

## Notes

- Uses `https://v6.db.transport.rest` — no API key needed, 100 req/min rate limit
- Ticket scan step is mocked (alert placeholder) — real implementation would decode UIC 918.3 Aztec barcode
- EVA numbers (DB station IDs) are hardcoded for preset routes; manual entry triggers a live station search
- Payout trigger threshold set to 60 min arrival delay — adjust in `refreshTracking()` function
- Auto-refresh interval: 60 seconds
