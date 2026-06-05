# Humanizer

*By TABARC-Code*

---

AI writes like nobody's watching. Which is the problem.

It doesn't mean to be dull. It's just optimising for the middle — the statistical centre of what sounds acceptable across every possible context. The result is prose that's technically correct, perfectly structured, and reads like it was assembled by a committee that had never met. No one wrote it. No one decided anything. It just emerged.

This skill exists to fix that.

---

## What it actually does

Humanizer is a Claude skill that takes AI-generated text and rebuilds it until it sounds like a person wrote it under real conditions — deadline pressure, an actual opinion, a specific audience in mind. Not just cleaner. *Different.*

It runs across five passes. The first detects problems against a library of 51 named patterns — everything from inflated significance and fake transition phrases through to the specific horror of modal stacking ("could potentially be worth exploring whether it might"). The last pass is a read-aloud. That's not optional. You'd be surprised how much survives the earlier passes and still sounds wrong when you say it out loud.

In between there's a self-audit pass where you answer honestly: what still sounds AI-generated? Two to five bullets. Then fix those things.

---

## Why not just use a "make this sound human" prompt

Fair question. Those work, up to a point. What they don't give you is a systematic reason for every change — something you can apply consistently, check against, and improve over time.

The 51-pattern library means every rewrite decision has a named cause. "This got cut because it's Pattern 39 — an in-conclusion paragraph that adds no new information." "This got rewritten because it's Pattern 49 — a symmetrical rebuttal that presents two views, calls both valid, and refuses to take a position." That's reproducible. It's auditable. And it means the skill gets better through use rather than drifting.

The Voice Engine is the other half. Simple humanising prompts remove AI tells. They don't add human signals. Asymmetric attention, earned digressions, self-correction mid-text — these are techniques that go beyond avoidance into active injection of marks that indicate a thinking person. Pattern removal gets you prose that isn't obviously synthetic. The Voice Engine gets you prose that sounds like someone specific.

---

## Before the first pass

Five pre-steps run before any rewriting starts.

**STEP 0** is triage. Level 1 is a light touch — vocabulary and punctuation, one pass. Level 3 is a full rebuild from meaning, not sentence. There's also a Level 0: already human. If the text passes the Four-Sentence Test and flows on read-aloud, the skill says so and stops. Over-editing genuinely good prose in service of pattern avoidance is worse than leaving it alone. Much worse, actually.

**STEP 0B** is voice matching. When you provide a sample of your own writing alongside the AI text, the skill reads the sample first and uses it as a hard constraint. The output should sound like you — not like generic humanised prose. It checks register, contraction habits, sentence length preference, how opinions surface. A voice-match check runs at the end to confirm.

**STEP 0C** is scope. This is where mixed AI-and-human text gets handled properly. If you wrote some paragraphs yourself and had AI generate others, the skill identifies the boundary and rewrites only the AI sections — matching them to your voice rather than averaging everything down.

**STEP 0D** is fact preservation. Every concrete fact — statistics, names, dates, direct quotes — gets noted before a word is changed, and verified again after. When a sentence is too vague to humanise without inventing facts, it gets bracketed: [ABSTRACTION: this sentence needs a real example the user must supply]. Those collect into a list at the end. Not scattered through the text. Not silently deleted. Surfaced.

**STEP 0E** checks whether the text is *supposed* to be neutral. Technical specifications. Legal documents. Compliance text. These shouldn't be humanised — the neutrality is a feature, not a bug. The skill identifies them and steps back, applying only vocabulary and chatbot-artefact fixes rather than the full humanisation pass.

---

## Conflict resolution

When the skill's rules conflict with something you've asked for, there's an explicit priority order.

Your stated constraints win. "Keep the em dashes in this section." "Don't rewrite the opening paragraph." Honoured — and documented: "I've kept [X] as instructed, though it would normally be flagged under [pattern]." STEP 0E wins over all patterns — intentional-register texts are exempt even if patterns fire. Fact preservation wins over humanisation — a specific number or name stays verbatim even if rephrasing around it would be cleaner. What the skill won't do is guess at what you want and silently apply it.

---

## The pattern library

Fifty-one patterns. All complete — Before, After, Detect signal, Fix rule.

The early ones are obvious: chatbot openers ("Great question!"), em dash overuse, sycophantic preambles before any content. Delete them and you're already halfway there. Pattern 7, AI vocabulary overuse, has a Detect signal based on cluster density — one "crucial" in a paragraph can be human; four vocabulary-ban words in 80 words isn't.

The middle section covers structural habits. Assembly feel — paragraphs that could be rearranged without anyone noticing — is harder to spot than individual word choices because individual sentences might be fine. The problem is at the level of the piece. Uniform paragraph length is similar. Reading a piece where every paragraph is the same size signals automatic generation before a single word is read.

The ones added from the slime-mould audit are the subtlest. Symmetrical rebuttal presents two opposing views, declares them both valid, and concludes that the truth lies somewhere in between. It's not wrong exactly. It just refuses to say anything. Fake transition phrases ("building on this idea", "with that in mind") simulate logical progression without providing it — remove them and the logical connection, if there was one, still holds. If it doesn't, that's useful to know. Modal stacking is the formal register version of hedge-stacking: "could potentially be worth exploring whether it might" as a single clause, three modals deep. One modal is precision. Two is hedging. Three is evasion.

Pattern 22 — filler phrases — has a full replacement table. Pattern 13 — em dash overuse — has a four-row conversion logic table covering asides, list intros, clause connectors, and mid-sentence clarifications. Because "replace with a comma" isn't always right, and the skill knows the difference.

---

## The Voice Engine

Avoiding AI patterns gets you prose that isn't obviously synthetic. It doesn't get you prose that sounds like a person.

The Human Voice Engine covers that second half. Rhythm variation, earned digressions, tonal shifts, specificity as the basic unit of authenticity. The advanced section covers asymmetric attention — humans don't distribute paragraph weight evenly, and AI does, and that evenness reads — plus earned digressions (going slightly off-topic and coming back), and self-correction mid-text.

That last one works. Genuinely. "Actually, that's not quite right" somewhere in a piece signals a thinking person in a way that a hundred perfectly accurate sentences don't.

---

## Domains

Five domain modes, each with a list of additional tells and a "what good looks like" section.

**Academic** catches the specific habits of AI academic prose — hedging constructions, impersonal passive voice where it doesn't serve the content, vague attribution dressed up as systematic review. **Business/corporate** catches even distribution of blame, meeting-speak, decisions made by unnamed forces. **Marketing/copywriting** catches the brochure tells — aspirational abstractions, "journey" and "experience" doing heavy lifting, solutions without problems. **Casual/blog/personal** catches over-correction in the other direction, where AI tries to sound informal and lands on a kind of performative casualness that no one actually uses. **Technical/developer** is its own particular problem: over-explaining what the reader clearly already knows ("a for loop iterates over each element"), passive instruction instead of direct instruction, every function described in the same three-sentence structure regardless of complexity.

Each domain applies on top of the core pattern library. Cross-domain rules — the read-aloud test, the Four-Sentence Test, contraction handling — run regardless of domain.

---

## The reference files

```
humanizer/
├── SKILL.md
└── references/
    ├── patterns.md             51 patterns — Before, After, Detect, Fix throughout
    ├── domains.md              Five domain modes — tells and "what good looks like" per domain
    ├── sentence-rewrites.md    100+ sentence-level examples across 20 categories, 13 paragraph
    │                           transforms, diagnostics A–H for the hardest patterns
    └── edit-checklist.md       Four-Sentence Test (canonical source), complete checklist,
                                15 Final Rules, scoring reference
```

Everything cross-links in both directions — every category in `sentence-rewrites.md` points to its pattern, every workflow step in `edit-checklist.md` points to the relevant pattern, the Voice Engine links to the 15 Final Rules. That took several audit cycles.

The kaizen log is in the `SKILL.md` frontmatter. The skill went from v3.0 to v3.15 and the log covers every structural change. More usefully: the skill contains an active self-improvement instruction. If during a run you rewrite a sentence three times and it still reads AI, you might have found a new pattern. Name it, write the Before and After, note why it isn't covered by the existing 51. Report it as a v+1 candidate. The library grew from 37 to 51 that way.

---

## Scoring

Seven dimensions: Directness, Rhythm, Trust, Authenticity, Density, Specificity, Voice.

Each has anchors at three levels — what a score of two looks like, five, eight — so the assessment isn't just a vibe check. Aggregate threshold is 56 out of 70. The fail-fast rule matters more: any single dimension at three or below triggers a mandatory rewrite regardless of the aggregate. A piece that's direct, dense, and specific but has no voice hasn't been humanised. It's been edited.

---

## Licence

MIT. Use it, modify it, don't remove the attribution.

---

*TABARC-Code. UK English. Version-tracked. Kaizen-threaded. Built across more audit cycles than was probably necessary, and better for it.*
