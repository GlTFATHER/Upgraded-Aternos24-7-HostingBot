# 🤖 ABUXAR BOT — Minecraft AFK Bot

<div align="center">

![Version](https://img.shields.io/badge/version-3.0-blue?style=for-the-badge)
![Node](https://img.shields.io/badge/node-%3E%3D16-green?style=for-the-badge&logo=node.js)
![License](https://img.shields.io/badge/license-MIT-purple?style=for-the-badge)
![Status](https://img.shields.io/badge/status-active-brightgreen?style=for-the-badge)
![Made by](https://img.shields.io/badge/made%20by-ABUXAR-orange?style=for-the-badge)

**A powerful 24/7 Minecraft AFK bot that keeps your Aternos server alive — hosted free on Render.com**

[Features](#-features) • [Setup](#-setup) • [Commands](#-admin-commands) • [Dashboard](#-dashboard) • [Config](#-configuration)

</div>

---

## ✨ Features

### 🛡️ Anti-Ban & Movement
- ✅ Randomized arm swinging, hotbar cycling, sneaking
- ✅ Circle walk with pathfinder
- ✅ Random jumping & looking around
- ✅ Micro-walk with random intervals to appear human

### 🔄 Auto Reconnect
- ✅ Exponential backoff reconnect system
- ✅ Throttle detection with extended delay
- ✅ Crash recovery — bot never stays offline
- ✅ Ghost bot prevention on reconnect

### ⚔️ Combat & Survival
- ✅ Auto attack mobs (with 1.9+ cooldown support)
- ✅ Target locking — sticks to same mob for 3 seconds
- ✅ Auto eat when food drops below 14
- ✅ Mob/player avoidance mode
- ✅ Auto sleep in beds at night

### 🔐 Auth & Security
- ✅ Auto `/login` and `/register` on cracked servers
- ✅ Failsafe login after 10s if no prompt detected
- ✅ Admin-only command system

### 📊 Dashboard & Monitoring
- ✅ Live web dashboard with health/food bars
- ✅ Online players list
- ✅ Real-time chat log (last 10 messages)
- ✅ Uptime, coordinates, server status
- ✅ Auto-refreshes every 5 seconds

### 💬 Chat & Discord
- ✅ Scheduled chat messages with custom interval
- ✅ Discord webhook notifications (connect/disconnect/kick/players)
- ✅ Player join/leave greetings
- ✅ Chat log saved to `chat-log.txt`

### 🖥️ Hosting
- ✅ Self-ping every 10 minutes to prevent Render sleep
- ✅ Memory monitoring
- ✅ Works 100% free on Render.com

---

## 📁 File Structure

```
ABUXAR_BOT/
│
├── index.js          # Main bot file — all logic lives here
├── settings.json     # All configuration — edit this to set up your bot
├── package.json      # Dependencies
├── chat-log.txt      # Auto-generated chat log (created on first message)
└── README.md         # This file
```

---

## ⚙️ Setup

### Step 1 — Configure Aternos
1. Go to [aternos.org](https://aternos.org)
2. Install **Paper** or **Bukkit** as your server software
3. Enable **Cracked mode** (green switch in settings)
4. Install these plugins:
   - `ViaVersion`
   - `ViaBackwards`
   - `ViaRewind`

### Step 2 — Edit `settings.json`
Open `settings.json` and change:
```json
"ip": "YOUR_ATERNOS_SERVER_ADDRESS",
"port": YOUR_PORT_NUMBER,
"username": "YourBotName"
```

### Step 3 — Upload to GitHub
1. Create a new GitHub repository
2. Upload these files:
   - `index.js`
   - `settings.json`
   - `package.json`

### Step 4 — Deploy on Render (Free)
1. Go to [render.com](https://render.com) and sign up
2. Click **New → Web Service**
3. Connect your GitHub repository
4. Set the following:
   - **Build Command:** `npm install`
   - **Start Command:** `node index.js`
   - **Instance Type:** Free
5. Click **Deploy**

### Step 5 — Set Environment Variable
In your Render dashboard → your service → **Environment** tab:
```
RENDER_EXTERNAL_URL = https://your-app-name.onrender.com
```
This activates the self-ping so Render never sleeps.

### Step 6 — Start Aternos & You're Done! 🎉
Start your Aternos server. The bot will connect automatically within a minute.

---

## 🖥️ Dashboard

Visit your Render URL in the browser to see the live dashboard:

| Card | Description |
|------|-------------|
| 🟢 Status | Online / Reconnecting |
| ⏱️ Uptime | How long the bot has been running |
| 📍 Coordinates | Bot's current X Y Z position |
| ❤️ Health & Food | Live bars showing health and hunger |
| 👥 Online Players | List of all players currently on the server |
| 💬 Recent Chat | Last 10 in-game chat messages |

---

## 🔧 Admin Commands

Only players listed in the `admins` array in `settings.json` can use these:

| Command | Description |
|---------|-------------|
| `!pos` | Bot replies with its current coordinates |
| `!uptime` | Bot replies with how long it has been online |
| `!health` | Bot replies with current health and food level |
| `!follow <player>` | Bot follows the specified player |
| `!stop` | Bot stops all movement |
| `!say <message>` | Bot says a message in chat |

---

## 🔧 Configuration

Full `settings.json` reference:

```json
{
  "name": "AFK Bot",                    // Bot display name (shown on dashboard)

  "bot-account": {
    "username": "HEISENBERG",           // Bot's Minecraft username
    "password": "",                     // Leave empty for cracked servers
    "type": "offline"                   // "offline" for cracked, "microsoft" for premium
  },

  "server": {
    "ip": "your-server.aternos.me",     // Your Aternos server IP
    "port": 12345,                      // Your Aternos server port
    "version": "",                      // Leave empty to auto-detect
    "try-creative": false               // Set true if bot has OP
  },

  "admins": ["ABUXAR", "HEISENBERG"],   // Players who can use !commands

  "utils": {
    "auto-auth": {
      "enabled": true,
      "password": "yourpassword"        // Password for /login on cracked servers
    },
    "anti-afk": {
      "enabled": true,
      "sneak": true                     // Keep bot sneaking
    },
    "chat-messages": {
      "enabled": true,
      "repeat": true,
      "repeat-delay": 120,              // Seconds between messages
      "messages": ["Hello!", "I'm here"]
    },
    "chat-log": true,                   // Save chat to chat-log.txt
    "auto-reconnect": true,
    "auto-reconnect-delay": 2000,
    "max-reconnect-delay": 120000
  },

  "discord": {
    "enabled": false,                   // Set true to enable Discord notifications
    "webhookUrl": "YOUR_WEBHOOK_URL",
    "events": {
      "connect": true,
      "disconnect": true,
      "chat": false,
      "playerJoin": true
    }
  },

  "chat": {
    "respond": true,                    // Auto reply to "hi" / "hello"
    "greet-players": true               // Welcome players when they join
  }
}
```

---

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `mineflayer` | ^4.23.0 | Minecraft bot framework |
| `mineflayer-pathfinder` | ^2.4.5 | Navigation & pathfinding |
| `minecraft-data` | ^3.60.0 | Minecraft game data |
| `express` | ^4.18.2 | Web dashboard & API |

---

## 🌐 API Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /` | Live dashboard UI |
| `GET /stats` | JSON stats (health, coords, players, chat) |
| `GET /health` | Basic health check |
| `GET /ping` | Keep-alive ping |
| `GET /tutorial` | Setup guide page |

---

## ⚠️ Tips to Avoid Getting Banned

- Don't use obvious bot usernames like `BOT_123`
- Keep `repeat-delay` at 120+ seconds for chat messages
- Enable `look-around` and `random-jump` for natural movement
- Consider disabling `circle-walk` on strict servers
- Add more variety to your chat messages list

---

## 🙏 Credits & Acknowledgements

This project is an upgraded and extended version of the original bot created by **GlTFATHER**.

| | |
|---|---|
| 👤 **Original Author** | [MrJuice3046](https://github.com/MrJuice3046) |
| 📦 **Original Repo** | [Aternos24-7-HostingBot](https://github.com/MrJuice3046/Aternos24-7-HostingBot) |

The original project was used as a reference and base. This version builds on top of it with the following additions:
- Admin command system (`!pos`, `!uptime`, `!health`, `!follow`, `!stop`, `!say`)
- Live web dashboard with health bars, player list, and chat log
- Player join/leave Discord notifications
- Chat log saved to file
- `/stats` API endpoint
- Improved anti-ban randomization
- Bug fixes for ghost bots, double reconnects, and attack cooldowns

All credit for the original architecture and idea goes to **MrJuice3046**. This repo exists purely to build upon that work — not to take credit for it.

---

## 📄 License

MIT License — free to use, modify and distribute.

---

<div align="center">
Original by <a href="https://github.com/MrJuice3046"><strong>MrJuice3046</strong></a> • Upgraded by <strong>ABUXAR</strong>
</div>
