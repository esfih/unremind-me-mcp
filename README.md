# UnRemind.me MCP Server

Remote [MCP](https://modelcontextprotocol.io) server for
**[UnRemind.me](https://unremind.me)** — context-aware reminders that surface
when your *situation* matches, instead of firing at a fixed time.

An "Unreminder" carries context tags — where you are, what device you have,
whether you're online, who's around, how much time and energy you have — and
surfaces when your current context matches. Tasks can also be **delegated to
AI agents**, each with scoped access rights and an audit log the owner
reviews.

[![smithery badge](https://smithery.ai/badge/submissions-epan/unremind-me)](https://smithery.ai/servers/submissions-epan/unremind-me)

**Endpoint** · `https://unremind.me/mcp`
**Transport** · Streamable HTTP (JSON-RPC 2.0) · **Auth** · Bearer token ·
**Tools** · 16 · **Prompts** · 4

---

## Connect

1. Install UnRemind.me ([Android](https://unremind.me/) or the
   [web app](https://app.unremind.me/)) and sign in.
2. In the app: **Settings → AI agents → MCP access → Create token.** The token
   is shown once.
3. Add the server to your MCP client:

```json
{
  "mcpServers": {
    "unremind": {
      "type": "streamable-http",
      "url": "https://unremind.me/mcp",
      "headers": { "Authorization": "Bearer unr_YOUR_TOKEN" }
    }
  }
}
```

Verified with Claude and ChatGPT custom connectors (desktop and mobile).
Full walkthrough: **<https://unremind.me/mcp/>**

Each token is a separate *agent* in the app, with its own access rights, its
own audit log, and an optional expiry. Revoke any of them from the same
screen without affecting the others.

## Tools

See **[TOOLS.md](TOOLS.md)** for all 16 with descriptions. Every tool carries
MCP behavioural annotations (`readOnlyHint`, `destructiveHint`,
`idempotentHint`, `openWorldHint`) so a client knows which are safe to call
without confirming and which must not be blindly retried.

## Prompts

Four user-invocable prompts, available from your MCP client's prompt menu:

| Prompt | |
|---|---|
| **What can I do right now?** | Give it your available minutes and what you have with you; it finds the tasks that actually fit |
| **Plan my day** | Reviews overdue/due-soon work and checks real calendar conflicts before proposing times |
| **Capture this as an Unreminder** | Turns raw text into a well-tagged task |
| **Resume where I left off** | For an agent starting a session: orient, then continue instead of starting cold |

## Where to start

`orient` is the one to call first — it returns who the user is, how they want
to be worked with, what you were last doing, and what needs attention. One
call instead of guessing.

## Discovery documents

| | |
|---|---|
| Capability manifest | <https://unremind.me/.well-known/ai-capabilities.json> |
| Auth metadata (RFC 9728) | <https://unremind.me/.well-known/oauth-protected-resource> |
| LLM-facing site map | <https://unremind.me/llms.txt> |
| Health / liveness | <https://unremind.me/health> |

A `401` from the endpoint carries
`WWW-Authenticate: Bearer resource_metadata="…"`, so a compliant client can
discover the auth model without being told.

## Deep links

Every entity has both an app link and an https twin:

```
unremind://u/{id}              # opens the app
https://unremind.me/u/{id}     # always resolves
```

**Print both** when referring a person to something — you can't tell whether
they're reading on the device that holds the app or on a desktop where a
custom scheme resolves to nothing.

## Design notes for agent authors

- **`create_unreminder` submits for approval**; it does not silently appear in
  the user's list. Writes that a person will act on go through them.
- **Context tags describe what a task *requires*** to be doable (`Computer`
  means the task needs a computer) — never what the user currently has.
- **`save_progress` notes are yours, not a source of truth.** The user edits
  tasks in the app between sessions; always re-read the live task before
  acting on a recollection.

## Status

Production. Server `unremind-mcp` v2.0.0. Liveness at
<https://unremind.me/health> (`200` healthy / `503` degraded), checked
continuously.

Issues and questions: [open an issue](https://github.com/esfih/unremind-me-mcp/issues)
or <mailto:support@unremind.me>.

## License

[MIT](LICENSE) for this repository's contents. The UnRemind.me service itself is
governed by its [Terms](https://unremind.me/terms) and
[Privacy Policy](https://unremind.me/privacy).

## Listed on

- [Smithery](https://smithery.ai/servers/submissions-epan/unremind-me)
