# Active Context

## Current Focus
Whispering desktop app -- fixing Linux-specific issues and maintaining a fork with patches.

## Recent Changes
- [2026-04-01] Forked EpicenterHQ/epicenter to rob88pt/epicenter
- [2026-04-01] Fixed terminal paste: detect terminal windows via `xprop WM_CLASS` and send Ctrl+Shift+V instead of Ctrl+V
- [2026-04-01] Fixed Groq transcription: updated `tauri-plugin-http` from 2.5.4 to 2.5.7 to fix `fetch_cancel_body` command not found
- [2026-04-01] Built and installed patched `.deb` locally
- [2026-04-01] Opened PR EpicenterHQ/epicenter#1575

## Next Steps
- [ ] Verify terminal paste works with the installed `.deb` release build
- [ ] Monitor PR #1575 for upstream review/merge
- [ ] Sync fork when upstream merges the PR or releases a new version

## Blockers / Open Questions
- The xprop-based terminal detection hasn't been tested in the release `.deb` yet (only confirmed in dev build)
- VAD (voice-activated detection) mode shows "Failed to get recording stream" errors -- may be a separate issue

## Session Notes
- User runs Linux Mint with GNOME Terminal
- xdotool v3.20160805 does not have `getwindowclassname` -- had to use `xprop` instead
- Dev build uses `http_localhost_1420` for localstorage origin vs `tauri_localhost_0` in production -- settings don't transfer between dev/prod
