---
name: magic-hour
description: Create and edit images and videos with Magic Hour. Use when the user wants to generate an image, turn an image into a video, or edit media (face swap, lip sync, talking photo, background removal, upscaling).
---

# Magic Hour

Use the Magic Hour MCP tools to create and edit images and video.

## How to work
- Creation tools are asynchronous. After starting a project, call the matching `wait_for_*_project` tool until it finishes, then show the result. Videos can take a minute or more.
- Upload local media before passing its file path to a tool. Keep signed download URLs exactly as returned.
- Leave optional `resolution` and `model` unset unless the user asks for them.
- For video, prefer AI Image Editor followed by Image-to-Video so characters stay consistent. Use Text-to-Video only when consistency doesn't matter.
- Real generations spend Magic Hour credits. Say so before starting large or repeated jobs.

## Use responsibly
Use face, head and body swap, lip sync and similar tools only with the user's own likeness or content they are authorized to use. Do not use them for impersonation, deception, sexual content, or content involving minors.

## Try
- "Create a cinematic image of a crowded Thai night market with a neon Pad Thai sign."
- "Turn that image into a 5-second video with a slow camera push-in."
- "Add stylish sunglasses to this photo and keep the result realistic."
