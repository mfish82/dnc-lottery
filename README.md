# 🎲 Degens n' Coffee — Alliance Lottery System

A single-file web app for running weekly prize lotteries for the Degens n' Coffee Discord community. No server, no build tools — just open the HTML file in a browser and connect it to your GitHub repo.

---

## ✨ Features

- **Multi-tier prize system** — Legendary, Epic, Elite, and Advanced tiers with configurable winner counts
- **Custom prizes** — Add one-off prize tiers for any round
- **Fair randomization** — Fisher-Yates shuffle guarantees every participant has an equal chance
- **GitHub-backed persistence** — Participants and history are stored in your repo and synced automatically
- **Winner history** — Full record of every past round saved to `history.json`
- **Discord formatting** — One-click copy of results formatted for Discord announcements
- **Animated reveals** — Winners appear with staggered animations for a dramatic effect
- **Tooltips** — Hover over any button or element for a detailed explanation

---

## 📁 Repository Structure

```
dnc-lottery/
├── index.html          # The entire app — styles, layout, and logic in one file
├── participants.json   # List of eligible participant names (array of strings)
├── history.json        # Record of all past lottery rounds and winners
└── README.md           # This file
```

---

## 🚀 Setup

### 1. Host the app
The app runs entirely in the browser. You can:
- Open `index.html` directly from your computer (double-click it), or
- Host it via [GitHub Pages](https://pages.github.com/) for easy access from any device

### 2. Generate a GitHub Personal Access Token
The app needs a token to read and write `participants.json` and `history.json`.

1. Go to [GitHub Settings → Developer Settings → Personal Access Tokens → Fine-grained](https://github.com/settings/tokens?type=beta)
2. Click **Generate new token**
3. Set the following permissions for this repository:
   - **Contents: Read and Write**
4. Copy the generated token (starts with `github_pat_`)

### 3. Configure the app
1. Open the app in your browser
2. Click **⚙ Settings** in the top-right corner
3. Enter:
   - **GitHub Username** — your GitHub username (e.g. `mfish82`)
   - **Repository Name** — `dnc-lottery`
   - **Branch** — `main`
   - **GitHub PAT** — the token you generated above
4. Click **Test Connection** to verify everything works
5. Click **Save & Connect**

The app will load all participants and history from your repo automatically.

---

## 🎮 How to Run a Lottery

1. **Check participants** — names appear in the left panel. Grayed-out names have already won this round
2. **Select prize tiers** — click any tier to toggle it on/off for this round
3. **Optionally add custom prizes** — enter a name and winner count, click **+**
4. **Click ⚡ Run Lottery** — winners are revealed with animated cards
5. **Copy for Discord** — click 💬 **Copy for Discord** and paste the result into your server
6. **Start a new round** — click **↺ New Round** to reset winner flags and increment the round counter

---

## 👥 Managing Participants

### Edit directly in the app
- Type a name in the bottom-left input and press **Enter** or click **+** to add
- Hover over any name and click **✕** to remove
- Changes save to `participants.json` on GitHub automatically (requires token)

### Edit the JSON file directly
`participants.json` is a simple array of strings:
```json
[
  "PlayerOne",
  "PlayerTwo",
  "PlayerThree"
]
```
You can edit this file directly in GitHub or with any text editor.

---

## 🏆 Prize Tiers

| Tier | Icon | Default Winners | Color |
|------|------|----------------|-------|
| Legendary | 👑 | 1 | Gold |
| Epic | 💎 | 2 | Purple |
| Elite | ⚔️ | 5 | Blue |
| Advanced | 🛡️ | 10 | Green |

### Changing winner counts
Edit the `TIERS` array near the top of the `<script>` section in `index.html`:
```js
const TIERS = [
  {id:'legendary', icon:'👑', label:'Legendary', qty:1},  // change qty here
  {id:'epic',      icon:'💎', label:'Epic',      qty:2},
  {id:'elite',     icon:'⚔️', label:'Elite',     qty:5},
  {id:'advanced',  icon:'🛡️', label:'Advanced',  qty:10},
];
```

---

## 🎨 Customizing the Look

All colors are defined as CSS variables at the top of the `<style>` block in `index.html`. Edit the `:root` block to retheme the entire app:

```css
:root {
  --gold: #c8973a;       /* Primary accent color */
  --bg-base: #0a0c12;   /* Page background */
  --legendary: #c8973a; /* Legendary tier color */
  --epic: #9b6ef0;      /* Epic tier color */
  /* etc. */
}
```

---

## 💾 Data Format

### participants.json
```json
["Name One", "Name Two", "Name Three"]
```

### history.json
```json
[
  {
    "round": 3,
    "date": "Feb 22, 2026",
    "entries": [
      {"name": "PlayerOne", "prize": "Legendary", "tierClass": "legendary"},
      {"name": "PlayerTwo", "prize": "Epic", "tierClass": "epic"}
    ]
  }
]
```

---

## ⚙️ Settings Reference

| Setting | Description |
|---------|-------------|
| GitHub Username | Your GitHub account username |
| Repository Name | The repo containing the lottery files |
| Branch | Usually `main` |
| GitHub PAT | Personal Access Token with Contents: Read & Write |

Settings are saved in your browser's `localStorage` — they persist across sessions on the same device/browser but won't carry over to other devices.

---

## 🔒 Security Notes

- Your PAT token is stored in your browser's `localStorage`. Do not use this app on shared or public computers.
- Generate a **fine-grained token** scoped only to this repository — don't use a token with broad permissions.
- Regenerate your token periodically for good security hygiene.

---

## 🛠️ Built With

- Vanilla HTML, CSS, and JavaScript — no frameworks or dependencies
- [GitHub Contents API](https://docs.github.com/en/rest/repos/contents) for reading and writing JSON files
- [Google Fonts](https://fonts.google.com/) — Cinzel, Rajdhani, Share Tech Mono
