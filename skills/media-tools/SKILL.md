---
name: media-tools
description: Compresses, converts, resizes, and batch-processes local images and videos with ImageMagick and FFmpeg, including target-size reduction and upload compatibility. Use whenever the user wants to make an image or video smaller, convert its format, fit a size limit, or prepare it for X/Twitter, Instagram, WhatsApp, email, or the web, even if they do not mention this skill by name. Not for editing, OCR, subtitles, PDF, or audio-only tasks.
---

# Media Tools

Turn the user's goal into a finished local image or video. Keep the interaction simple: choose technical settings yourself and discuss only decisions that materially change the result.

## Scope

Handle image and video compression, conversion, resizing, compatibility, target file size, and directory batches. Do not handle PDF, Office, CAD, standalone audio, OCR, subtitles, background removal, watermarking, filters, joining, or substantial editing.

## Workflow

1. Identify the input files and intended result. A named platform is a goal, not a request for technical settings.
2. Ask at most one short question, only to locate the input or resolve a choice that changes the visible result, such as Instagram Feed versus Reels or whether cropping is acceptable. Otherwise proceed with conservative defaults.
3. Check for local tools before processing:
   - Video: `ffmpeg` and `ffprobe`.
   - Images: prefer ImageMagick 7 `magick`. On systems using ImageMagick 6, verify that `convert -version` identifies ImageMagick and use `convert` with `identify`; never use the unrelated Windows `convert.exe`.
4. If a tool is missing, stop and provide one installation command appropriate for the detected operating system and package manager. Do not install it automatically.
5. Inspect the source locally before choosing settings. Use `ffprobe` for video and `magick identify` or the verified ImageMagick `identify` for images.
6. Create a clearly named output beside the source or in a new output directory. Never overwrite, rename, or delete the source; even a replacement request produces a new file.
7. Process entirely with local commands. Do not upload media or fall back to a cloud conversion service.
8. Verify the output locally before reporting success.

## Processing Rules

- Resolve inputs to absolute paths before invoking a tool. Pass paths as arguments without `eval` or command-string interpolation, and prevent leading-hyphen filenames from being parsed as options.
- Run the installed media tools directly. Do not create helper scripts or additional project files for the task.
- Prefer broadly compatible outputs when the user names a publishing destination: JPEG or PNG for images; MP4 with H.264 video, AAC audio, `yuv420p`, even dimensions, and `+faststart` for video.
- Preserve aspect ratio. Do not crop, stretch, rotate, or remove audio unless the user requests it or approves the visible change.
- Preserve resolution first. Reduce quality or bitrate before reducing dimensions; lower resolution only when necessary to satisfy the goal.
- For a strict video size limit, reserve about 3% below the limit, calculate bitrate from duration, and use two-pass encoding when available. Do not use `-fs` as the primary method because it may truncate the output.
- For a strict image size limit, search quality progressively and reduce dimensions only if quality adjustment alone cannot meet the limit.
- For batches, write to a separate output directory, keep filenames recognizable, process only matching media files, and report individual failures without discarding successful outputs.
- For current platform-specific limits, consult the platform's official public documentation when necessary. This lookup may use the network, but the media file must remain local. Do not claim compliance with a rule that was not verified.

## Verification

Confirm that the output exists, is non-empty, opens with the relevant local probe, and matches the requested format, dimensions, and size limit. For video, verify duration and streams with `ffprobe`; when corruption is plausible, run a local decode check with FFmpeg. A successful command exit alone is not sufficient.

## Response

Report only what helps the user use the result:

```text
Completed: <output path>
Size: <before> -> <after>
Result: <whether the requested size or destination requirement was met>
```

If processing fails, explain the cause in ordinary language and give the single most useful next action. Show codecs, bitrates, quality scores, and commands only when the user asks or they are necessary to explain a failure.
