---
title: Cadenza
description: "Simple command-line tool to edit Halo Wars: DE Wwise sounds."
layout: default
nav_order: 6
permalink: /tools/cadenza
image: https://raw.githubusercontent.com/HaloWarsModding/HaloWarsModding.github.io/master/resources/images/metadata/header.png
toc: true
---

# Cadenza <span class="label label-green">Stable</span>
{: .no_toc }

[Download Cadenza](https://github.com/HaloWarsModding/Cadenza/releases/download/0.0.1/Cadenza_win-x64_v0.0.1.zip){: .btn .btn-purple }

Cadenza is a small command-line tool that lets you pull sounds out of Halo Wars: Definitive Edition, edit them, and then put them back into the game.

Think of it as:

"Unpack sound files > edit them > repack for the game."

1. TOC
{:toc}

---

## What Cadenza Works With

Halo Wars: DE uses Wwise, which splits audio into a few file types:

- `.pck` - big container files that hold a bunch of sounds and banks  
- `.bnk` - SoundBanks (events, sound references, etc.)  
- `.wem` - actual audio data (the sound files inside the game)

Cadenza helps you go from these formats to something editable and back again.

---

## How It Works 

### Extraction

You point Cadenza at a `.pck` file.

Cadenza then:

- Reads the `.pck` structure (header and tables, but you don’t need to care about that)
- Finds all:
  - `.wem` sound files
  - SoundBanks (`.bnk`)
- Sorts things by language (ENG, FRA, etc.)
- Saves everything to normal files on disk

At the same time, Cadenza creates a project file next to the extracted stuff:

- `something.cadenzaproj`
- This file remembers:
  - Which sounds were in the package
  - How they were organized
  - What needs to be rebuilt later

You don’t have to manually track any of that, the project file is the recipe for rebuilding.

---

### Editing & Recompilation

Once you’ve extracted everything, you can edit:

- The **audio files** (WAVs that came from `.wem`)
- The **SoundBanks** (events and references)

#### SoundBanks to `.bnkinfo`

Halo Wars: DE uses SoundBank version 113.

Raw `.bnk` files are not fun to edit, so Cadenza:

- Uses **Wwiser.NET** to read `.bnk` files  
- Converts them into simpler `.bnkinfo` text-like files

`.bnkinfo` files are meant to be:

- Easier to read and modify
- A flattened, human-editable form of the SoundBank

You can use them to adjust things like:

- Which event plays which sound
- Which media IDs are referenced

After editing `.bnkinfo`, Cadenza can:

- Turn them back into proper version 113 `.bnk` files ready for the game

#### Rebuilding Packages

After you’re done editing:

- WAVs (replacing or modifying audio)
- `.bnkinfo` (changing events or mappings)

You run Cadenza again, this time on the `.cadenzaproj` file.

Cadenza will:

- Rebuild any updated `.bnk` files
- Rebuild the `.pck` package(s)
- Put all your edited assets back into the right places

End result: new `.pck` with your custom audio, that the game can use like the original.

---

## Credits

Cadenza makes use of a couple of existing projects:

- HashDepot (Sedat Kapanoglu)
  - Provides the FNV-1 hashing implementation.  
  - Cadenza adds helper methods and xUnit tests on top.  

- Wwiser.NET
  - Used to parse SoundBank metadata.  
  - This is what makes exporting to and from `.bnkinfo` possible.
