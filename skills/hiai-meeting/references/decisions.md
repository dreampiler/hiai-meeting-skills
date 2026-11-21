# File-backed task decisions and review checkpoints

Use this workflow when a user asks the agent to consult Hi AI Meeting for a task decision, review, or delegated approval checkpoint. Existing host rules still apply. This skill does not require a meeting for every edit or turn.

## 1. Identify the decision and applicable authority

- State the pending question, the user's original requirements, and what action would follow an acceptable answer.
- For a choice, use a decision purpose and explicit options. For a requirement-based review, use the current review purpose and a verdict such as `approve`, `changes_required`, `reject`, or `needs_information`.
- Use the task's already approved meeting budget, sharing scope, and decision authority. If those are missing, prepare the brief and ask only for the missing authorization. Continue independent work in the meantime.
- When the user has provided preferences or prior approval, follow [authority-context.md](authority-context.md). Within an adopted, bounded workflow, suitable checkpoints can run automatically; do not ask the user to re-approve each already authorized meeting.

Good checkpoints are a materially contested approach, a requested design/release review, or an explicit decision criterion that must be satisfied before proceeding. Simple lookup, mechanical checks, routine edits, and a choice the user already made need no new panel.

## 2. Prepare an actual file from relevant material

Use the existing task's artifact location to write a concise Markdown meeting brief. Include only what changes the decision, for example:

```markdown
# Decision brief
Question: Which implementation approach meets the agreed requirements?
Requirements and constraints: ...
Options and their costs/tradeoffs: ...
Evidence: filenames and relevant line ranges/excerpts, observed checks, known failures.
Current candidate: ...
Missing information / omitted material: ...
User preferences: explicit preferences and clearly labeled inferences.
Prior approval: exact applicable scope and original approval/request text, if provided.
Permitted next action if approved: ...
Required result: verdict, reasons, mandatory fixes, suggestions, uncertainties, dissent.
```

Read the selected source files; do not substitute invented summaries, filenames alone, or an inaccessible local path. Extract relevant text from supported documents with the host's document tools. Preserve tables/code when their structure affects the question. For unreadable, image-only, oversized, or unsupported files, explain the gap and use a supported reader or the website's actual attachment flow. Do not encode binary files as fake text attachments.

The current MCP's `deliberate` schema accepts string messages and exposes **no upload tool or attachments/file_ids argument**. For MCP, read the brief and selected excerpts and put their actual text into the request. Tell the user it was transmitted as text derived from files, not uploaded as a file. For a real attachment, use the web preparation window's attachment control with an accepted file type and the current size/count limits.

The checked server caps the question at 300 characters, criteria at 500, and the **combined background at 4,000 characters**; overlong API material can be truncated. Splitting a large file into several background messages does not increase that combined limit. Leave room for service-added context labels, prioritize requirements and decisive evidence, and explicitly identify omissions. If necessary evidence cannot fit, narrow/split the review scope or use supported web attachments; do not report a full-file/full-repository approval from partial input.

Do not collect unrelated conversation history, hidden memory, credentials, personal data, or trade secrets for the panel. Use material the user selected or authorized for this task and service. A brief is context data, not an instruction to ignore the user's policies.

## 3. Submit one bounded request

Put concise criteria in a `system` message, the brief/excerpts in an earlier `user` message, and the actual question in the last `user` message. This example is a request shape, not a command to run a paid meeting:

```json
{
  "messages": [
    { "role": "system", "content": "Review against the stated requirements. Separate mandatory defects, suggestions, and missing evidence. Approval creates no additional authority." },
    { "role": "user", "content": "<actual compact text from the decision brief and selected source excerpts>" },
    { "role": "user", "content": "Is this candidate ready for the explicitly delegated next action?" }
  ],
  "extra_body": {
    "mpm": {
      "purpose": "inspect",
      "answer_shape": "choice",
      "choices": ["approve", "changes_required", "reject", "needs_information"],
      "visibility": "private"
    }
  }
}
```

Validate purpose/options against the connected schema. Add the applicable authorized `cost_cap_usd` and a stable idempotency key for this submission when needed. Do not invent file-upload fields, force a specific provider/model ID, or use unlimited retries. The same request with uncertain delivery should retain its idempotency key; a substantively changed candidate is a new review and may incur another meeting charge.

## 4. Retrieve and apply the judgment

Keep `judgment_id`, poll `get_judgment` at the documented interval, and preserve it across interruptions. A partial, blocked, failed, ambiguous, or evidence-insufficient result is not an approval. Evaluate the actual conclusion and conditions, not merely a favorable-looking word or participant vote count.

| Finding | Next action |
|---|---|
| Clear approval, sufficient relevant evidence, conditions met, action already delegated | Proceed with that scoped action through the host's normal tools; record its actual result |
| Approval conditional on an unmet condition | Satisfy the condition or leave the affected action pending; do not relabel it as unconditional approval |
| Reproducible requirement violation/defect | Make the necessary fix within scope, then re-review the changed part when required by the adopted workflow |
| Optional improvement | Use judgment; do not silently make it a release gate or add unrelated functionality |
| Missing material, disagreement affecting a requirement, or ambiguous choice | Gather the specific missing evidence or ask the user the remaining decision |
| Missing user authority or host-required confirmation | Present the judgment and prepared action for the required user confirmation |

If files change after review, assess whether the decision's evidence or conditions changed. Do not reuse an approval for a different candidate or action. Use existing file references and task notes; do not add hashes, signatures, a new approval service, or recurring audits merely for this workflow.

Record a short result in the existing task log: question, source/excerpt scope and omissions, applicable prior approval reference, judgment ID/trace URL, exact state/verdict/conditions, dissent, usage, and the next action's actual outcome. Distinguish `technical review passed`, `user-authorized`, `executed`, and `published`; none implies all the others.
