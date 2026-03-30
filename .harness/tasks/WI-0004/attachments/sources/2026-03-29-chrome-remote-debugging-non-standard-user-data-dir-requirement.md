# Source Note

- Linked work items: WI-0004


- Date: 2026-03-29
- Source: Chrome remote debugging non-standard user data dir requirement
- URL: https://developer.chrome.com/blog/remote-debugging-port
- Type: official browser security blog
- Accessed date: 2026-03-29
- Trust level: high
- Notes: Chrome's March 17, 2025 security change says `--remote-debugging-port` and `--remote-debugging-pipe` are no longer honored for the default Chrome data directory. They must be paired with `--user-data-dir` pointing to a non-standard directory, and Chrome for Testing remains the recommended browser for automation scenarios.

## Optional Detail

- Topic: Chrome remote debugging non-standard user data dir requirement
- Publisher or owner: Chrome for Developers
- Published date: 2025-03-17
- Claim area: security boundary for remote debugging and automation profile isolation
- Supports: `WI-0004` decision to prefer preflight and explicit conflict reporting over blind retries against a shared persistent Chrome profile
- Conflicts with:
