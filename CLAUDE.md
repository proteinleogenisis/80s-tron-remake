# CLAUDE.md

## Project Overview
Single-file 80s-style Tron light-cycle game with real-time online multiplayer via PeerJS (WebRTC). Everything lives in `index.html` — HTML, CSS, and JS together.

## Architecture
- **Networking**: PeerJS (WebRTC peer-to-peer). Host drives the authoritative game loop; guest sends direction inputs and receives state.
- **Game loop**: Host runs `setInterval(hostTick, TICK)` at 35ms. Each tick moves players, checks collisions, sends full state to guest.
- **Grid**: Flat `Uint8Array(COLS * ROWS)` — 0 = empty, 1 = P1 trail, 2 = P2 trail.
- **Room codes**: 5-char alphanumeric code → PeerJS peer ID `tron-<code>`.

## Key Constants
- `CELL = 4` px per grid cell
- `COLS = 200`, `ROWS = 125` (800×500 canvas)
- `TICK = 35` ms per game tick
- P1 = cyan (`#00e5ff`), P2 = orange (`#ff6600`)

## Network Message Types
| type | direction | purpose |
|------|-----------|---------|
| `dir` | guest → host | player direction change |
| `state` | host → guest | full authoritative game state each tick |
| `roundEnd` | host → guest | scores + winner info |
| `newRound` | host → guest | trigger new round |

## Common Tasks
- **Change speed**: modify `TICK` (lower = faster)
- **Change grid size**: modify `CELL`, canvas width/height, `COLS`/`ROWS`
- **Add power-ups**: add to grid values (3+), handle in `hostTick`, sync via `state` message
- **Add more players**: extend `players` array and network protocol
