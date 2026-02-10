# Plan: Enhance SKILL.md Based on questioning-framework.md

## Context

The `socratic-coach` project has two files:
- **`SKILL.md`** (302 lines) — the operational skill definition read at runtime
- **`questioning-framework.md`** (315 lines) — the deep-reference framework

`questioning-framework.md` contains several highly actionable tools (lookup tables, taxonomies, concrete techniques) that `SKILL.md` references conceptually but never provides. This makes `SKILL.md` aspirational in places where it should be operational. There's also a broken file path and some content duplication that risks drift.

**Goal:** Make SKILL.md more self-sufficient for runtime coaching by pulling in the most actionable framework content, while keeping it scannable (~346 lines, +14%).

---

## Changes to SKILL.md (7 changes, ordered by priority)

### 1. Fix broken reference path (line 69)

**File:** `SKILL.md:69`

```
# Current
references/questioning-framework.md

# Change to
questioning-framework.md
```

No `references/` folder exists. Simple factual fix.

---

### 2. Add Evidence Taxonomy table (new subsection after line 103)

**Insert between** end of section 3 ("Progressive Deepening") and section 4 ("Informed Questions").

```markdown
### Evidence Taxonomy — Quick Reference

When the user cites evidence, identify its type before probing:

| Type | Failure Mode | Follow-up |
|------|-------------|-----------|
| **Empirical** (data, metrics) | Cherry-picking, small sample | "What does the full dataset show? What are you NOT measuring?" |
| **Testimonial** (experts, users) | Authority bias, stated vs. revealed preference | "Do their actions match their words? Who sees it differently?" |
| **Analogical** (similar cases) | False analogy, different context | "What's different about your situation?" |
| **Logical** (if A then B) | Hidden premises, invalid inference | "Are both premises actually true?" |
| **Intuitive** (gut feeling) | Confirmation bias — but sometimes a real signal | "What pattern might your subconscious be picking up?" |
```

**Why:** SKILL.md tells the agent to probe evidence (line 96) but gives no way to classify evidence types or pick the right follow-up. This table is the single highest-value addition.

---

### 3. Add Compass Method navigation table (after Evidence Taxonomy)

**Insert after** the Evidence Taxonomy, before section 4.

```markdown
### Signal-to-Action Map (The Compass Method)

| Signal from the user | Where to go |
|---------------------|-------------|
| Vague language ("it's just better") | Clarify — ask for specifics |
| States something as obvious ("everyone knows...") | Probe assumptions |
| Claims a trend or outcome | Test evidence (use taxonomy above) |
| Fixated on one approach | Open alternatives — "What's the opposite view?" |
| Has a plan but seems uneasy | Map consequences — "And then what?" |
| Keeps circling the same point | Go meta — "Is this the right question?" |
| Strong emotion | Slow down, clarify, then go meta |
| Just had an "aha" moment | Go deeper — "What follows from that?" |
| Contradicts something said earlier | Surface it — "Earlier you said X, now Y. What shifted?" |
| Deflects with humor or dismissal | Check trust, then gently return |
| Cites authority without analysis | Test evidence (testimonial type) |
| Says "I should" repeatedly | Go meta — "Should according to whom?" |
```

**Why:** SKILL.md says "follow the contradiction, not a script" (lines 82-84, 101-103) but never provides a concrete signal-to-action lookup. This table operationalizes the core navigation philosophy.

---

### 4. Add "Question Beneath the Question" table (after line 65)

**Insert after** "Stay alert for the question beneath the question." in section 1 (Opening).

```markdown
| They ask | They might really be asking |
|----------|---------------------------|
| "Should we build or buy?" | "Do I trust my team to execute?" |
| "How should I price this?" | "Am I confident enough in the value?" |
| "Should I take this job?" | "Am I running toward something or away from something?" |
| "What's the right architecture?" | "How do I make a decision I can't fully undo?" |
| "How do I manage this person?" | "Should this person be on my team at all?" |
```

**Why:** SKILL.md introduces the concept (line 64-65) but provides zero examples. Without examples, the instruction is aspirational. This table makes it concrete.

---

### 5. Expand "Consequences" with the Second-Order Test (line 98)

**Expand inline** — don't create a new section.

```markdown
# Current (line 98)
- **Consequences** (late): What follows from each path? What's the second-order effect?

# Change to
- **Consequences** (late): What follows from each path? What's the second-order effect?
  Use the **"And then what?"** chain: push from first-order ("If we cut prices, we win
  more deals") → second-order ("Can we service them all?") → third-order ("Does margin
  drop enough to kill the product that won those deals?").
```

**Why:** Names the technique and gives a concrete worked example in 3 lines.

---

### 6. Add Perspective Prompts to domain sections (lines 243, 250, 257, 264)

**Add one bullet** to each of the four domain sections under "Adapting to Context":

- **Product/Strategy** (after line 243): `- **Perspectives to invoke:** End user, skeptical buyer, support team, competitor's PM, the customer who churns`
- **Career/Personal** (after line 250): `- **Perspectives to invoke:** Your mentor, your 80-year-old self, someone who chose the other path`
- **Technical Architecture** (after line 257): `- **Perspectives to invoke:** The engineer maintaining this at 3 AM, the new team member in 6 months, the security auditor`
- **Creative/Writing** (after line 264): `- **Perspectives to invoke:** The reader who puts it down after page 3, the critic, someone from a completely different culture`

**Why:** Gives the agent ready-made perspectives for the Alternatives phase, per domain.

---

### 7. Add two missing anti-patterns (after line 301)

**Append** to the Anti-Patterns section:

```
9. **The Socratic Bully** — Using questions as weapons to prove the user wrong rather than to help them think better. Check your intent.
10. **The Infinite Recursion** — Asking meta questions about meta questions endlessly. At some point, thinking must serve action. Help them land when they're ready.
```

**Why:** Covers two real failure modes missing from SKILL.md's list but present in the framework.

---

## Changes to questioning-framework.md (3 deduplication changes)

### 8a. Replace duplicated Gentle Disconfirmation (lines 69-83)

Replace the full technique block with:
```
### Technique: Gentle Disconfirmation (for the Confident Expert)

See SKILL.md section "Handling the Confident Expert" for this technique.
```

### 8b. Replace duplicated Anti-Patterns (lines 303-315)

Replace the full list with:
```
## Anti-Patterns to Avoid

See SKILL.md "Anti-Patterns" section for the complete list of 10 anti-patterns.
```

### 8c. Add cross-reference in Ethos/Pathos section (after line 275)

Add: `For the operational signal table, see SKILL.md section "Reading Ethos and Pathos."`

Keep the framework's version (conceptual/philosophical) — it serves a different purpose than SKILL.md's operational version.

---

## What's deliberately NOT being added to SKILL.md

- Full Dialectical Ladder ASCII art — visual, not operational
- Full question banks per level — framework's primary purpose; SKILL.md already has curated examples
- Pacing Guide — SKILL.md already covers this via Progressive Deepening
- Full Ethos/Pathos/Logos essay — SKILL.md's operational version is sufficient

---

## Verification

After making changes:
1. Confirm SKILL.md renders correctly as Markdown (no broken tables)
2. Verify the `questioning-framework.md` reference path resolves
3. Verify no content was accidentally deleted from either file
4. Check final line count is ~349 for SKILL.md and ~301 for framework
5. **Agent testing:** Run 2–3 test coaching sessions using the updated SKILL.md and verify:
   - The agent uses the Evidence Taxonomy to classify evidence and pick type-specific follow-ups
   - The agent uses the Compass Method table to select question types based on user signals
   - The "Question Beneath the Question" table triggers when surface questions appear
   - Tables are formatted in a way the model can parse and act on at inference time

   Test prompts:
   - "Coach me on whether to pivot my startup" (should hit Evidence + Consequences)
   - "I need to figure out our pricing" (should trigger Question Beneath the Question)
   - "Everyone says we should go enterprise" (should trigger Compass Method → Probe assumptions)

---

## Revision Log

### Revision 1 — Post-Review Adjustments

Based on review feedback, 4 additional changes were made:

| Change | File | What |
|--------|------|------|
| A | SKILL.md | Moved "And then what?" chain from inline bullet to blockquote callout after the arc, restoring visual rhythm |
| B | questioning-framework.md | Restored 2-sentence philosophical summary in Gentle Disconfirmation (was over-deduped) |
| C | questioning-framework.md | Restored explanatory summary in Anti-Patterns section (was over-deduped) |
| D | enhance_plan.md | Added agent-testing verification step with 3 test prompts |

Two concerns required no changes:
- Line count target (347 is fine — don't constrain quality for a number)
- Change #6 perspective prompts (no real redundancy with Compass Method — different purposes)
