---
name: obsidian-second-brain
description: Turns an Obsidian vault (a folder of markdown notes) into a persistent knowledge base Claude reads from and writes to — capturing new information as linked notes, answering questions from what's already stored, and keeping the vault organized. Use this whenever the user asks to save/capture something in their notes or vault, says things like "merk dir das", "speicher das in Obsidian", "leg dazu eine Notiz an", "was weiß ich schon über X", "durchsuch meine Notizen", "zweites Gehirn", "second brain", or wants Claude to remember something across sessions in their own notes rather than in chat memory. Works purely through normal file read/write on the vault folder — no MCP server, plugin, or account needed.
---

# Obsidian Second Brain

Treats an Obsidian vault as durable, user-owned memory: plain markdown files on disk, organized with [[wikilinks]] and frontmatter, that Claude can read from and write to directly. No MCP server or plugin required — Obsidian itself just renders whatever is in the folder, so writing a well-formed `.md` file is enough for it to show up correctly linked in the app.

## Find the vault

Before doing anything else, find the vault folder:

1. Check whether the user already told you the path earlier in this session or it's recorded somewhere obvious (e.g. a project's `CLAUDE.md`).
2. If not, ask for it once: "Wo liegt dein Obsidian-Vault (Ordner-Pfad)?" Don't guess a path.
3. Once you know it, treat it as a stable fact for the rest of the session — don't ask again.

If the user wants this to work automatically in future sessions without re-asking, suggest they add the path to their `~/.claude/CLAUDE.md` (e.g. `Obsidian vault: /path/to/vault`) — that's the user's call, not something to do unprompted.

## Understand the vault's own conventions before writing to it

Every vault develops its own house style. Before creating or editing notes, look at a handful of existing notes (`Glob` for `*.md`, `Read` a few) to pick up:

- Frontmatter schema in use (e.g. `title`, `tags`, `created`, `aliases`) — match it, don't invent a different schema
- File naming pattern (Title Case vs kebab-case vs date-prefixed)
- Folder structure (flat vault, PARA-style `Projects/Areas/Resources/Archive`, topic folders, etc.)
- Whether there's a daily-notes folder or a MOC ("Map of Content") / index note pattern

If the vault is empty or has no discernible pattern, use plain, sensible defaults: `Title Case.md` filenames, minimal frontmatter (`tags`, `created`), and note when you're introducing structure so the user can correct it early rather than after 50 notes.

## Capturing new information

When the user wants something saved:

1. **Search before creating.** Grep the vault for the topic first — extending an existing note beats creating a near-duplicate. Obsidian vaults degrade fast when the same topic lives in three unlinked notes.
2. **Decide: append or new note.** If a clearly-matching note exists, append a section to it. Otherwise create a new note.
3. **Link it in, don't leave it orphaned.** Add `[[wikilinks]]` to related existing notes you find, and — if the vault uses a MOC/index/hub-note pattern — add a link to the new note there too. An unlinked note is invisible in Obsidian's graph and easy to lose.
4. **Keep frontmatter consistent** with what you observed (tags, dates, etc.).
5. Tell the user briefly what you filed and where (note title/path), so they can correct the filing if it's wrong.

## Answering from the vault

When the user asks what they already know/wrote about something:

1. Grep across the vault for relevant terms (try a few synonyms — people don't always tag consistently).
2. Read the matching notes fully, not just the grep line, so you get real context.
3. Synthesize an answer and cite which note(s) it came from (by title, so the user can open them), rather than presenting it as if you already knew it.
4. If nothing relevant is found, say so — don't fabricate vault content that isn't there.

## Guardrails

- This is the user's personal knowledge base, often years of accumulated notes. Prefer additive changes (new notes, appended sections, new links). Don't rewrite, restructure, or delete existing notes' content without asking first — a bad guess here is expensive to undo by hand.
- Don't invent facts and file them as if they came from the user — only write down what the user actually told you or what's demonstrably true, and say when something is your own synthesis versus their original words.
- If a note's content in the vault conflicts with what the user is telling you now, surface the conflict rather than silently overwriting the old note.
