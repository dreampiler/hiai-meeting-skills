# Create a web meeting and read its result

Checked on 2026-11-21 against the live preparation dialog, Store, API-key settings, a public meeting's result tabs, and the site's [user guide](https://hiai-meeting.com/getting-started) and [new-meeting guide](https://hiai-meeting.com/guide). Use the labels displayed in the user's selected language. Do not copy the current user's balance, meeting contents, keys, or account details into examples.

## Prepare

For a new user, follow [getting-ready.md](getting-ready.md) through sign-in and usage/credit preparation. An API key and MCP are **not** required for the web workflow. Someone who only wants to read can open public meetings without signing in.

Before entering a question, identify the desired result, options if any, relevant non-confidential context, and constraints such as budget or deadline. A general request to use the website does not authorize payment, publication, or starting a charged meeting on the user's behalf.

## 1. Open the meeting preparation window

After signing in, select **+ 새 회의** in the top bar. A preparation window headed **회의를 시작하기 전에** opens on an unexecuted meeting draft. The site may show a suggested question and remember previous meeting settings. Replace a suggested question if it is not the user's question; check the current visibility, purpose, and other carried-over settings instead of assuming a clean default.

If the user stops before starting, use **닫기** to leave the preparation flow. In the checked flow, closing discarded that unexecuted draft and returned to the entry page; it did not start a meeting. Do not confuse a draft with a running or paid meeting.

## 2. Fill the five main sections

| Section | What to do |
|---|---|
| **1 질문** | State the actual question in one sentence with enough context to distinguish the options. Replace any suggested topic. The current limit is shown in the form. |
| **2 목적** | Choose the intended experience: discussion, comparison/decision, review, explanation, co-creation, and so on. This sets suitable participant/round/output defaults. See [meeting types](https://hiai-meeting.com/meeting-types) when unsure. |
| **3 목표와 자료** | State what should be in hand at the end. Add necessary materials or supported attachments without personal data, credentials, or trade secrets. News commentary and Easy explainer expose source-text and source-URL fields; a URL alone is not automatically fetched as article content. |
| **4 웹 검색 · 공개 · 피드백** | Check search, visibility, and when the facilitator may ask the user for direction. Search can cost more. Use private visibility unless public sharing is explicitly desired. |
| **5 프리셋** | Start with a preset matching the desired depth; inspect its participant count, rounds, output, maximum cost, and time. A preset fills settings, but does not make them free. |

The web form's fields and MCP argument names are not interchangeable. Do not paste an MCP JSON request into a web input or infer API enum values from translated button labels.

If necessary, open **상세 설정** to adjust participants/models/personas, flow and rounds, or result format/closing method. The **서식** is what document is produced; **마무리 방식** is how the discussion ends. If a downloadable result is wanted, select an available output instead of **없음**. Locked personas, features, or output formats need the corresponding entitlement; choose an available alternative when the user does not want to purchase one.

### Small example

- **질문:** “For a small team this week, should we improve onboarding documentation or build a new integration first?”
- **목적:** 결정하기 (Make a decision).
- **목표:** “Choose one priority and explain its tradeoffs, remaining disagreements, and the first three actions.”
- **자료:** A short description of the team's available time and the two options, excluding private customer information.
- **제약조건** under the relevant detailed result settings: The user's actual deadline or budget, if supplied.
- **공개 범위:** 비공개 unless the user requests publication.
- **산출물:** An available conclusion/summary/report format that matches the purpose.

This example prepares a meeting; it is not an instruction to run it or a claim that it has been run.

## 3. Check before starting

Read **예상 최대 청구** and **예상 시간** at the bottom. Subscription users may also see the estimated share of monthly usage. These are estimates/limits, not the actual final charge. Changing settings changes the estimate.

Confirm the selected question, materials, participants, visibility, output, and the user's willingness to spend the displayed usage/credits before **회의 시작**. Do not turn public visibility on to obtain a free meeting. The current public pricing page says web meetings are charged; conditional Android free meetings do not provide a free web or MCP test.

The site checks the input and may show warnings that the user must acknowledge. If safety blocks the request, explain the returned reason instead of bypassing it. A disabled start button can reflect a missing question/participants, an unavailable persona/output, or unacknowledged warnings. For low balance, explain the displayed choices and the risk of stopping early; do not buy credits automatically.

## 4. Follow a running meeting

After starting, the server runs the meeting. Closing a tab is not a stop command and does not imply the billable work stopped. Return through **내 회의** to the same meeting instead of creating a duplicate.

Use **대화 로그** to read participant remarks and the facilitator's round summaries. If a feedback card asks for direction, choose or write the intended direction; do not confuse it with a new meeting. A search card can offer a billed search, continuing without search, or ending on available material. Additional spending needs the user's decision.

Distinguish server pause/continue controls from **화면 재생 일시정지** and playback speed: changing the display is not necessarily stopping the meeting. **회의 종료** can offer ending with existing records or generating an output before ending; output generation may cost more. Read the current dialog before acting. An early stop or partial result is not full completion.

## 5. Open results

1. Open **내 회의** from the top navigation. Search/filter by meeting and state. For completed meetings, use **결과 보기**; blocked/cancelled/expired entries can offer **로그 보기**, while active entries offer entry to the meeting. API-created meetings also appear here and can be filtered by API-key name when that control is available.
2. In the meeting room, use the available tabs:
   - **대화 로그:** the original remarks and supporting links.
   - **회의록:** facilitator summaries, when available.
   - **산출물:** generated result, when present. A link such as **산출물 보기 →** can jump there.
3. Read the conclusion together with evidence, assumptions, uncertainty, dissent, unresolved risks, and next verification steps. Where offered, **로그에서 보기 ↥** links back to the supporting remark. A consensus or adoption score is not proof of factual correctness.
4. Check the end reason, actual usage, and whether the result is partial. No output or an unavailable tab does not necessarily mean the record is lost: the meeting may still be running, have no selected output, or have ended before output generation.

On public meetings, the top state can refer to playback even when the underlying meeting has ended; check its end reason and available record instead of interpreting “재생 중” as a new server execution.

## 6. Download or continue

For the user's own meeting with an output, open **산출물 → 내려받기 ▾** and select an available format. The guide lists Markdown, text, Word, PDF, HTML, and judgment JSON, with PowerPoint, spreadsheet/CSV, or calendar export only for suitable output types. Availability depends on that meeting and the viewer's rights; do not promise every format on every public meeting. A download click is not proof that a file saved: verify the returned file through the host's download mechanism when assisting.

**조건을 바꿔 다시 돌리기**, **이어가기**, and **이 문서로 새 회의** create a new meeting. They are not free result retrieval or resumption of the same judgment, so review the new settings and cost before starting.

Keep publication separate from reading or downloading. **공개하기**, a private share-link issue action, and sharing a file can expose content to other people. A private share link is still readable by whoever holds the address. Do not publish, issue a share link, or delete a meeting merely to demonstrate the workflow.

For changed UI, use the current [user guide](https://hiai-meeting.com/getting-started), [new-meeting setup](https://hiai-meeting.com/guide), [pricing](https://hiai-meeting.com/pricing), and [FAQ](https://hiai-meeting.com/faq). Explain what was observed and what still needs the user's login, payment, or a real authorized meeting.
