# Source Note

- Linked work items: WI-0004


- Date: 2026-03-29
- Source: Playwright persistent user data dir warning
- URL: https://playwright.dev/python/docs/api/class-browsertype#browser-type-launch-persistent-context
- Type: official API documentation
- Accessed date: 2026-03-29
- Trust level: high
- Notes: Playwright documents that `launch_persistent_context()` uses a `user_data_dir` for persistent storage, browsers do not allow multiple instances with the same directory, and Chrome automation should avoid the user's default browsing profile. The official guidance is to use a separate directory for automation because pointing to the main Chrome user data directory can make pages fail to load or cause the browser to exit.

## Optional Detail

- Topic: Playwright persistent user data dir warning
- Publisher or owner: Playwright
- Published date: unknown
- Claim area: persistent profile concurrency and supported Chrome profile usage
- Supports: `WI-0004` diagnosis that a dedicated preflight should detect conflicting persistent-profile ownership before retrying the Playwright browser path
- Conflicts with:
