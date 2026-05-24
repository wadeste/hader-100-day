# Task 008: refinement-cycle

## Workflow
strategy-research-loop

## Type
PROMPT (LLM reasoning — deepen existing research)

## Description
When all queue topics are complete, enters refinement mode to deepen existing research, add missing data, and improve strategic recommendations.

## Prompt
```
All queue items are complete. Now enter refinement mode.

1. Read `research-log.md` to review existing findings
2. Pick the FIRST topic in the queue that has `[x]`
3. Identify ONE area that could be deepened:
   - Missing data points or more recent information?
   - Competitor analysis that's thin?
   - Strategic implications that need more depth?
   - Actionable recommendations that are too vague?
   - New developments since the original research?
4. Research the gap (web search, data lookup)
5. Append updated findings to `research-log.md` with a "Refinement — {YYYY-MM-DD}" section under the original topic
6. Commit: `git add -A && git commit -m "refine: deepen {topic_title} — {what changed}"`
7. Move to the next topic on the next iteration. Keep cycling through all topics.

**Good refinements:**
- Added recent competitor pricing data
- Expanded strategic implications with financial modelling
- Turned vague recommendations into specific action items with timelines
- Incorporated new market research or regulatory changes

**Bad refinements:**
- Rephrasing existing findings without adding substance
- Adding generic platitudes ("this is important", "further research needed")
- Repeating the same analysis with slightly different wording
```

## Acceptance Criteria
- [x] Reads existing `research-log.md` to identify gaps
- [x] Picks one topic to deepen
- [x] Performs new research on the identified gap
- [x] Appends refinement to `research-log.md` with date stamp
- [x] Commits with descriptive message
- [x] Moves to next topic on subsequent iterations

## Cycle Log
- [x] Cycle 188: Segmentation-Specific Positioning — Tier Differentiation
- [x] Cycle 189: ASQA Compliance Documentation for AI Enrollment Calls
- [x] Cycle 190: Market Sizing Quantification — TAM/SAM/SOM
- [x] Cycle 191: AI Tools Benchmarking — VAPI, Retell, Bland comparison
- [x] Cycle 192: Competitive Analysis Deep-Dive — Study Buddy/Area Ten Verification
- [x] Cycle 193: GTM Channel Strategy Deep-Dive — Missing Channel Research
- [x] Cycle 194: Pricing Model Deep-Dive — Missing Pricing Analysis
- [x] Cycle 195: Website CRO and SEO Research — Missing Website Strategy
- [x] Cycle 196: CAC Modelling Deep-Dive — Missing Financial Model
- [x] Cycle 197: Competitive Moat Analysis — Missing Defensible Advantage
- [x] Cycle 198: AI Courses Market — Missing AI Qualification Research
- [x] Cycle 199: Community Services Expansion — Missing Community Services Research
- [x] Cycle 200: Customer Discovery Interviews — Missing Discovery Framework
- [x] Cycle 201: 100-Day Plan Synthesis — Missing Executive Presentation
- [x] Cycle 202: Partnership Opportunity Scan — Missing Partner Research
- [x] Cycle 203: Social Proof Strategy — Hader Case Study, Warm Referrals, Flywheel Model
- [x] Cycle 204: AI Skill Packages — TAZ Workflow, Compliance Checklist, Suite Positioning
- [ ] Cycle 205: (next topic — revisit any remaining thin areas)