# README

> See [Johnny.Decimal > JDex](https://jdcm.al/11.05/) for background.

This repository contains skills for use with your favourite LLM.

# [`jdex`](/jdex)

- Requires environment variable `JDEX_ROOT`.
  - This should point to the root of your JDex, e.g. your Obsidian vault's root.
  - E.g. `export JDEX_ROOT=/Users/john/escaped\ path/to/jdex`.
- Looks for an optional `.johnnydecimal` in your current folder.
  - This should contain a single line which is the most relevant ID for this folder, e.g.
  - `id: 12.34`
  - Failing this, looks for `[12.34]` in the current folder name.
  - Failing this, the skill will ask the user for the ID. It has been instructed to **not guess**. (But it's an LLM so, y'know.)
- Invoke the skill mentioning your JDex, e.g. `read my jdex and catch up`.
- If the dotfile is present, the LLM will start with that ID, and prefer that ID for all future documentation-related instructions.
  - If it isn't, you'll be asked for an ID. The skill prefers not to guess.

# [`johnnydecimal`](/johnnydecimal)

- Provides context to your LLM re: canonical Johnny.Decimal structure.
- Isn't user-invokable; is invoked by `jdex`.
