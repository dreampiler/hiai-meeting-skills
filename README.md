# Hi AI Meeting skill

Use [Hi AI Meeting](https://hiai-meeting.com) from an AI assistant: prepare a useful meeting, connect its MCP tools, retrieve asynchronous results, and preserve the reasoning and disagreements.

Version 1.1.0 adds walkthroughs checked against the live site on 2026-11-21:

- [Signup/login, credits, API-key issuance, and non-meeting connection checks](skills/hiai-meeting/references/getting-ready.md).
- [Create a web meeting, check visibility and cost, read results, and download available files](skills/hiai-meeting/references/website.md).
- [Client settings and MCP request/result examples](skills/hiai-meeting/references/calling.md).

Web-only users do not need MCP or an API key. The assistant should start at the user's current step and keep signup, payment, authenticated discovery, and actual meeting completion distinct.

This repository distributes usage instructions only. It contains no backend source code, user meeting records, API keys, or automatic paid-meeting execution. Installing it does not make a purchase or connect an account.

## Install the skill

Install from the public `dreampiler/hiai-meeting-skills` repository:

```sh
npx skills add dreampiler/hiai-meeting-skills --skill hiai-meeting
```

For local installation, use the skill folder with your host's supported local-skill installation flow. The folder is `skills/hiai-meeting/` and includes its `references/` directory.

The root `plugin.json` packages a **skills-only** portable plugin named `hiai-meeting-guide`. `.claude-plugin/plugin.json` provides the Claude plugin manifest for the same guidance. A future connector-inclusive plugin must be registered separately where required; this package does not advertise a bundled MCP connection.

Gemini CLI can install the same skill through the root `gemini-extension.json` package:

```sh
gemini extensions install https://github.com/dreampiler/hiai-meeting-skills
```

The public repository's `gemini-cli-extension` topic enables discovery by the Gemini CLI extension gallery. Installation support and an actual gallery listing are separate checks.

## Connect the tools

The remote MCP endpoint is `https://hiai-meeting.com/v1/mcp`. It exposes `deliberate` and `get_judgment`. Issue your own personal API key in the site's Settings → API keys and configure it through your client's secret mechanism. Do not send your key in a prompt or commit it to Git.

See [connection examples](skills/hiai-meeting/references/calling.md) for Codex and Gemini CLI. Consumer web apps and official directories may require OAuth; CLI API-key support is not evidence of OAuth availability.

## Example requests

- “Use Hi AI Meeting to compare these two launch plans against my cost and deadline constraints.”
- “Help me connect Hi AI Meeting MCP in Codex without putting a key in this chat.”
- “Retrieve my existing judgment and explain its conclusion and remaining disagreements.”

Before an actual meeting, authorize the cost and the material sent to the service. Public-page lookups and setup explanations do not require a meeting.

## Cost and data

API/MCP meetings use subscription usage or credits. They do not have a free single-use allowance. Meetings are private by default; do not make one public unless the user requests it. Meeting inputs can be sent to multiple external model providers. Do not include credentials, personal data, or trade secrets. Multiple AIs agreeing is not a guarantee of correctness.

- [Developer documentation](https://hiai-meeting.com/developers)
- [Pricing](https://hiai-meeting.com/pricing)
- [Privacy policy](https://hiai-meeting.com/legal/privacy)
- [Terms](https://hiai-meeting.com/legal/terms)
- [Contact](https://hiai-meeting.com/contact)

Distribution status, review submissions, and compatibility should be checked against the actual directory listing. A local package is not proof of directory approval.
