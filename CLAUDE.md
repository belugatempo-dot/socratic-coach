# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code custom skill** — not a software project. There is no build system, no tests, no dependencies. The repository contains Markdown files that define a Socratic coaching agent's behavior at inference time.

## Architecture

| File | Role | Read at runtime? |
|------|------|-----------------|
| `SKILL.md` | **Complete skill definition.** Contains frontmatter triggers, intensity calibration, all operational instructions, lookup tables, domain adaptations, and memory hooks. Single authoritative source. | Yes — this is the skill file. |
| `elite-level-coach-refactor-plan-20260319.md` | **Planning artifact.** Documents the enhancement decisions. Not read at runtime. | No. |

### Single-File Design

All coaching logic lives in `SKILL.md` (~520 lines). This eliminates:
- Cross-reference overhead at runtime
- Content drift between files
- Confusion about which file owns which content

## Editing Guidelines

- **Line budget matters.** SKILL.md is read into context at inference time. Every line costs tokens. Keep it under ~550 lines unless there's a strong reason.
- **Tables are operational.** The lookup tables (Evidence Taxonomy, Compass Method, Ethos/Pathos signals, Domain Adaptations) are the most actionable parts. The agent pattern-matches against them during sessions. Preserve their structure.
- **Intensity calibration is in frontmatter.** Trigger phrases for gentle/default/challenge modes are defined in the YAML frontmatter description field.
- **Test changes by coaching.** After editing SKILL.md, run test coaching sessions to verify the agent uses the new content.

### Test Prompts

```
1. "Coach me on whether to pivot my startup" (Evidence + Consequences)
2. "I need to figure out our pricing" (Question Beneath the Question)
3. "Everyone says we should go enterprise" (Compass Method → Assumptions)
4. "挑战我关于这个决定" (Chinese + Challenge intensity)
5. "Help me think through a difficult conversation with my manager" (Interpersonal domain)
6. "I want some gentle coaching about my career direction" (Gentle intensity)
```
