# Pending workflow

`publish-mcp-registry.yml.txt` belongs at
`.github/workflows/publish-mcp-registry.yml`.

It could not be pushed with the current token: GitHub refuses to let an OAuth
app create or update a workflow file without the `workflow` scope. Nothing is
wrong with the file — this is purely a token-scope restriction.

To install it, either:

```bash
gh auth refresh -s workflow          # one device-code prompt, then re-push
```

or paste the file into the GitHub web editor at
`.github/workflows/publish-mcp-registry.yml`.

Then publish to the official MCP Registry with
**Actions → Publish MCP Server → Run workflow** — it authenticates via GitHub
OIDC, so there is no login step.
