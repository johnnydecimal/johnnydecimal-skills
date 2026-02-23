---
name: jdex
description: Read and write to the user's JDex — their Johnny.Decimal index. Use this skill whenever the user mentions their JDex, asks to check/fetch/update documentation, or references a Johnny.Decimal ID (e.g. 12.34, 90001).
---

# Prerequisites

- This skill requires the `johnnydecimal` skill for JD system context.
- Do NOT load the `jdhq` skill unless the user explicitly asks you to document JDHQ source code.

# Use of the JDex

- FIRST: run `echo $JDEX_ROOT` to get the JDex root directory. The variable is called JDEX_ROOT — not JDEX_PATH, not JDEX_DIR, not anything else. If it's empty, STOP. Tell the user: "The `$JDEX_ROOT` environment variable isn't set. Set it to the root of your JDex and restart your shell." Do not continue with this skill and do not try to find the JDex any other way (no `find`, no `mdfind`, no guessing).
- Each entry is a Markdown file. To find one, glob from `$JDEX_ROOT`: e.g. `**/12.34*` for ID 12.34, or `**/90001*` for 5-digit ID 90001.
- When the user says "document this" or "write it up" in the context of this skill, they mean write it in the JDex entry — not in a local CLAUDE.md, README, or any other file.
- Follow links in the `Related` metadata field when they're relevant to the task. Reading a linked entry for context is fine — but the active ID does not change. All writes go to the active ID's entry unless the user explicitly gives you a different ID.
  - Create links where relevant. Use the shortest `[[12.34 Title]]` wiki-link syntax.

# Which ID to use

- Your **active ID** is determined once per session, in this priority order:
  1. A `.johnnydecimal` dotfile in or above the working directory (see below).
  2. A bracketed ID in the current folder name, e.g. `my-project [12.34]`.
  3. An ID the user explicitly provides when asked.
- Once an active ID is set, **stick with it**. All reads, writes, and documentation go to that ID's JDex entry.
- Do NOT browse, scan, or explore the JDex looking for other entries. The JDex is not a task list to trawl through. You work on the active ID.
- Only switch to a different ID if the user explicitly gives you a new one — e.g. "now look at 56.78" or "update 90001". Mentions of other IDs in note content, related links, or conversation context are NOT instructions to switch.
- If you're unsure whether the user wants a different ID, ask. Do not assume.

# The .johnnydecimal dotfile

- At the start of a conversation, check for a `.johnnydecimal` file in or above the working directory.
- If it exists, read it. The `id` field is the active ID for this folder.
  - This is a statement of intent from the user. It means: this is the note. Read it, write to it, document in it. Do not go searching for other files or create new ones.
- If no dotfile or bracketed ID exists and the user hasn't provided an ID, STOP. Ask the user: "Which JDex ID should I use?" Do not search the JDex for a match, do not infer from the project name, and do not continue until the user gives you one.
