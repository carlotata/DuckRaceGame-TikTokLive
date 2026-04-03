# 🦆 Duck Race LIVE — TikTok Interactive Game

A real-time duck racing game powered by your TikTok LIVE stream. Viewers boost their favorite country's duck by sending gifts or typing chat commands — the duck that crosses the finish line first wins!

---

## 📋 Table of Contents

- [How It Works](#how-it-works)
- [Requirements](#requirements)
- [Setup & Installation](#setup--installation)
- [Running the Game](#running-the-game)
- [How to Play (For Streamers)](#how-to-play-for-streamers)
- [How Viewers Participate](#how-viewers-participate)
- [Countries & Gift IDs](#countries--gift-ids)
- [Game Features](#game-features)
- [Troubleshooting](#troubleshooting)
- [File Structure](#file-structure)

---

## How It Works

```
TikTok LIVE Stream
       │
       ▼
  server.js  ←── Reads gifts & chat via tiktok-live-connector
       │
       ▼
 WebSocket (ws://localhost:8080)
       │
       ▼
  index.html  ←── Duck race UI in your browser
```

The bridge server (`server.js`) connects to your TikTok LIVE and listens for gifts and chat messages. It forwards these events over a local WebSocket to the browser game (`index.html`), which then moves the ducks in real time.

---

## Requirements

- **Node.js** v16 or higher
- A **TikTok LIVE** account (you must be live when connecting)
- A modern web browser (Chrome recommended for OBS capture)

---

## Setup & Installation

**1. Install dependencies**

```bash
npm install
```

This installs:
- `tiktok-live-connector` — reads your TikTok LIVE stream events
- `ws` — WebSocket server library

**2. No other configuration needed** — gift IDs and boost values are already set.

---

## Running the Game

**Step 1 — Start your TikTok LIVE** on your phone or PC.

**Step 2 — Start the bridge server**

```bash
node server.js
```

You should see:
```
⚡ Boys vs Girls bridge ready on ws://localhost:8080
```

**Step 3 — Open the game in your browser**

Open `index.html` directly in your browser (double-click it, or drag it into Chrome).

**Step 4 — Connect to your stream**

In the bottom-right panel of the game:
1. Type your TikTok username (with or without `@`)
2. Click **▶ GO LIVE**
3. The status dot turns green and shows `LIVE: @yourusername` when connected

**Step 5 — The race starts automatically!**

Once connected, the race begins on its own. After each race, a new one starts automatically after 3 seconds.

---

## How to Play (For Streamers)

- **Tell your viewers** which country's gift boosts which duck (see the gift list panel on the right side of the game).
- **Show the game** on stream via OBS Browser Source or Window Capture.
- Use the **↺ Reset** button to manually reset the race at any time.
- Use the **▶ START** button to manually start a race.

### Suggested OBS Setup

1. Add a **Browser Source** or **Window Capture** pointed at `index.html`
2. Set the resolution to match your stream layout
3. The game has a dark background, so it overlays well

---

## How Viewers Participate

### 🎁 Sending Gifts (Strongest Boost)
Each country has a dedicated TikTok gift. Sending that gift boosts that country's duck by **+5%** progress.

| Country | Flag | Gift Name | Gift ID | Chat Command |
|---|---|---|---|---|
| 🇵🇭 Philippines | 🇵🇭 | Bibingka | 16757 | `/philippines` `/ph` `/pilipinas` |
| 🇺🇸 USA | 🇺🇸 | Fire 🔥 | 5583 | `/usa` `/us` `/america` |
| 🇮🇩 Indonesia | 🇮🇩 | Rose 🌹 | 5655 | `/indonesia` `/id` |
| 🇧🇷 Brazil | 🇧🇷 | Ice Cream Cone 🍦 | 5827 | `/brazil` `/br` `/brasil` |
| 🇮🇳 India | 🇮🇳 | GG | 6064 | `/india` `/in` |
| 🇲🇾 Malaysia | 🇲🇾 | You're Awesome | 15232 | `/malaysia` `/my` |
| 🇯🇵 Japan | 🇯🇵 | TikTok | 5269 | `/japan` `/jp` `/jpn` |

### 💬 Chat Commands (Small Boost)
Viewers can type a command in chat to boost a duck by **+0.3%** (no gift required):

```
/ph          → Boosts Philippines 🇵🇭
/usa         → Boosts USA 🇺🇸
/indonesia   → Boosts Indonesia 🇮🇩
/brazil      → Boosts Brazil 🇧🇷
/india       → Boosts India 🇮🇳
/malaysia    → Boosts Malaysia 🇲🇾
/japan       → Boosts Japan 🇯🇵
```

> Commands must start with `/` — for example: `/ph` or `/usa`

---

## Game Features

- **🏁 Real-time duck race** — 7 country ducks race across a river
- **🚀 Surge events** — Ducks randomly surge to make races unpredictable and exciting
- **🏆 Win Board** — Tracks how many races each country has won across all races in the session
- **📡 Live Feed** — Shows recent gifts and chat boosts as they happen
- **📊 Progress bars** — Shows each duck's % progress at the bottom
- **👥 Viewer count** — Displays current live viewer count in the header
- **🪙 Coin tracker** — Counts total gifts received during the session
- **Auto-restart** — New race begins automatically 3 seconds after a winner is declared
- **Test mode** — Click any gift row in the panel to manually trigger a boost (useful for testing without being live)

---

## Troubleshooting

**"Connection failed: Could not reach bridge server on localhost:8080"**
→ Make sure `node server.js` is running before clicking GO LIVE in the browser.

**"Failed to connect to TikTok"**
→ You must be actively LIVE on TikTok when connecting. The stream cannot be in a pending or ended state.

**Gifts are not being detected**
→ Check the console output of `server.js`. Gift events will print when received. Verify the correct Gift IDs are mapped (they can vary by region).

**Ducks are moving but gifts don't boost them**
→ The gift ID sent by TikTok may differ from what's configured. Check the server console for the actual `giftId` value being received and update `GIFT_BOOST` / `GIFT_GIRL_ADD` constants in `server.js` and `COUNTRIES` in `index.html` accordingly.

**The game window is blank**
→ Make sure you're opening `index.html` from the same folder where `server.js` is running. Both files must be in the same project directory.

---

## File Structure

```
project/
├── index.html        ← The game UI (open this in your browser)
├── server.js         ← TikTok bridge server (run with Node.js)
├── package.json      ← Node.js dependencies
└── package-lock.json ← Dependency lock file
```

---

## Boost Summary

| Action | Boost Amount |
|---|---|
| 🎁 Send a gift | +5% progress |
| 💬 Type a chat command | +0.3% progress |

Races are designed to be close and exciting — even a well-boosted duck can be caught by a natural surge from another. The first duck to reach **100%** wins!
