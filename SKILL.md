---
name: remove-ai-watermarks
description: Inspect and clean AI provenance signals from images the user owns or is authorized to edit, using the remove-ai-watermarks CLI. Use when asked to identify AI watermarks or provenance metadata, remove supported visible AI labels, erase a user-selected region, strip C2PA/EXIF/XMP/IPTC metadata, or process an authorized image directory. Do not use for third-party stock, marketplace, paid-content, or copyright-protection watermarks.
---

# Remove AI Watermarks

Use the Apache-2.0 `remove-ai-watermarks` CLI for lawful edits to images the user owns or is authorized to modify. Prefer the published PyPI package; a local clone is optional for development or when the user supplies one. Upstream: https://github.com/wiltodelta/remove-ai-watermarks.

## Guardrails

- Confirm ownership or authorization if it is not already clear.
- Do not remove stock, marketplace, paid-content, or third-party copyright-protection marks.
- Flag that disclosure or provenance requirements may still apply; removal does not prove an image is human-made or erase server-side history.
- Preserve the original. Write output to a new path and report the change.
- Start with inspection. Treat an absent local signal as unknown, not clean.

## Set up the CLI

Require Python 3.10.1 or later. Select an installation method available on the host; do not assume `uv`, a shell, or a filesystem layout.

- Use `uv tool install remove-ai-watermarks` when `uv` is available.
- Use `pipx install remove-ai-watermarks` when `pipx` is available.
- Otherwise, create a virtual environment and install with `python -m pip install remove-ai-watermarks`.
- On macOS or Linux with Homebrew, `brew install wiltodelta/tap/remove-ai-watermarks` is also supported.
- If a local source checkout is provided, install it from that checkout (`python -m pip install .`) or follow its own development instructions.

Read [command reference](references/commands.md) for platform-specific activation, optional extras, and command forms.

## Workflow

1. Run `remove-ai-watermarks identify <input>` and summarize detected signals and limits.
2. Select the narrowest operation:
   - `visible` for recognized visible AI labels;
   - `erase` only with a user-supplied region;
   - `metadata --remove` for provenance metadata only;
   - `invisible` only when the user understands that the full image is regenerated;
   - `batch` for authorized directories.
3. Write to a new output file. For `visible` and `erase`, inspect the affected region; for metadata removal, run `identify` on the result.
4. State which output was created, what was detected/removed, and any uncertainty.

Use `--force` for invisible processing only after explaining that a detector miss is not proof of absence and obtaining the user's confirmation.