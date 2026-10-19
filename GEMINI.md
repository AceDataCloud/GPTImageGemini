# GPT Image by Ace Data Cloud

This independent GPT Image extension loads service-specific tools and a `gpt-image-create` workflow skill. It is not endorsed by the service owner or Google and does not change Gemini CLI's main model/login.

Call only `openai_list_image_models` for a reference-only first check. It returns documentation, not a generation or balance result.

Use the native password setting `Ace Data Cloud GPT Image API Token` for credentials; never ask for a Key in chat or expose it. For the requested paid operation, check current price, model and parameters and stay within the user's authorized budget. Submit once, retain the task ID, query the same ID with `openai_get_task` using parameter `id`, and do not regenerate to poll or retry. Task-query permission does not grant generation permission. Return only actual terminal media URLs; pending, connection and green CLI status are not final output or unique-billing evidence.

This extension is only for GPT Image models. openai_list_image_models may also list DALL-E or Nano Banana; report/select only supported gpt-image-* IDs. Always set model explicitly to a current supported GPT Image ID before generation/edit, because the underlying server default may be DALL-E. Image edit takes image as one URL or a real ordered array (maximum per live schema), not image_urls and not a comma-separated/JSON-stringified array. Task query uses id, not task_id; omit trace_id unless the user supplied the original trace ID, since trace_id takes precedence.
