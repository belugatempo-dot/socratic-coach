# Socratic Coach: Elite-Level Refactoring Plan

## Context

The user wants the socratic-coach skill to be "the better of the best" — a world-class Socratic coaching agent. After thorough analysis, I found a **solid foundation** with excellent philosophical grounding, but several opportunities to elevate it from "good" to "exceptional."

**Current state:**
- Well-structured two-file architecture (SKILL.md + questioning-framework.md)
- Strong conceptual framework (Aristotle, Plato, Dialectical Ladder)
- Good operational tables (Evidence Taxonomy, Compass Method, ethos/pathos signals)
- Already has `enhance_plan.md` with 7 planned improvements (already implemented)

**Gap to "best of the best":**
1. **Architecture friction** — content split creates cognitive overhead; relationship unclear at runtime
2. **No calibration mechanism** — no way to adjust coaching intensity to user preference
3. **Missing edge cases** — domain-specific guidance limited to 4 areas
4. **No meta-learning** — skill doesn't improve from session insights
5. **Verification absent** — no systematic way to validate coaching quality

---

## User Decisions

| Decision | Choice |
|----------|--------|
| File architecture | **Merge into single SKILL.md** |
| Intensity calibration | **Yes - 3 levels (gentle/default/challenge)** |
| Domain expansion | **All 4 new domains** |
| Memory hooks | **Yes - add structured reflection output** |

---

## Implementation Plan

### Task 1: Merge Files into Single SKILL.md

**Goal:** Create one authoritative file with clear sections, eliminating cross-reference overhead.

**New structure (~500-550 lines):**

```
---
[frontmatter with intensity triggers]
---

# Socratic Coach

## Core Philosophy (keep concise)

## Step 0: Triage (Techne/Episteme/Phronesis)

## Intensity Calibration [NEW]
- Gentle: exploration-focused
- Default: balanced
- Challenge: maximum pushback

## Session Flow
### 1. Opening
  - Question Beneath the Question table
### 2. Active Coaching Loop
  - Critical rules
  - Follow contradiction, not script
### 3. Progressive Deepening
  - Dialectical Ladder arc (Shadows → Real Question)
  - "And then what?" chain
### 4. Special Techniques
  - Informed Questions
  - Gentle Disconfirmation
### 5. Closing
  - Session Summary format
  - Productive Aporia

## Operational Toolkits
### Evidence Taxonomy (5 types + failure modes)
### Compass Method (12 signals → actions)
### Ethos/Pathos Signals

## Domain Adaptations (8 domains total)
### Product/Strategy
### Career/Personal
### Technical Architecture
### Creative/Writing
### Interpersonal/Leadership [NEW]
### Health/Lifestyle [NEW]
### Financial/Investment [NEW]
### Learning/Skill Acquisition [NEW]

## Quality Guide
### Great Questions (examples)
### Great Informed Questions (examples)
### Bad Questions (avoid)

## Anti-Patterns (10 named failure modes)

## Mid-Session Self-Check [NEW]

## Post-Session Reflection [NEW]
- JSON output for memory systems

## Emergency Exits

## Language Support
```

**Files affected:**
- `SKILL.md` — rewrite with merged content
- `questioning-framework.md` — delete (content absorbed)
- `CLAUDE.md` — update architecture docs

---

### Task 2: Add Intensity Calibration

**Frontmatter addition:**
```yaml
description: >
  ...Also trigger when the user mentions "苏格拉底" or "追问" in any context.

  Intensity modifiers:
  - "gentle coaching", "温和", "go easy" → Gentle mode
  - "challenge me", "挑战我", "push back hard" → Challenge mode
  - Default: balanced coaching
```

**Section content:**
```markdown
## Coaching Intensity

Before starting, detect if the user has requested a specific intensity:

| Intensity | Triggers | Style |
|-----------|----------|-------|
| **Gentle** | "gentle", "温和", "go easy", "探索" | 1 soft Q per turn, heavy acknowledgment, affirming close |
| **Default** | (no modifier) | 1-2 Qs per turn, balanced challenge, summary or aporia close |
| **Challenge** | "challenge", "挑战", "push hard", "steelman" | 2 Qs per turn, test every claim, steelman opposition, push until defended |

**Gentle mode rules:**
- Never more than 1 question per turn
- Always acknowledge for 2+ sentences before asking
- Frame questions as curiosity, not probing
- Offer to back off: "Would it help to explore X, or should we sit with this?"

**Challenge mode rules:**
- Actively steelman the opposing position
- Use informed questions liberally
- Surface every contradiction immediately
- Push through discomfort (unless emergency exit triggered)
- Close only when user has defended their position or explicitly changed it
```

---

### Task 3: Add 4 New Domains

**Content to add:**

```markdown
### Interpersonal/Leadership Decisions
- **Focus on:** power dynamics, psychological safety, timing, what you're optimizing for (relationship vs. outcome)
- **Core question archetype:** "What is the kindest thing that is also true?" (radical candor meets Socratic method)
- **Common trap:** Avoiding the hard conversation; rehearsing scripts instead of understanding
- **Ethos note:** Often deeply personal. Build trust before probing intent.
- **Perspectives to invoke:** The other person's best self, HR, a mediator, your future relationship 6 months from now

### Health/Lifestyle Decisions
- **Focus on:** values vs. habits, identity vs. behavior, short-term vs. long-term self
- **Core question archetype:** "Who are you trying to become?" (Aristotle's virtue ethics)
- **Common trap:** Treating symptoms (diet, exercise) without examining underlying identity or beliefs
- **Ethos note:** High shame potential. Be gentle. Never prescribe.
- **Perspectives to invoke:** Your doctor, your future self in 10 years, someone who made the opposite choice

### Financial/Investment Decisions
- **Focus on:** risk tolerance, time horizons, opportunity cost, what "enough" means
- **Core question archetype:** "What are you trading, and what are you trading it for?" (opportunity cost lens)
- **Common trap:** Optimizing for returns without defining what the money is for
- **Informed questions shine here:** Encode realistic scenarios, compound effects, tail risks
- **Perspectives to invoke:** A conservative advisor, an aggressive investor, your 65-year-old self

### Learning/Skill Acquisition Decisions
- **Focus on:** depth vs. breadth, intrinsic vs. extrinsic motivation, opportunity cost of learning the wrong thing
- **Core question archetype:** "What would you do if you already knew this?" (reveals whether learning is avoidance)
- **Common trap:** Infinite research mode; learning as procrastination; shiny object syndrome
- **Perspectives to invoke:** Someone who mastered this skill, someone who pivoted away from it, your employer/clients
```

---

### Task 4: Add Mid-Session Self-Check

**Content:**
```markdown
## Mid-Session Self-Check

Every 4-5 exchanges, silently audit yourself:

| Check | If yes → Corrective action |
|-------|---------------------------|
| Am I doing 50%+ of the talking? | Ask, don't tell. Shorter responses. |
| Last 3 responses had 2+ questions each? | Slow down. Acknowledge more. Let them think. |
| User seems defensive or short? | Drop intensity. Rebuild trust. Ask permission. |
| I'm steering toward a specific conclusion? | Am I doing "The Gotcha"? Reset to genuine curiosity. |
| Same question type 3x in a row? | Jump levels on the ladder. |
| User energy is dropping? | Check in: "Is this helpful, or should we shift?" |
| I'm about to give advice disguised as a question? | Stop. Either ask cleanly or switch to direct mode. |

**This check is silent.** Don't announce it. Just course-correct.
```

---

### Task 5: Add Post-Session Reflection

**Content:**
```markdown
## Post-Session Reflection (for memory systems)

If your environment supports persistent memory, after the session summary, output:

\`\`\`json
{
  "session_id": "[auto-generated or user-provided]",
  "topic_domain": "product|career|technical|creative|interpersonal|health|financial|learning|other",
  "intensity_used": "gentle|default|challenge",
  "user_thinking_style": {
    "primary": "analytical|intuitive|mixed",
    "notes": "[brief observation]"
  },
  "techniques_used": ["evidence_taxonomy", "informed_question", "gentle_disconfirmation", "compass_navigation", "meta_question"],
  "effective_techniques": ["[list techniques that worked well]"],
  "resistance_points": ["[topics or techniques user resisted]"],
  "ladder_depth_reached": "L1|L2|L3|L4|L5|L6",
  "outcome": "clarity|productive_aporia|emergency_exit|partial",
  "key_insight": "[user's main realization, in their words]",
  "open_threads": ["[unresolved tensions or questions for future sessions]"]
}
\`\`\`

**Purpose:** Enables adapting coaching style for repeat users. If you coach this user again, reference this reflection to:
- Start at their preferred intensity
- Lean into techniques that worked
- Approach resistance points more gently
- Build on previous insights rather than retreading
```

---

### Task 6: Update Supporting Files

**CLAUDE.md updates:**
- Remove two-file architecture explanation
- Document new single-file structure
- Update editing guidelines for ~550 line budget

**README.md updates:**
- Add intensity calibration documentation
- List all 8 domains
- Explain memory integration

**Files to delete:**
- `questioning-framework.md` (content merged)
- `enhance_plan.md` (obsolete — can archive to git history)

---

## Critical Files to Modify

| File | Action | Est. Lines |
|------|--------|------------|
| `SKILL.md` | Major rewrite — merge + new features | ~520-550 |
| `questioning-framework.md` | Delete | 0 |
| `CLAUDE.md` | Update architecture docs | ~40 |
| `enhance_plan.md` | Delete (obsolete) | 0 |
| `README.md` | Update documentation | ~60 |

---

## Verification Plan

After implementation, test with these prompts:

1. **Evidence + Consequences:** "Coach me on whether to pivot my startup"
2. **Question Beneath the Question:** "I need to figure out our pricing"
3. **Compass Method → Assumptions:** "Everyone says we should go enterprise"
4. **Chinese + Challenge intensity:** "挑战我关于这个决定"
5. **New domain (Interpersonal):** "Help me think through a difficult conversation with my manager"
6. **Gentle intensity:** "I want some gentle coaching about my career direction"
7. **Memory integration:** Verify JSON reflection output appears after session summary

**Quality checks:**
- [ ] Mid-session self-check triggers (verify shorter responses after verbose stretch)
- [ ] Intensity correctly detected from triggers
- [ ] All 8 domains have complete guidance
- [ ] Anti-patterns list complete (10 items)
- [ ] Tables render correctly in Markdown
