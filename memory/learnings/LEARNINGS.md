# Learnings Log

Discoveries, patterns, and non-obvious solutions. Recurring patterns get promoted to CLAUDE.md.

---

### LRN-001: xdotool version differences across distros
- **Logged:** 2026-04-01
- **Area:** backend
- **Priority:** high
- **Pattern-Key:** linux.xdotool_version_compat
- **Recurrence-Count:** 1
- **First-Seen:** 2026-04-01
- **Last-Seen:** 2026-04-01
- **Context:** xdotool v3.20160805 (shipped with Ubuntu 24.04/Mint) does not have `getwindowclassname`. Newer versions do. Code that uses xdotool must account for older versions.
- **Resolution:** Use `xprop -id $(xdotool getactivewindow) WM_CLASS` as a portable alternative. Works on all X11 systems regardless of xdotool version.
- **See Also:** ERR-001
- **Status:** pending

---

### LRN-002: Tauri JS/Rust plugin version sync is critical
- **Logged:** 2026-04-01
- **Area:** config
- **Priority:** critical
- **Pattern-Key:** tauri.plugin_version_sync
- **Recurrence-Count:** 1
- **First-Seen:** 2026-04-01
- **Last-Seen:** 2026-04-01
- **Context:** `bun install` updates JS plugins to latest semver-compatible version, but `cargo build` uses Cargo.lock which may pin an older Rust version. The JS side can call commands that don't exist in the older Rust side, causing silent failures.
- **Resolution:** Pin exact versions in Cargo.toml to match the JS plugin version. Check both `package.json` and `Cargo.lock` versions when debugging Tauri plugin errors.
- **See Also:** ERR-002
- **Status:** pending

---

### LRN-003: Tauri dev vs production use different localstorage origins
- **Logged:** 2026-04-01
- **Area:** config
- **Priority:** medium
- **Pattern-Key:** tauri.dev_prod_storage_origin
- **Recurrence-Count:** 1
- **First-Seen:** 2026-04-01
- **Last-Seen:** 2026-04-01
- **Context:** Dev mode uses `http_localhost_1420` origin, production uses `tauri_localhost_0`. WebView localstorage (API keys, settings) is scoped to origin, so copying the localstorage file between dev/prod doesn't work -- different filenames.
- **Resolution:** Re-enter settings manually in dev mode, or rename the localstorage file to match the target origin.
- **See Also:** --
- **Status:** pending
