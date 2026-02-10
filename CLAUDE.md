# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Claude Code custom skill** — not a software project. There is no build system, no tests, no dependencies. The repository contains Markdown files that define a Socratic coaching agent's behavior at inference time.

## Architecture

| File | Role | Read at runtime? |
|------|------|-----------------|
| `SKILL.md` | **Primary skill definition.** Contains the frontmatter trigger, all operational instructions, and lookup tables the agent uses during coaching sessions. | Yes — this is the skill file. |
| `questioning-framework.md` | **Deep reference.** The Dialectical Ladder (6 question levels), detailed question banks per level, the Compass Method navigation table, and philosophical foundations. Cross-referenced by SKILL.md. | Yes — referenced from SKILL.md. |
| `enhance_plan.md` | **Planning artifact.** Documents the enhancement decisions and revision log. Not read at runtime. | No. |

### Content Relationship

SKILL.md is the **operational** document — it tells the agent what to do. questioning-framework.md is the **conceptual** document — it explains why and provides depth. Where content exists in both files:

- **SKILL.md owns** the canonical version of: Evidence Taxonomy table, Compass Method signal table, "Question Beneath the Question" table, anti-patterns list, ethos/pathos signal table, domain perspective prompts.
- **questioning-framework.md owns** the canonical version of: Dialectical Ladder (6 levels with full question banks), Compass Method with ladder-level mappings, philosophical framing (Plato's cave, Aristotle's rhetoric).
- **Deduplication rule:** When content overlaps, one file has the full version and the other has a brief summary + cross-reference. Never duplicate full content in both files — it will drift.

## Editing Guidelines

- **Line budget matters.** SKILL.md is read into context at inference time. Every line costs tokens. Currently ~349 lines — keep it under ~400 unless there's a strong reason.
- **Tables are operational.** The lookup tables (Evidence Taxonomy, Compass Method, Question Beneath the Question, ethos/pathos signals) are the most actionable parts of SKILL.md. The agent pattern-matches against them during sessions. Preserve their structure.
- **The Progressive Deepening arc (Shadows → ... → The Real Question) should stay visually clean.** Each stage is a single-line bullet. Extended techniques go in callouts or separate subsections, not inline.
- **Test changes by coaching.** After editing SKILL.md or questioning-framework.md, run test coaching sessions to verify the agent actually uses the new content. See enhance_plan.md's verification section for test prompts.
