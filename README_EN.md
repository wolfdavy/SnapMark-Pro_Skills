# SnapMark

> Lossless screenshot content transcription skill — not an OCR tool, not a summarizer, but "what's in the screenshot is what you get."

## What is it

SnapMark is an AI skill in [Agent Skills](https://agentskills.io) standard format (SKILL.md) that enforces **strict lossless transcription** when AI coding assistants process screenshots: extract body content as-is — no summarizing, no rewriting, no translating, no polishing, no additions.

## Key features

| Feature | Description |
|---------|-------------|
| **Zero addition** | Never adds titles, numbering, explanations, summaries, or any content not present in the screenshot |
| **Zero deletion** | Complete preservation of all body text — nothing is omitted |
| **Body-first** | Prioritizes body text, emails, slides, chat logs, code, tables, and headings |
| **Auto-filter** | Automatically skips watermarks, browser toolbars, taskbars, scrollbars, window borders, and other non-content UI elements |
| **Structure preserved** | Maintains original heading levels, line breaks, paragraphs, numbering, indentation, and table structure |
| **Table recognition** | Clear tables output as Markdown tables; unclear ones as plain text blocks |
| **Code preservation** | Code screenshots retain indentation, blank lines, comments — no auto-formatting or optimization |
| **Multi-image ordered** | Multiple screenshots output strictly in input order, separated only by `---` |
| **Uncertainty marking** | Unclear content marked with `[unclear]` / `[partially visible]` / `[unreadable]` — no guessing allowed |

## Use cases

- WeChat / Enterprise WeChat / Feishu / QQ screenshots → extract chat logs
- Teams screenshots → extract meeting conversations
- PPT screenshots → extract slide text
- Word screenshots → extract document content
- Excel screenshots → extract table data
- Code screenshots → extract source code
- Webpage screenshots → extract page content
- Chat history screenshots → convert to text archive

## Usage

### Option 1: Direct conversation

Send a screenshot to an AI assistant with SnapMark installed, and simply say:

```
Extract the content from this screenshot
```

The AI will automatically load the skill and output following strict lossless transcription rules.

### Option 2: Invoke as a skill

In tools with skill system support (e.g., WorkBuddy, Claude Code), invoke directly by skill name:

```
/skill snapmark
```

## Installation paths

SnapMark follows the [Agent Skills open standard](https://agentskills.io) and works with major AI coding assistants. Place the `SKILL.md` file in the corresponding directory:

### Project-level installation (follows the repo, shared with team)

| AI tool | Path | Notes |
|---------|------|-------|
| **WorkBuddy** | `.workbuddy/skills/snapmark/SKILL.md` | Native support, auto-loaded |
| **Claude Code** | `.claude/skills/snapmark/SKILL.md` | Native support, triggered on demand |
| **GitHub Copilot** | `.github/skills/snapmark/SKILL.md` | Project-level skills directory |
| **Cursor** | `.cursor/skills/snapmark/SKILL.md` | Project-level skills directory |
| **Windsurf** | `.windsurf/rules/snapmark.md` | Copy SKILL.md content as a rule file |
| **Cline** | `.cline/rules/snapmark.md` | Copy SKILL.md content as a rule file |
| **Continue** | `.continue/rules/snapmark.md` | Copy SKILL.md content as a rule file |
| **Codex (OpenAI)** | `AGENTS.md` | Append SKILL.md content to AGENTS.md |
| **Gemini CLI** | `GEMINI.md` | Append SKILL.md content to GEMINI.md |
| **Aider** | `CONVENTIONS.md` | Append SKILL.md content to CONVENTIONS.md |
| **Trae** | `.trae/rules/snapmark.md` | Copy SKILL.md content as a rule file |

### User-level installation (personal global, works across all projects)

| AI tool | Path |
|---------|------|
| **WorkBuddy** | `~/.workbuddy/skills/snapmark/SKILL.md` |
| **Claude Code** | `~/.claude/skills/snapmark/SKILL.md` |
| **GitHub Copilot** | `~/.copilot/skills/snapmark/SKILL.md` |
| **Cursor** | `~/.cursor/skills/snapmark/SKILL.md` |

### Installation examples

```bash
# WorkBuddy (project-level)
mkdir -p .workbuddy/skills/snapmark
cp SKILL.md .workbuddy/skills/snapmark/SKILL.md

# Claude Code (user-level, global)
mkdir -p ~/.claude/skills/snapmark
cp SKILL.md ~/.claude/skills/snapmark/SKILL.md

# Cursor (project-level rule)
mkdir -p .cursor/rules
cp SKILL.md .cursor/rules/snapmark.md

# GitHub Copilot (append to instructions file)
echo "" >> .github/copilot-instructions.md
cat SKILL.md >> .github/copilot-instructions.md
```

## How it works

SnapMark uses **Progressive Disclosure**:

1. **Layer 1**: The `name` and `description` in YAML frontmatter are always in context (~100 tokens). The AI uses this to decide whether to activate the skill.
2. **Layer 2**: When the user sends a screenshot, the AI loads the SKILL.md body (10 core principles + checklist).
3. **Layer 3**: The AI executes each principle and verifies against the checklist before outputting.

## SnapMark-Strict mode

Automatically activated when detecting the following screenshot types:

- WeChat / Enterprise WeChat / Teams / Feishu / QQ chat screenshots
- PPT / Word / Excel document screenshots
- Code screenshots

In Strict mode, the AI maximizes preservation of original layout, mixed Chinese-English formatting, line breaks, indentation, table layout, and code formatting. Overlay watermarks are automatically removed.

## License

MIT License — free to use, modify, and distribute.

## Standard

This skill follows the [Agent Skills open standard](https://agentskills.io) and is compatible with all AI coding assistants that support this standard.
