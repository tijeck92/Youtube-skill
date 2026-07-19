# Youtube-skill

A small collection of Claude Agent Skills, starting from a request to help solve everyday problems using YouTube — grown to include personal knowledge management along the way.

## Skills

- [`skills/youtube-howto-finder`](skills/youtube-howto-finder/SKILL.md) — searches the web for relevant, real YouTube videos matching a described problem and presents a short, curated list. Uses only the built-in web search tool; no third-party API keys, accounts, or credentials required.
- [`skills/obsidian-second-brain`](skills/obsidian-second-brain/SKILL.md) — turns an Obsidian vault into a persistent knowledge base Claude reads from and writes to: capturing new notes, linking them into the existing vault, and answering questions from what's already stored. Works via plain file read/write on the vault folder — no MCP server, plugin, or account needed.

## Install

Copy a skill folder into your Claude Code skills directory:

```bash
cp -r skills/youtube-howto-finder ~/.claude/skills/
cp -r skills/obsidian-second-brain ~/.claude/skills/
```
