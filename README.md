# Socratic Coach

A [Claude Code custom skill](https://docs.anthropic.com/en/docs/claude-code) that turns Claude into a Socratic coaching agent. Instead of giving direct answers, the agent helps users think through decisions, strategies, and complex problems by asking probing questions.

## What It Does

When a user says "coach me", "help me think through", "Socratic mode", "challenge my thinking", "play devil's advocate", or the Chinese equivalents "苏格拉底" / "追问", the skill activates and Claude shifts into a structured coaching mode:

- **Triages** whether coaching is appropriate (judgment calls get coaching; factual questions get direct answers)
- **Adapts intensity** based on user preference (gentle, default, or challenge mode)
- **Asks 1–2 probing questions per turn**, following contradictions rather than a script
- **Classifies evidence** (empirical, testimonial, analogical, logical, intuitive) and probes type-specific failure modes
- **Reads emotional subtext** — adjusting pace and directness based on trust and stakes
- **Closes with a session summary** and optional memory reflection for repeat users

Supports English and Chinese. Includes an emergency exit — say "just tell me what to do" and the agent switches to direct advice.

## Intensity Calibration

The skill supports three coaching intensities:

| Mode | Trigger Phrases | Style |
|------|-----------------|-------|
| **Gentle** | "gentle", "温和", "go easy", "探索" | 1 soft question per turn, heavy acknowledgment, exploration-focused |
| **Default** | (no modifier) | 1-2 questions per turn, balanced challenge and support |
| **Challenge** | "challenge", "挑战", "push hard", "steelman" | 2 questions per turn, tests every claim, steelmans opposition |

## Domain Coverage

The skill provides specialized guidance for 8 decision domains:

1. **Product/Strategy** — market assumptions, competitive blind spots, opportunity cost
2. **Career/Personal** — values alignment, fear vs. wisdom, reversibility
3. **Technical Architecture** — scaling assumptions, failure modes, maintenance burden
4. **Creative/Writing** — audience clarity, core message, essential form
5. **Interpersonal/Leadership** — power dynamics, psychological safety, radical candor
6. **Health/Lifestyle** — identity vs. behavior, values vs. habits, shame awareness
7. **Financial/Investment** — risk tolerance, time horizons, opportunity cost
8. **Learning/Skill Acquisition** — depth vs. breadth, learning as avoidance detection

## Memory Integration

For environments with persistent memory, the skill outputs a structured JSON reflection after each session:

```json
{
  "topic_domain": "product|career|technical|...",
  "intensity_used": "gentle|default|challenge",
  "user_thinking_style": { "primary": "analytical|intuitive|mixed" },
  "techniques_used": ["evidence_taxonomy", "informed_question", ...],
  "effective_techniques": [...],
  "resistance_points": [...],
  "ladder_depth_reached": "L1|L2|L3|L4|L5|L6",
  "outcome": "clarity|productive_aporia|emergency_exit|partial",
  "key_insight": "...",
  "open_threads": [...]
}
```

This enables adapting coaching style for repeat users — starting at preferred intensity, leaning into techniques that worked, and building on previous insights.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | The complete skill definition — all operational instructions, lookup tables, and anti-patterns. |
| `CLAUDE.md` | Guidance for Claude Code when editing this repository. |
| `elite-level-coach-refactor-plan-20260319.md` | Planning artifact documenting enhancement decisions. |

## Usage

Place `SKILL.md` in your Claude Code skill directory. The skill triggers automatically on matching phrases — see the frontmatter in `SKILL.md` for the full trigger list.

## Key Concepts

- **Dialectical Ascent:** Sessions climb from surface-level shadows through beliefs, evidence, and perspectives toward the real question — following contradictions, not a fixed sequence.
- **Evidence Taxonomy:** Five evidence types (empirical, testimonial, analogical, logical, intuitive), each with known failure modes and targeted follow-up questions.
- **Compass Method:** A signal-to-action map — vague language triggers clarification, "everyone knows" triggers assumption probing, strong emotion triggers slowing down.
- **Informed Questions:** The agent encodes real domain knowledge into questions without stating conclusions, giving the user something concrete to think against.
- **Productive Aporia:** Not every session ends with an answer. Sometimes the most valuable outcome is a better question.
- **Mid-Session Self-Check:** Silent audit every 4-5 exchanges to course-correct on talking ratio, question density, and user energy.
