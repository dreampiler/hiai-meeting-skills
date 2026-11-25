# Connection and calling reference

The current service documentation and connected tool schema take precedence over these examples. A skill install does not connect MCP or grant permission for paid meetings.

For signup/login, credit preparation, the one-time API-key issue screen, and a connection test that does not start a meeting, first read [getting-ready.md](getting-ready.md). For creating and reading meetings on the website, use [website.md](website.md).

## OAuth for supported remote MCP clients

1. Add a custom remote Streamable HTTP MCP server with URL `https://hiai-meeting.com/v1/mcp`. Select OAuth and automatic client registration when the client offers those options. Use the host's supported setup path. A directory listing is a separate publication step.
2. Continue to the Hi AI Meeting consent page. If asked to sign in, use the existing Google, Apple, or email route and return to consent. The user checks the displayed account, app, and permissions, then chooses whether to allow the connection.
3. List the tools after reconnecting. `mcp:judgment:read` reads the signed-in account's judgments. `mcp:meeting:create` separately permits `deliberate`, which can use credits. Connecting and listing tools consume no meeting credits.
4. To revoke access, open [MCP connection management](https://hiai-meeting.com/api/mcp/oauth/connections) from Hi AI Meeting Settings → API keys.

The [resource discovery document](https://hiai-meeting.com/.well-known/oauth-protected-resource/v1/mcp) and [authorization server metadata](https://hiai-meeting.com/.well-known/oauth-authorization-server) describe the OAuth flow. Automatic registration accepts supported Claude, ChatGPT and Google callback families. If a client uses a different callback, check compatibility or use the API-key method below.

## Personal API-key clients

Set `HIAI_API_KEY` using your environment's secret configuration. Do not commit its value. The value belongs in the transport's Authorization header, never the URL or a meeting message.

### Codex

Add this server using Codex's supported MCP configuration flow:

```toml
[mcp_servers.hiai]
url = "https://hiai-meeting.com/v1/mcp"
bearer_token_env_var = "HIAI_API_KEY"
```

### Gemini CLI

The corresponding entry in Gemini CLI settings is:

```json
{
  "mcpServers": {
    "hiai": {
      "httpUrl": "https://hiai-meeting.com/v1/mcp",
      "headers": { "Authorization": "Bearer <YOUR_PERSONAL_API_KEY>" }
    }
  }
}
```

This is a connection-shape example: replace the placeholder locally, never in chat or a committed file. Prefer your installed CLI version's supported secret mechanism. Do not assume `${HIAI_API_KEY}` expands safely in a remote header: Gemini CLI sanitizes sensitive environment variables and behavior must be verified for the installed version. If a protected local settings file is used, it contains the key and must remain private. Gemini CLI and the Gemini consumer app have separate integration and distribution flows. See the [official MCP configuration guide](https://geminicli.com/docs/tools/mcp-server/).

### Claude Code and other clients

Use the host's remote Streamable HTTP MCP settings for `https://hiai-meeting.com/v1/mcp` and configure the Authorization header through its secret mechanism. Avoid putting a literal key in a shell command, where it can enter shell history. The [developer guide](https://hiai-meeting.com/developers) also documents Claude Code and opencode settings.

### Cursor

In your private Cursor MCP configuration, add the same remote URL with an Authorization header that references `HIAI_API_KEY` using Cursor's documented `${env:HIAI_API_KEY}` syntax. In a Cursor plugin that exposes an API-key field, enter the value through the plugin's Configure screen. See [Cursor MCP configuration](https://cursor.com/docs/mcp).

## Submit an authorized decision meeting

Tool arguments, illustrated without a fixed preset ID:

```json
{
  "messages": [
    { "role": "system", "content": "Compare cost, implementation time, and reversibility. Preserve the user's stated requirements." },
    { "role": "user", "content": "A small team can ship either a documentation improvement or a new integration this week. No private customer data is included." },
    { "role": "user", "content": "Which should the team prioritize this week, and why?" }
  ],
  "extra_body": {
    "mpm": {
      "purpose": "decide",
      "answer_shape": "choice",
      "choices": ["Documentation improvement", "New integration"],
      "visibility": "private"
    }
  }
}
```

This is an example, not a request to run a meeting. Add `cost_cap_usd` if the user has specified a cost limit. Add `idempotency_key` if you need explicit retry control. Other meeting purposes and presets should come from the current schema or authenticated model list.

`deliberate` returns an ID and state. It does not return the final deliberation immediately:

```json
{ "judgment_id": "<returned ID>", "status": "created" }
```

Retrieve with `get_judgment`:

```json
{ "judgment_id": "<the same returned ID>" }
```

If the host wraps MCP output in `content` text blocks, parse the returned JSON and check `isError` before interpreting it as a result.

## Response interpretation

| Field | Meaning |
|---|---|
| `status` | Exact progress or terminal state; never infer completion just from a returned response |
| `result.decision` | The conclusion, which may paraphrase an option |
| `result.answer` | Narrative answer and supporting reasoning |
| `result.raw.sections` | Detailed sections such as dissent, open risks, and next verifications |
| `result.raw.adoption` | Participant adoption scores and reasoning |
| `result.preset` | Applied preset, including substitutions |
| `usage` | Billed usage according to the service's credit/subscription conventions |
| `trace_url` | Link to the full meeting record, subject to access controls |

For `partial`, show what was actually obtained and what is missing. For `blocked`, report the refusal. For `failed`, give the returned error and a useful next step. Authentication and balance failures require fixing that condition, not repeated paid submissions.
