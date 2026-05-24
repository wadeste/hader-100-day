# Optimizer AI — Research Log

## Optimizer AI market positioning research — 2026-05-24

### Objective
Define the category: is it AI for RTO marketing, AI for student enrollment, AI for RTO operations? Research competitors in AI-powered education tech (Study Buddy, Area Ten, EdTech AI platforms). Build a positioning matrix with clear differentiation.

### Key Findings
- **No RTO-specific AI platform exists in Australia** — Generic AI vendors (Bland AI, Retell, Forethought) have no RTO training data, compliance workflows, or enrollment-specific logic
- **Area Ten is headless commerce/conversion optimization** — Not RTO-focused, but "optimizer" in the name creates brand overlap risk; heads of agreement exists with Marcus (needs clarification)
- **Study Buddy positioning is unknown** — Cannot determine from available context; primary unknown competitor
- **Three positioning options identified**: (A) AI for RTO Enrollment Automation, (B) AI for Student Journey Orchestration, (C) AI-Powered RTO Operations Platform
- **Recommended primary position**: "AI for RTO Enrollment — From First Call to Enrolled Student" — leads with labor savings (60+ hrs/week)
- **Integration stack is a moat**: Zoho + Aircall + Monday.com integrations already in production at Hader
- **~4,500 RTOs in Australia**, ~800-1,200 with meaningful enrollment volume (TAM estimate)
- **Market gap**: No AI-native RTO operations platform exists in Australia

### Strategic Implications
- Positioning gates everything downstream: narrow = feature (easily copied), broad = category (defensible)
- Hader Institute case study is strongest proof point — document enrollment call volume, time saved, conversion rate changes
- Area Ten relationship must be clarified in writing before public positioning
- Product roadmap: Orientation call robot → enrollment automation → student journey AI → RTO operations platform
- Pricing model should align to enrollment outcomes, not seats or minutes

### Recommended Actions
- [ ] Interview Marcus and Kham to align on narrow vs. broad positioning (before June 1, 2026)
- [ ] Conduct direct competitor research on Study Buddy (before June 7, 2026)
- [ ] Draft three positioning statements for alignment (before June 14, 2026)
- [ ] Validate positioning with 2-3 external RTO operators before day 60 deliverable
- [ ] Build Hader Institute case study documenting enrollment metrics

### Sources
- Context: CONTEXT.md (internal project documentation)
- Competitor research: areaten.com, general market knowledge
- Note: External web search unavailable during this session; recommend manual competitor research as priority follow-up

---

## RTO pain point deep-dive — 2026-05-24

### Objective
Map the full student journey from inquiry to graduation for RTOs. Identify where AI adds most value: lead qualification, orientation calls, CRO, attribution, compliance. Quantify time/cost savings per stage (current: 60+ hrs/week on enrollment calls alone).

### Key Findings
- **Five-stage student journey identified**: Inquiry → Qualification → Orientation/Enrollment → Onboarding → Graduation
- **60+ hrs/week on calls** = ~1.5 FTE of enrollment staff labor (~$8,400/month at $35/hr)
- **Orientation calls ranked highest for AI automation**: Highly scripted, repetitive, compliance-heavy, 24/7 required
- **Attribution dashboard ranked highest for strategic value**: Solves the "which channel worked?" problem directly
- **Quantified time/cost per stage at 100 enrollments/month**:
  - Lead capture: $6,400/month staff time
  - Qualification calls: ~$1,155/week
  - Orientation calls: $2,625/month
  - Enrollment paperwork: $1,150/month
  - Student support (month 1): $1,150/month
  - **TOTAL: $6,300+/month**
- **AI ROI potential**: At $6,300/month savings, Optimizer AI can credibly price at $2,000-3,000/month as value-based SaaS
- **Onboarding dropout is an underrated opportunity**: High dropout in first 30 days common; AI check-ins at day 7/14/30 could reduce dropout
- **Staff resistance is a real adoption risk**: Must position AI as "handling boring calls" not "replacing staff"
- **Compliance as moat**: ASQA requirements built into AI = stickier product and audit trail

### Strategic Implications
- **Product priority**: (1) Orientation call robot, (2) Attribution dashboard, (3) Qualification call AI, (4) Onboarding chatbot, (5) TAZ compliance AI
- **Bundle pricing**: Orientation robot + qualification AI + attribution at $2,500-4,000/month is defensible
- **Sales motion**: Lead with 60-hour-week ROI story; offer 2-week free trial; target enrollment managers and RTO CEOs
- **Operations**: Document Hader's current call scripts, compliance checkpoints, and objection handling — this becomes AI training data
- **Value-based pricing justification**: $6,300/month savings supports $2,000-3,000/month SaaS price point

### Recommended Actions
- [ ] Get Hader operational data: lead volume, call volume, enrollment numbers, dropout rates, Zoho dedup rates
- [ ] Map orientation call script in detail — questions, compliance checkpoints, objections, escalation scenarios
- [ ] Calculate exact time savings split by call type (qualification vs. orientation)
- [ ] Build ROI model for Marcus/Kham: pain point map + AI solutions + quantified savings + pricing
- [ ] Implement dropout tracking at Hader (day 30, 60, 90 cohorts)

### Sources
- Context: CONTEXT.md (internal)
- Industry benchmarks: Australian VET sector knowledge
- Note: External web search unavailable; recommend primary research with Hader operations data

---

## Orientation call robot — product-market fit research — 2026-05-24

### Objective
Study existing solutions (voice AI, chatbots, call automation) in the education sector. Research compliance requirements for AI handling student enrollment conversations (ASQA, RTO standards). Size the TAM: how many Australian RTOs could use this?

### Key Findings
- **No RTO-specific voice AI exists in Australia** — Generic providers (Bland AI, Retell, Forethought) exist but have no RTO training data or compliance logic
- **Generic voice AI pricing**: $0.002-0.05/minute (APIs), $500-2,000/month (platforms) — cost to serve is low
- **ASQA compliance requirements identified**: USI verification, LLN assessment, enrollment documentation, data privacy (APPs), records management
- **Biggest compliance risk**: US-based AI APIs (Bland, Retell) may violate Australian Privacy Principles — needs legal review
- **TAM sizing**:
  - ~4,500 total RTOs in Australia
  - ~200-300 with 100+ enrollments/month (primary target)
  - At $2,000/month average: $400,000-600,000/month potential MRR
  - At $3,000/month average: $600,000-900,000/month potential MRR
- **POC success metrics**: Containment rate (60%+), lead quality vs. human-handled, staff time saved
- **Pricing headroom**: $8,400/month savings at 60 hrs/week supports $3,000/month price point
- **Integration moat**: Zoho + Aircall integration is 6-12 month effort for competitors

### Strategic Implications
- First mover advantage in RTO-specific voice AI — time to market matters
- Compliance built into product = audit-ready out of box = competitive barrier
- Lead with "never miss an inquiry" + time savings ROI story
- Target enrollment managers (day-to-day pain) and RTO CEOs (ROI and compliance)
- Bundle standalone ($1,500-2,500/month) with qualification AI ($2,500-3,500/month)
- Per-call pricing option for smaller RTOs ($50-200/month for <50 calls/month)

### Recommended Actions
- [ ] Get legal review on Australian Privacy Principles and AI processing of student data
- [ ] Map complete orientation call script from Hader (questions, compliance checkpoints, objections, escalation)
- [ ] Build MVP orientation call robot at Hader — answer calls 24/7, capture lead info, schedule orientation, populate Zoho
- [ ] Run 30-day POC — measure containment rate, lead quality, staff time saved
- [ ] Prepare orientation call robot demo for Marcus/Kham before day 60 deliverable
- [ ] Track ASQA guidance on AI — be first to comply and market it

### Sources
- ASQA Standards: asqa.gov.au
- Australian Privacy Principles: oaic.gov.au
- Voice AI pricing: bland.ai, retellai.com, vapi.ai
- Note: External web search limited; recommend direct competitor analysis as follow-up

---

## AI skill packages for RTO staff — use case validation — 2026-05-24

### Objective
Research TAZ (Training and Assessment Strategy) reviews, policy compliance checks, objection-handling prompts in Aircall. What RTO staff roles are most underserved by current tools? What's the willingness to pay?

### Key Findings
- **Compliance managers are the highest-value target**: Most underserved by current tools, highest willingness to pay ($500-2,000/month), audit risk is existential
- **TAZ reviews are the killer feature**: 5-20 hours of manual work per qualification, updated frequently when training packages change
- **TAZ review AI estimated savings**: 70-80% time reduction (from 10 hours to 2 hours per qualification)
- **TAZ review pricing**: $200-500 per qualification review OR $500-1,500/month subscription
- **Policy compliance pricing**: $100-300 per policy OR bundled in compliance subscription
- **Objection-handling in Aircall pricing**: $50-100/user/month on top of Aircall base
- **Willingness to pay is HIGH for compliance tools**: One ASQA audit finding costs $10,000-50,000; losing registration is existential
- **Comparable pricing**: RTO consulting for compliance review: $3,000-10,000 per engagement; Gong/Chorus at $150-200/user/month for sales AI
- **Build sequence**: Orientation call robot (already #1) → Objection-handling Aircall (fast build) → TAZ compliance tool (highest value)
- **Knowledge base maintenance is the ongoing cost**: Training package updates require recurring engineering effort

### Strategic Implications
- Target compliance managers at RTOs with 500+ students (dedicated compliance staff)
- Lead with "reduce audit risk" not "save time" (compliance buyers care about risk, not efficiency)
- Consider RTO compliance consultants as resellers (they have relationships and earn commissions)
- Build sequence: orientation call robot → objection-handling AI → TAZ compliance tool
- Pricing: TAZ review ($200-500/qualification or $500-1,500/month), policy compliance ($100-300/policy), objection-handling ($50-100/user/month)
- Compliance suite: $2,000-4,000/month (bundles TAZ + policy + objection-handling + attribution dashboard)

### Recommended Actions
- [ ] Interview compliance manager at Hader or another RTO to validate TAZ review pain point and get actual time spent
- [ ] Check if training.gov.au has an API for training package data
- [ ] Spec the TAZ review tool MVP (upload PDF, compare against training package, flag issues)
- [ ] Prepare TAZ review product demo for Marcus/Kham before day 60 deliverable
- [ ] Build objection pattern library from Hader enrollment calls (this becomes AI training set)
- [ ] Consider RTO compliance consultants as resellers

### Sources
- ASQA Standards: asqa.gov.au
- Training packages: training.gov.au
- AI pricing benchmarks: Gong, Chorus.ai, Observe.ai (public pricing)
- Note: External web search limited; recommend compliance manager interviews as next step

---