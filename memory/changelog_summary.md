# Changelog Summary

## Current State
Forked from EpicenterHQ/epicenter. Two fixes applied: Linux terminal paste (Ctrl+Shift+V detection) and tauri-plugin-http version mismatch (2.5.4 -> 2.5.7). PR #1575 open upstream. Patched `.deb` installed locally, pending terminal paste verification.

## Major Milestones
- **[2026-04]** Forked repo, fixed terminal paste and Groq transcription, opened upstream PR

## Key Decisions
- Use `xprop` for WM_CLASS detection instead of newer xdotool commands (see [[decisions.md]] ADR-001)
- Pin `tauri-plugin-http = "2.5.7"` explicitly to prevent JS/Rust version drift

## Recent Focus
- Getting Whispering app building and running on Linux Mint
- Fixing clipboard paste for terminal usage
- Fixing broken Groq cloud transcription due to plugin version mismatch
