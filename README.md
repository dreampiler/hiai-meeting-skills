# Hi AI Meeting — multi-AI meetings and workflow skill

With [Hi AI Meeting](https://hiai-meeting.com), several AI participants discuss the same question, respond to one another across rounds, and leave a record of the reasoning, agreements, and disagreements. A facilitator summarizes the discussion. Users can read public meetings or configure their own participants, purpose, flow, and result.

Hi AI Meeting은 여러 AI가 한 질문을 함께 토론하고, 발언·회의록·결론과 남은 이견을 기록하는 서비스입니다. 이 저장소의 스킬은 사이트 이용부터 MCP 회의, 파일 자료를 활용한 작업 의사결정과 사전 승인 범위의 검토까지 안내합니다.

## What you can use the service for

| Purpose | Example use |
|---|---|
| Watch a debate | See where viewpoints agree or clash |
| Group chat | Read a short informal exchange among AI participants |
| Counseling friends | Hear supportive AI viewpoints, without claiming professional counseling |
| Easy explainer | Explain a difficult topic for the intended reader |
| News commentary | Discuss supplied article material and distinguish facts from opinion |
| Widen ideas | Collect alternatives before narrowing to a choice |
| Make a decision | Compare options using explicit cost, deadline, or other criteria |
| Create together | Divide roles to prepare a document or selected output |
| Get a review | Check a plan, document, or code against requirements |

Purpose, output format, and closing method are separate choices. Some meetings leave a conversation or collection of ideas rather than one verdict. Model/persona choices, web search, reasoning, evidence modes, and some outputs depend on current availability, cost, or entitlements. AI agreement does not guarantee accuracy, and personas are simulated viewpoints rather than credentialed humans.

## What is on the website

- **Public meetings:** search, keywords, featured records, and recent/popular lists; public records can be read without signing in.
- **Meeting room:** follow remarks round by round, read facilitator summaries, inspect evidence and dissent, and view available results.
- **My meetings and Shelf:** find one's own web/API meetings, saved public meetings, available personas/features, and personal personas, presets, or document templates.
- **Results:** conclusion, criteria, evidence, assumptions, uncertainty, dissent, unresolved risks, and next checks. Available downloads include document formats and, for suitable outputs, presentation, spreadsheet/CSV, or calendar files.
- **Models, personas, and statistics:** explore participant choices and public-meeting activity. Within-service statistics are not a general benchmark of model intelligence.
- **Store and Settings:** view usage/credits, current subscriptions/products, purchases, account/display preferences, and personal API keys.

See the [service introduction](https://hiai-meeting.com/about), [meeting purposes](https://hiai-meeting.com/meeting-types), and [capability map](skills/hiai-meeting/references/capabilities.md).

## File-backed decisions and prior approval

An agent can write a concise Markdown brief from selected requirements, code, documents, checks, and alternatives, then ask a meeting for a decision or review. The current MCP exposes `deliberate` and `get_judgment` with text messages and **no native file-upload argument**. For MCP, the assistant transmits the brief's extracted text within the current background limit; a filename alone gives the panel no file. Actual file attachments use the website's supported attachment flow.

The user can adopt a bounded meeting-assisted workflow: consult a panel at a material decision or review checkpoint, then proceed when the verdict is clear and the action was already delegated. Explicit preferences guide recommendations; original prior approval defines authority. This can support technical approvals and decisions within specific pre-approved spending/publication limits. It cannot create permission, impersonate the user, or bypass required platform confirmation or direct user steps. The meeting itself executes no payment, permission change, or publication.

- [Prepare files and apply task review results](skills/hiai-meeting/references/decisions.md)
- [Pass preferences and explicit prior-approval context](skills/hiai-meeting/references/authority-context.md)

Version **1.1.1** keeps the 1.1.0 onboarding guides and adds the capability map, file-backed decisions, and explicit prior-approval context. Site/API facts were checked on 2026-11-21:

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
- “Prepare a review brief from these files. If the meeting confirms the documentation-only publication conditions I explicitly approved, proceed through the normal publishing tools.”
- “Use my supplied preferences and prior-approval document to assess whether this proposed action meets its conditions. Report missing authority instead of guessing.”

Before an actual meeting, authorize the cost and the material sent to the service. Public-page lookups and setup explanations do not require a meeting.

## Cost and data

API/MCP meetings use subscription usage or credits. They do not have a free single-use allowance. Meetings are private by default; do not make one public unless the user requests it. Meeting inputs can be sent to multiple external model providers. Do not include credentials, personal data, or trade secrets. Multiple AIs agreeing is not a guarantee of correctness.

- [Developer documentation](https://hiai-meeting.com/developers)
- [Pricing](https://hiai-meeting.com/pricing)
- [Privacy policy](https://hiai-meeting.com/legal/privacy)
- [Terms](https://hiai-meeting.com/legal/terms)
- [Contact](https://hiai-meeting.com/contact)

Distribution status, review submissions, and compatibility should be checked against the actual directory listing. A local package is not proof of directory approval.
