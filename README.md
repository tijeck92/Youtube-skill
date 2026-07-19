# Youtube-skill

A Claude Agent Skill that finds real YouTube tutorials for problems you describe (repairs, DIY, cooking, software/tech issues, learning something new) instead of, or alongside, a text explanation.

## Skills

- [`skills/youtube-howto-finder`](skills/youtube-howto-finder/SKILL.md) — searches the web for relevant, real YouTube videos matching a described problem and presents a short, curated list. Uses only the built-in web search tool; no third-party API keys, accounts, or credentials required.

## Install

Copy the skill folder into your Claude Code skills directory:

```bash
cp -r skills/youtube-howto-finder ~/.claude/skills/
```
