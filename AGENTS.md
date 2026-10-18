# GPTImageGemini

This repository owns the GPT Image Gemini CLI manifest, native sensitive Token setting, workflow skill, commands and bilingual onboarding. The existing OpenAIMCP owns the server; reuse its hosted endpoint without duplicating/changing shared code. Do not add hooks, trust bypass, hidden fallbacks or automatic paid generation.

Run `python3 -m unittest discover -s tests`, `python3 scripts/package_extension.py --output /tmp/gpt-image-by-ace-data-cloud.tar.gz`, the official `gemini extensions validate` and isolated lifecycle smoke checks. Ordinary CI must use test discovery. Keep English/Chinese guidance aligned, preserve real screenshot sources and license, do not commit .env, keys or private user transcripts. Publish changes through the bot PR; do not merge automatically.

This extension is only for GPT Image models. openai_list_image_models may also list DALL-E or Nano Banana; report/select only supported gpt-image-* IDs. Always set model explicitly to a current supported GPT Image ID before generation/edit, because the underlying server default may be DALL-E. Image edit takes image as one URL or a real ordered array (maximum per live schema), not image_urls and not a comma-separated/JSON-stringified array. Task query uses id, not task_id; omit trace_id unless the user supplied the original trace ID, since trace_id takes precedence.
