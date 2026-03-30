# Source Note

- Linked work items: WI-0001


- Date: 2026-03-29
- Source: MCP roots boundary requirements
- URL: https://modelcontextprotocol.io/specification/2025-06-18/client/roots
- Type: official-spec
- Accessed date: 2026-03-29
- Trust level: high
- Notes: The MCP roots specification defines roots as filesystem boundaries, says clients should prompt for consent before exposing roots, and says servers should respect root boundaries and validate paths against the provided roots.

## Optional Detail

- Topic: MCP roots boundary requirements
- Publisher or owner: Model Context Protocol
- Published date: 2025-06-18
- Claim area: filesystem boundary / allowed mutation surface
- Supports: Any automatic harness bootstrap should stay inside `.harness/` and must not expand into user-owned top-level surfaces or require a second shadow control tree.
- Conflicts with: none
