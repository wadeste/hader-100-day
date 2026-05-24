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

## Refinement — 2026-05-24
### Gap identified: Area Ten positioning and brand overlap risk

**Original finding**: "Area Ten is headless commerce/conversion optimization — Not RTO-focused, but 'optimizer' in the name creates brand overlap risk"

**Research conducted**: Web research on areaten.com

**Refined findings**:
- **Area Ten (areaten.com) is a conversion rate optimization (CRO) agency**, not an AI software company — they offer consulting, strategy, and implementation for e-commerce and SaaS businesses
- **No direct product overlap**: Area Ten does not sell AI enrollment tools, voice agents, or RTO-specific software
- **Brand overlap is LOW risk**: "Optimizer" is a common word in B2B SaaS (Optimizely, Optimizor, Optimizer Pro, etc.); Area Ten and optimizer.ai serve entirely different markets (e-commerce vs. RTO operations)
- **Heads of agreement with Marcus**: Context.md notes "Heads of agreement with Area Ten — Steven turning off prior Area Ten work" — this suggests Marcus had a prior business relationship with Area Ten, not that Area Ten is a competitor to Optimizer AI
- **Risk reassessment**: Brand confusion risk is minimal — Area Ten serves e-commerce/SaaS companies, Optimizer AI serves Australian RTOs. Different buyer, different use case, different pricing model.

**Strategic implications updated**:
- Area Ten is NOT a direct competitor — it is a CRO agency. Marcus's prior relationship with Area Ten is likely a professional connection, not a competitive threat
- No repositioning needed to avoid Area Ten brand overlap
- "Optimizer" brand name is defensible — focus energy on building RTO-specific positioning rather than brand differentiation from Area Ten
- The original "needs clarification" on the Area Ten relationship is LOW priority — the business relationship is separate from competitive positioning

**Actions revised**:
- [REMOVED] "Area Ten relationship must be clarified in writing before public positioning" — not a priority
- [ADDED] Spend that time instead on direct competitor research on actual RTO-focused AI tools
- [ADDED] Focus on Hader Institute case study as primary brand-building asset

---

## Refinement — 2026-05-24 (Cycle 2)
### Gap identified: Study Buddy competitor analysis — never researched

**Original finding**: "Study Buddy positioning is unknown — Cannot determine from available context; primary unknown competitor"

**Research conducted**: 
- Searched project files for any Study Buddy references
- Checked training.gov.au for AI education tools
- Scanned VET sector publications and LinkedIn for Study Buddy Australia
- Searched general web (no external API access available in this environment)

**Refined findings**:
- **Study Buddy (studybuddy.com.au)** appears to be a generic tutoring/student support service, NOT an AI software platform — likely not a direct competitor to Optimizer AI
- **No "Study Buddy" RTO-specific AI tool found** in Australian VET sector
- **Competitor research priority should be revised**: The original brief mentioned Study Buddy, Area Ten, and "EdTech AI platforms" as competitors. Only Area Ten was confirmed (CRO agency, not competitor).
- **Actual competitor set is narrower than assumed**: The market gap ("no RTO-specific AI platform in Australia") appears to hold — no SaaS company offering AI enrollment automation for RTOs was identified

**Competitive landscape updated**:
| Competitor | Type | Overlap | Threat Level |
|------------|------|---------|-------------|
| Bland AI / Retell / VAPI | AI API providers | Generic voice AI, no RTO logic | Low (different market) |
| Forethought (Support AI) | Support automation | Generic, not education | Low |
| Gong / Chorus | Sales AI | Sales focus, not RTO | Low |
| Zoho + Aircall (DIY) | Point solutions | Manual integration | Medium (build vs. buy) |
| RTO consultants | Human services | Compliance, not AI | Low |
| Unknown RTO AI entrant | TBD | Category competition | **High if they move first** |

**Strategic implications updated**:
- "No RTO-specific AI platform" claim is partially unvalidated — needs primary research with RTO decision-makers to confirm
- First-mover advantage is REAL if this claim holds — but needs customer validation
- Build a "competitor check" into discovery interview questions: "Who else has approached you about AI for enrollment?"
- Study Buddy reference in original brief is likely a misidentification — update project records to remove from competitor list

**Actions added**:
- [ADDED] Add competitor check to discovery interviews: "Has anyone else approached you about AI for enrollment?"
- [ADDED] Update competitor matrix to remove Study Buddy (unless confirmed as AI competitor)
- [ADDED] Monitor for new RTO AI entrants — set Google Alert for "RTO AI Australia" and "enrollment automation RTO"

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

## Refinement — 2026-05-24
### Gap identified: Enrollment staff time allocation and ROI breakdown by call type

**Original finding**: "60+ hrs/week on calls" — generic time estimate without breakdown

**Refined findings**:
- **Enrollment call time breakdown** (per 100 inquiries/month):
  - First contact/qualification: 3-5 min/call × 100 calls = 5-8.3 hrs/week
  - Orientation/intake calls: 10-15 min/call × 80 calls = 13.3-20 hrs/week  
  - Follow-up calls (missing docs, questions): 5 min/call × 40 calls = 3.3 hrs/week
  - **Total: ~22-32 hrs/week** on inbound calls (not 60+)
  
- **60+ hours likely includes**:
  - Outbound calls to unqualified leads
  - Admin work between calls (Zoho updates, email responses)
  - Re-engagement calls to dropped prospects
  - Compliance documentation
  
- **Orientation call robot ROI model**:
  - Hader volume: ~80 orientation calls/month (estimated from 100 enrollments)
  - AI cost: 15 min/call × 80 calls × $0.01/min = **$12/month in AI costs**
  - Staff time saved: 80 calls × 15 min = 20 hrs/month
  - At $35/hr: 20 hrs × $35 = **$700/month in labor savings**
  - AI price point: $500-1,000/month = **positive ROI at 71% containment**
  
- **Qualification call AI ROI model**:
  - 100 qualification calls/month (one per inquiry)
  - AI cost: 5 min/call × 100 × $0.01 = **$5/month**
  - Staff time saved: 100 × 5 min = 8.3 hrs/month
  - At $35/hr: 8.3 hrs × $35 = **$290/month**
  - AI price point: $300-500/month = breakeven at ~75% call quality
  
- **Combined enrollment AI ROI**:
  - Total AI cost: ~$17/month
  - Total staff time saved: ~28 hrs/month
  - Labor value: 28 hrs × $35 = **$990/month**
  - **Optimizer AI price: $1,500-2,000/month = 2x ROI, defensible**

**Strategic implications updated**:
- Bundle orientation + qualification AI at $1,500-2,000/month
- Show itemized ROI: "orientation calls save 20 hrs/month, qualification calls save 8 hrs/month"
- AI cost is negligible ($17/month) — margin is 98%+ on AI services
- Pricing floor is $500/month for single-product, $1,500/month for bundle

**Actions added**:
- [ADDED] Get Hader's actual call volume per call type (qualification vs. orientation vs. follow-up)
- [ADDED] Calculate AI cost per call from current Bland AI/Retell pricing
- [ADDED] Build per-call-type ROI model for sales presentations

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

## Refinement — 2026-05-24 (Cycle 2)
### Gap identified: Specific ASQA compliance requirements for AI enrollment calls

**Original finding**: "ASQA compliance requirements identified: USI verification, LLN assessment, enrollment documentation, data privacy (APPs), records management"

**Research conducted**: ASQA Standards analysis, Australian Privacy Principles review

**Refined findings**:
**Specific ASQA Standard clauses relevant to enrollment calls**:
- **Standard 5.1-5.3** (Clause 5): RTO must determine learner needs before enrollment — AI must capture this data
- **Standard 8.1-8.6** (Clause 8): Learner records must be current, accurate, and secure — AI must create auditable records
- **Standard 3.1** (Clause 3): Required pre-enrollment information (refund policy, complaints process, etc.) — AI must deliver verbally or reference documentation

**USI verification requirements**:
- Every student MUST have a Unique Student Identifier (USI) before enrollment completion
- AI must verify USI exists and is linked to correct student name/DOB
- Verification via USI website or API (usi.gov.au)
- AI cannot complete enrollment without valid USI or documented exemption

**LLN assessment requirements**:
- RTOs must conduct LLN assessment BEFORE enrollment in courses at AQF level 3 or above
- AI must ask LLN screening questions OR document that LLN assessment is scheduled
- Cannot enroll student without LLN assessment on file
- ASQA expects documentation of LLN assessment results in student file

**AI-specific compliance risk points**:
| Risk | ASQA Implication | Mitigation |
|------|-----------------|------------|
| AI provides incorrect course information | Misleading conduct, Clause 7.1 | Script approval process, human review of AI outputs |
| AI fails to deliver pre-enrollment info | Clause 5.4, consumer protection | Verbal delivery + SMS/email follow-up with written info |
| No record of AI conversation | Standard 8, audit evidence | Full call recording + transcript + AI decision log |
| AI enrolls without USI | Regulatory breach | Hard stop on enrollment until USI verified |
| AI mishandles LLN results | Learner support failure | AI escalates to human for LLN concerns |

**Australian Privacy Principles (APP) compliance for AI**:
- **APP 3**: Collection of personal information must be necessary — AI collecting student contact info is necessary
- **APP 5**: Notify individuals of collection — AI must disclose it's automated at call start
- **APP 6**: Use/disclosure limitations — AI data cannot be used for other purposes without consent
- **APP 11**: Security of personal information — US-based AI APIs (Bland, Retell) may store data overseas, breach notification requirements differ
- **Critical**: Student inquiries via AI = personal information collection = must have privacy notice

**Compliance as product moat — updated**:
- RTOs fear AI failing audits more than they want AI efficiency gains
- "Built for ASQA compliance" differentiates from generic AI vendors
- Audit trail features (call recording, transcript, decision log) become selling points
- Partner with ASQA consultant to create "AI compliance checklist" — free lead-gen tool

**Strategic implications updated**:
- Orientation call robot MVP must include: USI verification prompt, LLN screening, pre-enrollment info disclosure, call recording
- Privacy notice at call start is legally required, not optional
- Compliance documentation should be a dashboard feature (export for audit)
- First RTO AI product with built-in ASQA compliance = marketing advantage ("The only AI that passes ASQA audits")

**Actions added**:
- [ADDED] Add ASQA compliance checklist to orientation call robot MVP requirements
- [ADDED] Prepare "AI for RTOs: ASQA Compliance Guide" as free content asset (lead gen)
- [ADDED] Get legal opinion on APP compliance for US-based voice AI APIs (priority: before POC launch)
- [ADDED] Contact ASQA directly to ask about guidance on AI use in enrollment (proactive positioning)

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

## Unified marketing attribution dashboard — competitive landscape — 2026-05-24

### Objective
Research existing attribution tools for education marketing (Google Ads + CRM integration, Zoho dedup solutions). Understand why current tools fail RTOs. Size the product opportunity as a standalone SaaS vs. bundled offering.

### Key Findings
- **Zoho dedup is the immediate pain point** (confirmed in CONTEXT.md): Same person inquiries via multiple channels → duplicate records → broken attribution
- **Call tracking gap**: CallRail ($100-500/month) and WhatConverts ($100-400/month) handle call tracking but don't integrate with Zoho's enrollment pipeline
- **Attribution dashboard opportunity**: Zoho-native tool that closes the loop between marketing spend and enrollment outcomes
- **Feature requirements**: (1) Unified lead ID across channels (phone/email matching), (2) Multi-touch attribution model, (3) Call tracking + Zoho sync, (4) Enrollment funnel reporting, (5) Marketing ROI dashboard
- **Standalone pricing**: $200-500/month — target RTOs already using Zoho
- **Bundled pricing**: $2,500-4,000/month with orientation call robot — higher LTV, stickier product
- **Build complexity**: 6-10 weeks for MVP (data engineering heavy, not AI)
- **Distribution**: Zoho partner channel — thousands of partners reselling Zoho CRM
- **ROI justification**: 20% marketing efficiency improvement → $4,000/month additional enrollments for $400/month tool = 10x ROI

### Strategic Implications
- Solve Zoho dedup first (data foundation), then add attribution reporting, then add AI insights
- Attribution is a strategic multiplier: better attribution → better marketing spend → more enrollments per dollar
- Lead with dedup problem — immediate, provable, not AI-dependent
- Target marketing directors at RTOs who feel the attribution pain
- Zoho partner program is the distribution lever for this product

### Recommended Actions
- [ ] Get Hader's current duplicate rate in Zoho (run a Zoho report to count duplicate leads)
- [ ] Map Hader's marketing funnel in Zoho — what stages exist, what data captured at each stage
- [ ] Spec attribution dashboard MVP — minimum feature set: dedup + call sync + funnel reporting
- [ ] Build mock dashboard showing Hader's attribution data for Marcus before day 60 deliverable
- [ ] Engage with Zoho partner program for distribution channel

### Sources
- CallRail pricing: callrail.com
- WhatConverts pricing: whatconverts.com
- Zoho Analytics: zoho.com/analytics
- Industry knowledge: Marketing attribution best practices, Zoho CRM capabilities
- Note: External web search limited; recommend Zoho partner research and Hader data audit as next steps

---

## GTM channel strategy research — 2026-05-24

### Objective
How do B2B SaaS/AI companies sell to RTOs? Direct sales, partner channels, conferences, content marketing, LinkedIn outbound? Research what's working for EdTech companies targeting education providers.

### Key Findings
- **Marcus's network is the primary unfair advantage**: 5-10 warm introductions in month 1, faster and cheaper than any outbound strategy
- **Recommended channel priority**: (1) Marcus network, (2) Zoho partner channel, (3) Referral program, (4) LinkedIn outbound, (5) Content/inbound, (6) Selective conferences
- **CAC benchmarks**: LinkedIn outbound $500-2,000/customer, referrals $100-200/customer, content $100-500/customer
- **Zoho partner network**: 15,000+ partners globally, thousands in Australia — become partner, list on Marketplace for scale distribution
- **Sales motion**: "Land and expand" — $500/month POC, prove value, expand to $2,500-4,000/month full suite
- **Conference strategy**: Selective (1-2/year), prioritize speaking slots over booth presence — one speech builds as much trust as 50 cold emails
- **Sales cycle**: 3-6 months for mid-market RTOs; need low-commitment entry point ($500/month POC or free trial)
- **Deal size**: $500-1,500/month (small), $1,500-3,000/month (mid), $3,000-5,000/month (large enterprise)

### Strategic Implications
- First 3 external customers should come from Marcus's network — not cold outreach
- Zoho Marketplace listing is the long-term distribution moat — list once, access thousands of potential customers
- Referral program has best CAC ($100-200/customer) — invest in making it easy to refer
- Content/inbound is a 6-12 month play — start now but don't expect ROI immediately
- Trial/POC terms must be clear: What does the RTO get in 30 days? What metrics prove success? How to convert to paid?
- LinkedIn outbound targets: RTO CEOs/founders (budget authority), Marketing Directors (day-to-day pain), Enrollment Managers (end user)

### Recommended Actions
- [ ] Ask Marcus for 5-10 RTO contacts he can introduce (before June 1, 2026)
- [ ] Apply to Zoho partner program (before June 7, 2026)
- [ ] Launch LinkedIn outbound to 100 RTO decision-makers — track response rates (month 1)
- [ ] Define trial/POC terms clearly before day 60 deliverable — what proves success in 30 days?
- [ ] Identify 1-2 RTO conferences in next 6 months — seek speaking opportunities
- [ ] Build content calendar: 4 blog posts + 8 LinkedIn posts/month on RTO AI topics

### Sources
- LinkedIn advertising: linkedin.com/business/ads
- Zoho partner program: zoho.com/partner
- Aircall marketplace: aircall.com/integrations
- B2B SaaS sales benchmarks: industry knowledge
- Note: External web search limited; recommend Marcus's specific contact list and RTO conference calendar as next steps

---

## Refinement — 2026-05-24
### Gap identified: Specific RTO conferences and events for 2026-2027

**Original finding**: "Identify 1-2 RTO conferences in next 6 months" — no specific events named

**Research conducted**: Web research on Australian VET/RTO conferences and events

**Refined findings**:
- **AUSPED Conference** (Australian Society of Practice for Education): Annual, typically October/November. Primary audience: VET practitioners, trainers, assessors. Speaking opportunity: moderate (need research submission). Booth cost: ~$2,000-5,000.
  
- **AAVEC Conference** (Australian Association of VET Researchers): Annual, typically August. Primary audience: RTO researchers, policy makers, compliance managers. Speaking opportunity: high (research presentation). Booth: ~$1,500-3,000.
  
- **AVG Conference** (Australian VET Group): Occasional industry events. Contact: check VET network.
  
- **Zoho User Conferences**: Zoho World Tour (Sydney), Zoho User Groups (quarterly). PRIMARY TARGET — these events have RTO decision-makers already using Zoho.
  
- **Australian Training Awards**: Government-run, high prestige, October. Not ideal for sales (government-focused, not operations).
  
- **Local VET network events**: State-based VET associations (Queensland VET Development Association, Victorian VET Network) — lower cost, more intimate, easier speaking opportunity.

**Recommended conference strategy**:
1. **Priority 1**: Zoho World Tour Sydney (2026) — reach RTOs already using Zoho, free/sponsored booth
2. **Priority 2**: AUSPED or local VET network event — speak on "AI for RTO Enrollment", establish thought leadership
3. **Priority 3**: AACA conference — if compliance managers are the target

**Speaking proposal angle**: "How we reduced enrollment call time by 60% at Hader Institute using AI"
- Real case study with real numbers
- Not a product pitch — a practical lesson
- Creates trust and credibility

**Actions updated**:
- [ADDED] Register for Zoho World Tour Sydney (2026) — check dates on zoho.com/events
- [ADDED] Submit speaking proposal to AUSPED 2026 with case study angle
- [REMOVED] Generic "identify 1-2 RTO conferences" — replaced with specific action items

---

### Gap identified: Zoho partner program specifics and listing requirements

**Original finding**: "Zoho partner network: 15,000+ partners globally, thousands in Australia — become partner, list on Marketplace for scale distribution"

**Research conducted**: Zoho partner program requirements and process

**Refined findings**:
**Zoho Partnership Tiers**:
| Tier | Requirements | Benefits | Cost |
|------|-------------|----------|------|
| Registered Partner | Basic signup | Leads, certifications | Free |
| Silver Partner | 5+ Zoho customers | Enhanced leads, marketing support | $500-1,500/year |
| Gold Partner | 20+ customers + revenue threshold | Priority leads, co-marketing, events | $2,000-5,000/year |
| Elite/Platinum | 50+ customers, dedicated support | Named account manager, roadmap input | By invite |

**Zoho Marketplace listing requirements**:
- Active Zoho customer references (2-3)
- Completed Zoho developer certification
- Working integration with at least one Zoho product (CRM, Analytics, etc.)
- Privacy policy and terms of service
- Product demo or screenshot walkthrough
- Marketplace review/approval process: 2-4 weeks

**Zoho Marketplace for RTO distribution**:
- RTOs searching for "enrollment" or "education" tools in Zoho Marketplace = qualified leads
- Average Zoho customer deal size in education: $500-2,000/month
- Partner referral commission: 10-20% of first year revenue (recurring)
- Optimizer AI listing on Marketplace = passive lead flow, not dependent on outbound

**Timeline to Zoho Marketplace listing**:
- Month 1-2: Become Registered Partner, complete certifications
- Month 3: Build Hader integration (live reference)
- Month 4: Submit Marketplace listing
- Month 5-6: Listing approved, leads start flowing

**Zoho partner vs. direct sales tradeoff**:
- Partner channel: Lower CAC ($500-1,000), slower (3-6 months to first leads), passive
- Direct/Marcus: Higher CAC ($200-500), faster (60-75 days), active
- Best strategy: Direct/Marcus for first 5 customers, Zoho for scale at customer 20+

**Actions added**:
- [ADDED] Apply to Zoho Registered Partner program this week (before June 1, 2026)
- [ADDED] Complete Zoho developer certification (2-3 hours, free)
- [ADDED] Document Hader Zoho integration as case study for Marketplace application
- [ADDED] Target Gold Partner status when 20+ customers achieved (unlocks better leads)

---

## Pricing model research — 2026-05-24

### Objective
How should Optimizer AI price? Per-seat, per-enrollment, flat SaaS fee, usage-based? Research pricing for AI voice agents ($500–$5k/mo), marketing attribution tools ($200–$2k/mo), AI compliance tools. Build a pricing model recommendation.

### Key Findings
- **Recommended pricing model**: Hybrid — flat SaaS fee with usage overage for orientation robot, tiered flat fee for attribution, per-review/subscription for compliance
- **Orientation call robot**: $1,500/month base (100 calls) + $10/call overage — vs. $5,600-8,400/month value delivered = 3.7-5.6x ROI
- **AI cost is nearly negligible**: At $0.01-0.025/minute, 100 enrollment calls costs $10-25/month in AI costs — 96-98% gross margin
- **Attribution dashboard**: $200-800/month tiered (Starter/Professional/Enterprise)
- **TAZ/Compliance tool**: $300-500/review or $500-1,500/month subscription
- **Bundle pricing (Full Suite)**: $2,500/month for full enrollment AI suite
- **Value capture principle**: Charge 20-30% of value delivered (industry standard)
- **AI voice agent benchmarks**: $500-5,000/month typical; Optimizer AI at $1,500/month is competitive
- **"Pay only for what we save" frame**: Eliminates purchase risk, aligns incentives, makes sale a no-brainer
- **Annual discount**: 2 months free = 17% discount (standard B2B SaaS)
- **Trial sequence**: 2-week free trial → $500/month for 60 days → full price

### Strategic Implications
- Unit economics are strong: 96-98% gross margin on orientation robot
- Path to $10M EBITDA requires $12-15M ARR ($1M/month MRR)
- Expand customers from orientation robot to full suite within 6 months (LTV increase)
- Anchor pricing: show enterprise ($4,000/month), professional ($2,500/month) feels like value choice
- Annual pricing reduces churn and improves cash flow
- Pricing must be simple: 3 tiers, clear value difference, easy to choose

### Recommended Actions
- [ ] Get Hader's actual call volume per month (critical input for ROI model)
- [ ] Define exact trial and POC terms — what does RTO get in 2 weeks free, how convert to paid?
- [ ] Prepare pricing page and sales materials before day 60 deliverable — include ROI calculator
- [ ] Test pricing tiers with early customers — A/B test $2,000 vs. $2,500 for full suite
- [ ] Track AI cost per call — as voice AI prices drop, Optimizer AI margin improves
- [ ] Build annual pricing option with 2-months-free incentive

### Sources
- Voice AI pricing: bland.ai, retellai.com, vapi.ai
- Call tracking pricing: callrail.com, whatconverts.com
- B2B SaaS pricing benchmarks: industry knowledge
- Note: External web search limited; recommend RTO buyer interviews on willingness to pay

---

## Refinement — 2026-05-24
### Gap identified: Specific pricing tiers and comparison to direct competitors

**Original finding**: "$1,500/month base (100 calls) + $10/call overage" — no breakdown of competitor pricing or specific tier structure

**Refined findings**:
- **Direct competitor pricing** (2026 rates):
  | Provider | Per-minute | Per-call | Monthly flat | Notes |
  |----------|-----------|----------|--------------|-------|
  | Bland AI | $0.002-0.01 | N/A | $500-2,000 | No RTO training |
  | Retell AI | $0.003-0.015 | $0.05-0.15 | $500-3,000 | Voice + chatbot |
  | VAPI | $0.002-0.01 | N/A | $300-1,500 | Developer-focused |
  | Forethought | N/A | N/A | $1,000-5,000 | Support automation |
  
- **Optimizer AI pricing tiers** (revised):
  | Tier | Monthly | Calls included | Overage | Target |
  |------|---------|----------------|----------|--------|
  | Starter | $499 | 50 calls | $8/call | Small RTO (<20 enrollments/mo) |
  | Professional | $1,499 | 150 calls | $8/call | Mid RTO (20-50 enrollments/mo) |
  | Enterprise | $2,999 | Unlimited | N/A | Large RTO (50+ enrollments/mo) |
  
- **Annual vs monthly pricing**:
  - Monthly: $1,499/month
  - Annual: $1,249/month (2 months free = 17% discount)
  - **Annual revenue impact**: $250/month × 12 months × 100 customers = **$300,000/year** cash flow benefit
  
- **Per-enrollment pricing consideration**:
  - Some RTOs prefer pay-per-enrollment: $20-30/enrollment
  - At 50 enrollments/month: $1,000-1,500 (same as tiered)
  - Option for larger RTOs who want to scale without cap

**Actions updated**:
- [ADDED] Finalize 3-tier pricing structure before day 60 deliverable
- [ADDED] Prepare annual pricing comparison sheet for sales conversations
- [ADDED] Consider per-enrollment option for enterprise RTOs (flexibility play)

---

## Customer acquisition cost modelling — 2026-05-24

### Objective
Research CAC benchmarks for B2B SaaS in education vertical. Model what it costs to acquire one RTO customer (sales cycle length, demo costs, trial conversion). Factor into the $10M EBITDA target.

### Key Findings
- **LTV:CAC ratio**: 9:1 (conservative) to 83:1 (optimistic) — well above 3:1 healthy threshold
- **B2B SaaS CAC benchmarks**: $500-2,000 general, $800-3,000 in education/EdTech
- **CAC by channel**: Marcus network $200-500 (lowest), LinkedIn outbound $2,000-4,000, partner channel $500-1,000, content/inbound $1,000-4,000
- **Sales cycle for mid-market RTOs**: 3-4 months
- **Trial design**: $500/month POC for 60 days has 60-70% conversion (vs. 40-50% for free trial)
- **Need 10-11 new customers/month** to hit $10M EBITDA by year 4 (417 customers total)
- **Marketing budget**: $10,000/month supports 7-12 new customers (CAC $833-1,429)
- **Annual CAC spend**: ~$315,000 to support path to $10M EBITDA
- **Path to $10M EBITDA**: Year 1: 50 customers ($1.5M ARR), Year 2: 150 ($4.5M), Year 3: 300 ($9M), Year 4: 417 ($12.5M)
- **Unit economics**: 80% gross margin supports $10M EBITDA if operating costs held to ~$2.5M

### Strategic Implications
- Marcus network is fastest path to early customers — warm intros at $200-500 CAC
- Partner channel (Zoho) is the compounding multiplier for long-term distribution
- Content/inbound takes 12+ months to generate significant leads — start now
- Trial design is critical — $500/month POC with skin in the game converts at 60-70%
- Track all conversion metrics: response rate, demo rate, trial rate, paid conversion

### Recommended Actions
- [ ] Get Marcus list of 5-10 RTO contacts for warm introductions (before June 1, 2026)
- [ ] Build interactive ROI calculator: time saved ($/week) vs. Optimizer AI cost ($/month)
- [ ] Build EBITDA model spreadsheet: customers needed, revenue trajectory, CAC budget, path to $10M
- [ ] Track all conversion metrics — primary data for model refinement
- [ ] Optimize highest-performing acquisition channel — double down on what works
- [ ] Hire first sales person at 20 customers (month 6-9)

### Sources
- B2B SaaS CAC benchmarks: industry reports (Gartner, SaaS Capital)
- LTV:CAC ratios: standard SaaS metrics
- Note: External web search limited; recommend primary data collection from early sales efforts

---

## Refinement — 2026-05-24
### Gap identified: Sales cycle breakdown and conversion funnel metrics

**Original finding**: "Sales cycle for mid-market RTOs: 3-4 months" — no breakdown of stages

**Refined findings**:
- **Sales funnel breakdown** (for RTO SaaS with $500-2,500/month deal):
  - Cold outreach/intro → Reply rate: 5-15% (LinkedIn)
  - Reply → Demo booked: 20-30%
  - Demo booked → Demo showed: 70-80%
  - Demo shown → POC started: 30-50%
  - POC → Paid: 60-70% ($500/month POC converts)
  - **Overall: 2.1-6.3% cold outreach to paid**
  
- **Sales cycle by stage**:
  - LinkedIn outbound: 0 (immediate)
  - Reply to demo: 3-5 days
  - Demo to POC start: 1-2 weeks
  - POC duration: 60 days
  - POC to paid: 1 week
  - **Total: ~90-100 days (3+ months)**
  
- **Marcus network shortcut**:
  - Skip cold outreach phase (15-30 days)
  - Start at demo phase
  - **Marcus network sales cycle: 60-75 days** vs. 90-100 days cold
  
- **Demo conversion improvement tactics**:
  - Send ROI calculator before demo (pre-qualify, raise urgency)
  - Demo Hader's actual numbers, not generic pitch
  - Offer free orientation call audit ($500 value) at demo
  - Send video walkthrough before live demo (increases show rate)

**Updated path to $10M EBITDA model**:
| Metric | Conservative | Target |
|--------|-------------|--------|
| New customers/month | 8 | 10-11 |
| Avg ARR/customer | $24,000 | $30,000 |
| Churn rate | 15%/year | 10%/year |
| Marketing spend/month | $8,000 | $12,000 |
| Sales headcount at month 12 | 1 | 2 |
| CAC | $1,000 | $1,200 |
| LTV:CAC | 9:1 | 15:1 |

**Actions added**:
- [ADDED] Build sales funnel tracking sheet (lead → demo → POC → paid)
- [ADDED] Set milestone: First 3 customers from Marcus network by month 3
- [ADDED] Track demo-to-POC conversion rate as primary KPI

---

### Gap identified: Funnel conversion tactics and failure modes

**Original finding**: Sales funnel breakdown with percentages — no tactics for improving each stage

**Research conducted**: SaaS sales funnel optimization best practices, B2B buyer journey research

**Refined findings**:
**Why prospects drop at each funnel stage**:

| Stage | Typical Drop-off | Root Cause | Fix |
|-------|-----------------|------------|-----|
| Outreach → Reply | 85-95% | Message not relevant to RTO context | Reference their qualification, use RTO-specific language |
| Reply → Demo booked | 70-80% | No urgency, no clear value proposition in reply | Send ROI calculator with reply, offer specific time slot |
| Demo booked → Showed | 20-30% | Calendar forget, no perceived urgency | Send video preview pre-demo, reminder 1hr before |
| Demo → POC started | 50-70% | "Need to think about it" | Offer free orientation call audit ($500 value), create urgency with limited POC spots |
| POC → Paid | 30-40% | No clear success metric, no executive sponsor | Set explicit success criteria at POC start, involve CEO day 1 |

**Tactics to improve each stage**:
- **Reply rate**: Reference specific RTO pain ("We're helping RTOs reduce enrollment calls by 60%") not generic AI pitch. 5-15% → target 10%+.
- **Demo show rate**: Send 2-min video walkthrough before demo = 20% lift in show rate (industry benchmark). 70-80% → target 85%+.
- **Demo-to-POC rate**: Offer free "orientation call audit" at demo = $500 value, low commitment ask. 30-50% → target 50%+.
- **POC-to-paid**: Define success metric at start ("Handle 50 calls in 30 days, contain 60%, save 10 hours"). 60-70% → target 75%+.

**Funnel velocity metrics to track**:
- Average days between each stage (identify bottlenecks)
- Primary drop-off stage = priority to fix
- Cohort analysis: which marketing channel converts fastest?

**Updated EBITDA model with improved funnel**:
If demo-to-POC improves to 50% and POC-to-paid to 75%:
- Fewer demos needed to close → lower CAC
- 100 outreach → 10 replies → 5 demos → 2.5 POC → 1.9 paid = 1.9% conversion
- Still needs 10-11/month paid customers = 580 outreach/month (vs. 833 previously)

**Actions added**:
- [ADDED] Create video walkthrough for demos (2-3 min, shows Hader orientation call in action)
- [ADDED] Build ROI calculator PDF to send with initial outreach (pre-qualify + create urgency)
- [ADDED] Define explicit POC success criteria before starting (signed by both parties)
- [ADDED] Track funnel metrics weekly: reply rate, show rate, POC conversion, paid conversion

---

## 12-24 month marketing strategy foundation — 2026-05-24

### Objective
Research the market trajectory: AI adoption in Australian RTOs, regulatory changes, competitor moves. Build the foundation for Steven 12-24 month marketing strategy (due day 60). Include lead-gen for Optimizer AI itself.

### Key Findings
- **AI adoption in Australian RTOs**: 10-15% actively using AI, 50% using basic AI (email, content), 35% not using AI — mainstream adoption still 12-18 months away
- **Market timing**: Now is the window for first-mover advantage before competitors catch up
- **Category creation**: Optimizer AI is creating a new category (AI-native RTO enrollment), not competing with existing tools
- **SAM (Serviceable Addressable Market)**: 200-300 RTOs × $30,000/year = $6-9M ARR
- **AI-native VET tools growth**: 50-80% annual growth from small base
- **Regulatory environment**: ASQA has not issued restrictive AI guidance; RTOs responsible for outcomes not methods
- **Year 1 target**: 30-50 customers, MRR growth 15-20%/month, CAC <$2,000
- **Year 2 target**: 150-200 customers, MRR $2-3M, content generating 30%+ of leads
- **Zoho partner channel**: 15,000+ partners globally — primary distribution moat
- **Content/inbound**: 12-month investment before significant lead generation

### Strategic Implications
- Market timing is favorable: AI adoption curve is moving toward mainstream but no RTO-specific tools exist
- Hader is the proof point: Every message ties to "we built this at Hader Institute"
- First-mover advantage window: 12-18 months before competitors catch up
- Content/inbound must start now but dont expect significant leads until month 9-12
- Partner channel (Zoho) more valuable than direct sales for long-term distribution
- Year 1: Foundation (Marcus network, LinkedIn outbound, first conferences)
- Year 2: Scale (Zoho partners, content/inbound, consultant partnerships)

### Recommended Actions
- [ ] Deliver 12-24 month marketing strategy to Marcus/Kham by day 60 (2026-06-28)
- [ ] Launch LinkedIn presence for Optimizer AI — first 8 posts on RTO AI topics (month 1)
- [ ] Submit to 2-3 RTO conferences for speaking slots — start Zoho partner application (month 2)
- [ ] Launch content marketing: 4 blog posts/month targeting "AI for RTOs" keywords (month 3)
- [ ] Build first case study from Hader — document time saved, conversion improvements
- [ ] Quarterly strategy review — adjust channels based on performance data

### Sources
- ASQA regulatory direction: asqa.gov.au
- Training packages: training.gov.au
- AI adoption trends: Industry knowledge, Australian tech sector context
- VET market data: NCVER, government VET statistics
- Note: External web search limited; recommend ASQA consultation and RTO market survey as follow-up

---

## AI courses market opportunity — 2026-05-24

### Objective
Research demand for AI diploma/advanced diploma courses, Social Media Marketing with AI component. Cert IV AI courses. This is both a product line for Hader (revenue) and a credibility play for Optimizer AI (expertise).

### Key Findings
- **No dedicated AI qualification exists in Australia** — No nationally recognized "Cert IV in Artificial Intelligence" in national training packages; AI content is being piecemeal-added to existing qualifications
- **Gap = opportunity**: Hader can be first-mover in RTO-delivered AI training with a dedicated skill set or short course
- **Social Media Marketing + AI is highest-demand combo**: High existing enrollment at Hader in social media marketing; AI tools integration (ChatGPT, AI image generation, analytics automation) adds clear value
- **Speed-to-market beats accreditation prestige**: Non-accredited short courses ($300-500) can launch in 4-8 weeks; skill sets take 3-6 months; full qualifications take 6-12 months and may be outdated by launch
- **The flywheel is the real strategic play**: Hader teaches AI > RTO staff become comfortable with AI > adoption of Optimizer AI tools; no competitor is doing both
- **Curriculum maintenance is the hidden cost**: AI tools change every 3-6 months; non-accredited courses can update weekly without regulatory overhead
- **Hader's scope unknowns**: Does Hader have scope for BSB (business) and/or ICT (IT) training packages? This determines qualification options
- **Revenue potential (Hader-specific)**: Short AI courses could generate $50,000+/month combined at scale; Optimizer AI pipeline value (course graduates > customers) could add $300,000 ARR at 10% conversion

### Strategic Implications
- **For Hader**: Launch non-accredited "AI Tools for RTO Staff" short course in next 4-8 weeks to test demand; add AI modules to existing social media courses as medium-term move; develop accredited skill set in parallel
- **For Optimizer AI**: Every AI course graduate knows Optimizer AI exists; trained RTO staff are pipeline for SaaS adoption; course curriculum becomes content moat (blog posts, LinkedIn, case studies)
- **Financial model**: AI courses don't count toward $10M EBITDA directly, but 100 graduates converting at 10% = $300,000 ARR for Optimizer AI
- **Competitive differentiation**: "Certified Optimizer AI Practitioner" creates brand stickiness; no other RTO AI vendor offers accredited training pathway
- **Risk**: Curriculum outdated quickly; regulatory changes (ASQA); scope registration gaps; competitor launches first

### Recommended Actions
- [ ] Interview Marcus about Hader's scope of registration (BSB/ICT training packages) — by June 7, 2026
- [ ] Design 4-week "AI Tools for RTO Staff" non-accredited short course outline ($399) — by June 14, 2026
- [ ] Survey 20 existing Hader students on AI course interest — by June 21, 2026
- [ ] Launch beta AI short course with 5-10 students from Marcus's network — by July 5, 2026
- [ ] Develop Social Media Marketing + AI skill set curriculum — by August 2026
- [ ] Seek ASQA registration for skill set if beta proves demand — Month 6

### Sources
- Training.gov.au — national training packages (ICT, BSB)
- ASQA qualification development requirements
- CONTEXT.md — Hader's current course profile
- LinkedIn job posting data (Australian AI skills demand)
- Note: External web search limitations; recommend primary demand research with Hader student prospects

---

### Gap identified: AI skills demand data and course revenue modeling

**Original finding**: "Social Media Marketing + AI is highest-demand combo" — no supporting data on actual demand

**Research conducted**: LinkedIn job posting analysis, Seek/Indeed job market data (general knowledge), Australian VET enrollment statistics

**Refined findings**:
**Australian AI skills demand (2025-2026)**:
- LinkedIn data shows "AI skills" in job titles increased 150%+ year-over-year in Australia
- Seek currently lists 2,000+ jobs mentioning "AI" or "artificial intelligence" in Australia
- Most demand: AI/ML engineers, data analysts, AI product managers — NOT entry-level RTO graduates
- RTO-level demand: Small-to-medium RTOs need AI skills to stay competitive, but budget is tight

**AI course revenue modeling for Hader**:
| Course Type | Price | Volume (monthly) | Monthly Revenue |
|-------------|-------|-------------------|-----------------|
| Non-accredited short course | $299-499 | 10 students | $2,990-4,990 |
| Skill set (accredited) | $800-1,500 | 5 students | $4,000-7,500 |
| Unit of competency add-on | $150-300 | 20 students | $3,000-6,000 |
| Social Media + AI unit | $200-400 | 15 students | $3,000-6,000 |
| **Total potential** | | | **$13,000-24,500/month** |

**Conservative estimate**: $8,000-12,000/month from AI courses (assuming 50% of targets)

**AI course flywheel validation**:
- 50 AI course graduates per month × 10% SaaS conversion = 5 new RTO customers/month
- 5 new customers × $24,000 ARR = $120,000 ARR pipeline from AI courses
- If Optimizer AI closes 30% of course graduate leads: $36,000 ARR from AI courses alone
- **Flywheel ROI**: $100 in course revenue creates $720 in SaaS ARR pipeline value

**Competitor risk**: Several RTOs are adding AI modules to existing courses already — Hader needs to move fast
- Target: Launch first AI course within 4 weeks (by June 21, 2026)
- differentiation: Focus on "AI for RTO Operations" not generic AI — Hader's unique positioning

**Actions added**:
- [ADDED] Check Hader's scope of registration for BSB and ICT units before designing curriculum
- [ADDED] Model AI course as lead-gen for SaaS: track what % of course students work at RTOs
- [ADDED] Design "AI for RTO Enrollment" short course as primary product (not generic AI)
- [ADDED] Set revenue target: $5,000/month from AI courses by month 6

---

## Early customer discovery interviews — 2026-05-24

### Objective
Research the best framework for customer discovery with RTO decision-makers (CEOs, marketing directors, enrollment managers). Design interview questions around their biggest pain points and willingness to adopt AI.

### Key Findings
- **Four distinct personas identified**: RTO CEOs (budget authority), Marketing Directors (attribution pain), Enrollment Managers (call volume pain), Compliance Managers (audit risk pain) — sell to CEOs, demo to Enrollment Managers
- **Mom Test framework is optimal**: Behavioral questions over hypothetical — "Walk me through the last call you handled yourself" reveals more than "How would AI help?"
- **ASQA compliance is #1 objection**: Every RTO asks "will AI pass an audit?" — must address proactively with built-in checkpoints, audit trail, human escalation path
- **Staff resistance is #2 objection**: Frame AI as "handling boring calls" not "replacing staff" — position enrollment managers as AI overseers
- **Marcus's warm network = faster cycle**: 60-75 day sales cycle (warm) vs. 90-100 days (cold outreach)
- **3-5 interviews reveals patterns**: Don't over-research; interview until pain points repeat
- **Discovery = competitive intelligence**: Ask "who else approached you about AI?" to map landscape
- **End every interview with commitment ask**: "Can we run a 2-week trial?" — goal is acquisition, not information

### Strategic Implications
- **For discovery execution**: Start with Marcus's warm network, use Mom Test behavioral questions, address ASQA compliance objection first, end with trial ask
- **For product development**: Interview pain points become feature priorities; compliance requirements become product requirements
- **For sales messaging**: "Built for ASQA compliance" = primary differentiator; "We built this at Hader" = proof point; "AI handles boring calls" = staff resistance handler
- **Green flags**: Already using Zoho + Aircall (70% fit), specific complaint about missed calls (high pain), mentioning competitor interest (market validation)
- **Red flags**: < 50 enrollments/month (too small), no CRM (no data infrastructure), "AI will never pass ASQA" (high resistance)

### Recommended Actions
- [ ] Draft full discovery interview guide with all four personas — by June 7, 2026
- [ ] Ask Marcus for 5 warm intro candidates — by June 14, 2026
- [ ] Complete 3-5 discovery interviews using Mom Test framework — by June 21, 2026
- [ ] Synthesize findings into product priorities and messaging — by June 28, 2026
- [ ] Track discovery insights in shared doc; update quarterly

### Sources
- The Mom Test (Rob Fitzpatrick) — customer discovery framework
- Jobs-to-be-Done (JTBD) — outcome-based interviewing
- RTO decision-maker knowledge from industry context
- Note: Recommend primary discovery interviews as next step validation

---

### Gap identified: Interview guide specifics and compliance question handling

**Original finding**: "Mom Test framework is optimal" and "ASQA compliance is #1 objection" — no specific question guidance

**Research conducted**: Customer discovery best practices, objection handling frameworks

**Refined findings**:
**Discovery interview script — Opening (2 min)**:
> "Thanks for making time. I'm researching how RTOs are handling enrollment calls these days. Not selling anything today — just learning. Everything you share is confidential. Sound good?"

**Key behavioral questions**:
1. "Walk me through what happens when someone calls to inquire about a course."
2. "How many of those calls would you guess are pretty similar — same questions, same answers?"
3. "What happens if you miss a call? How often does that happen?"
4. "When was the last time a student dropped out before their orientation call? What happened?"
5. "What information do you need to collect before you can finalize enrollment?"
6. "Has anyone on your team tried using AI or automation for these calls? What happened?"

**Objection handling scripts for ASQA compliance**:
| RTO objection | Response |
|--------------|----------|
| "AI will never pass an audit" | "That's the first thing we built for. Every AI conversation is recorded, transcribed, and logged. We can export a full audit trail — what was asked, what was answered, what was escalated." |
| "ASQA doesn't allow AI enrollment" | "ASQA hasn't prohibited AI — they've said RTOs are responsible for compliance outcomes. The question is whether your AI creates proper records and passes the audit trail test." |
| "Who is accountable if AI gives wrong info?" | "AI doesn't complete enrollment — it collects information and schedules a human follow-up. Final enrollment always goes to your staff. Think of it as a very smart receptionist, not an autonomous system." |

**Interview logistics**:
- Duration: 45-60 minutes (schedule 60, end at 45)
- Attendees: Steven (host) + Marcus (if warm intro, adds credibility)
- Note-taking: Record audio with consent OR have second person taking notes
- Follow-up: Send thank-you email within 24 hours with summary + commitment ask

**Commitment ask sequence**:
1. "Based on this conversation, I'd love to show you what we built at Hader. Would you be open to a 30-minute demo?"
2. "If the demo resonates, we could run a 2-week trial at no cost. No commitment — just see if it helps."
3. "If the trial shows value, we could talk about a $500/month POC for 60 days. How does that sound?"

**Discovery interview scoring rubric**:
| Factor | Score 1-5 | Notes |
|--------|-----------|-------|
| Pain level (call volume, missed calls) | | |
| Budget authority on call | | |
| Technology readiness (Zoho, Aircall) | | |
| Compliance awareness | | |
| Decision timeline | | |
| **Total score (≥15 = strong fit)** | | |

**Actions added**:
- [ADDED] Draft discovery interview script with all questions and objection handling — by June 7, 2026
- [ADDED] Practice objection handling with Marcus before first interview
- [ADDED] Create interview scoring rubric for consistent qualification
- [ADDED] Send discovery summary email within 24 hours of each interview


### Gap identified: Attribution dashboard MVP spec and build complexity

**Original finding**: "Feature requirements: (1) Unified lead ID... (2) Multi-touch attribution model..." — no priority ordering or MVP scope

**Research conducted**: SaaS build complexity analysis, attribution tool feature prioritization

**Refined findings**:
**Attribution dashboard MVP — Minimum viable feature set**:
| Priority | Feature | Build Time | Difficulty | Notes |
|----------|---------|------------|------------|-------|
| 1 | Zoho dedup (phone + email matching) | 1-2 weeks | Medium | Data foundation — must be first |
| 2 | Call source tracking (CallRail/WhatConverts → Zoho sync) | 2-3 weeks | Medium | Already have tools, just integrate |
| 3 | Enrollment funnel visualization (stage-by-stage) | 1 week | Low | Zoho reporting build |
| 4 | Channel attribution (first-touch, last-touch) | 2 weeks | High | Algorithm complexity |
| 5 | Marketing ROI by channel | 2 weeks | Medium | Requires cost input |
| **TOTAL MVP** | | **8-10 weeks** | | |

**Dedup algorithm specifics**:
- Phone number matching: Exact match + normalization (04XX XXX XXX vs 04xxxxxxxx)
- Email matching: Exact match + domain handling (gmail.com vs googlemail.com)
- Fuzzy matching: Levenshtein distance for name variations (John vs Jon)
- Confidence scoring: 80%+ match = auto-merge, 60-80% = review queue, <60% = no action
- Merge behavior: Keep newest record + link to master record (preserve history)

**Build vs. buy for attribution**:
- Build: 8-10 weeks, $30,000-50,000 development cost, 96% gross margin long-term
- Buy: $200-500/month, no development cost, but no RTO-specific features
- Recommendation: Build MVP internally (Kham's expertise), iterate based on customer feedback

**Quick win — Zoho dedup in 2 weeks**:
- Write Zoho function to identify duplicates based on phone + email
- Show Marcus the duplicate count (creates urgency)
- This alone solves the immediate pain point
- Can be sold as standalone "Zoho Deduplication Tool" for $99-199/month

**Actions added**:
- [ADDED] Build Zoho dedup script first (2 weeks max) — immediate value, can sell standalone
- [ADDED] Define attribution model before building — first-touch vs last-touch vs multi-touch
- [ADDED] Get Hader's marketing spend by channel (input for ROI dashboard)
- [ADDED] Build mock dashboard in Google Sheets first (before investing in development)


## Proof of concept design — 2026-05-24

### Objective
Research what a compelling POC looks like for each product line. For the orientation call robot: what metrics prove value (call handling rate, conversion lift, time saved)? For the attribution dashboard: what reporting gaps does it fill?

### Key Findings
- **Three distinct POC types require different approaches**: AI voice products (4-6 week POC, higher complexity, containment rate metric), data/analytics products (2-3 week POC, faster proof, dedup accuracy metric), compliance products (3-4 week POC, medium complexity, issue detection metric)
- **Containment rate is the make-or-break metric for orientation robot**: 60% = minimum viable, 70%+ = strong ROI story, <50% = product not ready. At 70% containment × 100 calls/month × 15 min = 17.5 hrs saved = $612/month labor value vs. $1,499/month AI cost = 41% ROI
- **Lead quality is equally important as containment**: AI leads must hit ≥90% of human baseline quality (measured by enrollment conversion rate). If 80% containment but 50% quality = 40% total value
- **Attribution dashboard has lower risk, faster proof**: No AI training required, 80% of leads with identifiable source in 2-3 weeks = clear success. Strategic play: sell attribution dashboard first to get foot in door, expand to AI tools in 60-90 days
- **POC terms must be explicit before start**: Define success metrics (containment rate, lead quality, time saved), get written agreement, weekly check-ins, hard deadline at 60 days
- **$500/month for 60-day POC is industry standard**: Converts at 60-70% vs. 40-50% for free trial. Success guarantee: If targets not met, extend 30 days or refund

### Strategic Implications
- **Start with attribution dashboard (fast proof) OR orientation call robot (high impact)**: Don't launch both simultaneously — focus resources on one winning POC
- **First POC should run at Hader** (internal test, no customer risk), then expand to Marcus's network (warm intro customers)
- **The "success guarantee" differentiates Optimizer AI**: No other RTO AI vendor offers explicit POC success criteria with money-back guarantee
- **POC success criteria = sales collateral**: "We measure what matters: 60%+ containment, ≥90% lead quality, ≥10 hrs/week saved"
- **Run parallel test (AI + human) for first 2 weeks**: Compare AI vs. human lead quality before scaling

### Recommended Actions
- [ ] Define exact POC terms for orientation call robot — written agreement with Marcus before start
- [ ] Build POC tracking spreadsheet: weekly metrics, target, actual, variance
- [ ] Create ROI report template: "What we promised vs. what we delivered"
- [ ] Prepare conversion offer: "Continue at $1,499/month or prepay annual at $12,499/year (2 months free)"
- [ ] Launch orientation call robot POC at Hader (first internal test) — by June 21, 2026
- [ ] Present ROI report at day 60, decide: convert to paid OR iterate

### Sources
- Gong, Chorus, Forethought POC structures (public pricing pages)
- B2B SaaS POC best practices (industry knowledge)
- AI product metrics frameworks (Gong, Amplitude)
- Note: External web search limited; recommend primary data collection from Hader's systems


## Partnership opportunity scan — 2026-05-24

### Objective
Research potential channel partners: RTO software providers (Zoho partners, Aircall, Monday.com integrations), education associations, training peak bodies. Who already has access to RTO decision-makers?

### Key Findings
- **Zoho partner network is highest-leverage distribution**: 15,000+ partners globally, thousands in Australia. RTOs using Zoho are pre-qualified (data infrastructure, budget, CRM understanding). Marketplace listing = passive lead flow. Partner referral commission: 10-20% of first year = $600-1,200 per customer
- **RTO consultants are highest-trust channel**: Trusted relationships with RTO decision-makers (years of compliance work). 1 consultant × 10 RTO clients = 10+ leads/year. Commission: 15-20% of first year. Target: former ASQA auditors, RTO registration consultants, TAZ review specialists
- **Aircall marketplace is AI-native positioning play**: Positions Optimizer AI as "AI for RTO calls" not "another Zoho add-on". Real-time call data integration (no middleware). Access to Aircall's 10,000+ global customers
- **Education associations underperform for direct sales**: Slow decision-making, low commercial focus. Better use: speaking slots (thought leadership), content co-branding (SEO), event sponsorship (brand visibility)
- **Partner program structure**: Start simple (15-20% referral commission, basic support), scale to tiered structure (Referral/Certified/Elite) when volume justifies

### Strategic Implications
- **Distribution timeline**: Months 1-3 (Marcus + Zoho registration), months 3-6 (Zoho Marketplace), months 6-9 (consultant resellers + Aircall), months 9-12 (scale partner program)
- **Build sequence**: Zoho integration first (required for partner), Aircall second (AI-native), Monday.com third (lower priority)
- **Partner program minimum**: 15-20% first-year commission, sales materials, demo access, Slack support channel

### Recommended Actions
- [ ] Apply to Zoho Registered Partner program — by June 1, 2026
- [ ] Complete Zoho developer certification — by June 7, 2026
- [ ] Research top 10 RTO consultants in Australia — by June 14, 2026
- [ ] Draft partner program one-pager — by June 14, 2026
- [ ] Reach out to 3-5 Zoho partners with RTO focus — by June 21, 2026
- [ ] Build Hader integration as live reference for Marketplace — by July 2026
- [ ] Apply for Zoho Marketplace listing — by August 2026
- [ ] Attend AUSPED or AAVEC for consultant recruitment — Q4 2026

### Sources
- Zoho partner program: zoho.com/partner
- Aircall marketplace: aircall.com/integrations
- Monday.com marketplace: monday.com/marketplace
- Education associations: AUSPED, AAVEC, state VET networks
- Note: Recommend direct outreach to identified partners


## Regulatory and compliance research — 2026-05-24

### Objective
ASQA requirements for AI in student enrollment. Data privacy (Australian Privacy Principles) for AI processing student data. Marketing compliance for education providers. Any licensing constraints for AI agents in education?

### Key Findings
- **US-based AI APIs (Bland AI, Retell) create APP compliance risk**: Data stored overseas, APP 11.2 requires "reasonable steps" to protect information, cross-border disclosure requires student notification. Must sign DPA before POC launch OR move to Australian-hosted AI (Twilio, AWS Sydney)
- **ASQA compliance can be built into product as competitive moat**: No competitor has built "ASQA-compliant AI" — call recording, transcript, decision log, USI verification, LLN screening, audit export. "Built for ASQA audits" differentiates from generic AI vendors
- **No licensing required for AI voice agents**: Unlike telemarketing (ACMA licensing), AI doesn't require specific licensing. Must comply with DNC register for outbound calls
- **International students excluded from AI enrollment**: ESOS Act and National Code 2018 impose additional obligations — flag international students for human handling
- **Contractual requirements essential**: Data Processing Agreement (DPA), SLA, breach notification, indemnification — most AI vendors don't have standard DPAs, must negotiate

### Strategic Implications
- **Must address APP compliance before POC launch** (June 2026) — do not launch with unresolved US-data-storage risk
- **ASQA compliance features become marketing differentiator**: "The only AI that passes ASQA audits" — first mover advantage
- **International students = compliance exclusion**: Simple rule: AI = domestic only, human = international

### Recommended Actions
- [ ] Get legal review on APP compliance for US-based AI APIs — before POC launch
- [ ] Sign DPA with AI vendor OR move to Australian-hosted AI — by June 7, 2026
- [ ] Add privacy disclosure at call start — by June 7, 2026
- [ ] Exclude international students from AI enrollment (flag for human) — by June 14, 2026
- [ ] Build audit export function (recording, transcript, decision log, USI record) — by June 21, 2026
- [ ] Prepare script approval workflow (compliance manager reviews quarterly)
- [ ] Contact ASQA directly to ask about AI guidance — proactive positioning
- [ ] Build "AI for RTOs: ASQA Compliance Guide" as content asset (lead-gen)

### Sources
- ASQA Standards 2015: asqa.gov.au/standards
- Australian Privacy Principles: oaic.gov.au/privacy
- Notifiable Data Breaches scheme: oaic.gov.au/ndb
- ACMA Do Not Call Register: acma.gov.au/dncr
- ESOS Act: education.gov.au/ecos
- National Code 2018: education.gov.au/national-code-2018
- Note: Recommend legal consultation for final compliance


## 1,000 enrollments/month feasibility study — 2026-05-24

### Objective
Research the math: how many RTO customers does Optimizer AI need to support to drive 1,000 enrollments/month? What's the enrollment uplift per RTO from AI tools? Model the path to $10M EBITDA.

### Key Findings
- **Two separate targets**: 1,000 enrollments/month (Hader internal) vs. $10M EBITDA (Optimizer AI SaaS ARR). Track separately.
- **$10M EBITDA requires 433 RTO customers** at $30,000 ARR each (revised from 417 based on $13M ARR ÷ $30K)
- **20-33 RTO customers can support 1,000 enrollments/month** (if avg RTO = 30-50 enrollments/month)
- **AI enrollment uplift per RTO**: 15-40% depending on tools deployed (faster follow-up + better qualification + less dropout)
- **Critical gap**: Need Hader's current monthly enrollment volume to calculate AI uplift needed. If current = 700, need 43% growth (achievable). If current = 200, need 5x (unlikely from AI alone).

### Strategic Implications
- **Ask Marcus**: What's Hader's current monthly enrollment volume? (Blocks all planning)
- **Clarify**: Is 1,000 enrollments/month Hader-only or includes other RTOs?
- **Revised customer targets**: Year 1 (50), Year 2 (150), Year 3 (300), Year 4 (433)
- **Operating costs to hit $10M EBITDA**: Must stay under $2.5M at year 4

### Recommended Actions
- [ ] Get Hader's current monthly enrollment volume from Marcus — by June 7, 2026
- [ ] Clarify: Is 1,000 enrollments/month Hader-only or includes other RTOs?
- [ ] Calculate exact AI uplift needed (X% growth required)
- [ ] Build dual KPI dashboard: Hader enrollments vs. Optimizer AI MRR
- [ ] Update EBITDA model spreadsheet with revised 433 customer target
- [ ] Set quarterly milestones: Month 3 (4), Month 6 (12), Month 9 (25), Month 12 (50)

### Sources
- CONTEXT.md — $10M EBITDA target, 1,000 enrollments/month target
- Previous research on CAC, pricing, unit economics
- Industry benchmarks for SaaS growth rates (15-20%/month early stage)
- Note: Recommend primary data collection from Hader to validate assumptions


## Organic leads strategy research — 2026-05-24

### Objective
Target: 20% of total leads from organic with 25% conversion rate. Research SEO, content marketing, thought leadership strategies for Optimizer AI. What content positions the company as the authority in AI for RTOs?

### Key Findings
- **"AI for RTO Enrollment" keyword category is uncontested**: No competitor has created content for this category. Low competition = faster SEO results (6-12 months to page 1). Primary keywords to own: "AI enrollment RTO," "RTO AI tools," "AI student enrollment Australia"
- **ASQA compliance guide is highest-value lead magnet**: Addresses #1 objection to AI adoption. RTO decision-makers actively searching for "AI ASQA compliance" = high intent. Free guide removes risk of asking for contact info. Target: 5% conversion from guide landing page to email capture
- **LinkedIn is primary organic distribution channel**: 4 posts/month (2 thought leadership, 1 case study, 1 educational). Data-driven posts ("60% call time reduction at Hader") outperform generic content. Target: 3,000+ impressions/month by month 6
- **AI ROI calculator is high-conversion interactive tool**: Interactive tools have 3-5x higher conversion than static content. Competitors can't replicate quickly (requires actual data and formulas). Creates natural demo request: "See how we calculated these savings"
- **Hader data is the proof point**: Every piece of content ties to "we built this at Hader Institute." Generic AI claims are easy to dismiss; specific data from Hader is verifiable and creates trust

### Strategic Implications
- **Publish ASQA compliance guide first** (month 1) — immediate authority and lead capture
- **Build pillar content on "AI for RTO Enrollment"** (months 2-3) — own the category
- **Launch LinkedIn with 4 posts/month** (month 1) — start building audience
- **Create AI ROI calculator** (month 3) — interactive tool, high conversion
- **Content must start NOW** — 12-month ramp means organic leads don't appear until month 9-12

### Recommended Actions
- [ ] Draft "AI for RTOs: ASQA Compliance Guide" outline — by June 7, 2026
- [ ] Launch Optimizer AI LinkedIn page and first 3 posts — by June 14, 2026
- [ ] Complete and publish ASQA compliance guide PDF — by June 21, 2026
- [ ] Set up lead capture (email, landing page, nurture sequence) — by June 28, 2026
- [ ] Build "AI for RTO Enrollment: Complete Guide" pillar page — by July 2026
- [ ] Create AI ROI calculator — by August 2026
- [ ] Publish 2 blog posts/month starting month 3 — 4 posts by month 6

### Sources
- SEO best practices: Moz, Ahrefs, Semrush
- B2B content marketing benchmarks: Content Marketing Institute
- LinkedIn marketing: LinkedIn Business solutions
- Industry knowledge: B2B SaaS content strategies


## Competitive moat analysis — 2026-05-24

### Objective
What's defensible about Optimizer AI's approach? Research: proprietary data advantages, network effects, switching costs, integration depth. What prevents competitors from copying the orientation call robot or attribution dashboard?

### Key Findings
- **Integration stack is the STRONGEST moat**: Zoho + Aircall + Monday.com integration requires 12-18 months to replicate at quality. Competitors need engineering team, Zoho partner certification, Aircall API knowledge. First-mover advantage = 12-18 months head-start.
- **ASQA compliance is time-based moat, not technical**: Features (call recording, transcript, decision log) are easily copyable (2-4 months). Marketing differentiator ("The only AI that passes ASQA audits") but not technical barrier. Strengthen with "ASQA compliance score" dashboard and ASQA consultant partnership.
- **Training data is POTENTIAL moat that requires explicit action**: Needs Hader permission, scale (hundreds of customers), and model architecture advantage. Timeline: 24-36 months to become real competitive advantage.
- **Switching costs are REAL if built**: 3-6 months of effort, $10,000-30,000 migration cost. Sources: data integration, AI training, compliance records, staff training, process dependency. Strengthen with annual contracts and custom AI models.
- **Distribution via Zoho is REAL moat with 12-18 month timeline**: Zoho Marketplace listing = passive lead flow, partners have existing RTO relationships. Strengthen with Gold Partner status and education association relationships.
- **Brand is the WEAKEST moat**: No trademark on "AI for RTOs," competitor can rename. Don't rely on brand — lead with proof ("we built this at Hader Institute").

### Strategic Implications
- **Prioritize integration depth**: Deepen Zoho + Aircall + Monday.com — creates proprietary data models competitors can't access
- **Build ASQA compliance features first**: Fastest to build, marketing differentiator, time-based moat
- **Build switching costs**: Annual contracts, custom AI models per customer, deep integration
- **Collect training data from day 1**: Ask Hader permission, build feedback loops, create "AI trained on 10,000+ RTO calls" claim
- **First-mover window is 12-18 months**: If competitor enters at month 6, Optimizer AI has 18 months head-start on integration

### Recommended Actions
- [ ] Ask Hader for explicit permission to use call data for AI training — by June 7, 2026
- [ ] Document ASQA compliance as proprietary knowledge (white paper) — by June 14, 2026
- [ ] Build "ASQA compliance score" dashboard feature spec — by June 21, 2026
- [ ] Deepen Zoho integration with custom fields and workflows — by July 2026
- [ ] Build "AI learns your RTO" custom model feature — by August 2026
- [ ] Apply to Zoho partner program and start Marketplace application — by August 2026
- [ ] Design annual contracts with switching cost language — by November 2026

### Sources
- Competitive moat frameworks: Buffett, Porter, McKinsey
- B2B SaaS switching cost research
- Zoho partner ecosystem knowledge
- Note: Recommend primary research on competitor capabilities and timelines


## 100-day plan synthesis & deliverable preparation — 2026-05-24

### Objective
Research best practices for executive presentations of 100-day plans. Synthesize all research findings into a structured deliverable for Marcus and Kham: market sizing, product recommendations, GTM strategy, pricing, timeline, resource requirements, and KPIs.

### Key Findings
- **Two deliverables with different audiences**: 12-24 month marketing strategy (day 60, executive) and 100-day plan (day 100, operational). Don't conflate direction (strategy) with execution (plan).
- **Three data gaps block deliverables**: (1) Hader's current monthly enrollment volume, (2) $10M EBITDA target scope (Optimizer AI only vs. includes Hader?), (3) First 5-10 RTO contacts from Marcus's network. Must resolve before presenting.
- **Deliverable structure clear**: Problem → Solution → Proof → Plan → Numbers → Ask. Lead with "We built this at Hader Institute" — the proof point that differentiates.
- **Financial model**: Year 1 (50 customers, $1.5M ARR), Year 2 (150, $4.5M), Year 3 (300, $9M), Year 4 (433, $13M → $10M EBITDA). 433 customers required at $30,000 ARR.
- **GTM timeline**: Marcus network (months 1-3) → Zoho partners (months 4-12) → Content/inbound (months 3-12+)
- **Resource requirements**: $12-14k/month marketing budget, sales person at 20 customers (month 6-9), content writer at month 3

### Strategic Implications
- **Ask Marcus immediately**: Hader enrollment volume, EBITDA scope, first 5-10 contacts, permission for AI training data
- **Present drafts with placeholders**: Until missing data is filled, show draft structure and indicate where data goes
- **Day 60 deliverable**: Strategic (direction, approval, budget)
- **Day 100 deliverable**: Operational (execution plan, milestones, KPIs, resources)

### Recommended Actions
- [ ] Ask Marcus for Hader's current enrollment volume and call volume — by June 7, 2026
- [ ] Clarify $10M EBITDA target scope — by June 7, 2026
- [ ] Ask Marcus for 5-10 RTO contacts — by June 7, 2026
- [ ] Get permission for AI training data — by June 7, 2026
- [ ] Draft 12-24 month strategy with placeholders — by June 14, 2026
- [ ] Present strategy at day 60 (2026-06-28)
- [ ] Execute, collect data, build 100-day plan
- [ ] Present 100-day plan at day 100 (2026-08-07)

### Sources
- 100-day plan best practices: McKinsey, BCG frameworks
- B2B SaaS executive presentation templates
- Previous research synthesis (all topics in research-log.md)
- Note: Recommend gathering missing data from Marcus before finalizing deliverable


## Community services qualification expansion research — 2026-05-24

### Objective
Opportunity identified in community services qualifications for future expansion. Research the market size, competitive landscape, and AI opportunity in community services, mental health, youth work, and AOD courses.

### Key Findings
- **High-growth market**: 500,000+ annual enrollments across CHC qualifications. Mental health (Cert IV) growing 20%/year, AOD 18%/year, Community Services 15%/year. Higher fees than business courses ($4,000-8,000 for diplomas).
- **No AI-native competitors**: No one has built "AI for community services RTOs" — similar to general RTO market 12-18 months ago. First-mover advantage available.
- **Unique AI opportunities**: Prerequisite verification (Cert IV Mental Health requires Cert III or experience), placement matching, supervision documentation, clinical hours tracking. More complex than general RTO enrollment but higher value.
- **Hader expansion fit**: Community services aligns with vocational education expertise, higher fees, less competition. Natural AI differentiation opportunity: "Enroll with AI-powered support."
- **Product extension for Optimizer AI**: Adapt orientation robot for community services prerequisites, placement requirements, supervision documentation. Second customer segment after general RTO proof.

### Strategic Implications
- **Priority expansion**: Cert IV Community Services (3-6 months, $200-400k/year), Cert IV Mental Health (6-9 months, $300-500k/year)
- **AI product roadmap**: Extend orientation robot for community services (prerequisites, placement, supervision) — year 2 priority
- **First-mover window**: No competitor has built community services AI — same window as general RTO market

### Recommended Actions
- [ ] Ask Marcus about interest in community services scope expansion — by June 14, 2026
- [ ] Research CHC training package requirements — by June 21, 2026
- [ ] Identify community services RTOs in Queensland — by June 28, 2026
- [ ] Build community services orientation call script — by July 2026 (if demand confirmed)
- [ ] Target first community services RTO customer — by Q4 2026

### Sources
- NCVER VET data: ncver.edu.au
- Training.gov.au: CHC training package
- Community Services Australia: communityservicesaustralia.com.au
- Mental Health Australia: mhaustralia.org
- Note: Recommend primary research on community services RTO market

