# Humanizer-Cluade-Skill-V3.16 --- Humanize-your-text
Full-enforcement humanisation engine. Detects 51 synthetic writing patterns and rebuilds prose until it sounds like a specific person wrote it. 'Ish it still needs a human look over.
---
# Humanizer v3.15
6
**Author:** TABARC-Code  
**Version:** 3.16  
**Licence:** MIT  
**Layer:** L2 — Execution  
**Module:** Writing Quality / AI Pattern Detection

---

## What It Does

Full-enforcement humanisation engine. Detects (51) synthetic writing patterns and rebuilds prose until it sounds like a specific person wrote it. Not just cleaner but different rhythm, concrete specificity, opinions that surface, sentences that stop when they've said something. but

---

## File Structure

```
humanizer/
├── SKILL.md                    Master file — conflict resolution, pre-steps, rules, passes, scoring
└── references/
    ├── patterns.md             51-pattern library (all complete with Before/After) + Human Voice Engine
    ├── domains.md              Academic / business / marketing / casual / technical-developer
    ├── sentence-rewrites.md    100+ sentence examples (20 categories) + 13 paragraph transforms
    └── edit-checklist.md       Four-Sentence Test (canonical) + complete checklist + 15 Final Rules
```

All four reference files fully bidirectionally linked. All 51 patterns complete with Before/After examples.

---

## OK Key Features

**Conflict resolution** — explicit priority order when thee  skill rules conflict with user instructions. User explicit constraints always win; STEP 0E (intentional register) wins over all patterns.

**Level 0 triage** — iff the text already passes the Four-Sentence Test and flows on read-aloud, say so. Over-editing genuinely human prose is worse than leaving it alone.

**ABSTRACTION brackets** — sentences that cannot be humanised without inventing facts get bracketed and surfaced as a collected action list, not scattered inline..

**STEP 0E** — intentional-register texts (specs, legal, compliance) are exempt from humanisation. The skill identifies and stops rather than breaking what is deliberately neutral.


---

## Licence

MIT
