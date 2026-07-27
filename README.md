# Remove AI Watermarks Skill

[![skills.sh](https://skills.sh/b/shiweifu/remove-ai-watermarks-skill)](https://skills.sh/shiweifu/remove-ai-watermarks-skill/remove-ai-watermarks)

A portable agent skill for inspecting and cleaning AI provenance signals from images you own or are authorized to edit. It guides agents through the [`remove-ai-watermarks`](https://github.com/wiltodelta/remove-ai-watermarks) CLI, with cross-platform setup and careful verification.

## Install

Install it with the skills CLI:

```sh
npx skills add https://github.com/shiweifu/remove-ai-watermarks-skill --skill remove-ai-watermarks
```

The skill works with Codex and other agents supported by [skills.sh](https://skills.sh). The installer chooses the appropriate agent directory, or you can pass its `--agent` option.

## What it covers

- Inspect visible marks and provenance signals with `identify`.
- Remove supported visible AI labels with localized inpainting.
- Erase a user-selected image region.
- Strip supported C2PA, EXIF, XMP, and IPTC metadata.
- Process an authorized image directory.
- Use optional diffusion pipelines for invisible watermark disruption, with clear quality and hardware warnings.

The skill supports `uv`, `pipx`, standard Python virtual environments, and Homebrew where available. It requires Python 3.10.1 or later, but does not assume a particular operating system, shell, or local source path.

## Example workflow

```sh
# Inspect first
remove-ai-watermarks identify input.png

# Remove detected supported visible marks into a new file
remove-ai-watermarks visible input.png -o clean.png

# Check the result
remove-ai-watermarks identify clean.png
```

For platform-specific setup, optional model backends, and invisible-watermark processing, see [the command reference](references/commands.md).

## Scope and responsible use

Use this skill only for images you own or are authorized to edit. It is not intended for stock previews, marketplace marks, paid-content overlays, or other third-party copyright-protection watermarks.

Removing local metadata or a detected mark does not prove an image is human-made, remove provider-side generation history, or guarantee that an external verifier will reject the output. AI-disclosure laws and platform rules may still apply. Preserve the original file, write to a new output path, and review the result.

## Upstream project

This repository packages guidance for the open-source [`wiltodelta/remove-ai-watermarks`](https://github.com/wiltodelta/remove-ai-watermarks) CLI. It does not bundle the upstream source code or models. Install the CLI separately using the instructions in this skill.

## License

This skill is available under the [Apache License 2.0](LICENSE).
