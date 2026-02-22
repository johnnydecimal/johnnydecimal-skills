---
name: jdex
description: Read and write to the user's JDex — their Johnny.Decimal index. Use this skill whenever the user mentions their JDex, asks to check/fetch/update documentation, or references a Johnny.Decimal ID (e.g. 12.34, J-0131).
---

# Prerequisites

- This skill requires the `johnnydecimal` skill for JD system context.
- Do NOT load the `jdhq` skill unless the user explicitly asks you to document JDHQ source code.

# Use of the JDex

- FIRST: run `echo $JDEX_ROOT` to get the JDex root directory. The variable is called JDEX_ROOT — not JDEX_PATH, not JDEX_DIR, not anything else. If it's empty, STOP. Tell the user: "The `$JDEX_ROOT` environment variable isn't set. Set it to the root of your JDex and restart your shell." Do not continue with this skill and do not try to find the JDex any other way (no `find`, no `mdfind`, no guessing).
- Each entry is a Markdown file.
- The user can refer you to the JDex by way of a Johnny.Decimal ID.
  - E.g. they might say "check the documentation at 12.34".
  - Match the file using a glob from `$JDEX_ROOT`: e.g. `**/12.34*` for ID 12.34, or `**/J-0131*` for job J-0131. Substitute the actual ID the user gives you.
- When the user says "document this" or "write it up" in the context of this skill, they mean write it in the JDex entry — not in a local CLAUDE.md, README, or any other file.
- Follow links in the `Related` metadata field when they're relevant to the task.
  - Create links where relevant. Use the shortest `[[12.34 Title]]` wiki-link syntax.

# The .johnnydecimal dotfile

- At the start of a conversation, check for a `.johnnydecimal` file in or above the working directory.
- If it exists, read it. The `id` field is the Johnny.Decimal project ID for this folder.
  - This is a statement of intent from the user. Unless directed otherwise, this is the JDex entry you should act on — read it, write to it, document in it. Do not go searching for other files or create new ones. The dotfile is telling you: "this is the note."
- If it doesn't exist and the user hasn't provided an ID, ask them for one. Do not guess.
