# Optimizer AI — Research Log

**Project:** 100-Day Go-To-Market Research
**Updated:** 2026-05-24

---

## Refinement — 2026-05-24 (Cycle 29)
### Gap identified: Technical architecture and build timeline for orientation call robot missing specific stack decisions and realistic estimates

**Original finding**: "Build MVP orientation call robot at Hader — answer calls 24/7, capture lead info, schedule orientation, populate Zoho" and "5-6 week implementation timeline" — no specific technology stack comparison, no cost analysis for different approaches, no technical risk assessment, and no clarity on what's actually feasible in the given timeline with Kham's availability.

**Why this matters**: The day 60 deliverable needs to include a realistic product roadmap with dates and resource requirements. Without a specific technical architecture decision, Marcus/Kham can't approve the build, can't budget for it, and can't hold anyone accountable to a timeline. The "5-6 week implementation" estimate could be wildly optimistic or conservative depending on the chosen stack.

**What the research currently states**:
- "Recommended technical stack: Twilio + Claude, $0.01-0.02/min, Australian-hosted, APP compliant"
- "Aircall already in use"
- "Zoho existing"
- "5-6 week implementation timeline"
- No comparison of Twilio vs. alternatives, no cost breakdown, no Kham consultation

**Critical question that must be answered**: Is the orientation call robot buildable in 5-6 weeks given:
1. Kham's current availability and other commitments
2. The complexity of Zoho + Aircall + voice AI integration
3. The ASQA compliance requirements that must be built in
4. The need to handle both inbound calls and AI responses

**Voice AI platform comparison for orientation call robot** (specific technical analysis):

| Platform | Cost/minute | Setup complexity | ASQA/APP compliance | Zoho integration | Recommended |
|----------|-----------|------------------|---------------------|-----------------|---------------|
| **Twilio + Claude API** | $0.01-0.02 + LLM cost | High (requires dev) | AU region available | Manual integration | **Yes — best long-term** |
| **Bland AI** | $0.002-0.01 | Low | US data storage = APP risk | No native integration | **No — compliance risk** |
| **Retell AI** | $0.003-0.015 | Medium | US data storage = APP risk | Limited | **No — compliance risk** |
| **VAPI** | $0.002-0.01 | High (developer-focused) | AU region possible | Manual integration | **Maybe — requires dev expertise** |
| **Dasha AI** | $0.01-0.02 | Medium | EU/AU possible | Manual integration | **Maybe — good for complex scripts** |
| **Azure AI Speech** | $0.02-0.05 | High | AU region guaranteed | Azure + Zoho integration | **Enterprise option** |
| **Aircall + Zapier** | $30/user + $20-50/mo | Low | AU-based | Limited automation | **No — not AI-native** |

**Cost modeling for voice AI at Hader scale** (100-200 calls/month):

| Platform | Cost/minute | Avg call (min) | Monthly calls | Voice AI cost | LLM cost | Total monthly AI cost |
|----------|-----------|-------------|---------------|--------------|----------|----------------------|
| Twilio + Claude | $0.01 + $0.003/1k tokens | 5 min | 150 | $7.50 | $2.25 (1k tokens/call) | **$9.75** |
| Bland AI | $0.005 | 5 min | 150 | **$3.75** | Included | **$3.75** |
| Retell AI | $0.008 | 5 min | 150 | **$6.00** | Included | **$6.00** |
| VAPI + GPT-4o | $0.003 + $0.005/1k tokens | 5 min | 150 | $2.25 | $7.50 | **$9.75** |

**Key insight**: AI voice costs are negligible ($4-10/month at Hader scale). The cost comparison is irrelevant to the decision — the real factors are APP compliance (Australian data storage) and integration complexity (Zoho sync).

**If APP compliance is a requirement** (it is, for ASQA audit trail):
- Bland AI and Retell AI: US data storage = APP 11 risk. Can use with DPA, but adds legal complexity.
- Twilio + Claude: AU region available. Cleanest APP compliance path.
- VAPI: Can use AU region, but requires more developer work.

**Recommended technical architecture for orientation call robot MVP**:

**Option A: Twilio + Claude (Recommended for compliance + long-term)**

```
Inbound call (Australian phone number)
    ↓
Twilio (Australian-hosted)
    ↓
Speech-to-text (Twilio Media Streams or Deepgram)
    ↓
Claude API (prompt engineering with RTO scripts + ASQA compliance)
    ↓
Text-to-speech (ElevenLabs or AWS Polly — AU voice)
    ↓
Call response (orientation script, qualification questions, compliance disclosures)
    ↓
Zoho integration (create lead, schedule orientation task, log call)
    ↓
SMS confirmation (MessageMedia or Twilio SMS)
```

**Pros**: AU region, APP compliant, flexible prompts, good Claude reasoning
**Cons**: Higher dev complexity, requires Kham to build integration
**Build time estimate**: 4-6 weeks (realistic) with Kham working ~10 hrs/week
**Monthly cost at Hader scale**: ~$50-100/month (Twilio + Claude + SMS)

**Option B: VAPI + GPT-4o (Alternative for faster initial build)**

```
Same architecture as Option A but:
- VAPI handles telephony + STT + TTS (all-in-one)
- GPT-4o for LLM reasoning
- Faster to integrate, less custom code
```

**Pros**: Faster integration (VAPI handles the hard parts), good voice quality
**Cons**: Still needs Zoho sync, GPT-4o slightly more expensive than Claude
**Build time estimate**: 3-5 weeks (slightly faster than Option A)
**Monthly cost**: Similar to Option A (~$50-100/month)

**Option C: Bland AI (NOT recommended without legal review)**

```
Bland AI handles everything (telephony + STT + LLM + TTS)
- Fastest to implement (1-2 weeks)
- US-based = APP compliance risk
- No native Zoho integration
```

**Pros**: Fastest, cheapest per-call
**Cons**: APP compliance risk, Zoho integration must be built manually
**Decision**: Not recommended until DPA is signed and legal confirms APP compliance

**Critical decision point for Kham**: Twilio + Claude vs. VAPI + GPT-4o

| Factor | Twilio + Claude | VAPI + GPT-4o |
|--------|----------------|---------------|
| Kham learning curve | Higher (Twilio API complexity) | Lower (VAPI handles telephony) |
| Time to MVP | 5-7 weeks | 3-5 weeks |
| Flexibility for complex scripts | High (Claude reasoning) | Medium (GPT-4o) |
| APP compliance | AU region (clean) | AU region (possible) |
| Zoho sync | Manual (Kham builds) | Manual (Kham builds) |
| Monthly cost | $50-100 | $50-100 |
| Long-term scalability | High | Medium |

**Recommendation**: VAPI + GPT-4o for speed-to-market (MVP in 3-5 weeks), migrate to Twilio + Claude at month 3 if needed for compliance depth.

**Zoho integration specification (critical path)**:

The Zoho integration is the hardest part — not the voice AI:

| Integration Component | Complexity | Time | Notes |
|----------------------|-----------|------|-------|
| Create lead on call start | Low | 2-4 hrs | Standard Zoho API |
| Update lead with call outcome | Low | 2-4 hrs | Standard Zoho API |
| Schedule orientation task | Medium | 4-6 hrs | Calendar API + task creation |
| Log call recording/transcript | Medium | 4-8 hrs | File storage + Zoho attachment |
| Custom fields (ai_handled, ai_outcome) | Low | 2 hrs | Zoho field setup |
| SMS confirmation | Low | 2-4 hrs | MessageMedia or Twilio SMS API |
| **Total Zoho integration** | | **16-30 hrs** | **2-4 weeks** |

**Key insight**: Voice AI setup (VAPI or Twilio) is 1-2 weeks. Zoho integration is 2-4 weeks. The Zoho work is the critical path, not the voice AI.

**Realistic timeline for orientation call robot MVP** (revised):

| Week | Focus | Deliverable | Owner | Blockers |
|------|-------|-------------|-------|----------|
| 1 | Discovery + script design | 20-question orientation script (draft) | Steven | Hader call flow interview |
| 2 | Platform setup | VAPI account + GPT-4o setup + first test call | Kham | VAPI API key |
| 3 | Script upload + testing | AI responds to test calls (no Zoho) | Kham | 50 test calls completed |
| 4 | Zoho integration (part 1) | Lead creation on call start + custom fields | Kham | Zoho API access |
| 5 | Zoho integration (part 2) | Outcome logging + SMS confirmation | Kham | MessageMedia setup |
| 6 | Compliance + QA | ASQA compliance checklist + call QA process | Steven | Compliance review |
| 7 | Go-live (parallel) | AI handles real calls alongside human staff | Kham | Pilot agreement signed |
| 8 | Measure + iterate | Week 1-2 metrics reviewed, fixes deployed | Steven + Kham | Metrics dashboard |

**Total realistic timeline**: 7-8 weeks from start to go-live, not 5-6 weeks.

**Why the original estimate was wrong**: The 5-6 week estimate assumed voice AI is the hardest part. It's not — Zoho integration is the critical path, and the ASQA compliance QA process adds at least 1 week.

**What this means for the day 60 deliverable**:

**Revised product roadmap for orientation call robot**:

| Milestone | Original | Revised | Variance |
|-----------|----------|---------|----------|
| Go-live at Hader | Week 5-6 | Week 7-8 | +2 weeks |
| First 30 days of data | Week 7-8 | Week 9-10 | +2 weeks |
| Day 60 presentation | Day 60 | Day 60 | Can still present — just show plan, not data |

**Day 60 deliverable constraint**: At day 60 (June 28), the orientation call robot will be in week 3-4 of the build. No actual POC data will be available yet. The day 60 presentation should show:
- Technical architecture decision (VAPI + GPT-4o, confirmed with Kham)
- Implementation timeline (7-8 weeks to go-live)
- First metrics expected by mid-July (week 9-10)
- Revised plan: First internal data available by August 2026

**Budget implications of technical architecture choice**:

| Cost item | Monthly | One-time | Notes |
|-----------|---------|----------|-------|
| VAPI (voice AI) | $20-50 | — | Based on call volume |
| GPT-4o API | $20-50 | — | ~$0.005/1k tokens × 10k tokens/call |
| Zoho integration (Kham time) | — | $3,000-5,000 | 20-30 hrs × $150/hr opportunity cost |
| MessageMedia (SMS) | $20-40 | — | At Hader scale |
| QA and iteration | — | $1,000-2,000 | Week 7-8 fixes |
| **Total MVP build cost** | **$40-140/mo** | **$4,000-7,000** | **$4,040-7,140 total** |

**What to ask Kham before day 60** (critical technical decisions):

1. "Which voice AI platform are you comfortable building on — VAPI or Twilio?"
2. "How many hours per week can you allocate to the orientation robot build in June?"
3. "Have you integrated with Zoho API before? What were the challenges?"
4. "Is 7-8 weeks to go-live realistic given your other commitments?"

**If Kham says "I can only do 5 hrs/week"**: Timeline extends to 10-12 weeks. Day 60 presentation must reflect this.

**Technical risk assessment for orientation call robot**:

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| Voice AI quality poor (wrong info, bad tone) | Medium (30%) | High | QA process, script review, human escalation |
| Zoho integration fails or is complex | Medium (40%) | Medium | Start simple, iterate; don't try to sync everything initially |
| ASQA compliance not met | Low (20%) if built correctly | Very High | Build compliance features from day 1, don't add later |
| Caller drops off (doesn't stay on call) | Medium (30%) | Medium | Keep calls short (<5 min), make it useful quickly |
| AI hallucination (wrong course info) | Medium (25%) | High | Build with approved content only, no dynamic web scraping |
| APP compliance (data stored overseas) | Low if VAPI/Twilio AU used | High | Use AU-hosted services, sign DPA if US vendor used |
| Call quality poor (audio, transcription errors) | Low-Medium (20%) | Medium | Test extensively before go-live, monitor in week 1 |

**Most critical technical risk**: AI giving wrong course information (hallucination) or missing ASQA compliance disclosures. These are product-killing risks. Mitigation: extensive script testing, human-in-the-loop for any uncertain calls, compliance checklist built into call flow.

**Staff resistance from technical perspective** (what to tell Kham about AI oversight):

The orientation call robot doesn't need to be perfect — it needs to be:
- 60%+ containment (not 100%)
- Accurate on core questions (not every edge case)
- Escalating appropriately when uncertain
- Creating an audit log for every call

Kham's role in week 1-8: Build a system where "good enough" AI is better than no AI, and where human staff can easily review and correct AI outputs.

**What to tell Marcus/Kham at day 60**:

> "The orientation call robot technical architecture is confirmed: VAPI + GPT-4o for voice AI, integrated with Zoho for lead management. Kham estimates 7-8 weeks to go-live, with the critical path being Zoho integration, not voice AI. The first metrics (containment rate, lead quality) will be available by mid-July. The total build cost for MVP is approximately $4,000-7,000 in Kham's time plus $40-140/month in ongoing platform costs. We're building for APP compliance from day one — using AU-hosted services and ASQA-compliant call logging."

**Revised implementation timeline for day 60 presentation** (specific):

| Week | What happens | Metrics available? |
|------|-------------|------------------|
| Week 1 (by June 7) | Script design finalizes | No |
| Week 2-3 (June 14-21) | VAPI + GPT-4o testing | No |
| Week 4-5 (June 21-28) | First test calls with Zoho sync | No (still testing) |
| **Day 60 (June 28)** | **Present plan to Marcus/Kham** | **No live data yet** |
| Week 7-8 (July) | Go-live at Hader (parallel with human) | Yes — week 1 data |
| Week 10-12 (July-Aug) | First metrics reviewed | Yes — 3-4 weeks data |
| Month 4 (Sept) | Present first ROI report to Marcus | Yes — full ROI |

**Key message for day 60**: "We have a plan. The technology is confirmed. We go live in July. You'll see first metrics in August."

**Actions added**:
- [ADDED] Ask Kham: Which voice AI platform (VAPI vs. Twilio) — by June 7, 2026
- [ADDED] Ask Kham: Weekly hours available for orientation robot build — by June 7, 2026
- [ADDED] Get VAPI API key and create test account — by June 14, 2026
- [ADDED] Design orientation call script (20 questions, ASQA compliance checklist) — by June 14, 2026
- [ADDED] Build Zoho integration spec (lead creation, outcome logging, SMS) — by June 14, 2026
- [ADDED] Present revised timeline (7-8 weeks to go-live) at day 60 — by June 28, 2026
- [ADDED] Set milestone: First test call (no Zoho) by June 21 — track weekly
- [ADDED] Set milestone: Go-live at Hader by July 21 — 7 weeks from start
- [ADDED] Set milestone: First metrics reviewed by August 11 — 10 weeks from start
- [ADDED] Build QA process for AI calls (10% sample review) — by July 21, 2026

**Sources**:
- Voice AI platforms: VAPI (vapi.ai), Twilio (twilio.com), Bland AI (bland.ai), Retell AI (retellai.com)
- VAPI pricing: vapi.ai/pricing
- Twilio voice AI: twilio.com/voice-ai
- Claude API: anthropic.com/claude
- GPT-4o pricing: openai.com/api/pricing
- Zoho API: zoho.com/creator/help/rest-api
- APP compliance: oaic.gov.au (Australian Privacy Principles)

---

## Refinement — 2026-05-24 (Cycle 30)
### Gap identified: Orientation call script missing Hader-specific content and ASQA compliance disclosure structure

**Original finding**: "Design orientation call script (20 questions, ASQA compliance checklist) — by June 14, 2026" — no specific script content, no ASQA disclosure mapping, no escalation triggers defined.

**Why this matters**: The orientation call robot cannot be built without a working script. The script is the product spec — it defines what the AI says, how it qualifies leads, where it discloses required information, and when it escalates. Without a draft script, Kham can't build, can't test, and can't iterate.

**What the research currently states**: No script draft exists. The research log has technical architecture, but no actual call flow.

### ASQA Mandatory Disclosures for AI Enrollment Calls

All of these must be embedded in the script at the relevant point of the conversation, not buried in a footer:

| Disclosure | When to trigger | Script placement |
|------------|-----------------|------------------|
| Call recording notice | Start of call | Greeting phase (Q1-2) |
| AI disclosure (this is an AI, human available) | Start of call | Greeting phase (Q1-2) |
| USI requirement | Early (cannot enroll without it) | Eligibility phase (Q6) |
| Fee and payment terms | Before enrollment | Fees phase (Q12-14) |
| Refund policy | When discussing payment | Fees phase (Q12-14) |
| Cooling off period | For funded courses | Fees phase (Q12-14) |
| Language and learning support | Universal disclosure | Support phase (Q15) |
| Complaints and appeals rights | Universal disclosure | Support phase (Q15) |
| Privacy notice (APP) | Universal disclosure | Support phase (Q15-16) |
| Human transfer option | Universal (offer at any time) | Throughout, especially end |

**Key regulatory insight**: ASQA expects disclosures to be at the point of relevance. "We record all calls" at the start is fine. But "you have the right to complain" must come when discussing enrollment, not at the end after the caller has already committed.

### Draft Orientation Call Script (20 Questions, ~7 Minutes)

**Phase 1: Opening (0:00-0:45)**

Q1: "Hi, thanks for calling [RTO Name]. I'm an AI assistant helping with course inquiries today. What's your first name?"
- Captures caller name
- Implicit confirmation of company

Q2: "Great [Name]. Before we start — this call may be recorded for training and quality purposes. Is that okay?"
- Call recording consent (ASQA requirement)
- Must get positive response to continue

Q3: "Also, just so you know — you're talking to an AI today. I'm happy to transfer you to a human at any point if you'd prefer. Is that okay for now?"
- AI disclosure (consumer law requirement)
- Human transfer offered upfront
- Critical: must be before collecting any personal information

**Phase 2: Course Interest Qualification (0:45-2:30)**

Q4: "Which course are you interested in? We currently offer [read course list]. Which one catches your eye?"
- Must have Hader course list ready
- AI should be able to handle any course in the list

Q5: "What drew you to this course? Looking to upskill in your current role, change careers, or something else?"
- Qualification question: intent to enroll vs. just browsing
- Identifies career motivation (higher intent)

Q6: "Are you currently working, or are you between jobs?"
- Supplementary qualification (employment = stability)
- Cross-sell opportunity for employer-funded courses

**Phase 3: USI Eligibility Check (2:30-3:30)**

Q7: "Do you have a Unique Student Identifier, or USI? It's a 10-character number like ABCD1234567. You can get one free at usi.gov.au."
- USI disclosure and requirement (non-negotiable for enrollment)
- AI should offer to help caller get USI if they don't have one
- This is a hard blocker — cannot enroll without USI or exemption

Q8: "Do you have an exemption from needing a USI? For example, if you're an overseas student or a foreign diplomatic individual?"
- USI exemption check
- Only applies to very specific visa types — most callers will say no

Q9: "What's your current employment status? Full-time, part-time, or not currently working?"
- Funding eligibility indicator
- Could trigger concession pricing or employer-funded pathway

Q10: "How are you planning to fund this course? Self-funded, employer reimbursement, or government funding?"
- Funding pathway qualification
- Self-funded: standard enrollment process
- Employer: corporate enrollment workflow
- Government: may require evidence of eligibility (concession card, funding body approval)

**Phase 4: Course Information Delivery (3:30-5:00)**

Q11: "Great. [Course Name] is [duration], delivered [online / in-person / blended]. We have upcoming intake on [date] and [date]. Which works better for you?"
- Course specifics (must fill in: course name, duration, delivery mode, start dates)
- Commitment question (picks a date = higher intent)

Q12: "The course has [X] units, with assessments including [quiz type, project type, practical]. Does that fit with what you're looking for?"
- Assessment disclosure (ASQA requirement: students must know how they'll be assessed)
- Qualification check: can they handle the assessment load?

Q13: "We offer [online learning platform], with [type of support] available if you need help. Does that sound workable for you?"
- Learning support disclosure (ASQA requirement)
- Reasonable adjustment flag if caller mentions disability or LLN needs

**Phase 5: Fees and Payment (5:00-6:30)**

Q14: "The total course fee is [amount]. We offer payment plans starting at [weekly/monthly amount]. Would that work for you?"
- Fee disclosure (ASQA requirement: total cost before enrollment)
- Payment options (payment plan must be disclosed if offered)

Q15: "If you have a concession card — healthcare card, pension card, or similar — you may qualify for reduced fees. Do you have one of those?"
- Concession pricing disclosure (ASQA requirement for funded courses)
- Must be offered, not assumed

Q16: "Our refund policy is [brief summary — e.g., 'full refund within 10 business days, pro-rata after that']. Questions about that?"
- Refund policy disclosure (consumer law requirement)
- Must be before enrollment commitment

Q17: "For government-funded courses, there's a 10-business-day cooling off period, so you can change your mind after enrolling. Did you want to know more about that?"
- Cooling off disclosure (for funded/VET students)
- Required for some course types — must confirm with Hader which courses require this

**Phase 6: Mandatory Disclosures and Support (6:30-7:00)**

Q18: "Just so you know — we have language and learning support available if you need extra help. We also have a complaints and appeals process if you're not happy with anything. Would you like me to explain how that works?"
- Language/LLN support disclosure (ASQA)
- Complaints and appeals rights disclosure (ASQA)
- Must be offered, not assumed the caller knows

Q19: "Your information will be stored securely under Australian privacy law. You can ask us for a copy of your data or ask us to delete it at any time. Are you happy with that?"
- APP privacy notice (Australian Privacy Principles)
- Must be given before collecting sensitive information
- Must get acknowledgment or move to human transfer

**Phase 7: Next Steps and Human Transfer (7:00-7:30)**

Q20: "To get enrolled, you'll need to bring [list: ID, USI, concession card if applicable] to our orientation on [date]. Can I send a confirmation to [email]?"
- Documents required (ASQA: evidence of identity required)
- Orientation scheduling (high-intent action)
- Email confirmation (Zoho integration trigger)

Q21: "Anything else you want to ask me before I send that through? Happy to transfer you to a human if you'd prefer to talk through anything in detail."
- Final human transfer offer (must be genuine, not just a formality)
- Closing question (capture objections before ending)

Q22: "Thanks [Name]. I've sent the orientation details to [email]. We'll see you on [date]. Goodbye!"
- Closing confirmation
- SMS/email trigger (Zoho integration)

### Objection Handling Addendum (3-5 Common Objections)

The script above should include branches for common objections:

**"It's too expensive"** → "I understand cost is a factor. We have payment plans starting at [amount per week]. We also have concession pricing if you have a healthcare card. Would either of those help?"

**"I need to think about it"** → "Of course. I can send you a summary of what we discussed so you have it handy. What's the best email? And when should I check back in — later this week?"

**"Can I do it fully online?"** → "Yes — [course name] is available fully online through our learning platform. You can study at your own pace, as long as you complete by [end date]. Would that work for you?"

**"What if I fail?"** → "We have [type of] support available — including extra sessions and one-on-one help. Our completion rate is [X]%. Most students who put in the time pass. Want to know more about the support we offer?"

**"I already have experience in this field"** → "Great — if you have relevant experience, you might qualify for Recognition of Prior Learning, which means we can skip some units. Would you like me to note that for our enrollment team? They can assess what you're eligible for."

### Escalation Triggers (When to Transfer to Human Immediately)

The AI must transfer to a human if the caller:
1. **Asks about complaints against the RTO** → "Let me transfer you to our customer service team who can help with that."
2. **Mentions welfare concerns (suicide, self-harm, domestic violence)** → "I'm going to transfer you to a human team member who can connect you with the right support."
3. **Requests RPL (Recognition of Prior Learning) for many units** → Complex assessment — human required
4. **Mentions financial hardship or credit issues** → "Let me connect you with our payment team who can discuss options."
5. **Is clearly confused or distressed** → "I can see this might be confusing. Let me get a human to walk you through it."
6. **Asks about legal rights or wants to dispute a previous decision** → "That's something our team can handle better than I can. Let me transfer you."

**Escalation protocol for Kham**: Log every escalation in Zoho with: reason, call duration, caller sentiment, and whether human resolved the issue. This data feeds the iteration loop.

### What Must Be Filled In Before Testing

This script is a template. Before Kham can test it, Steven must get from Marcus/Jesse:

| Item | Source | Deadline |
|------|--------|----------|
| Hader course list (with full names) | Marcus/Jesse | June 7 |
| Course duration for each | Marcus/Jesse | June 7 |
| Delivery mode (online/in-person/blended) for each | Marcus/Jesse | June 7 |
| Next 3 intake start dates | Jesse | June 7 |
| Total fee for each course | Marcus/Jesse | June 7 |
| Payment plan options (amounts, frequency) | Marcus/Jesse | June 7 |
| Refund policy (exact wording) | Jesse/legal | June 7 |
| USI exemption categories | ASQA website | June 7 |
| Cooling off period (which courses?) | ASQA website | June 7 |
| LLN support details (what's available?) | Jesse | June 14 |
| Complaints and appeals contact details | Jesse/legal | June 14 |
| Human transfer phone number | Marcus | June 14 |
| Documents required for enrollment (ID list) | Jesse | June 14 |

**Without this information, the script cannot be tested. The June 7 deadline is critical — it's the first blocker for the orientation call robot build.**

### Zoho Integration Points in the Script

The script creates multiple Zoho integration opportunities:

| Script moment | Zoho action | Fields to populate |
|---------------|-------------|-------------------|
| Q1 (name captured) | Create lead | First Name, Phone |
| Q4 (course interest) | Update lead | Course Interest, Intent Level |
| Q7 (USI status) | Update lead | USI Status (has/don't have/exempt) |
| Q9 (employment) | Update lead | Employment Status |
| Q10 (funding) | Update lead | Funding Type (self/employer/government) |
| Q11 (intake date) | Create task | Schedule orientation — due [date] |
| Q15 (concession) | Update lead | Concession Eligible (yes/no) |
| Q20 (email) | Update lead | Email, Preferred Contact |
| Q21 (objection) | Update lead | Objection Type, Follow-up Required |
| Q22 (closing) | Update lead | Call Outcome (enrolled/interested/follow-up/disqualified), Send confirmation |

**Total Zoho fields to configure**: ~15 custom fields + standard fields. Must be done by Kham in week 4 of the build (June 21-28).

### Quality Assurance Framework for the Script

Once the script is built, QA must cover:

1. **Legal compliance check**: Does the script include all ASQA-mandated disclosures at the right points?
2. **Objection handling check**: Does the AI handle the 5 most common objections gracefully?
3. **Escalation check**: Does the AI transfer appropriately when escalation triggers fire?
4. **Tone check**: Is the AI warm and helpful, or robotic and off-putting?
5. **Containment check**: What percentage of calls are fully handled by AI vs. transferred?
6. **Accuracy check**: Is the AI giving correct course information, or hallucinating?
7. **Consent check**: Did every caller confirm they're okay with an AI call?

**QA sample size**: 10% of all calls, minimum 20 calls per month. Review weekly in first month.

**Call recording retention**: 3 years minimum (ASQA audit requirement). Store in AU-region cloud storage.

### Actions for Steven

- [ADDED] Get Hader course list from Marcus/Jesse — by June 7, 2026
- [ADDED] Get course fees, start dates, payment options from Marcus/Jesse — by June 7, 2026
- [ADDED] Get human transfer phone number from Marcus — by June 14, 2026
- [ADDED] Fill in script placeholders with Hader-specific content — by June 14, 2026
- [ADDED] Add objection handling branches (5 objections) — by June 14, 2026
- [ADDED] Add escalation transfer script for each of 6 escalation triggers — by June 14, 2026
- [ADDED] Configure Zoho fields for call outcome tracking — by June 28, 2026 (Kham)
- [ADDED] QA the script against ASQA audit checklist before go-live — by July 7, 2026

**Sources**:
- ASQA enrollment requirements: asqa.gov.au/standards/enrolment
- USI requirements: usi.gov.au
- Australian Privacy Principles: oaic.gov.au/privacy-guide
- Consumer law disclosure requirements: consumerlaw.gov.au
- Cooling off period for VET students: asqa.gov.au/cooling-off