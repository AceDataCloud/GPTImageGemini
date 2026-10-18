---
name: gpt-image-create
description: Create or edit GPT Image image through Ace Data Cloud in Gemini CLI, or retrieve an original task result. Use the installed GPT Image MCP tools and current service schema, not model-provider configuration.
---

# GPT Image with Ace Data Cloud

## Choose only the requested service operation

Use MCP server `gpt-image-by-ace-data-cloud` and the actual prefixed tool names discovered by Gemini CLI. The package allowlist is: `openai_list_image_models`, `openai_generate_image`, `openai_edit_image`, `openai_get_task`.

Call only `openai_list_image_models` for a reference-only first check. It returns documentation, not a generation or balance result.

This extension is only for GPT Image models. openai_list_image_models may also list DALL-E or Nano Banana; report/select only supported gpt-image-* IDs. Always set model explicitly to a current supported GPT Image ID before generation/edit, because the underlying server default may be DALL-E. Image edit takes image as one URL or a real ordered array (maximum per live schema), not image_urls and not a comma-separated/JSON-stringified array. Task query uses id, not task_id; omit trace_id unless the user supplied the original trace ID, since trace_id takes precedence.

## Authentication and paid actions

Token setup belongs in Gemini CLI native extension settings, not the conversation. Direct setup questions to `gemini extensions config gpt-image-by-ace-data-cloud` and the repository's illustrated README. Do not read credential stores, print tokens, bypass Allowed APIs or infer balance from a reference tool result.

Inspect current tool schemas and current price before a paid operation. Ask only for missing task-relevant choices; preserve the user's requested model, input and budget. Do not silently add fallback models or chargeable operations. For user-supplied reference media, confirm the user is authorized to use it. Main-model inference and Ace image tools have separate costs.

## Submit once, retrieve the original task

1. Submit the chosen authorized generation/edit once and retain its task ID and any original trace ID.
2. Query `openai_get_task` with **`id`**, using the original ID. Never use a generation tool for polling. Honor the server's pacing and state fields.
3. Keep pending/processing distinct from terminal complete/failed. If a bounded wait or network call times out, retain the same ID for a later lookup; do not resubmit automatically.
4. On terminal success, show the actual image URLs and metadata. On failure, preserve the returned error/ID. A task ID or successful CLI turn is not a completed artifact or proof of unique billing.
5. When the user supplies an old task ID, only retrieve that task. If no ID is supplied, ask for it; do not create or invent one.

401: check the native password setting and Key expiry. 403: inspect actual permission/moderation details. For balance issues, review current account information. For 429/5xx/timeouts, keep original IDs and avoid a second paid submission. Never include the Token in error output.
