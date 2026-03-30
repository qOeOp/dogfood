# Playwright Profile Conflict Reproduction

- Linked work items: WI-0004

- Date: 2026-03-29
- Scope: Codex desktop Playwright browser tool in the dogfood runtime
- Reproduction step: invoke the Playwright browser tool against `https://example.com`
- Observed behavior: Chrome opens a blank-tab style handoff into an existing session, the launched process exits with code `0`, and Playwright reports `browserType.launchPersistentContext: Failed to launch the browser process`
- Browser launch evidence:
  - launch command used `--user-data-dir=/Users/vx/Library/Caches/ms-playwright/mcp-chrome`
  - launch command used branded Google Chrome plus `--remote-debugging-port=<ephemeral-port>`
  - process output included `正在现有的浏览器会话中打开。`
- Local runtime evidence:
  - `/Users/vx/Library/Caches/ms-playwright/mcp-chrome` contains `SingletonLock`, `SingletonSocket`, and `SingletonCookie`
  - `lsof +D /Users/vx/Library/Caches/ms-playwright/mcp-chrome` showed a live Chrome owner process `PID 78343`
  - the live owner command line includes `--user-data-dir=/Users/vx/Library/Caches/ms-playwright/mcp-chrome`
- Interpretation: the current Playwright tool path is attempting a persistent-context launch against a profile directory that already has a live owner, so Chrome reuses the existing session instead of giving Playwright a fresh automation-owned browser process
- Recommended handling boundary: treat this as a preflight-detectable profile-ownership conflict; do not blindly retry and do not auto-kill the live owner by default
