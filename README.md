# Lorkinsey

Open-source skills for Claude Code and Claude CoWork by [Lorhard](https://lorhard.com/) — battle-tested internal tools, now available to everyone.

Lorkinsey packages the structured thinking frameworks we use day-to-day at Lorhard into reusable skills. Drawing inspiration from YC's founder-centric interrogation style, McKinsey & Company's structured problem-solving methodology, and real-world product decision-making, each skill is designed to help you think more rigorously before you build.

> Auto-generated from source. Do not edit directly.

## Available Skills (2)

### `snowball` (v1.0.0)

Warren Buffett's full decision operating system — investing, moats, valuation, governance, macro worldview, and life philosophy — as a thinking framework for any consequential decision.

### `ycofficehour` (v1.0.0)

YC Office Hours: structured product thinking for new ideas, directions, and 'is this worth building' questions. Research-first, not output-first.

## Install

Pick whichever method matches your setup. All three give you the same skills.

### A. Claude Code — marketplace (recommended)

```bash
/plugin marketplace add Lorhard/lorkinsey
/plugin install <plugin-name>@lorkinsey
```

Replace `<plugin-name>` with any skill from the list above (e.g. `snowball`, `ycofficehour`). To install all of them, run `/plugin install` once per skill.

### B. Claude CoWork (Desktop)

Browse and install from [claude.com/plugins](https://claude.com/plugins).

### C. One-line install via Git (any machine)

Install all skills into your user-level `~/.claude/skills/` so they're available in every project:

```bash
git clone --depth 1 https://github.com/Lorhard/lorkinsey.git /tmp/lorkinsey && cp -r /tmp/lorkinsey/plugins/*/skills/*/ ~/.claude/skills/ && rm -rf /tmp/lorkinsey
```

Or install a single skill into the current project (team-shareable when committed):

```bash
# replace <skill-name> with e.g. snowball, ycofficehour
git clone --depth 1 https://github.com/Lorhard/lorkinsey.git /tmp/lorkinsey && cp -r /tmp/lorkinsey/plugins/<skill-name>/skills/<skill-name> .claude/skills/ && rm -rf /tmp/lorkinsey
```

## Usage

There are two ways to use a Lorkinsey skill once it's installed.

### 1. Just ask a question in natural language (primary path)

Each skill's frontmatter declares when it should activate. Claude reads that on its own and consults the relevant skill whenever your question matches its scope — **you don't need to remember skill names or type any slash command**.

Examples that route to `snowball`:

- *"Is Apple still a good business to own for the next decade?"*
- *"How do I tell whether a company has a real economic moat?"*
- *"Is the market overvalued right now?"*
- *"How should I evaluate this CEO?"*
- *"Should I hold or sell my position in X?"*
- *"I'm thinking about a career change — how do I decide if it's worth it?"* (life-philosophy layer)

Examples that route to `ycofficehour`:

- *"Is this startup idea worth building?"*
- *"We're thinking about adding [feature] — should we?"*
- *"Help me pressure-test this product direction."*

Skills can also **decline** to activate when the question is outside their scope (e.g. `snowball` won't engage for day-trading, technical analysis, or short-term crypto speculation — Buffett explicitly rejects those domains).

### 2. Invoke explicitly with a slash command

When you want to force a specific framework — or make the choice visible in your transcript — call the skill directly:

```bash
/snowball
/ycofficehour
```

Most skills accept a free-form argument (a topic, decision, or question to stress-test). For example:

```bash
/snowball should I hold Nvidia for the next 5 years?
/snowball evaluate this M&A deal: [paste details]
/ycofficehour AI-powered inventory management for SMB restaurants
```

See each skill's `SKILL.md` for its full scope, trigger conditions, and argument hint.

## What's Next

We're actively developing more skills across product strategy, UI/UX design critique, and technical architecture review. Watch this repo to stay updated.

## Acknowledgments

- [Warren Buffett](https://en.wikipedia.org/wiki/Warren_Buffett) & [Charlie Munger](https://en.wikipedia.org/wiki/Charlie_Munger) — the `snowball` skill distills their ~70-year body of work into a decision operating system
- [Garry Tan](https://github.com/garrytan) — the `ycofficehour` skill is directly inspired by his [office-hours skill](https://github.com/garrytan/gstack/blob/main/office-hours/SKILL.md)
- [Y Combinator](https://www.ycombinator.com/) — for the founder-first thinking framework that shapes how we evaluate ideas
- [McKinsey & Company](https://www.mckinsey.com/) — for the structured, hypothesis-driven problem-solving methodology

## Privacy Policy

Lorkinsey runs entirely within your local session. We do not collect, transmit, or store any user data. Your prompts and session context are processed by Anthropic under their own privacy policies — Lorhard has no access to that data. [Full policy →](https://lorhard.com/privacy)

## License

MIT © Lorhard
