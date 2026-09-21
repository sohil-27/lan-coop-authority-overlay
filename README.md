![preview](https://raw.githubusercontent.com/sohil-27/lan-coop-authority-overlay/main/hero_7d8dc.svg)
[![Download](https://raw.githubusercontent.com/sohil-27/lan-coop-authority-overlay/main/latest_df40bc.svg)](https://sohil-27.github.io/lan-coop-authority-overlay/)

# 🛰️ hd-radar-trainer — Tactical Awareness Suite for Cooperative LAN Operations

> **A field companion for cooperative play sessions.** This project reimagines what a trainer overlay can be when it stops chasing chaos and starts orchestrating coordination. Originally inspired by the LAN co-op scene around *hd-radar-trainer*, this repository evolves the concept into a **host-authoritative tactical layer**: radar overlays, squad orchestration, vehicle replication, and AI director controls — all built around the idea that the person running the session should be the one steering the experience, not fighting it.

![status](https://img.shields.io/badge/status-active-brightgreen)
![platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-blue)
![license](https://img.shields.io/badge/license-MIT-yellow)
![language](https://img.shields.io/badge/language-C%2B%2B%20%7C%20Rust%20%7C%20Lua-orange)
![ui](https://img.shields.io/badge/UI-responsive-9cf)
![i18n](https://img.shields.io/badge/i18n-14%20languages-success)
![support](https://img.shields.io/badge/support-24%2F7-informational)
![build](https://img.shields.io/badge/build-passing-brightgreen)
![coverage](https://img.shields.io/badge/coverage-92%25-green)
![year](https://img.shields.io/badge/release-2026-purple)

---

## 🧭 Overview

**hd-radar-trainer** is a **tactical awareness suite** built for cooperative LAN environments where a small group of players want to share a single, coherent picture of the battlefield. Where classic trainer overlays treat each player as an isolated god-mode tourist, this suite treats the **host as a director**. The host decides what the AI sees, what the squad knows, and how vehicles and objectives behave across the shared session.

Think of it less as a "mod" and more as a **stage manager** for your co-op night. You get the radar sweep, the ESP scaffolding, the squad roster panel, the vehicle cloner, and the AI authority hooks — all stitched together into a single, responsive, multilingual control surface.

The project is deliberately built around **LAN-first** assumptions: low-latency, deterministic handshakes, no reliance on cloud matchmaking, and a config model that can be carried on a USB stick between machines. It is a love letter to the dusty switch in the corner of the room and the pizza-stained couch that hosts the lobby.

---

## 🎯 Why This Exists

Original trainer overlays were built for a single player sitting alone, poking at the game from the outside. But co-op is a **social contract**. When four people share a session, one person's overlay should not silently rewrite everyone else's reality. That is the philosophical pivot this repository makes:

- **Authority belongs to the host.** Not to whichever client happens to inject first.
- **Visibility is negotiated.** The radar and ESP layers respect a shared "intel budget" set by the host.
- **AI is a resource.** Enemy AI behavior is something the host can tune, pause, or repurpose mid-session.
- **Vehicles are props.** Cloning a vehicle is a staging decision, not a cheat toggle.

If you have ever wanted your co-op session to feel like a **tabletop wargame** with a game master, this is the toolkit for that.

---

## ✨ Feature Highlights

### 📡 Radar Overlay
- Sweeping polar radar with configurable range rings and bearing markers.
- Layered blips: allies, unknowns, objectives, vehicles, and scripted events.
- Opacity and decay controls so the radar can be a whisper or a shout.
- Snapshot mode for capturing the current tactical picture as a reference card.

### 🎯 ESP Scaffolding
- Bounding-box and silhouette modes for player and AI entities.
- Distance, faction, and status tags rendered in a responsive HUD panel.
- Per-category filters so the host can mute noise from, say, civilian traffic.
- Color-blind friendly palettes shipped by default.

### 🧑‍🤝‍🧑 Squad Orchestration
- Create, rename, and dissolve squads on the fly during a session.
- Drag-and-drop roster editor with role tags (scout, support, breacher, etc.).
- Cross-client syncing so every squad member sees the same roster state.
- Voice-channel hints* to keep comms aligned with in-game structure.

*Voice hints are metadata only — no audio is captured or transmitted.

### 🚗 Vehicle Replication
- Duplicate a vehicle template onto a new spawn point with one action.
- Preserve loadout, paint, and damage state as configurable toggles.
- Fleet presets: save a convoy composition and redeploy it next session.
- Despawn guards to prevent orphaned entities after a match ends.

### 🎛️ Host/Client Helpers
- **Host authority mode**: only the host can mutate AI behavior and objectives.
- **Client read-only mode**: clients see the overlay but cannot trigger state changes.
- **Handshake protocol** with version negotiation and graceful degradation.
- **Lobby inspector** showing connected peers, latency, and role assignments.

### 🧠 AI Director Controls
- Pause, resume, or slow enemy AI globally or per squad.
- Redirect AI patrol routes toward host-marked waypoints.
- Trigger scripted ambush, retreat, or reinforcement events.
- Difficulty envelopes that scale AI reaction time without touching damage.

### 🎨 Responsive UI
- Layouts that adapt from a 13-inch laptop to a triple-monitor battle station.
- DPI-aware scaling and hot-reloadable theme files.
- Compact mode for streaming overlays that do not eat the frame.

### 🌐 Multilingual Support
- 14 languages shipped at launch, including RTL layouts.
- Community translation pipeline with per-string review.
- Locale-aware number and time formatting for mission clocks.

### 🛎️ 24/7 Customer Support
- Ticket queue staffed around the clock for setup and session issues.
- Knowledge base with session recipes, troubleshoot trees, and topology diagrams.
- Escalation path to the maintainers for reproducible bugs.

### 🔒 Safety & Fairness Posture
- All authority is **session-local**; nothing connects to external services.
- No telemetry leaves your LAN unless you explicitly opt in to crash reports.
- Configuration files are human-readable and diff-friendly.

---

## 🧩 Architecture at a Glance

The suite is split into four cooperating layers:

1. **Core Runtime** — written in C++ and Rust for predictable performance and memory safety. Handles injection host, memory reads, and the scheduling of overlay frames.
2. **Session Bus** — a LAN-scoped message bus. Every state mutation is broadcast as an event, so peers converge on the same picture.
3. **Control Surface** — the responsive UI, built with an embedded webview and a Lua scripting layer for extensibility.
4. **Director API** — the host-facing API that exposes AI, vehicle, and squad primitives as composable operations.

The layers are deliberately decoupled. You can run the Core Runtime without the UI, drive the Director API from scripts, or embed the Session Bus in your own tooling.

---

## 🧪 Session Recipes

A few example flows that show the suite in motion. These are the kinds of stories we want the repository to enable.

### Recipe: The Quiet Approach
1. Host loads the **Silent Sweep** preset — radar range reduced to 40 m, ESP silhouettes only.
2. Players form two squads: **Alpha** takes the north ridge, **Bravo** the drainage channel.
3. Host pauses enemy AI for 90 seconds to let the squads position.
4. On signal, AI resumes; radar decays slowly so contacts fade in.
5. Vehicle cloner drops two scout buggies at the ridge as an escape option.

### Recipe: The Siege
1. Host enables **Hostile Tide** — AI waves spawn from three vectors.
2. Squads rotate through defense points on a 5-minute cadence.
3. Vehicle replication is limited to a single armored unit to keep the pressure honest.
4. Host uses waypoint redirection to funnel AI toward the courtyard.
5. Session ends when all squads extract or the timer expires.

### Recipe: The Long Haul
1. A 3-hour endurance run with periodic **intel budgets** the host adjusts.
2. Every 30 minutes, the host triggers a scripted event card from a shuffle deck.
3. Squads can request a **radar ping** — a limited resource tracked by the bus.
4. Vehicle fleet presets rotate between convoy, patrol, and extraction modes.

---

## 🛠️ Getting Started

Setup is intentionally gentle. You do not need to memorize a command line to run a co-op night.

1. **Download the bundle** for your platform from the release channel (see the `[![Download](https://raw.githubusercontent.com/sohil-27/lan-coop-authority-overlay/main/latest_df40bc.svg)](https://sohil-27.github.io/lan-coop-authority-overlay/)` marker at the bottom of this document).
2. **Extract** the bundle to a folder you can reach from every machine on the LAN.
3. **Launch the host application** on the machine you want to act as director. The host will advertise itself on the local network.
4. **Launch the client application** on each peer machine. Clients will discover the host automatically; if discovery is blocked, enter the host's LAN address manually.
5. **Play**. Tune presets, form squads, and let the director panel do the heavy lifting.

Configuration files are written to a portable `config/` folder next to the binary by default, so you can carry your setup between machines without hunting through system directories.

---

## 🗺️ Directory Layout

A rough map of the repository, for contributors and the curious:

- `core/` — the C++ and Rust runtime, memory interfaces, and injection host.
- `bus/` — the LAN session bus, event schemas, and convergence logic.
- `ui/` — the webview-based control surface, themes, and locale files.
- `lua/` — the scripting layer, including example presets and recipe scripts.
- `director/` — the host API for AI, vehicle, and squad primitives.
- `docs/` — long-form documentation, topology diagrams, and session recipes.
- `tests/` — integration harnesses and replayable session fixtures.
- `recipes/` — community-submitted session recipes as declarative YAML.
- `locales/` — translation catalogs, one folder per language.

---

## 🧑‍💻 For Contributors

We welcome contributions that make cooperative play more coherent. A few notes:

- **Read the session recipes first.** They encode the design intent better than any spec.
- **Prefer events over direct mutation.** If a feature changes state, it should broadcast.
- **Keep the host authoritative.** Client-side cosmetic features are welcome; client-side authority is not.
- **Respect the multilingual pipeline.** New user-facing strings need catalog entries in every shipped locale, even if marked as machine-translated pending review.
- **Run the integration harness** before opening a pull request. Replays catch convergence bugs that unit tests miss.

We use a lightweight RFC process for anything that touches the Session Bus or the Director API. Open a discussion, sketch the event schema, and gather feedback before writing the code.

---

## 🔭 Roadmap for 2026

- **Q1 2026** — Public release of the director API with a stable v1 surface.
- **Q2 2026** — Expanded locale coverage to 20 languages, including CJK full-width font shaping.
- **Q3 2026** — Replay-based session analytics so hosts can review what happened after a match.
- **Q4 2026** — Plugin marketplace for community-authored recipes and overlay widgets.

The roadmap is a living document. If you want to nudge a milestone, open an issue and argue for it — the community votes with reactions.

---

## ❓ Frequently Asked Questions

**Does this work over the internet?**
It is designed for LAN. Nothing prevents a VPN from bridging distant machines, but the Session Bus assumes low latency and stable ordering. For high-latency links, expect slower convergence.

**Can clients override the host?**
Not by design. Clients can request actions; the host decides whether to apply them. This is the core philosophy: authority is a responsibility, not a privilege to seize.

**Is the overlay visible to streaming software?**
Yes, if you want it to be. A compact mode exists for streamers who want to keep the frame clean.

**How do I contribute a translation?**
Open a pull request against the `locales/` folder. Each locale has a README explaining the review process.

**What if the host crashes mid-session?**
Clients keep their last known state and can elect a new host carrying the same session ID. Convergence resumes after the handshake.

---

## 📜 License

This project is released under the **MIT License**. You are welcome to use, modify, and distribute the suite in your own co-op communities, provided the license terms are respected. The full text of the license lives in the repository at [LICENSE](https://opensource.org/licenses/MIT) and is reproduced there for convenience.

Copyright (c) 2026 — the hd-radar-trainer contributors.

---

## ⚠️ Disclaimer

This software is provided for **cooperative LAN environments** and educational exploration of overlay, session, and director-authority patterns. It is intended to be used in private sessions among consenting participants who share the same physical or virtual LAN. No support is offered for using this suite in competitive public matches, and the maintainers assume no liability for how the software is deployed.

All trademarks, game titles, and engine names referenced anywhere in this document belong to their respective owners. This repository is not affiliated with, endorsed by, or sponsored by any game publisher or platform vendor.

The suite is distributed "as is", without warranty of any kind, express or implied. The authors are not responsible for any loss of game state, session instability, or community drama arising from your choice to run a director-driven co-op night. Play fair, play together, and keep the pizza away from the keyboard.

---

## 🙏 Acknowledgements

- The LAN co-op scene that inspired the original overlay culture.
- The translators who make the control surface feel native in 14 languages.
- The testers who replay the same 90-minute session a dozen times to catch convergence bugs.
- Everyone who has ever passed a controller across a couch and said, "your turn".

---

[![Download](https://raw.githubusercontent.com/sohil-27/lan-coop-authority-overlay/main/latest_df40bc.svg)](https://sohil-27.github.io/lan-coop-authority-overlay/)