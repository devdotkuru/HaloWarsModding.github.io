---
title: Cadenza Tool
description: "Command-line sound extractor/editor for Halo Wars: Definitive Edition Wwise packages."
permalink: /tools/cadenza
layout: default
nav_order: 2
image: https://raw.githubusercontent.com/HaloWarsModding/HaloWarsModding.github.io/master/resources/images/metadata/header.png
toc: true
---

# Cadenza <span class="label label-green">Stable</span>
{: .no_toc }

**[Download Cadenza v0.0.1](https://github.com/HaloWarsModding/Cadenza/releases/download/0.0.1/Cadenza_win-x64_v0.0.1.zip){: .btn .btn-purple }**

Cadenza is a command-line sound extractor and editor for Halo Wars: Definitive Edition Wwise packages.


1. TOC
{:toc}

---

## How It Works

### Extraction
- Point Cadenza at a `.pck` file to parse the package header and look-up tables, pulling out embedded `.wem` streams and SoundBanks by language. A `.cadenzaproj` file is written alongside the extracted assets to capture the package configuration for rebuilding later.​:codex-file-citation[codex-file-citation]{line_range_start=26 line_range_end=28 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L26-L28"}​
- During extraction, Cadenza can decode `.wem` files that use the RIFF/PCM (`0xFEFF`) encoding directly to WAV for preview and editing without Wwise installed.​:codex-file-citation[codex-file-citation]{line_range_start=27 line_range_end=29 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L27-L29"}​

### Editing & Recompilation
- SoundBank data (version 113 for Halo Wars: DE) is flattened to simpler `.bnkinfo` files using Wwiser.NET output so you can adjust events or media references before recompiling.​:codex-file-citation[codex-file-citation]{line_range_start=30 line_range_end=31 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L30-L31"}​
- After editing WAVs or `.bnkinfo` data, point Cadenza at the generated project file to rebuild `.bnk` and `.pck` outputs with the adjusted assets in place.​:codex-file-citation[codex-file-citation]{line_range_start=31 line_range_end=32 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L31-L32"}​

---

## Capabilities at a Glance

- **File packages (`.pck`)** — organize media and language maps, extract contents, and regenerate packages from the `.cadenzaproj` manifest.​:codex-file-citation[codex-file-citation]{line_range_start=38 line_range_end=39 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L38-L39"}​
- **SoundBanks (`.bnk`)** — decode Halo Wars: DE banks with Wwiser.NET, export them as editable `.bnkinfo`, then recompile back to version 113 `.bnk` files.​:codex-file-citation[codex-file-citation]{line_range_start=38 line_range_end=39 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L38-L39"}​
- **Wwise encoded media (`.wem`)** — decode/encode RIFF/PCM (`0xFEFF`) assets to standard WAV (signed 16-bit PCM) so edits can be dropped back into the project.​:codex-file-citation[codex-file-citation]{line_range_start=39 line_range_end=40 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L39-L40"}​

---

## Credits

- **HashDepot (Sedat Kapanoglu)** — FNV-1 hashing implementation adapted from the HashDepot project under MIT license, with helper methods and xUnit tests added for Cadenza.​:codex-file-citation[codex-file-citation]{line_range_start=46 line_range_end=47 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L46-L47"}​
- **Wwiser.NET (ME3Tweaks)** — leveraged to parse SoundBank metadata before generating `.bnkinfo` files for editing.​:codex-file-citation[codex-file-citation]{line_range_start=46 line_range_end=47 path=docs/CadenzaTool.md git_url="https://github.com/devdotkuru/Cadenza/blob/main/docs/CadenzaTool.md#L46-L47"}​
