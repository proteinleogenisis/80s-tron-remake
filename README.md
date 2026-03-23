# TRON: Online Multiplayer

An 80s-style Tron light-cycle game you can play with a friend in real time — no server required.

## Play

Open `index.html` in a browser (or host it anywhere static). No build step, no dependencies to install.

**To start a game:**
1. Player 1 clicks **CREATE ROOM** and shares the 5-character code
2. Player 2 enters the code and clicks **JOIN ROOM**
3. The game starts automatically after both players connect

## Controls

| Action | Keys |
|--------|------|
| Move up | `W` or `↑` |
| Move down | `S` or `↓` |
| Move left | `A` or `←` |
| Move right | `D` or `→` |

Touch/swipe controls are supported on mobile.

## How It Works

- **P2P networking** via [PeerJS](https://peerjs.com/) (WebRTC) — players connect directly, no backend needed
- The host (room creator) runs the authoritative game loop and sends state to the guest each tick
- Players leave glowing light trails; crash into a trail or the wall and you lose the round
- Score is tracked across rounds; rounds restart automatically after 2.5 seconds

## Tech Stack

- Vanilla HTML/CSS/JS — everything in a single `index.html`
- [PeerJS](https://peerjs.com/) for WebRTC signaling and data channels
- [Orbitron](https://fonts.google.com/specimen/Orbitron) + [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) fonts for the retro aesthetic

## Hosting

Drop `index.html` on any static host (GitHub Pages, Netlify, etc.) and share the URL. Players need to be on the same URL for PeerJS room codes to match.
