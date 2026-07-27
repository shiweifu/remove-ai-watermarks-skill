# CLI command reference

Require Python 3.10.1 or later. Use the first supported installation method; all install the same `remove-ai-watermarks` command.

## Installation

### uv

```sh
uv tool install remove-ai-watermarks
```

### pipx

```sh
pipx install remove-ai-watermarks
```

### Standard Python virtual environment

Create and activate a virtual environment, then install the package:

```sh
python -m venv .venv
python -m pip install --upgrade pip
python -m pip install remove-ai-watermarks
```

Activate it before invoking the CLI:

```sh
# macOS/Linux
. .venv/bin/activate

# Windows PowerShell
.\.venv\Scripts\Activate.ps1

# Windows Command Prompt
.venv\Scripts\activate.bat
```

### Homebrew (macOS/Linux)

```sh
brew install wiltodelta/tap/remove-ai-watermarks
```

### Local source checkout

From the repository root, install the current checkout into an active virtual environment:

```sh
python -m pip install .
```

For development dependencies or a project-specific workflow, follow the checkout's `docs/installation.md`.

## Core commands

```sh
remove-ai-watermarks identify input.png
remove-ai-watermarks visible input.png -o clean.png
remove-ai-watermarks erase input.png --region x,y,width,height -o clean.png
remove-ai-watermarks metadata input.png --remove -o clean.png
remove-ai-watermarks batch ./images --mode visible
```

`visible` automatically checks registered marks. `erase` supports repeated `--region` values and should only be used for regions the user has identified. `metadata --remove` uses format-aware removal; it does not reconstruct image pixels.

## Optional features

Install extras with the same installer used for the core package:

```sh
# pip / virtual environment
python -m pip install "remove-ai-watermarks[migan]"
python -m pip install "remove-ai-watermarks[lama]"
python -m pip install "remove-ai-watermarks[gpu]"
python -m pip install "remove-ai-watermarks[qwen-zimage]"

# uv tool
uv tool install --force "remove-ai-watermarks[migan]"
```

Use `--backend migan` or `--backend lama` after installing the corresponding fill backend. Model downloads may occur on first use. The `gpu` extra supports CUDA, XPU, MPS, and CPU where the underlying runtime supports them; CPU runs can be very slow. `qwen-zimage` is CUDA-only.

## Invisible processing

```sh
remove-ai-watermarks invisible input.png -o clean.png
remove-ai-watermarks invisible input.png -o clean.png --cpu-offload
remove-ai-watermarks invisible input.png -o clean.png --force
remove-ai-watermarks invisible input.png -o clean.png --pipeline qwen-zimage --force
```

Diffusion processing changes the whole image and cannot guarantee a proprietary verifier will reject the result. Do not use `--force` without user confirmation.

## Verification

Run `identify` before and after metadata work. Visually inspect any inpainted or regenerated output. For an important provider-specific claim, use that provider's verifier when available; local detection alone is not conclusive.