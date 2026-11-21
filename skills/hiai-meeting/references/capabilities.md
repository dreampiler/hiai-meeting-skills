# Hi AI Meeting: capabilities and use cases

Based on the public service introduction, meeting-purpose guide, user guide, and developer interface checked on 2026-11-21. This is a feature map, not a promise of free use, a benchmark, or a list of fixed model IDs.

## Purpose and result

| Purpose on the site | Good fit | What to look for afterward |
|---|---|---|
| 토론 구경 / Watch a debate | Understand how views differ on a question | Positions, rebuttals, and the discussion record |
| 수다 모임 / Group chat | A short, informal exchange among AI participants | Conversation; no output document by default |
| 상담 친구들 / Counseling friends | Hear supportive viewpoints on a concern | Collected suggestions; not professional counseling |
| 쉬운 해설 / Easy explainer | Explain an unfamiliar topic for the intended audience | An explainer with levels and terms |
| 뉴스 논평 / News commentary | Discuss issues raised by supplied article material | Commentary and distinctions between facts and opinions |
| 아이디어 넓히기 / Widen ideas | Expand and compare possible approaches | Ideas and alternatives; not necessarily one winning choice |
| 결정하기 / Make a decision | Choose among options using explicit criteria | A supported conclusion, tradeoffs, and remaining dissent |
| 함께 만들기 / Create together | Divide roles to prepare a document or other work | The selected output, subject to available formats/entitlements |
| 점검받기 / Get a review | Check a plan, document, or code against requirements | Findings, reasons, changes, and a review verdict |

Purpose, output format, and closing method are separate choices. A summary/report is not guaranteed when no output was selected. The web UI and MCP may expose different settings, so use the live tool schema for machine-readable values.

## How the meeting works

Participants contribute viewpoints across rounds and respond to earlier remarks; a facilitator summarizes the round and helps converge or collect the views. Users can choose model/persona configurations and presets, adjust permitted round and utterance settings, and optionally enable modes such as web search, reasoning, evidence presentation, or source checking where offered. These can affect cost or require an entitlement. A persona is a simulated role/viewpoint, not a credentialed human expert.

Result views can retain the original conversation, facilitator summaries, and a generated output with conclusion, criteria, evidence, assumptions, uncertainty, dissent, unresolved risks, and next checks. Depending on purpose and output, the site offers document/spreadsheet/presentation/calendar downloads. Read the available controls for that meeting rather than promising all formats.

## The site's main areas

| Area | What users can do |
|---|---|
| [Home](https://hiai-meeting.com) | Search and browse public meetings, featured records, keywords, and recent/popular lists |
| Meeting room | Read/replay remarks, inspect evidence and summaries, follow progress, and view available outputs |
| [My meetings](https://hiai-meeting.com/meetings) | Find one's own web/API meetings, inspect results/status/usage, and manage visibility or deletion through explicit controls |
| [Shelf](https://hiai-meeting.com/shelf) | Revisit saved public meetings and available personas, purchased features, personal presets/personas, or document templates |
| [Personas](https://hiai-meeting.com/personas) and [models](https://hiai-meeting.com/models) | Explore participant choices and current model information; some choices are entitlement-dependent |
| [Stats](https://hiai-meeting.com/stats) | Explore activity in public meetings; within-service model/persona records are not general model-performance rankings |
| [Store](https://hiai-meeting.com/billing) | View usage/credits and current products, subscriptions, purchases, and refund paths |
| [Settings](https://hiai-meeting.com/settings) | Manage account/display/notifications/subscription and personal API keys |
| [Developer guide](https://hiai-meeting.com/developers) | Connect MCP or the OpenAI-compatible API; API-created meetings can also be opened on the web |

## Agent-assisted work

Useful examples include comparing implementation options, reviewing a specification or patch against the user's requirements, assessing a proposed release, or co-creating an outline. Build a concise meeting brief from the relevant files rather than sending an entire repository. Follow [decisions.md](decisions.md) for the current file-transfer limits and [authority-context.md](authority-context.md) when prior user approval is part of the decision.

MCP currently exposes `deliberate` and `get_judgment`; it has no file-upload or payment/permission/publication tool. Local files can inform a meeting through extracted text in messages. Actual file attachments are a web-meeting capability, not something to invent as an extra MCP argument.

Public reading is free; running web/API meetings can consume subscription allowance or credits. The service can send meeting material to multiple external model providers. See the current [pricing](https://hiai-meeting.com/pricing), [privacy policy](https://hiai-meeting.com/legal/privacy), and [terms](https://hiai-meeting.com/legal/terms) for the applicable conditions. A group of AIs reaching agreement does not guarantee truth or replace the user's responsibility.
