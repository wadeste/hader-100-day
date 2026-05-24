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
- [x] Cycle 205: Unified Attribution Dashboard — Product Spec, Competitive Landscape, Roadmap
- [x] Cycle 206: Government Funding Landscape — VET Student Loans, State Subsidies, AI Flows
- [x] Cycle 207: Implementation Timeline + KPI Framework — Consolidated Milestones, Dashboard, Review Cadence
- [x] Cycle 208: Zoho Integration Deep-Dive — Technical Architecture, Data Model, Rollout Plan
- [x] Cycle 209: Financial Modelling — Unit Economics, Break-Even, Scenario Planning
- [x] Cycle 210: Customer Success — Lifecycle Stages, Health Scoring, Churn Prevention
- [x] Cycle 211: Legal Framework — MSA, DPA, SLA, AI Liability, Privacy Act
- [x] Cycle 212: International Expansion — NZ, UK, US Market, Multi-Region Architecture
- [x] Cycle 213: Investor Strategy — AU EdTech Investors, Pitch Deck, Exit Options
- [x] Cycle 214: AI Continuous Improvement — Data Flywheel, Performance Metrics, ML Roadmap
- [x] Cycle 215: Security Architecture — Infrastructure, Encryption, DR Plan, Incident Response
- [x] Cycle 216: Pilot Program and Beta Launch Strategy — 4-Phase Framework, Beta Structure, Conversion Funnel
- [x] Cycle 217: Sales Execution Scripts — LinkedIn Templates, Email Sequences, Objection Handling
- [x] Cycle 218: Onboarding and Implementation Playbook — 14-Day Timeline, Kickoff Agenda, Failure Prevention
- [x] Cycle 219: Content Marketing Strategy — 4-Purpose Framework, 12-Month Calendar, LinkedIn Templates
- [x] Cycle 220: Community Services Expansion — Detailed Competitive Landscape, AI Opportunities, First-Mover Advantage
- [x] Cycle 221: Voice AI Platform Cost Verification — VAPI $50 minimum, outbound free, 87% gross margins
- [x] Cycle 222: Sales Pipeline and Conversion Metrics — 8-stage framework, 4% overall conversion, hiring triggers
- [x] Cycle 223: Enrollment Feasibility — 1,000 enrollments/month math, 50 RTOs, goal hierarchy, tracking KPIs
- [x] Cycle 224: LinkedIn Paid Advertising — targeting parameters, CTR/CPC benchmarks, retargeting strategy, creative strategy
- [x] Cycle 225: Lead Scoring + Marketing Automation — BANT model, behavioral signals, nurture sequences, Zoho implementation
- [x] Cycle 226: Team Structure and Hiring Roadmap — Human Capital Plan, Salary Benchmarks, Org Charts
- [x] Cycle 228: Tier Upgrade Financial Triggers — Quantified Thresholds, Upgrade Scripts, Zoho Dashboard
- [x] Cycle 229: AI Regulation in Australia — Mandatory Requirements Timeline, Compliance Implications, Contract Updates
- [x] Cycle 230: Risk Management and Mitigation Framework — 18 Risks Across 5 Categories, Top 5 Critical Risks with Contingencies, Risk Dashboard, Escalation Path
- [x] Cycle 231: Ideal Customer Profile Firmographics — Industry Vertical Prioritization (IT/Business), Geographic Clustering (4 Metro Clusters), Funding Mix Analysis, Tech Stack Signals, ICP Scorecard (6 Criteria), Revised ICP Summary
- [x] Cycle 232: ASQA Audit Evidence Deep-Dive — Specific Audit Criteria (3-Phase), AI-Specific Scenarios (Verbal Consent, USI Exemptions, Vulnerable Populations), Compliance Cost Benchmarks ($36-63K/year), Updated Feature Checklist (7 Must-Have, 2 Recommended), Compliance Documentation Package (8 Documents)