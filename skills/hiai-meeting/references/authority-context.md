# User preferences and explicit prior approval

The panel can help decide **whether an already authorized action meets its conditions**. It cannot generate new user authority. Follow the user's adopted delegation and the host's actual execution/confirmation requirements.

## Prepare the context from selected sources

Use the user's supplied preference/approval file, current task instructions, or explicitly selected task records. Add the relevant sections to the existing meeting brief; a separate persistent profile database is unnecessary. Do not mine Claude memory or unrelated chat history, infer approval from silence, or persist a behavioral profile from conversation content.

Keep these two parts separate:

| Part | Include | How to use it |
|---|---|---|
| Preferences | Explicit priorities and selected past choices, their context, and any uncertain inference | Weight/recommend options; never treat a pattern of past choices as authorization |
| Prior approval | The user's actual grant, its target, conditions, limits, source, and any withdrawal | Define the executor's permitted action only within that exact scope |

A useful prior-approval section identifies the approving user, permitted action, target/resource/recipient, spend currency and per-action/cumulative limits if applicable, duration/frequency, preconditions, prohibited actions, and revocation/expiry. Include only fields that apply to that action; do not fabricate missing values or create new gates for unrelated work.

For relayed approval, preserve the complete original request and the complete user's approval text, with their conversation/document source and timestamp when available. Do not use a summary or excerpt as a substitute for the original grant. A self-contained standing instruction should be preserved as such; do not invent a preceding request. If the host's relay rule requires an original request that is unavailable, the panel may advise, but it must not certify the missing authority.

The panel only sees submitted text. A local filename, URL, or reference alone does not give it the source. The current MCP background limit also applies to approval quotes. If the full authority material cannot fit, do not silently shorten it and ask the panel to certify authorization. Keep the full original with the executor, limit the panel to evaluating factual/technical conditions, or obtain an explicit compact delegation from the user through the normal confirmation flow.

## Example of a delegation to propose, not assume

```markdown
Preference: Prefer reversible changes and the lowest total cost that meets the requirements.
Approved action: Publish the reviewed documentation-only patch to the named repository.
Target: <exact repository, branch/publication target, and approved file scope>.
Limits: No application behavior changes, secrets, paid purchases, or permission changes.
Condition: Required checks pass and the meeting finds no remaining requirement violation.
Validity: This task only; a later user correction or withdrawal takes precedence.
Original request and user approval: <full original text and source, not an invented grant>.
```

This template is **not** an approved policy. The user must actually adopt the applicable grant. A financial delegation would additionally need the actual payee, item/purpose, currency, amount limits, and recurring-payment conditions; “usually chooses cheap options” is not enough.

## What a meeting-assisted approval can do

1. Read the supplied original grant and distinguish it from preferences.
2. Check whether the proposed action is within the named scope and whether its required factual/technical conditions are met.
3. Return a scoped verdict with reasons, unmet conditions, uncertainty, and dissent. A useful verdict states the action and target, not just “approved.”
4. If the result is clear and the host permits execution under that prior approval, the executor proceeds without asking the same question again. Record the actual execution result separately.

For an ordinary purchase, this can mean selecting an eligible option within a user's specific approved merchant/item/limit; it does not mean a model can invent permission to spend. For publication, use the approved content and destination; approval for a private review is not approval to post it publicly. For access changes, remain within the exact approved principals/resources and the platform's confirmation rules.

## Boundaries the panel cannot replace

- Fresh user confirmation or direct input explicitly required by the host/platform, including legal-agreement acceptance, security-sensitive permission expansion, credential changes, or the host's action-time payment rules.
- Missing or ambiguous approval, a different target/recipient, a new recurring cost, a higher limit, expired/withdrawn authority, or an explicit user veto.
- Authentication, payment completion, identity checks, or a real execution receipt. A favorable judgment does not prove these happened.

When such a boundary remains, report the panel's recommendation and prepare the concrete action; request only the missing decision or direct user step. Continue independent authorized work. Do not describe the AI panel as the user, sign on the user's behalf, alter approval source records, or claim an actual purchase/publication/permission change from the meeting verdict alone.

The native MCP currently provides judgments only. Subsequent actions use the host's own authorized tools, not a fictitious MCP `pay`, `grant_access`, or `publish` tool. This is a task-scoped delegation workflow, not permission to autonomously change accounts or establish an always-on approval system.
