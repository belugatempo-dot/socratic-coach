# Socratic Coach

A [Claude Code custom skill](https://docs.anthropic.com/en/docs/claude-code) that turns Claude into a Socratic coaching agent. Instead of giving direct answers, the agent helps users think through decisions, strategies, and complex problems by asking probing questions.

## What It Does

When a user says "coach me", "help me think through", "challenge my thinking", or similar phrases, the skill activates and Claude shifts into a structured coaching mode:

- **Triages** whether coaching is appropriate (judgment calls get coaching; factual questions get direct answers)
- **Asks 1–2 probing questions per turn**, following the user's contradictions rather than a script
- **Classifies evidence** the user cites (empirical, testimonial, analogical, logical, intuitive) and probes type-specific failure modes
- **Reads emotional subtext** — adjusting pace and directness based on trust and stakes
- **Closes with a session summary** or honors productive confusion when no tidy answer exists

Supports English and Chinese. Includes an emergency exit — say "just tell me what to do" and the agent switches to direct advice.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | The skill definition. Contains all operational instructions, lookup tables, and anti-patterns the agent uses at runtime. |
| `questioning-framework.md` | Deep reference. The Dialectical Ladder (6 question levels), full question banks, the Compass Method, and philosophical foundations. |
| `enhance_plan.md` | Planning artifact documenting enhancement decisions and revision history. |
| `CLAUDE.md` | Guidance for Claude Code when editing this repository. |

## Usage

Place `SKILL.md` and `questioning-framework.md` in your Claude Code skill directory. The skill triggers automatically on matching phrases — see the frontmatter in `SKILL.md` for the full trigger list.

## Key Concepts

- **Dialectical Ascent:** Sessions climb from surface-level shadows through beliefs, evidence, and perspectives toward the real question — but follow contradictions, not a fixed sequence.
- **Evidence Taxonomy:** Five evidence types (empirical, testimonial, analogical, logical, intuitive), each with known failure modes and targeted follow-up questions.
- **Compass Method:** A signal-to-action map — vague language triggers clarification, "everyone knows" triggers assumption probing, strong emotion triggers slowing down.
- **Informed Questions:** The agent encodes real domain knowledge into questions without stating conclusions, giving the user something concrete to think against.
- **Productive Aporia:** Not every session ends with an answer. Sometimes the most valuable outcome is a better question.
