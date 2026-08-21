# DP Arcade: Trade Show Edition

Booth arcade for DentalPlans.com trade shows. One self-contained HTML file: lead capture gate, two games (Trivia Ladder and Savings Catcher), session tracking, per-device leaderboards, and cloud sync of every lead, game play, and feedback entry to a shared Google Sheet.

**Live booth URL:** https://jashydentalplans.github.io/DPTradeShow/

Current version: v2.1 (2026-08-21).

## How it works

- **Lead form gates the games.** Name, Practice, Email, Practice phone, ZIP, Role, plus 2 qualifier questions. Hot leads (does not accept DSPs + 25%+ uninsured patients) are flagged silently for same-day rep follow-up. Flags never show to attendees; they appear only in the staff dashboard and the data sheet.
- **Games:** Trivia Ladder (11-question DSP knowledge climb on a toothbrush ladder) and Savings Catcher (60-second catch game built on real DSP value props). Dollar values in Savings Catcher are illustrative and labeled as such.
- **Data pipeline:** every record is saved on-device first, then synced to a Google Apps Script webhook that writes tabs in the shared Google Sheet (Leads, Game Plays, Feedback, Test). Offline-safe: records queue locally on bad booth wifi and auto-retry; server-side record IDs prevent duplicates. The webhook URL is baked into the build, so a new device needs zero setup: open the URL and it syncs.
- **Multi-device:** each booth station keeps its own local leaderboards; all raw data flows to the one shared sheet.

## Booth ops runbook

1. Open the live URL in Chrome on each booth device. Keep the tab in the foreground and the device awake (hidden tabs pause the game by design).
2. The staff dashboard is behind the gear icon (bottom corner) with a staff PIN. From there: session stats, hot-lead list, CSV exports, cloud sync status, send test row, and full data wipe (double confirm).
3. No per-device setup is required for data capture. To point a device at a different sheet, paste a new webhook URL in the staff dashboard.
4. After the show: pull the lead list from the Google Sheet (or CSV export) and run the follow-up sequence. Hot leads get same-day contact.

## Repo contents

- `index.html`: the entire arcade (game code, styles, audio, data sync). Built from source parts and deployed as a single file to GitHub Pages.

Internal build notes, QA evidence, and the data-sheet link live in the DentalPlans project workspace (TradeShow-Build-Notes.md), not in this repo.
