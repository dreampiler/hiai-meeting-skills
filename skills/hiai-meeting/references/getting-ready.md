# Signup, credits, and MCP connection readiness

Verified against the live Hi AI Meeting signup dialog, Settings → API keys, Store, and public developer/pricing guides on 2026-11-21. Match the user's displayed language and current screen. Prices, product availability, and free-meeting switches can change; read the current site instead of quoting a fixed price from this skill.

## 1. Establish what the user needs

| User's goal | Preparation |
|---|---|
| Read public meetings | No signup, credits, or API key required |
| Create a meeting on the website | Sign in; check subscription usage/credits and the meeting estimate |
| Use MCP | Sign in and connect with supported OAuth or a personal API key. Check usage/credits before starting a meeting. |
| Use the OpenAI-compatible API | Sign in, issue a personal API key, and check usage/credits before starting a meeting. |
| Retrieve an existing result | Use the same account and existing meeting/judgment ID; do not start another meeting |

Ask only about the first missing step. A Hi AI Meeting account and its credits are separate from a ChatGPT, Claude, Gemini, or coding-agent subscription. The personal key here is a **Hi AI Meeting key**, not an OpenAI/Anthropic/Google provider key.

## 2. Sign up or log in

Open [Hi AI Meeting](https://hiai-meeting.com) and select **로그인** (Log in) in the top bar. The dialog contains **로그인** and **가입** tabs; login, signup, and password recovery happen in that dialog.

### New account

1. Select **가입**. Review the required terms and privacy consent separately; marketing consent is optional. The user makes those choices themselves.
2. Choose a signup method offered on the current screen:
   - **Google 계정으로 가입하기** or **Apple 계정으로 가입하기**: complete the provider's account selection and authorization. Complete a nickname if requested. Do not tell an existing user to create a second account just to connect a provider.
   - **Email**: enter email, a public nickname, password, and password confirmation, then select **가입 시작하기**. Follow the displayed password requirements. Enter the email verification code in the site's code field to finish signup; check spam or use the resend action if needed. Do not send the code to the assistant.
3. Check that the top bar shows the signed-in account menu. A submitted form alone is not proof of signup or login success.

If the site shows an invitation-only signup path, follow that displayed flow with a valid invitation instead of promising open signup. Do not bypass it. Do not invent a successful account creation, email delivery, or provider authorization.

### Existing account

Use the same method as the existing account: Google, Apple, or the email/password form. Use **비밀번호를 잊으셨나요?** under the login form for email password recovery. Provider account linking is managed in the site's account settings; signing up again may create a different account with a different balance and meetings. Have the user enter passwords, codes, and provider approvals directly on the site.

The top-right **화면·계정 설정** menu opens **설정**. Settings has account, display, sound, notifications, subscription management, and API-key sections. Reading or changing display preferences is not required to start using meetings.

## 3. Prepare usage or credits

1. Open **상점** / the top-bar credit balance, which leads to [Store](https://hiai-meeting.com/billing). Read **내 크레딧** and **이번 달 이용량**. Subscription usage and the credit balance are different counters.
2. If existing usage or credits are sufficient, continue without buying anything. Otherwise explain the alternatives: **크레딧 충전** for a credit pack, or **구독** for a subscription allowance and its included benefits. A subscription is not universally required if credits are sufficient.
3. For a credit pack, choose the displayed currency and pack, review the selected product and total, add it using the current Store controls, and review checkout. The user completes any payment through the supported checkout. For a subscription, also check the billing period and renewal conditions. Do not select a recurring plan merely to test a connection.
4. After a purchase, verify the successful purchase record and updated balance/allowance in Store or **최근 결제·구매** / [purchase history](https://hiai-meeting.com/billing/history). Pending checkout is not a successful payment; do not pay again just because the balance display has not refreshed.

The current pricing guide says web meetings consume usage/credits; conditional free meetings are available in the Android app, not as a free API/MCP trial. API/MCP meeting calls are billed and can be refused before starting when the balance is insufficient. Do not promise signup bonus credits, a free first API call, or a fixed currency-to-credit conversion. Check [current pricing](https://hiai-meeting.com/pricing) for the current rules. Connection discovery and result retrieval are different from starting a new meeting.

## 4. Issue a personal API key when needed

Web-only use does not require this step.

1. From the signed-in account menu, open **설정 → API 키**, or open [API-key settings](https://hiai-meeting.com/settings?tab=api-keys).
2. In **키 이름**, enter a recognizable label for that client, such as `Codex personal`; then select **키 발급**. The user issues and handles the key themselves unless they have expressly requested authorized assistance through the host's secure setup flow.
3. The complete key appears **once**. Copy it into the intended client's protected credential configuration before closing the issued-key panel. The list later displays only a prefix; a prefix is not a usable key. A lost key must be replaced, not recovered from the list.
4. Treat **폐기** as revocation, not a copy or disconnect button. Revoking a key stops clients using that key and is not a normal connection-test step. Revoke/replace a compromised or unused key through the site's explicit management flow when authorized.

The panel includes **도구별 설정** with client-specific examples and **이 키로 만든 회의 보기** for meetings created through a key. Use a name to distinguish clients; do not copy another person's account key. Store neither key values nor screenshots of the one-time key display in the skill or repository.

## 5. Connect and check without starting a paid meeting

1. Install this skill if needed, then configure an **independent MCP connection**. Skill installation alone creates no authenticated connection. Use [calling.md](calling.md) for client settings.
2. Set the remote **Streamable HTTP** MCP URL to `https://hiai-meeting.com/v1/mcp`. For OAuth, let the client open Hi AI Meeting and have the user review and allow the requested access. For a key-based client, configure `Authorization: Bearer <personal Hi AI Meeting key>` through its protected credential mechanism. The OpenAI-compatible API uses the separate base URL `https://hiai-meeting.com/v1` and a personal key.
3. Reload/reconnect using the client's MCP manager when required. Have the manager initialize the server and list its tools. Check that **deliberate** and **get_judgment** are advertised, including any host-added prefix. This tests connectivity and tool discovery; do **not** call deliberate as a connection test.
4. An optional authenticated `GET /v1/models` checks the API-side credentials and available preset list without creating a meeting, but is not a substitute for verifying MCP tool discovery. Keep Authorization out of displayed commands, shell history, and diagnostic logs.
5. Only after an actual meeting is requested and its cost/material are authorized should deliberate be called. Preserve its ID and follow the normal retrieval flow in the main skill.

OAuth access can be revoked in [MCP connection management](https://hiai-meeting.com/api/mcp/oauth/connections). For each client, check that its connection settings support the chosen method. Public directory approval and custom connections have separate setup steps.

## Common obstacles

| Symptom | Useful next step |
|---|---|
| Sign-in is shown again | Check account, session, and the original login method |
| API-key section is unavailable | Distinguish sign-in/permission failure from a feature temporarily unavailable; do not invent a key |
| HTTP 401 | For OAuth, reconnect and check whether access expired or was revoked. For API keys, check the Bearer configuration and key status locally. |
| HTTP 403 with insufficient scope | Check the required OAuth scope. Meeting creation requires separate user consent for `mcp:meeting:create`. |
| Missing MCP tools | Check URL/transport, connection enabled state, reconnection, and host support; skill installation is insufficient |
| Balance/entitlement error | Check Store usage, credits, requested features, and the returned error; successful authentication does not imply permission or balance for every preset |
| Failed/uncertain paid request | Keep the original judgment ID or idempotency key; retrieve its state instead of blindly creating another meeting |

Tell the user exactly what is verified: signed in, funding visible, key configured, tools discovered, or a specific meeting completed. Do not merge these into a single unsupported “everything works” claim.
