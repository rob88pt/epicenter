# Changelog

## [2026-04-01] - Terminal Paste Fix and HTTP Plugin Update

### Added
- Terminal window detection on Linux via `xprop WM_CLASS` in `write_text` command
- List of 23 known terminal emulator class names for matching
- Fallback matching on "terminal" and "term" substrings in WM_CLASS

### Changed
- `tauri-plugin-http` pinned from `"2"` to `"2.5.7"` in Cargo.toml
- Cargo.lock updated with tauri-plugin-http 2.5.7 and transitive dependency updates (tauri 2.9.4 -> 2.10.3, wry 0.53.5 -> 0.54.2, etc.)

### Fixed
- Clipboard paste now sends Ctrl+Shift+V in terminal emulators on Linux (was Ctrl+V which terminals ignore)
- Groq cloud transcription fixed -- `fetch_cancel_body` command was missing because JS plugin (2.5.7) was ahead of Rust plugin (2.5.4)

### Decisions
- Used `xprop -id $(xdotool getactivewindow) WM_CLASS` instead of `xdotool getwindowclassname` because xdotool v3.20160805 (shipped with Ubuntu/Mint) doesn't have `getwindowclassname`
- Pinned exact version `2.5.7` rather than `"2"` to prevent future version mismatches
- Put detection logic in `#[cfg(target_os = "linux")]` block -- macOS and Windows unaffected

### Problems & Solutions
- `xdotool getwindowclassname` not found -> used `xprop` via shell subprocess instead
- `http.fetch_cancel_body not allowed` -> root cause was JS plugin v2.5.7 calling a command that Rust plugin v2.5.4 didn't have; fixed by updating Rust side
- Dev build localstorage uses different origin than production (`http_localhost_1420` vs `tauri_localhost_0`) -> settings/API keys don't transfer; user must re-enter
- Missing system deps for Tauri build: libssl-dev, libclang-dev, libasound2-dev, libvulkan-dev, glslc, and various GTK/WebKit libs

### Files Affected
- `apps/whispering/src-tauri/src/lib.rs` - terminal detection and Ctrl+Shift+V logic
- `apps/whispering/src-tauri/Cargo.toml` - pinned tauri-plugin-http version
- `apps/whispering/src-tauri/Cargo.lock` - dependency updates
