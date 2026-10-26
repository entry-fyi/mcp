# Entry MCP server

Connect your AI assistant to [Entry](https://entry.fyi), your personal page and your writing. The assistant can read your profile and drafts, write and edit drafts, propose profile changes and ask you to publish. **You approve every public change in Entry.**

```
https://entry.fyi/mcp
```

A remote MCP server: Streamable HTTP, signed in with OAuth. There's nothing to install or run, and no API key. When your client connects, Entry asks you to sign in and choose which of your Entries to share and what the assistant may do.

- [Connect your assistant](#connect-your-assistant)
- [What the assistant can do](#what-the-assistant-can-do)
- [Tools](#tools)
- [Permissions](#permissions)
- [For client developers](#for-client-developers)
- [Agent Skills](#agent-skills)

## Connect your assistant

<details open>
<summary><b>Claude Code</b></summary>

```bash
claude mcp add --transport http entry https://entry.fyi/mcp
```

Then, inside Claude Code, run `/mcp` and sign in to Entry in your browser. Add `--scope user` to use it in every project.

Or install the plugin, which adds the server and the [Entry skills](https://github.com/entry-fyi/skills):

```
/plugin marketplace add entry-fyi/skills
/plugin install entry@entry
```
</details>

<details>
<summary><b>Claude</b> (claude.ai and desktop)</summary>

1. Open **Customize → Connectors** and choose **Add custom connector**. On Team and Enterprise plans an Owner adds it under Organization settings → Connectors → Add → Custom, and members then press Connect.
2. Name it Entry and paste `https://entry.fyi/mcp`.
3. Choose **Add**. Claude sends you to Entry: sign in, tick the Entries to share and choose **Allow**.
4. In a new chat press **+**, then **Connectors**, and turn Entry on.
</details>

<details>
<summary><b>ChatGPT</b></summary>

1. Open [ChatGPT Plugins](https://chatgpt.com/plugins). If your plan needs developer mode, turn it on first under Settings → Apps → Advanced.
2. Select **+**, then **Add custom MCP server**. Name it Entry.
3. Under Connection, paste `https://entry.fyi/mcp`. For authentication choose **OAuth** and leave any client ID and secret empty.
4. Read the risk warning, confirm, and create it.
5. ChatGPT sends you to Entry. Sign in, tick the Entries to share and choose **Allow**. Start a new chat and turn Entry on for it.
</details>

<details>
<summary><b>Cursor</b></summary>

[**Add to Cursor**](https://cursor.com/en/install-mcp?name=entry&config=eyJ1cmwiOiJodHRwczovL2VudHJ5LmZ5aS9tY3AifQ%3D%3D)

Or add it to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "entry": { "url": "https://entry.fyi/mcp" }
  }
}
```
</details>

<details>
<summary><b>VS Code</b></summary>

[**Add to VS Code**](https://insiders.vscode.dev/redirect/mcp/install?name=entry&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fentry.fyi%2Fmcp%22%7D) · [Add to VS Code Insiders](https://insiders.vscode.dev/redirect/mcp/install?name=entry&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fentry.fyi%2Fmcp%22%7D&quality=insiders)

Or add it to `.vscode/mcp.json`:

```json
{
  "servers": {
    "entry": { "type": "http", "url": "https://entry.fyi/mcp" }
  }
}
```
</details>

<details>
<summary><b>Codex CLI</b></summary>

```bash
codex mcp add entry --url https://entry.fyi/mcp
```

```bash
codex mcp login entry
```

Or add it to `~/.codex/config.toml`:

```toml
[mcp_servers.entry]
url = "https://entry.fyi/mcp"
```
</details>

<details>
<summary><b>Gemini CLI</b></summary>

```bash
gemini extensions install https://github.com/entry-fyi/skills
```

That adds the server and the Entry skills. Or add just the server:

```bash
gemini mcp add --transport http entry https://entry.fyi/mcp
```

Then, inside the Gemini CLI, run `/mcp auth entry` and sign in in your browser.
</details>

<details>
<summary><b>Antigravity CLI</b></summary>

Add it to `~/.gemini/config/mcp_config.json`:

```json
{
  "mcpServers": {
    "entry": { "serverUrl": "https://entry.fyi/mcp" }
  }
}
```
</details>

<details>
<summary><b>Zed</b></summary>

Add it to your `settings.json`:

```json
{
  "context_servers": {
    "entry": { "url": "https://entry.fyi/mcp" }
  }
}
```
</details>

<details>
<summary><b>Grok</b></summary>

1. Open [Grok connectors](https://grok.com/connectors). On Grok Business and Enterprise a team admin adds Entry first, in the xAI console under Grok Business → Connectors → Add Connector → Other.
2. Choose **New Connector**, then **Custom**. Name it Entry and paste `https://entry.fyi/mcp` as the Server URL.
3. Choose **Add Connector**. Grok sends you to Entry: sign in, tick the Entries to share and choose **Allow**.
</details>

<details>
<summary><b>Any other MCP client</b></summary>

Entry is a standard remote server, so any client that supports remote servers with OAuth works. A typical configuration:

```json
{
  "mcpServers": {
    "entry": { "type": "http", "url": "https://entry.fyi/mcp" }
  }
}
```

Where your client wants a key other than `url`, the URL goes in the same place.
</details>

The same steps, kept current, are at [entry.fyi/developers#connect](https://entry.fyi/developers#connect).

## What the assistant can do

Try asking:

- "Show my unfinished Entry drafts."
- "Create an article about my recent work."
- "Update the introduction of this draft."
- "Prepare this article for publication."
- "Change my headline to …"

It can:

- Read your Entry as you see it, including fields you haven't published, and your drafts and posts.
- Start a draft from your idea and edit it with you. Drafts are private until you publish them.
- Propose changes to your profile: name, headline, bio, location, links, availability.
- Ask you to publish a draft when it's ready.

It **can't** publish, unpublish or change your live page. A profile proposal or a publication request appears in Entry, where you see exactly what would change and approve or reject it. In ChatGPT and Claude, profiles, drafts and publication requests show as cards in the chat.

## Tools

| Tool | What it does | Writes? |
|---|---|---|
| `list_entries` | Lists the Entries this connection can reach | no |
| `get_entry_profile` | Reads a profile as the owner sees it, including unpublished fields | no |
| `list_drafts` | Lists working or published drafts, 20 at a time | no |
| `get_draft` | Reads one draft in full, with its revision | no |
| `create_draft` | Creates a private draft | adds a draft |
| `update_draft` | Saves changes to a draft against the revision last read | overwrites the fields sent |
| `propose_profile_update` | Proposes profile changes for the owner to approve | adds a proposal |
| `request_publication` | Asks the owner to publish a draft | adds a request |
| `get_publication_status` | Checks a publication request: pending, published, rejected, stale or withdrawn | no |

Every tool has an input and output schema with Entry's field limits (`maxLength`, `maxItems`) and explicit annotations (`readOnlyHint`, `destructiveHint`, `idempotentHint`, `openWorldHint`). Full schemas: [entry.fyi/developers#mcp-tools](https://entry.fyi/developers#mcp-tools).

## Permissions

When you connect, you choose which Entries the assistant may reach and which of five permissions it gets:

| Scope | Lets the assistant |
|---|---|
| `profile:read` | Read your profile |
| `drafts:read` | Read your drafts and posts |
| `drafts:write` | Create and edit drafts |
| `profile:propose` | Propose profile changes |
| `publish:request` | Ask you to publish a draft |

Disconnect any time from **Settings → Integrations → Connected apps** in Entry; access stops on the next request. Entry shares your content with an assistant only when you ask it to use Entry, and doesn't use it to train AI models. See the [privacy policy](https://entry.fyi/privacy).

## For client developers

| | |
|---|---|
| Endpoint | `POST https://entry.fyi/mcp` |
| Transport | Streamable HTTP, stateless, JSON responses (no sessions, no SSE). `GET` and `DELETE` are `405` |
| Auth | OAuth 2.1: authorization code with PKCE S256, dynamic client registration or a Client ID Metadata Document, `resource=https://entry.fyi/mcp` (RFC 8707) |
| Discovery | `401` with `WWW-Authenticate: Bearer resource_metadata="https://entry.fyi/.well-known/oauth-protected-resource/mcp"` |
| Authorization server | [`https://entry.fyi/.well-known/oauth-authorization-server`](https://entry.fyi/.well-known/oauth-authorization-server) |
| Personal access tokens | `Authorization: Bearer entry_pat_…`, made in Settings → Integrations, for testing with MCP Inspector |
| Limits | 120 reads and 30 writes a minute per connection; refusals carry `Retry-After` or `details.retryAfter` |
| MCP Apps | Cards for profiles, drafts and publication requests (`ui://entry/*`) in hosts that support them |

Check the server answers (without a token it must be `401` with a `WWW-Authenticate` header, which is how a client finds Entry's sign-in):

```bash
curl -i -X POST https://entry.fyi/mcp
```

Tool errors are tool results with `isError: true` and `{ code, message, details }`: `forbidden`, `not_found`, `conflict`, `validation_failed`, `limit_reached`, `rate_limited`, `bad_request`.

Entry also has a public, read-only API for published profiles (no auth) and an authenticated REST API for the same operations as this server: [entry.fyi/developers](https://entry.fyi/developers), [OpenAPI](https://api.entry.fyi/openapi.json).

## Agent Skills

[**entry-fyi/skills**](https://github.com/entry-fyi/skills) has Agent Skills that teach an agent to use Entry well: `entry` (this server, the right tool for each request, revisions and the approval boundary) and `entry-public-profiles` (looking people and companies up through the public API).

```bash
npx skills add entry-fyi/skills
```

## Support

- Help for owners: [entry.fyi/developers/support](https://entry.fyi/developers/support)
- Bugs and requests: [open an issue](https://github.com/entry-fyi/mcp/issues) or email hello@entry.fyi
- [Terms](https://entry.fyi/terms) · [Privacy](https://entry.fyi/privacy)
