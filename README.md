# GPT Image by Ace Data Cloud for Gemini CLI

Use GPT Image image generation/editing and retrieve the original task from Gemini CLI. **Ace Data Cloud** provides this independent integration; it is not an official GPT Image or Google product and does not add a main-model provider.

[简体中文](readme/README_zh_Hans.md) · [Current price](https://platform.acedata.cloud/models?utm_source=gemini-cli&utm_medium=referral&utm_campaign=evergreen&utm_content=gptimagegemini_pricing)

## 1. Install through Gemini CLI extensions

Install [Google Gemini CLI](https://geminicli.com/docs/get-started/installation/) and complete its current main-model authentication. Tested version: **0.64.0**. Google directs some unpaid/Google One users to [Antigravity CLI](https://github.com/google-gemini/gemini-cli#readme); this package does not claim Antigravity compatibility.

This is an independent native extension, with manifest ID **gpt-image-by-ace-data-cloud** and publisher **AceDataCloud/GPTImageGemini**. The official gallery crawls public root manifests with `gemini-cli-extension` topics; **this review package is not yet an indexed official card**. Main remains initialization until review/authorized merge. Install the review branch explicitly:

```bash
gemini extensions install https://github.com/AceDataCloud/GPTImageGemini --ref codex/gpt-image-native-extension
```

Read the native consent prompt. The extension adds only GPT Image MCP tools, the `gpt-image-create` Skill and `/gpt-image-check`, `/gpt-image-task`. No hooks, local server install or automatic media generation.

After a reviewed stable merge, the ordinary command will be:

```bash
gemini extensions install https://github.com/AceDataCloud/GPTImageGemini
```

## 2. Register/sign in and get a service Token

1. [Register or sign in to Ace](https://platform.acedata.cloud?utm_source=gemini-cli&utm_medium=referral&utm_campaign=evergreen&utm_content=gptimagegemini_register).
2. Open [Applications](https://platform.acedata.cloud/console/applications?utm_source=gemini-cli&utm_medium=referral&utm_campaign=evergreen&utm_content=gptimagegemini_api_key). Initialize **General application** if missing. Check GPT Image entitlement and current balance. A service application's Key is limited to that service; general keys remain subject to account/API restrictions.
3. Copy **API KEY** from the card, or **Manage Keys → Create** for a dedicated Key named `Gemini CLI GPT Image`.

![Copy an existing masked Ace Key or manage keys](_assets/tutorial/get-api-key-en.png)

4. Review expiration, usage limits and Allowed APIs. This workflow uses `/openai/images/generations`, `/openai/images/edits`, `/openai/tasks`. Allow only needed routes. Review [current pricing](https://platform.acedata.cloud/models?utm_source=gemini-cli&utm_medium=referral&utm_campaign=evergreen&utm_content=gptimagegemini_before_run) before a generation/edit.

![Create an optional dedicated Key](_assets/tutorial/create-api-key-en.png)

These are authentic masked shared Ace screens reused from SunoDify; the pictured `Dify tutorial` name is illustrative—use `Gemini CLI GPT Image` here. Retrieved/reviewed 2026-10-18; original capture date unspecified. [Exact sources and limits](_assets/tutorial/sources.json).

Paste only the raw Token, without `Bearer `, quotes or masked characters. A `platform-...` account-management token is not the service Key. Trial balance and permissions are whatever your account currently displays.

## 3. Use the native password setting

During install, paste the Key at **Ace Data Cloud GPT Image API Token**, not in chat. `sensitive: true` uses Gemini CLI's native secret storage (OS keychain if available, secure fallback otherwise). To change it:

```bash
gemini extensions config gpt-image-by-ace-data-cloud "Ace Data Cloud GPT Image API Token"
```

Extension-specific variable: `ACEDATACLOUD_GPT_IMAGE_TOKEN`. No manual MCP URL/JSON configuration is required. Restart Gemini CLI and check:

```bash
gemini extensions list
gemini mcp list
```

Expect `gpt-image-by-ace-data-cloud` enabled/connected. Respect administrator extension/MCP policy. Same-name MCP entries in settings take precedence.

![Official Gemini terminal reference, edited preview](_assets/tutorial/gemini-cli-reference.png)

**Official screenshot edit, not this extension's execution.** Edited 2026-10-17; source asset updated 2025-12-01, capture date/version unspecified. Bottom input receives requests, replies/tool results appear above. WriteFile, Hello World and “2 MCP servers” belong to the Google example; this does not show GPT Image's native password prompt or prove installation. [Sources](_assets/tutorial/sources.json), [Apache notice](THIRD_PARTY_NOTICES.md), [actual validation boundaries](VALIDATION.md).

## 4. First use without creating media

Run `/gpt-image-check` inside Gemini CLI. It calls `openai_list_image_models` for reference information, not media generation, balance or billing. Your configured main model can still charge for inference.

## 5. Authorized operation and same-task retrieval

This extension is only for GPT Image models. openai_list_image_models may also list DALL-E or Nano Banana; report/select only supported gpt-image-* IDs. Always set model explicitly to a current supported GPT Image ID before generation/edit, because the underlying server default may be DALL-E. Image edit takes image as one URL or a real ordered array (maximum per live schema), not image_urls and not a comma-separated/JSON-stringified array. Task query uses id, not task_id; omit trace_id unless the user supplied the original trace ID, since trace_id takes precedence.

Before the requested operation, inspect its current model/schema/price and confirm the user's budget. Submit once and preserve the returned original task ID. Then query **`openai_get_task(id=ORIGINAL_TASK_ID)`** until terminal success or failure; pending/processing is not completed media. A timeout or 5xx does not authorize regeneration.

For an already-submitted task:

```text
/gpt-image-task YOUR_ORIGINAL_TASK_ID
```

This command retrieves that ID only. No generation/edit or fabricated ID is needed. Show actual returned image URLs and terminal state; verify media and the matching consumption record separately. A connected server, task ID or green CLI turn does not prove a completed image/video, unique bill or revenue.

## Exposed tools

`openai_list_image_models`, `openai_generate_image`, `openai_edit_image`, `openai_get_task`.

Other services/tools from the underlying server are excluded. [Maintained server source](https://github.com/AceDataCloud/OpenAIMCP) owns the actual API contract; this repository does not duplicate it.

## Troubleshooting and charges

| Issue | Action |
|---|---|
| 401 / missing Key | Native config command; check raw service Key, expiration and service access. |
| 403 | Read actual permission/moderation error; check Allowed APIs. |
| No password prompt | Ensure extension settings are enabled; use config. Never paste Key into chat. |
| No tools | Restart, check extensions/MCP list and admin policy. Do not bypass restrictions. |
| Pending / timeout | Query original ID again; no automatic second paid submission. |
| Invalid input/model | Inspect the selected tool schema; do not copy another service's fields. |
| 429 / 5xx / failed | Preserve task/trace ID and inspect original history before deciding on any fresh operation. |

Ace media tools and the configured Gemini main model have separate prices. [Applications and usage](https://platform.acedata.cloud/console/applications?utm_source=gemini-cli&utm_medium=referral&utm_campaign=evergreen&utm_content=gptimagegemini_usage) report Credits; USD uses the current package price/amount. This repository claims no acquired registrations, paying users or revenue.

## Update/remove and publication gate

```bash
gemini extensions update gpt-image-by-ace-data-cloud
gemini extensions uninstall gpt-image-by-ace-data-cloud
```

[Validation](VALIDATION.md) · [Official gallery handoff](docs/GALLERY_SUBMISSION.md) · [Native extension mechanism](https://geminicli.com/docs/extensions/releasing/)

Code: MIT. Official screenshot derivative: Apache-2.0 with included license/notices. Service and Google/Gemini marks belong to their owners; no endorsement is implied.
