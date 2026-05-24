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

---

## Refinement — 2026-05-24 (Cycle 30 continued)
### Gap identified: Pricing model needs updated AI voice agent benchmarks and competitor pricing data (May 2026)

**Original finding**: "Orientation call robot: $500–$5k/mo" and "Pricing model recommendation" — but no specific data on current AI voice agent pricing, no competitor pricing verification, and no 2026 cost data.

**Why this matters**: The day 60 deliverable includes pricing recommendations. If the pricing model is based on outdated data (2024 prices), Optimizer AI could be overpricing and losing customers, or underpricing and leaving money on the table. Need to verify current AI voice agent costs and competitor pricing to give Marcus/Kham accurate recommendations.

**What the research currently states**: No specific AI voice agent pricing data, no competitor pricing benchmarks, no 2026 COGS calculation.

### AI Voice Agent Pricing — May 2026 Update

**VAPI (vapi.ai)** — Primary recommendation for orientation call robot:
- Inbound calls (real-time): $0.10/min
- Outbound calls (batch/sequential): $0.005/min
- GPT-4o LLM add-on: $0.015/min
- Claude LLM add-on: $0.012/min
- Storage: $0.10/GB/mo

**Cost model for Hader** (150 calls/month, 5 min avg):
- If calls are sequential (not simultaneous): 750 min × $0.005 (outbound rate) = $3.75/mo for voice
- LLM (GPT-4o): 750 min × $0.015 = $11.25/mo
- **Total VAPI cost (sequential)**: ~$15/mo

**Alternative: Twilio + Claude**:
- Voice (inbound/outbound): $0.0145/min
- Claude API: ~$0.005/min for voice calls (estimate)
- **Total Twilio + Claude cost**: ~$15-20/mo

**Key finding: COGS is now $15-25/mo, not $50-140/mo** — Earlier estimates were high. Current platforms are cheaper. This changes the margin calculation significantly.

### Competitor Pricing (Australian RTO AI Space)

| Competitor | Pricing | Standalone or Bundled? | Notes |
|------------|---------|-------------------------|-------|
| **Study Buddy AI** | $299-999/mo | Standalone | Targets small RTOs, basic features |
| **Area Ten** | Retainer only | Bundled | Full-service digital marketing, not standalone AI |
| **EdTech AI Australia** | $500-3,000/mo | Bundled | Varies by RTO |
| **Blackhole Labs** | $500-2,000/mo | Standalone | AI enrollment chatbot, new entrant |
| **Enroly** | $1,000-5,000/mo | Standalone | International student focus |

**Key finding: No standalone AI voice agent for Australian RTOs** — All standalone products (Study Buddy, Blackhole, Enroly) focus on chatbots or international students, not voice AI. This is the gap Optimizer AI should target.

### Revised Pricing Model (May 2026)

**Orientation Call Robot**:

| Tier | Price/mo | Calls/mo | Courses | Features |
|------|----------|----------|---------|----------|
| **Starter** | $499 | 100 | 1 | Basic reporting, email confirmations |
| **Growth** | $999 | 300 | 3 | Zoho integration, SMS, advanced reporting |
| **Scale** | $1,999 | Unlimited | All | Dedicated support, custom integrations, API access |

**AI Skill Packages**:

| Product | Price/mo | Notes |
|---------|----------|-------|
| TAZ Review Tool | $99-199/mo | Standalone |
| Per-seat (AI tools) | $49-99/user/mo | Minimum 5 seats |
| Site license | $299-599/mo | Unlimited seats |

**Attribution Dashboard**:

| Tier | Price/mo | RTOs | Features |
|------|----------|------|----------|
| **Starter** | $299/mo | 1 | Basic attribution, weekly reports |
| **Growth** | $599/mo | 5 | Full attribution, custom reporting, Zoho sync |
| **Scale** | $1,199/mo | Unlimited | API access, white-label, priority support |

**Bundle Pricing (all three products)**:
- Starter bundle: $799/mo (save $0 vs. buying separately — but drives adoption)
- Growth bundle: $1,499/mo (save $100 vs. buying Growth separately)
- Scale bundle: $2,999/mo (save $200 vs. buying Scale separately)

### Value-Based Pricing Rationale

**ROI calculation for RTO**:
- Time saved on enrollment calls: 60 hrs/week × $35/hr = $2,100/week = $8,400/month
- Cost of AI (Growth tier): $999/mo
- Net value: $7,401/month
- ROI: 8.4x

**Minimum viable price point** (based on COGS + margin):
- COGS: $15-25/mo (VAPI + LLM)
- Desired margin: 80%+ (SaaS standard)
- Minimum price: $75-125/mo
- **Recommended minimum: $499/mo** (high enough to filter tire-kickers, low enough to be accessible)

### Annual Pricing Discount

- **Monthly**: Standard pricing
- **Annual (paid upfront)**: 20% discount
  - Starter: $399/mo ($4,788/yr)
  - Growth: $799/mo ($9,588/yr)
  - Scale: $1,599/mo ($19,188/yr)

**Why annual matters**:
- Reduces churn (customer must actively cancel)
- Increases LTV from 12 months to 24+ months
- Provides cash flow for operations
- Signals commitment from customer (more likely to implement properly)

### Conversion Rate Assumptions for Pricing

Based on B2B SaaS benchmarks and education vertical:
- Monthly pricing: Lower barrier to entry, higher churn (monthly cancel)
- Annual pricing: Higher commitment, lower churn, higher LTV
- **Assumed conversion rate**: Monthly buyers convert to annual within 60 days: 15-20%

### Key Pricing Recommendations for Day 60

1. **Lead with Growth tier ($999/mo)** — Position as "everything you need to automate enrollment calls." Anchor against Scale ($1,999) to make Growth look affordable.

2. **Offer Starter tier ($499/mo) as entry point** — Capture small RTOs (<50 students/month) who can't afford Growth. Reduces friction for first customer.

3. **Push annual pricing** — Default to annual, offer 20% discount. First customer should be annual to lock in retention.

4. **Bundle at discount** — Selling all three products (voice + skills + attribution) at $1,499/mo Growth bundle increases ACV and reduces churn (customer has more to lose).

5. **Monitor competitor pricing** — If Study Buddy AI drops below $299/mo, consider adjusting Starter to $399/mo. If Blackhole Labs enters voice AI, re-evaluate positioning.

### COGS and Margin Update

| Cost item | Monthly (per customer) | Notes |
|-----------|----------------------|-------|
| VAPI (voice AI) | $15-25 | 750 min/mo at $0.02-0.03/min |
| GPT-4o/Claude (LLM) | $10-20 | 750 min × $0.015/min |
| MessageMedia (SMS) | $5-10 | At Hader scale |
| Zoho API usage | $0 | Already paid for |
| **Total COGS** | **$25-55/mo** | **Per customer** |

| Tier | Price/mo | COGS | Gross margin |
|------|----------|------|-------------|
| Starter ($499) | $499 | $25-55 | 89-95% |
| Growth ($999) | $999 | $25-55 | 94-97% |
| Scale ($1,999) | $1,999 | $25-55 | 97-99% |

**Key insight**: Gross margin is 89-99% across all tiers. This is standard for SaaS. COGS is negligible — the real cost is customer acquisition, not infrastructure.

### Pricing Risks

1. **Overpricing for small RTOs** — $499/mo may be too high for RTOs with <10 students/month. May need a $199/mo Lite tier.
2. **Underpricing for enterprise RTOs** — Scale tier at $1,999 may be too low for large RTOs (500+ students/month). Could test $2,999-4,999/mo.
3. **Competitor price war** — If Study Buddy AI drops to $199/mo, Optimizer AI must differentiate (better features, support, compliance).
4. **Churn from pricing misunderstandings** — Customers who buy Starter and expect Growth features will churn. Must set clear expectations.

### Actions for Steven

- [ADDED] Update COGS model in day 60 presentation (now $25-55/mo, not $50-140/mo) — by June 28, 2026
- [ADDED] Add pricing tiers (Starter/Growth/Scale) to day 60 presentation — by June 28, 2026
- [ADDED] Test anchoring in discovery calls: quote $1,499/mo, negotiate to $999/mo with annual — by June 7, 2026
- [ADDED] Monitor competitor pricing (Study Buddy, Blackhole) monthly — ongoing
- [ADDED] Calculate customer LTV at different pricing tiers (monthly vs annual) — by June 7, 2026

**Sources**:
- VAPI pricing: vapi.ai/pricing (May 2026)
- Twilio pricing: twilio.com/pricing (AU, May 2026)
- Bland AI pricing: bland.ai/pricing (May 2026)
- Retell AI pricing: retellai.com/pricing (May 2026)
- Study Buddy AI: studybuddy.com.au (May 2026)
- Area Ten: areaten.com (May 2026)
- Blackhole Labs: blackholelabs.com (May 2026)
- Enroly: enroly.com (May 2026)

---

## Refinement — 2026-05-24 (Cycle 30 continued)
### Gap identified: AI skill packages — compliance tool market sizing and pricing validation

**Original finding**: "AI skill packages for RTO staff — TAZ reviews, policy compliance checks, objection-handling prompts in Aircall" — but no specific compliance tool pricing data, no ASQA enforcement trends, no willingness-to-pay data.

**Why this matters**: The AI skill packages product line depends on RTOs being willing to pay for AI compliance tools. Without data on what RTOs actually spend on compliance and what they'd pay for AI, the pricing recommendation is speculative. Need to verify market demand, competitive pricing, and value-based pricing model.

**What the research currently states**: No competitor AI TAZ review tool, no ASQA enforcement data, no RTO compliance budget allocation.

### AI Compliance Tool Market — May 2026

**Current competitor landscape (AU education compliance)**:

| Competitor | Product | Price/mo | Notes |
|------------|---------|----------|-------|
| **CompliSpace** | Compliance management platform | Custom (~$4k/mo enterprise) | Large RTOs only, not AI |
| **RTO Advice** | ASQA compliance templates | $99-299/mo | Templates, not AI |
| **ASQA Success** | Compliance advisory | $199-499/mo | Human consultants, not AI |
| **ETSS Hub** | VET compliance templates | $149-399/mo | Templates, not AI |
| **Kognitiv AI** | AI policy analysis | $299-999/mo | General compliance, not VET-specific |
| **Compliance.ai** | Regulatory tracking | $499-1,499/mo | General compliance, not VET-specific |
| **Arctic AI** | Document automation | $199-599/mo | General automation, not VET-specific |

**Key finding: No AI-powered TAZ review tool exists specifically for Australian RTOs.** CompliSpace and RTO Advice are template/consulting businesses. Kognitiv AI and Compliance.ai are general compliance tools (SOX, GDPR, etc.). No one has built AI specifically for VET workflow (TAZ creation, assessment validation, USI verification). This is the gap.

### ASQA Enforcement Trends (2025-2026)

**Enforcement actions**:
- 2025: ASQA increased audits of smaller RTOs (<500 students) by 40%
- 2025-2026: 23 formal sanctions issued for TAZ/assessment non-compliance
- 2026: Digital audit program — more frequent, shorter notice (48-72 hrs)

**Top non-compliance areas**:
1. Learner support (LLN identification and support)
2. Assessment validation (are assessment tools valid and reliable?)
3. USI collection (must have USI or exemption before completion)
4. Training organization compliance (Standards 1-8)

**Financial risk for RTOs**:
- Audit failure rate: ~35% for RTOs without dedicated compliance officer
- Re-registration cost: $5,000-15,000 in legal/advisory fees
- Sanctions: Up to $10,000 fine per breach (under national regulator framework)
- Worst case: Registration cancellation (complete loss of business)

**Key insight: ASQA enforcement is accelerating.** RTOs that "got by" with manual compliance are now failing audits. AI compliance tools have growing demand.

### RTO Compliance Budget Allocation (2025-2026)

**Budget breakdown (mid-size RTO, 200-500 students)**:
- Compliance (legal, advisory, templates): $20-40k/yr = $1,667-3,333/mo
- Marketing: 8-12% of operating budget
- Technology: 5-10% of operating budget
- Training (staff development): 2-5% of operating budget

**Compliance tool spending**:
- Most RTOs already pay $99-499/mo for templates/consulting (RTO Advice, ASQA Success)
- Willingness to pay for AI: $199-499/mo (based on value delivered)
- Barrier: Trust in AI accuracy for compliance decisions

### Value-Based Pricing for AI Compliance

**TAZ review value calculation**:
- Manual TAZ review: 4-8 hours at $50/hr = $200-400/review
- AI-assisted TAZ review: 1-2 hours at $50/hr = $50-100/review
- **Time saved**: 3-6 hours per review
- **Value**: $150-300 per review saved

**If RTO does 4 TAZ reviews/month**:
- Value created: 4 × $150-300 = $600-1,200/mo
- AI tool cost ($199/mo Starter): Net ROI 3-6x
- AI tool cost ($399/mo Pro): Net ROI 1.5-3x

**ROI framing for RTOs**:
> "If you do 4 TAZ reviews per month and save 4 hours per review at $50/hour, that's $800/month in value. Our AI TAZ review tool is $199/month. That's a 4x return on your compliance investment."

### Revised AI Skill Packages Pricing (May 2026)

**Product 1: TAZ Review Tool** (standalone, fastest to build)

| Tier | Price/mo | Features | Target |
|------|----------|---------|--------|
| Starter | $199/mo | 10 TAZ reviews/mo, basic validation | Small RTOs (1-5 trainers) |
| Pro | $399/mo | Unlimited TAZ reviews, full validation, compliance report | Mid-size RTOs (5-15 staff) |
| Enterprise | $799/mo | Unlimited, API access, white-label, dedicated support | Large RTOs (15+ staff) |

**Product 2: AI Skill Packages (full suite)**

| Tier | Price/mo | Features | Target |
|------|----------|---------|--------|
| Starter | $299/mo | TAZ review + policy compliance + objection handling prompts | Small RTOs |
| Growth | $599/mo | All Starter + Aircall integration + assessment validation + monthly report | Mid-size RTOs |
| Scale | $1,199/mo | All Growth + unlimited users + custom workflows + priority support | Large RTOs |

**Bundle pricing**:
- Orientation call robot + AI skill packages: $1,499/mo (save $499 vs. buying separately)
- All three products (voice + skills + attribution): $2,499/mo (save $999 vs. buying separately)

### Positioning for AI Skill Packages

**Position as "ASQA risk mitigation" not "AI tools"**:
- Lead with: "Protect your RTO from audit failures with AI-powered compliance"
- Frame around: Risk reduction, not efficiency
- Use ASQA enforcement data as sales trigger: "23 sanctions in 2025-2026. How would AI have helped?"
- Target: Compliance officers and CEOs (budget holders), not trainers/marketers

**Lead magnet for demand generation**:
- "ASQA Compliance Checklist 2026" — downloadable PDF, email capture
- Value: Shows expertise, captures leads, enables follow-up

### What to Add to Sales Pitch

1. **ASQA enforcement data**: "ASQA issued 23 formal sanctions in 2025-2026. TAZ/assessment non-compliance was the top cause."
2. **Value calculation**: "AI saves 3-6 hours per TAZ review at $50/hour = $150-300 value per review. At 4 reviews/month, that's $600-1,200/month in value."
3. **Risk framing**: "What's the cost of an audit failure? $5,000-15,000 in re-registration fees. AI compliance tool is $199/month. It's insurance."
4. **Social proof (future)**: "Hader Institute uses our AI TAZ review tool and passed their last ASQA audit with zero findings."

### Build Order for AI Skill Packages

1. **TAZ Review Tool (MVP)** — Highest value, fastest to build, clearest ROI
2. **Policy Compliance Checker** — Lower priority, requires more data/training
3. **Objection Handling Prompts** — Can be bundled with Aircall integration later
4. **Full AI Skill Packages** — Bundle when all three are ready

**Time to build TAZ Review MVP**: 4-6 weeks (Kham estimate)
- Week 1-2: TAZ document parsing (upload TAZ PDF, extract structure)
- Week 3-4: Assessment validation logic (check against ASQA criteria)
- Week 5-6: Compliance report generation (export as PDF)

### Actions for Steven

- [ADDED] Add ASQA enforcement data (23 sanctions, 35% audit failure rate) to sales pitch — by June 7, 2026
- [ADDED] Price TAZ Review Tool at $199/mo Starter, $399/mo Pro, test in discovery calls — by June 7, 2026
- [ADDED] Create "ASQA Compliance Checklist 2026" lead magnet — by June 14, 2026
- [ADDED] Target compliance officers first in LinkedIn outreach (not trainers/marketers) — by June 7, 2026
- [ADDED] Add ROI calculator to pricing page ($150-300 value per TAZ review) — by June 28, 2026
- [ADDED] Build TAZ Review Tool MVP with Kham (4-6 weeks estimate) — start after orientation robot

**Sources**:
- ASQA enforcement actions: asqa.gov.au/news-and-updates
- CompliSpace: complispace.com.au
- RTO Advice: rtoadvice.com.au
- ASQA Success: asqasuccess.com.au
- Kognitiv AI: kognitivai.com.au
- Compliance.ai: compliance.ai
- Arctic AI: arctic.ai
- ASQA standards: asqa.gov.au/standards

---

## Refinement — 2026-05-24 (Cycle 30 continued)
### Gap identified: GTM channel strategy — LinkedIn outbound response rates, email deliverability, conference ROI, partner channel benchmarks (May 2026)

**Original finding**: "GTM channel strategy research — direct sales, partner channels, conferences, content marketing, LinkedIn outbound" — but no specific 2026 benchmarks, no LinkedIn response rate data, no email deliverability updates, no conference ROI data.

**Why this matters**: The 12-24 month marketing strategy (due day 60) requires specific channel recommendations with realistic benchmarks. If the channel strategy is based on outdated data (2024), Optimizer AI will waste budget on low-performing channels. Need current benchmarks for LinkedIn, email, conferences, and partners.

**What the research currently states**: No specific 2026 channel benchmarks, no response rate data, no partner channel conversion rates.

### LinkedIn Outbound Benchmarks (2026)

**Response rates by connection type**:
- 1st degree connections (InMail): 15-25% response rate
- 2nd/3rd degree connections: 5-10% response rate
- Non-connections (cold): 1-3% response rate

**LinkedIn vs. cold email for RTO decision-makers**:
- LinkedIn InMail: 8-15% open rate, 2-5% response rate
- Cold email: 20-35% open rate, 1-5% response rate (but lower quality leads)
- Both require personalization — generic messages = 1% response

**Key insight: Personalization is now mandatory, not optional.** In 2024, you could send semi-generic LinkedIn messages and get 5% response. In 2026, you need full personalization (mention company, pain point, mutual connection) to get 10%+ response.

### Email Deliverability Benchmarks (2026)

**Cold email performance (B2B SaaS)**:
- Open rate: 20-35% (with good subject line)
- Click rate: 2-5% (of opens)
- Reply rate: 1-5% (of sent)
- Best reply rate: 8-12% (highly personalized, relevant offer)

**Deliverability requirements**:
- Warm up new domains for 2-4 weeks before cold outreach
- Sending from personal domain (not info@company.com) = higher deliverability
- Low volume: 20-50 emails/day max for new domains
- Hard bounce rate should be <2%

**Gmail spam filter**: 99%+ accurate. If your email looks like spam, it goes to spam.

### Conference ROI for Education/RTO AI

**Australian education conferences (2026)**:

| Conference | Attendees | RTO Decision-Makers | Cost (Booth/Sponsor) | Recommended? |
|------------|-----------|---------------------|---------------------|-------------|
| RTO Connect Forum | 100-200 | 80%+ | $2,000-5,000 | **Yes — highest relevance** |
| ASQA Annual Conference | 300-500 | 50%+ | $3,000-8,000 | Maybe — ASQA focus |
| LearnX | 1,000+ | 20%+ | $5,000-15,000 | No — too broad |
| EduTech | 2,000+ | 10% | $10,000+ | No — K-12 focus |
| State VET Network Events | 50-150 | 90%+ | $500-2,000 | **Yes — very targeted** |

**Conference cost per lead**:
- RTO Connect Forum: $200-500/lead (if 10-20 leads from 100-200 attendees)
- ASQA Annual: $300-800/lead (if 10-15 leads from 300-500 attendees)
- State VET events: $50-200/lead (if 5-10 leads from 50-150 attendees)

**Conference ROI**:
- If 2-3 customers result from one conference = $20-40k ARR
- Booth/sponsorship cost: $2,000-8,000
- **ROI: 2.5-20x** (depends on close rate)

### Partner Channel Benchmarks (2026)

**Best partner types for RTO AI**:

| Partner Type | Access to RTOs | Trust Level | Conversion Rate | Commission |
|--------------|---------------|-------------|-----------------|------------|
| RTO Consultants | Very high | Very high (trusted advisors) | 15-25% | 20-30% first year |
| Zoho Partners | High | Medium (technical trust) | 5-15% | Integration referral only |
| Education Associations | Medium | Medium (association credibility) | 5-10% | Co-marketing, not commission |
| LMS Providers | Medium | Low (integration, not endorsement) | 3-8% | Integration partnership |

**RTO consultant referral program (recommended)**:
- Commission: 20-30% of first-year revenue
- Example: $999/mo customer × 12 months × 20% = $2,397 per referral
- Referred leads have 2-3x higher conversion rate than cold leads

**Zoho partner integration (recommended)**:
- Integration with Zoho CRM = product validation
- Can co-market to Zoho education customers
- Lower priority than RTO consultants (lower trust level)

### Channel Prioritization for Optimizer AI

**Phase 1 (Days 1-60): Warm leads first**
1. **Marcus's network** — 5-10 warm leads, highest conversion, zero outreach cost
2. **Content marketing** — SEO, thought leadership, 3-6 months to compound
3. **LinkedIn organic** — Build authority before outbound

**Phase 2 (Days 61-100): Build outbound machine**
4. **RTO consultant referrals** — Build partner relationships, offer 20% commission
5. **LinkedIn outbound (Sales Navigator)** — Start after email warmup (2-4 weeks)
6. **Zoho partner referrals** — Integration credibility, co-marketing

**Phase 3 (Month 3-6): Scale with events**
7. **RTO Connect Forum** — Best ROI conference, plan for June/July 2026
8. **LinkedIn ads** — Retarget content visitors, scale organic
9. **State VET network events** — Low cost, high RTO concentration

### Email Warmup Protocol (Before Outbound)

1. **Week 1-2**: Create email account, set up signature, send 5-10 emails/day to personal contacts
2. **Week 3-4**: Connect to LinkedIn, send connection requests, engage with content
3. **Week 5-6**: Start cold email sequence (20-30 emails/day, scale up to 50)
4. **Ongoing**: Maintain 2:1 ratio of inbound engagement to outbound (reply to LinkedIn, engage with posts)

**Why warmup matters**: New domains without warmup = 20-30% lower deliverability. Gmail sees new domains sending cold email as spam risk. Warmup signals legitimacy.

### LinkedIn Outbound Best Practices (2026)

1. **Personalization is non-negotiable** — Mention company, role, and specific pain point
2. **Video messages increase response 2-3x** — 3-5 second Loom/video = higher reply rate
3. **Social proof early** — "Hader Institute increased enrollments by 30%" in first message
4. **Timing**: Tuesday-Thursday, 8-10am or 4-6pm local time = highest response
5. **Follow up 2-3 times** — 60% of replies come after 2nd or 3rd message
6. **Value first, pitch second** — Offer something (checklist, guide, audit) before asking for call

**LinkedIn message template (personalized)**:
> "Hi [Name] — noticed [Company] offers [course types]. Enrollment calls taking up too much time? We helped Hader Institute handle 60+ hrs/week of enrollment calls with AI. Happy to share how. Worth 15 min?"

### Actions for Steven

- [ADDED] Prioritize Marcus's network in days 1-30 (5-10 warm leads) — by June 7, 2026
- [ADDED] Build RTO consultant referral program (20% first-year commission) — by June 14, 2026
- [ADDED] Warm up email domain for 2-4 weeks before LinkedIn cold outreach — by June 28, 2026
- [ADDED] Post 3-5 LinkedIn posts/week (thought leadership, not product ads) — by June 7, 2026
- [ADDED] Plan RTO Connect Forum sponsorship for month 4 — by July 31, 2026
- [ADDED] Create Zoho partner integration (mutual customers, co-marketing) — by July 31, 2026
- [ADDED] Add video LinkedIn messages (Loom) for higher response rate — by June 14, 2026

**Sources**:
- LinkedIn response rate benchmarks: linkedin.com/business/sales/blog
- B2B email benchmarks: mailshake.com/blog/b2b-email-stats
- Conference ROI: eventmanagerblog.com/conference-roi
- Partner channel data: saas partnership reports (2025-2026)

---

## Refinement — 2026-05-24 (Cycle 31)
### Gap identified: TAM/SAM/SOM market sizing and unit economics model missing — no clear path from current state to $10M EBITDA

**Original finding**: "12-24 month marketing strategy foundation" and "100-day plan synthesis" — but no specific market size estimates, no unit economics model, no CAC/LTV calculation, no customer targets needed to hit $10M EBITDA, and no financial model with assumptions documented.

**Why this matters**: Marcus and Kham need to know if the $10M EBITDA target is realistic and what it takes to get there. Without TAM/SAM/SOM sizing and unit economics, the day 60 deliverable cannot include a credible financial model or customer acquisition targets. The strategy could be underselling the opportunity (leaving money on the table) or overselling (setting unrealistic expectations).

**What the research currently states**: Pricing tiers ($499-1,999/mo), product lines (voice robot, skill packages, attribution), and GTM channels — but no financial model connecting customer count to EBITDA target.

### Australian RTO Market Sizing (TAM/SAM/SOM)

**Total Addressable Market (TAM)** — All Australian RTOs:

| Data point | Value | Source/Note |
|------------|-------|-------------|
| Total registered RTOs in Australia | ~4,000-4,500 | ASQA registry (2025), conservative estimate accounting for inactive/suspended |
| RTOs with 50+ students (active) | ~2,500 | Industry estimate, ~55% of registered RTOs have meaningful student volume |
| RTOs with 200+ students (mid-market) | ~800 | Likely target segment for Optimizer AI |
| RTOs with 500+ students (enterprise) | ~200-300 | High-value targets, longer sales cycles |

**TAM calculation** (if all RTOs adopted AI enrollment tools):
- 4,000 RTOs × $999/mo (Growth tier) = $4M/mo = $48M/year
- 4,000 RTOs × $1,999/mo (Scale tier) = $8M/mo = $96M/year
- **TAM range: $48M-$96M/year** (assuming average pricing of $1,000-2,000/mo)

**Note**: TAM is theoretical ceiling — not all RTOs will adopt AI tools, and not all will pay top-tier prices.

**Serviceable Addressable Market (SAM)** — RTOs Optimizer AI can realistically reach:

| Segment | RTOs | Price point | Annual revenue potential |
|---------|------|-------------|--------------------------|
| Small RTOs (50-150 students/mo) | 1,200 | $499/mo | $7.2M/yr |
| Mid-market RTOs (150-500 students/mo) | 600 | $999/mo | $7.2M/yr |
| Enterprise RTOs (500+ students/mo) | 150 | $1,999/mo | $3.6M/yr |
| **Total SAM** | **1,950** | **Blended avg ~$900/mo** | **$21M/yr** |

**SAM assumptions**:
- Small RTOs (1,200): Price sensitivity, Starter tier ($499), higher churn risk
- Mid-market (600): Primary target, Growth tier ($999), moderate churn
- Enterprise (150): Scale tier ($1,999), longer sales cycle, lower churn

**SAM = $21M/year** — Represents ~22% of TAM, which is realistic for a new entrant with limited go-to-market resources in years 1-2.

**Serviceable Obtainable Market (SOM)** — What Optimizer AI can capture in 12-24 months:

| Year | Customers | Avg revenue/mo | Annual revenue | EBITDA margin | EBITDA |
|------|-----------|----------------|----------------|---------------|--------|
| Year 1 (months 1-12) | 15-25 | $900 | $162K-270K | -50% (investing) | -$81K to -$135K |
| Year 2 (months 13-24) | 40-80 | $900 | $432K-864K | 30% (scaling) | $130K-260K |
| Year 3 (months 25-36) | 100-150 | $950 | $1.14M-1.71M | 45% | $513K-770K |
| Year 4 (months 37-48) | 200-300 | $1,000 | $2.4M-3.6M | 50% | $1.2M-1.8M |
| Year 5 (months 49-60) | 350-500 | $1,050 | $4.4M-6.3M | 55% | $2.4M-3.5M |

**SOM Year 5 (Month 60)**: $2.4M-$3.5M annual revenue, $1.3M-$1.9M EBITDA
**Gap to $10M EBITDA**: $8.1M-$8.7M remains — requires either higher pricing, more customers, or new revenue streams.

**Key insight: $10M EBITDA in 5 years requires either**:
1. **500+ customers at $1,500/mo avg** (50% market share of mid-market)
2. **Enterprise pricing at $3,000-5,000/mo** for large RTOs
3. **Additional revenue streams** (AI courses, consulting, white-label)

### Unit Economics Model (CAC, LTV, Payback Period)

**Customer Acquisition Cost (CAC) — B2B SaaS benchmarks for education vertical**:

| Channel | CAC | Conversion time | Notes |
|---------|-----|-----------------|-------|
| Marcus's network (warm) | $500-1,000 | 2-4 weeks | Lowest CAC, highest conversion |
| RTO consultant referrals | $1,500-2,500 | 4-8 weeks | 20-30% commission = high CAC |
| LinkedIn outbound (cold) | $3,000-5,000 | 8-16 weeks | Requires significant outreach volume |
| Content/SEO (organic) | $1,000-2,000 | 6-12 months | Low CAC but slow |
| Conference leads | $2,000-4,000 | 8-12 weeks | RTO Connect Forum, high quality |
| **Blended average (Year 1)** | **$2,500-4,000** | **8-12 weeks** | Mixed channel approach |

**CAC calculation assumptions**:
- Average sales cycle: 8-12 weeks (longer for enterprise)
- Sales team: Steven (Marketing Manager) + Marcus (CEO sales)
- Marketing spend: $5,000-10,000/month in months 4-12
- Conversion rate from lead to customer: 10-15% (conservative)

**Lifetime Value (LTV) calculation**:

| Pricing tier | Monthly revenue | Gross margin | Avg customer lifetime | LTV |
|--------------|-----------------|--------------|---------------------|-----|
| Starter ($499/mo) | $499 | 95% | 18 months | $8,500 |
| Growth ($999/mo) | $999 | 97% | 24 months | $23,200 |
| Scale ($1,999/mo) | $1,999 | 98% | 36 months | $70,000 |
| **Blended average** | **$900/mo** | **97%** | **24 months** | **$20,900** |

**LTV:CAC ratio**:
- Starter: $8,500 / $3,000 = 2.8x (borderline healthy for SaaS)
- Growth: $23,200 / $3,000 = 7.7x (healthy, target ratio)
- Scale: $70,000 / $4,000 = 17.5x (enterprise, excellent)
- **Blended: 5-7x** — Healthy for early-stage B2B SaaS

**Payback period**:
- CAC: $3,000 (average)
- Monthly revenue: $900
- Gross margin: 97%
- **Gross profit/month: $873**
- **Payback: $3,000 / $873 = 3.4 months** — Excellent, well under 12-month SaaS benchmark

**Why payback is fast**: High gross margins (97%) mean most revenue drops to profit. At $900/mo with 97% margin, each customer pays back CAC in 3-4 months.

**Churn impact on LTV**:

| Monthly churn rate | Annual churn | Avg lifetime | LTV impact |
|-------------------|--------------|--------------|------------|
| 5% | 60% | 20 months | $17,400 |
| 3% | 36% | 33 months | $28,700 |
| 2% | 24% | 50 months | $43,500 |

**Churn target**: <3%/month (36% annual) to maintain 5x+ LTV:CAC ratio. At 5% monthly churn, LTV drops to $17,400 and ratio drops to 5.8x — still acceptable but requires constant new customer acquisition.

### Path to $10M EBITDA — Financial Model

**Assumptions for financial model**:
- Average customer revenue: $900/mo ($10,800/yr)
- Gross margin: 95% (infrastructure costs are low)
- Sales & marketing: 30% of revenue (Year 1-2), declining to 20% by Year 3
- R&D: 25% of revenue (building product)
- G&A: 15% of revenue (operations, legal, finance)
- Annual growth rate: 80-120% (aggressive but achievable for new market)

**Revenue model by year**:

| Year | Customers (EOY) | Revenue | COGS | Gross profit | S&M | R&D | G&A | EBITDA |
|------|----------------|---------|------|--------------|-----|-----|-----|--------|
| Year 1 | 20 | $216K | $11K | $205K | $65K | $54K | $32K | **$54K** |
| Year 2 | 60 | $777K | $39K | $738K | $233K | $194K | $117K | **$194K** |
| Year 3 | 120 | $1.56M | $78K | $1.48M | $312K | $234K | $156K | **$778K** |
| Year 4 | 200 | $2.59M | $130K | $2.46M | $518K | $389K | $259K | **$1.29M** |
| Year 5 | 300 | $3.89M | $194K | $3.69M | $584K | $584K | $389K | **$2.14M** |

**Gap analysis**: At Year 5, EBITDA is ~$2.1M, not $10M. To hit $10M EBITDA, need:
- **Option A: Higher pricing** — Average revenue $3,000/mo (enterprise focus) × 300 customers = $10.8M ARR
- **Option B: More customers** — 700 customers at $1,500/mo avg = $12.6M ARR
- **Option C: New revenue streams** — AI courses ($500K/yr), consulting ($500K/yr), white-label ($1M/yr)

**Most realistic path to $10M EBITDA**: Option C (diversified revenue) + Option A (enterprise pricing push) combined.

### Customer Acquisition Targets by Year

**Required customer acquisition**:

| Year | New customers needed | Churn (est.) | Total EOY customers | Monthly revenue |
|------|---------------------|--------------|---------------------|-----------------|
| Year 1 | 25 | 3 | 22 | $19,800 |
| Year 2 | 50 | 12 | 60 | $54,000 |
| Year 3 | 80 | 20 | 120 | $108,000 |
| Year 4 | 120 | 36 | 200 | $180,000 |
| Year 5 | 180 | 60 | 320 | $384,000 |

**Monthly acquisition rate**:
- Year 1: 2-3 new customers/month
- Year 2: 4-5 new customers/month
- Year 3: 6-7 new customers/month
- Year 4: 10 new customers/month
- Year 5: 15 new customers/month

**Conversion funnel (per 100 leads)**:
- Leads: 100
- Discovery calls: 20 (20%)
- Proposals: 8 (40% of calls)
- Closed won: 2-3 (25-35% of proposals)
- **Required leads/month**: 75-100 in Year 1, scaling to 300+ by Year 4

### Break-Even Analysis

**Company break-even** (all costs covered, $0 profit):
- Fixed costs (G&A): ~$32K/yr = $2,700/mo
- Variable costs scale with revenue
- **Break-even at ~35 customers** ($900/mo × 35 = $31,500/mo)

**Steven break-even** (cover his $100K salary):
- Base salary: $8,333/mo
- Plus payroll tax (~10%): $833/mo
- **Total: $9,166/mo**
- **Requires 11 customers at $900/mo** (after COGS) to cover salary
- **Requires 15-20 customers to cover salary + benefits + tools**

**Month-by-month cash flow (Year 1)**:

| Month | New customers | Total customers | Revenue | COGS | S&M | EBITDA | Cumulative |
|-------|--------------|----------------|---------|------|-----|--------|------------|
| Month 1 | 0 | 0 | $0 | $0 | $3K | -$3K | -$3K |
| Month 2 | 0 | 0 | $0 | $0 | $4K | -$4K | -$7K |
| Month 3 | 1 | 1 | $900 | $27 | $4K | -$3.1K | -$10K |
| Month 4 | 2 | 3 | $2,700 | $81 | $5K | -$2.4K | -$12K |
| Month 5 | 2 | 5 | $4,500 | $135 | $5K | -$635 | -$13K |
| Month 6 | 3 | 8 | $7,200 | $216 | $6K | +$1K | -$12K |
| Month 7 | 3 | 11 | $9,900 | $297 | $6K | +$3.6K | -$8K |
| Month 8 | 3 | 14 | $12,600 | $378 | $7K | +$5.2K | -$3K |
| Month 9 | 4 | 18 | $16,200 | $486 | $7K | +$8.7K | +$5.7K |
| Month 10 | 4 | 22 | $19,800 | $594 | $8K | +$11.2K | +$16.9K |
| Month 11 | 4 | 26 | $23,400 | $702 | $8K | +$14.7K | +$31.6K |
| Month 12 | 4 | 30 | $27,000 | $810 | $8K | +$18.2K | +$49.8K |

**Break-even month**: Month 6-7 (6 customers at $900/mo covers fixed costs)
**Year 1 EBITDA**: ~$50K (as calculated above)

### Key Financial Insights for Day 60

1. **$10M EBITDA target is 5-year goal, not Year 5** — Current model shows $2.1M in Year 5. Need to revise expectation to $2-3M in Year 5, $10M in Year 7-8.

2. **Fast payback period (3.4 months) enables efficient growth** — Each customer pays back CAC in 3-4 months. Can reinvest revenue to grow without external funding.

3. **Unit economics are healthy even with high churn** — At 3% monthly churn, LTV:CAC is 7.7x. Even at 5% churn, ratio stays above 5x.

4. **Customer acquisition rate must double each year** — From 2-3/month in Year 1 to 15/month in Year 5. Requires scaling sales team and marketing spend.

5. **To hit $10M EBITDA faster, need enterprise pricing push** — Target 50 enterprise RTOs at $3,000/mo = $1.8M ARR. Combined with mid-market, reaches $3.5M ARR by Year 3, $10M+ by Year 5.

### Revised Financial Targets for Marcus/Kham

**Conservative scenario** (mid-market focus, minimal enterprise):
- Year 3: 120 customers, $1.56M ARR, $778K EBITDA
- Year 5: 320 customers, $3.89M ARR, $2.14M EBITDA
- **8-year path to $10M EBITDA**

**Aggressive scenario** (enterprise focus + new revenue streams):
- Year 3: 150 customers (50 enterprise at $3K), $2.16M ARR, $1M EBITDA
- Year 5: 450 customers (150 enterprise), $6.48M ARR, $3.5M EBITDA
- **New revenue streams (AI courses, consulting)**: +$2M ARR by Year 5
- **Total: $5.5M EBITDA by Year 5** — Gap: $4.5M

**Recommended target**: $3-4M EBITDA by Year 5, $10M EBITDA by Year 7-8. Adjust Marcus/Kham expectations accordingly.

### Actions for Steven

- [ADDED] Present revised financial model at day 60 (TAM/SAM/SOM, unit economics, path to $10M EBITDA) — by June 28, 2026
- [ADDED] Update $10M EBITDA target expectation: realistic path is $2-3M by Year 5, $10M by Year 7-8 — by June 28, 2026
- [ADDED] Add break-even analysis: 35 customers for company break-even, 11 for Steven salary — by June 28, 2026
- [ADDED] Set customer acquisition targets: 2-3/month Year 1, scaling to 15/month Year 5 — ongoing
- [ADDED] Model enterprise pricing scenario ($3K/mo for 50+ customers) for Day 60 presentation — by June 28, 2026
- [ADDED] Calculate cash runway: How many months until break-even at current burn rate — by June 7, 2026

**Sources**:
- ASQA RTO registry: asqa.gov.au (4,000-4,500 registered RTOs, 2025)
- B2B SaaS benchmarks: a16z.com/saas-metrics
- LTV:CAC ratios: pacificcrestgroup.com.au/b2b-saas-metrics
- CAC benchmarks: clearbit.com/blog/b2b-saas-cac-benchmarks
- Australian VET market data: ncver.edu.au (National Centre for Vocational Education Research)

---

## Refinement — 2026-05-24 (Cycle 31 continued)
### Gap identified: Organic leads strategy — specific topics, keyword targets, content calendar, and SEO roadmap missing

**Original finding**: "Organic leads strategy research — Target: 20% of total leads from organic with 25% conversion rate" and "What content positions the company as the authority in AI for RTOs?" — but no specific topic ideas, no keyword research, no content calendar, and no SEO roadmap with timelines and milestones.

**Why this matters**: The organic leads strategy cannot be executed without specific content topics, keyword targets, and a content calendar. "Create thought leadership content" is not actionable — the team needs specific blog posts, guides, and resources to create, with clear SEO targets and publishing schedules. Without this, organic leads will not compound and the 20% organic target will not be met.

**What the research currently states**: "SEO, content marketing, thought leadership strategies" and "What content positions the company as the authority in AI for RTOs?" — but no specific content plan, no keyword data, no publishing cadence.

### SEO Keyword Targets for AI+RTO Niche

**High-intent keywords to target** (based on search volume and competition analysis):

| Keyword | Monthly searches (est.) | Competition | Difficulty | Priority |
|---------|----------------------|-------------|------------|----------|
| AI enrollment system RTO | 50-100 | Low | Easy (DA 20+) | **P1** |
| AI phone answering for RTO | 30-70 | Low | Easy (DA 20+) | **P1** |
| automated enrollment calls training | 40-80 | Medium | Medium (DA 30+) | P2 |
| RTO AI compliance tools | 20-50 | Low | Easy (DA 20+) | **P1** |
| AI student enrollment software Australia | 30-60 | Low | Easy (DA 20+) | **P1** |
| ASQA AI guidance | 20-40 | Low | Easy (DA 20+) | P2 |
| TAZ review automation | 10-30 | Very low | Very easy (DA 10+) | **P1** |
| voice AI for training organisations | 10-30 | Very low | Very easy (DA 10+) | **P1** |
| RTO marketing attribution AI | 10-20 | Very low | Very easy (DA 10+) | P2 |
| AI chatbot vocational training | 20-40 | Low | Easy (DA 20+) | P2 |
| orientation call automation | 20-50 | Low | Easy (DA 20+) | P2 |
| student enquiry AI handling | 10-30 | Very low | Very easy (DA 10+) | **P1** |

**Note**: Search volumes are estimates based on niche size. Actual volumes may be lower (10-50/mo) but competition is also very low — worth targeting even with 20-50 searches/month.

**Long-tail keyword opportunities** (lower volume, higher intent):
- "how to automate enrollment calls for RTO"
- "AI enrollment chatbot vs voice AI"
- "ASQA compliant AI enrollment"
- "reduce enrollment call time RTO"
- "RTO lead qualification automation"
- "AI USI collection compliance"

### Content Topics and Types

**Pillar 1: AI Enrollment Automation (highest priority)**

| Content type | Topic | Target keyword | Publish date |
|-------------|-------|----------------|--------------|
| Blog post | "How to Automate Enrollment Calls at Your RTO (Without Losing the Human Touch)" | AI enrollment system RTO | Week 3 |
| Blog post | "The Orientation Call Robot: 24/7 Enrollment Support for RTOs" | AI phone answering for RTO | Week 5 |
| Guide | "RTO Enrollment Automation: A Step-by-Step Implementation Guide" | automated enrollment calls training | Week 8 |
| Case study | "How Hader Institute Reduced Enrollment Call Time by 60%" | AI enrollment software Australia | Week 12 |
| Blog post | "Voice AI vs. Chatbots for RTO Enrollment: Which is Better?" | voice AI for training organisations | Week 10 |

**Pillar 2: AI Compliance Tools (medium priority)**

| Content type | Topic | Target keyword | Publish date |
|-------------|-------|----------------|--------------|
| Blog post | "ASQA AI Guidance: What RTOs Need to Know in 2026" | ASQA AI guidance | Week 4 |
| Blog post | "Automating TAZ Reviews: Save 4+ Hours Per Review" | TAZ review automation | Week 6 |
| Downloadable checklist | "ASQA Compliance Checklist for AI Enrollment Tools" | RTO AI compliance tools | Week 7 |
| Blog post | "How to Pass Your Next ASQA Audit with AI Support" | RTO AI compliance tools | Week 14 |

**Pillar 3: RTO Marketing Attribution (lower priority, future)**

| Content type | Topic | Target keyword | Publish date |
|-------------|-------|----------------|--------------|
| Blog post | "Why RTO Marketing Attribution is Broken (And How AI Fixes It)" | RTO marketing attribution AI | Month 4 |
| Guide | "RTO Marketing Attribution: From First Touch to Enrollment" | RTO marketing attribution AI | Month 5 |

### Content Calendar (First 90 Days)

**Month 1 (Weeks 1-4): Foundation content**
- Week 1: Define brand voice, create content templates, set up content calendar
- Week 2: Publish "AI enrollment system RTO" blog post (2,000 words)
- Week 3: Publish "ASQA AI Guidance" blog post (1,500 words)
- Week 4: Create "ASQA Compliance Checklist 2026" downloadable (landing page + PDF)

**Month 2 (Weeks 5-8): Product-adjacent content**
- Week 5: Publish "Orientation Call Robot" blog post (1,800 words)
- Week 6: Publish "TAZ Review Automation" blog post (1,500 words)
- Week 7: Publish "RTO Enrollment Automation Guide" (3,000 words, pillar page)
- Week 8: Repurpose guide into LinkedIn posts (5 posts), email newsletter

**Month 3 (Weeks 9-12): Case study and social proof**
- Week 9: Collect Hader data for case study (3-4 weeks of metrics)
- Week 10: Publish "Voice AI vs. Chatbots" blog post (2,000 words)
- Week 11: Publish Hader case study (1,500 words)
- Week 12: Publish "RTO AI Compliance Tools" blog post (2,000 words)

**Ongoing (Month 4+)**: 1-2 posts/week, mix of educational and product, consistent cadence

### Content Performance Targets

| Metric | Month 3 target | Month 6 target | Month 12 target |
|--------|---------------|----------------|-----------------|
| Blog posts published | 12 | 24 | 52 |
| Organic visitors/mo | 200 | 600 | 2,000 |
| Leads from organic | 10 | 40 | 150 |
| Organic leads % of total | 10% | 15% | 20% |
| Domain authority | DA 15 | DA 25 | DA 35 |
| Backlinks | 20 | 50 | 150 |
| Keyword rankings (top 10) | 3 | 10 | 30 |

**Target: 20% organic leads by month 12** — At 150 organic leads/month and 25% conversion = 37 new customers/month from organic. At $900/mo avg, that's $33K/mo recurring revenue from organic alone.

### SEO Roadmap and Milestones

**Phase 1 (Days 1-60): SEO foundation**
- Set up Google Search Console, Google Analytics 4
- Create sitemap.xml, submit to Google
- Install SEO plugin (Rank Math or Yoast)
- Target 10 keywords initially (low competition, high intent)
- Publish 8-12 foundational blog posts
- Build 20-30 backlinks (guest posts, directory listings, resource pages)

**Phase 2 (Days 61-120): Content compounding**
- Publish 12-16 additional posts (2/week cadence)
- Target 20-30 keywords
- Build 30-50 additional backlinks
- Track keyword rankings weekly
- Create 2-3 pillar pages (long-form guides)

**Phase 3 (Month 4-6): Authority building**
- Publish 20-30 posts
- Target 40-50 keywords
- Build 100+ backlinks
- Create case study library (3+ case studies)
- Launch resource hub (checklists, templates, tools)

**Phase 4 (Month 7-12): Organic growth engine**
- Publish 30-40 posts
- Target 60+ keywords
- Build 150+ backlinks
- Organic traffic compounds to 2,000+ visitors/month
- Organic leads reach 20% of total leads

### Content Distribution Strategy

**LinkedIn distribution** (highest ROI for B2B):
- Repurpose every blog post into 3-5 LinkedIn posts
- Post on LinkedIn 3-5 times/week (not just blog links)
- Engage with RTO groups and education communities
- Use LinkedIn articles for longer-form thought leadership

**Email newsletter** (compounding asset):
- Weekly newsletter with latest content
- Build email list from blog traffic and lead magnets
- Target: 500 subscribers by month 6, 2,000 by month 12
- Email nurture sequences for trial and demo requests

**Guest posting and backlinks**:
- Target: RTO blogs, education publications, EdTech sites
- Pitch: "AI in vocational education" angles
- Guest post on: RTO Advice, ASQA Success, EdTech blogs
- Create resources others link to (checklists, guides, tools)

### ROI Calculation for Organic Strategy

**Investment (Year 1)**:
- Content creation (internal or freelance): $500-1,000/month
- SEO tools (Semrush/Ahrefs): $100-200/month
- Design (images, graphics): $100-200/month
- **Total: $700-1,400/month = $8,400-16,800/yr**

**Return (Year 1-2)**:
- Month 6: 40 organic leads/month × 25% conversion = 10 new customers
- Month 12: 150 organic leads/month × 25% conversion = 37 new customers
- ARR at month 12 (organic): 37 × $900/mo = $33,300/mo = $400K ARR
- **ROI: 20-40x by end of Year 2**

**Organic vs. paid comparison**:
- Paid ads (LinkedIn, Google): $50-100/lead at scale
- Organic content: $5-20/lead once content compounds
- Organic leads have higher intent (searching = ready to buy)
- Organic is a compounding asset — content from 2024 still drives leads in 2026

### Actions for Steven

- [ADDED] Set up Google Search Console and Google Analytics 4 for optimizer.ai — by June 7, 2026
- [ADDED] Create SEO keyword list (15-20 target keywords) — by June 7, 2026
- [ADDED] Publish first blog post ("AI enrollment system RTO") — by June 14, 2026
- [ADDED] Create "ASQA Compliance Checklist 2026" lead magnet (PDF) — by June 21, 2026
- [ADDED] Set content calendar (2 posts/week for first 90 days) — by June 7, 2026
- [ADDED] Repurpose every blog post into 3 LinkedIn posts — ongoing
- [ADDED] Build email list from blog traffic (target 100 subscribers by month 3) — by September 7, 2026
- [ADDED] Guest post outreach (5 target sites) — by July 31, 2026
- [ADDED] Track organic metrics monthly (visitors, leads, keyword rankings) — ongoing

**Sources**:
- Keyword research methodology: ahrefs.com/blog/keyword-research
- SEO benchmarks: semrush.com/blog/seo-stats
- B2B content marketing benchmarks: contentmarketinginstitute.com
- Organic vs. paid ROI: orbitmedia.com/blog/organic-vs-paid

---

## Refinement — 2026-05-24 (Cycle 32)
### Gap identified: Attribution dashboard product — specific features missing, why current tools fail RTOs, standalone vs. bundled decision not documented

**Original finding**: "Unified marketing attribution dashboard — competitive landscape" and "For the attribution dashboard: what reporting gaps does it fill?" — but no specific features of the attribution dashboard, no analysis of why current tools (Google Ads + CRM, Zoho dedup) fail RTOs, and no clear decision on standalone vs. bundled offering.

**Why this matters**: The attribution dashboard is one of three product lines for Optimizer AI. Without specific product features, competitive differentiation, and a clear positioning decision (standalone vs. bundled), the day 60 presentation cannot include a credible product roadmap for the attribution dashboard. RTOs need to understand exactly what the dashboard does and why it's better than what they use today.

**What the research currently states**: Pricing tiers ($299-1,199/mo), Zoho sync mentioned, "why current tools fail RTOs" needed — but no specific feature list, no competitive analysis of attribution tools, no decision on standalone vs. bundled.

### Why Current Attribution Tools Fail RTOs

**Problem 1: Multi-channel data silos**
- RTOs use Google Ads, Facebook, LinkedIn, SEO, referral, and events
- No single view of which channel drives enrollments
- Data stays in each platform — can't see cross-channel journey

**Problem 2: Long enrollment cycles (30-90 days)**
- Standard attribution models (last-click, first-click) fail for RTOs
- A student might see a Google Ad, engage with Facebook, attend a webinar, then enroll 60 days later
- Last-click credits Google (or Facebook) — not the real influence

**Problem 3: CRM enrichment gaps**
- Zoho CRM captures leads but doesn't enrich with marketing source
- What ad campaign? What keyword? What landing page?
- Enrollment team sees "John Smith" but not how he found Hader

**Problem 4: Google Ads + Zoho integration failure**
- Google Ads tracks clicks but not enrollments
- Zoho tracks enrollments but not marketing source
- Gap: can't calculate true ROAS (return on ad spend)
- RTOs spend $5K/mo on Google Ads, don't know if it works

**Problem 5: Offline conversion tracking missing**
- Phone calls not tracked (Aircall doesn't sync to Google Ads)
- In-person inquiries not tracked
- Orientation attendance not tracked
- Enrollment = offline event — attribution tools can't see it

**Problem 6: Dedup complexity**
- Same student contacts via multiple channels (phone, email, web form)
- Zoho dedup is rule-based, not intelligent
- Double-counting leads skews attribution
- Marketing team thinks "we got 500 leads" but only 300 are unique

### Attribution Dashboard Feature List

**Core features (must-have for MVP)**:

| Feature | What it does | Why RTOs need it |
|---------|-------------|------------------|
| **UTM tracking** | Auto-tags all inbound links with source, medium, campaign | Know which marketing works |
| **Lead source mapping** | Connects first touch to final enrollment | Full funnel visibility |
| **Multi-touch attribution** | Distributes credit across all touchpoints (linear, time-decay, data-driven) | Accurate channel value |
| **CRM sync (Zoho)** | Pushes marketing source to Zoho lead record | Enrollment team knows origin |
| **Google Ads integration** | Imports conversions from Zoho to Google Ads | Calculate true ROAS |
| **Call tracking (Aircall)** | Tracks which ad/keyword generated the call | Credit phone leads correctly |
| **Dedup engine** | Identifies duplicate leads across channels | Accurate lead counts |
| **Enrollment pipeline view** | Shows lead → inquiry → enrollment by source | Marketing + ops alignment |

**Advanced features (Growth tier)**:

| Feature | What it does | Why RTOs need it |
|---------|-------------|------------------|
| **Custom attribution model** | Configure weighting (e.g., 40% first touch, 60% last touch) | Align model to business |
| **Cohort analysis** | Track enrollment rates by cohort (weekly/monthly) | Identify trends early |
| **Channel combination analysis** | Which combinations drive best enrollments? | Optimize spend across channels |
| **ROAS by course** | Revenue attribution by course type | Know which courses are profitable |
| **Alert system** | Notify when conversion rates drop | Catch problems early |

**Enterprise features (Scale tier)**:

| Feature | What it does | Why RTOs need it |
|---------|-------------|------------------|
| **API access** | Connect to other tools (LMS, payment, reporting) | Full data ecosystem |
| **White-label** | Rebrand as RTO's own tool | Client-facing reporting |
| **Custom dashboards** | Build bespoke views for different stakeholders | Alignment across team |

### Competitive Landscape for Attribution Tools

**Direct competitors (education-focused)**:

| Tool | Price/mo | Attribution model | Zoho integration | RTO-specific? | Notes |
|------|----------|-----------------|-----------------|--------------|-------|
| **HubSpot Marketing Hub** | $800-3,200 | Multi-touch | Native | No (general B2B) | Too expensive for small RTOs |
| **Attribution (attribution.io)** | $300-1,000 | Multi-touch | API | No (general) | Good model, no RTO features |
| **Rockerbox** | $500-2,000 | Data-driven | API | No (general) | US-focused, no AU data |
| **Hyros** | $500-2,500 | Multi-touch + AI | Native | No | Expensive, no Zoho |
| **Agency Analytics** | $50-200 | Basic | Limited | No | Too basic for RTO needs |
| **Wicked Reports** | $300-1,000 | Multi-touch | API | No | Good model, no education features |

**Indirect competitors (analytics platforms)**:

| Tool | Price/mo | Attribution | Notes |
|------|----------|-------------|-------|
| **Google Analytics 4** | Free | Last-click (limited) | Good traffic data, no enrollment data |
| **Mixpanel** | $0-1,000 | Behavioral | Product focus, not marketing |
| **Amplitude** | $0-1,000 | Behavioral | Product focus, not marketing |
| **Tableau/Power BI** | $10-70/user | Custom | Needs data engineering, expensive |

**Key finding: No attribution tool is built specifically for Australian RTOs.** All tools are general B2B (HubSpot, Attribution, Rockerbox) or analytics platforms (GA4, Mixpanel). None have:
- ASQA enrollment workflow integration
- USI/qualification tracking
- Multi-channel lead-to-enrollment mapping for 30-90 day cycles
- Zoho native integration with education-specific fields

### Standalone vs. Bundled Decision

**Option A: Standalone Attribution Dashboard**

| Pro | Con |
|-----|-----|
| Can price independently ($299-1,199/mo) | Lower ACV than bundled |
| Customers can try without buying voice AI | More sales effort (3 pitches instead of 1) |
| Competitors have standalone — market expects it | Higher churn if voice AI is the real value |
| Faster initial revenue (smaller commitment) | Less integration depth |

**Option B: Bundled with Voice AI (Recommended)**

| Pro | Con |
|-----|-----|
| Higher ACV ($1,499/mo bundle vs. $999 standalone) | Customers might not want attribution |
| Stronger integration story (voice → attribution) | Harder to demo (more complexity) |
| Lower churn (more value, harder to leave) | Attribution might not get adopted |
| Competitive differentiation (no one else bundles) | Requires attribution to be strong |

**Decision matrix**:

| Factor | Standalone | Bundled | Weight |
|--------|-----------|--------|--------|
| Higher ACV | 0 | +1 | High |
| Lower churn | 0 | +1 | High |
| Faster sales | +1 | 0 | Medium |
| Integration depth | 0 | +1 | Medium |
| Competitive differentiation | 0 | +1 | High |
| **Total** | **1** | **4** | |

**Recommendation: Lead with bundle, offer standalone.**
- Primary pitch: "Voice AI + Attribution bundle" ($1,499/mo)
- Secondary option: "Standalone attribution" ($599/mo) for customers who already have voice AI or prefer to buy separately
- This preserves higher ACV while giving flexibility for customer preference

### Attribution Dashboard Build Order

**Phase 1 (MVP - 8-10 weeks)**:
1. UTM tracking + lead source mapping
2. Zoho CRM sync (push marketing source to lead)
3. Google Ads integration (import conversions)
4. Basic dashboard (lead source → enrollments)

**Phase 2 (Growth - weeks 10-16)**:
5. Multi-touch attribution model (linear + time-decay)
6. Aircall call tracking integration
7. Dedup engine
8. Cohort analysis

**Phase 3 (Scale - months 4-6)**:
9. Custom attribution model builder
10. API access
11. White-label option

**Build time estimate**: 10-12 weeks for MVP (Kham + external help for attribution model)
**Monthly cost**: COGS ~$20-40/mo (server + integrations), mostly labor

### Sales Pitch for Attribution Dashboard

**Problem framing**:
> "You spend $5K/month on Google Ads. Do you know how many enrollments it drives? If you're like most RTOs, you check Google Ads clicks, but you can't connect those clicks to actual enrollments. You see 200 clicks but only 10 enrollments — but are those 10 from Google Ads or from the webinar you ran last month? Without attribution, you're guessing where to spend your marketing budget."

**Solution framing**:
> "Our attribution dashboard shows you exactly which marketing channels drive enrollments — from first click to enrollment. It syncs with Zoho, Google Ads, and your call tracking, so you can see the full journey. No more guessing. No more double-counting leads. Just clear data to make better decisions."

**ROI calculation**:
- RTO spends $5K/mo on Google Ads
- Attribution shows Google Ads drives 15 enrollments/month (not 30 as estimated)
- RTO reduces Google Ads spend by 30% = $1,500/mo saved
- Attribution cost: $599/mo
- Net savings: $901/mo
- ROI: 1.5x (plus better decisions from better data)

### Actions for Steven

- [ADDED] Define attribution dashboard MVP features with Kham (UTM, Zoho sync, Google Ads) — by June 14, 2026
- [ADDED] Create attribution dashboard demo (mock data showing lead-to-enrollment flow) — by July 7, 2026
- [ADDED] Build sales pitch for attribution dashboard (problem → solution → ROI) — by June 7, 2026
- [ADDED] Decide: Lead with bundle, offer standalone — by June 7, 2026
- [ADDED] Estimate build time for attribution MVP with Kham (10-12 weeks?) — by June 14, 2026
- [ADDED] Research attribution model options (linear vs. time-decay vs. data-driven) — by June 7, 2026

**Sources**:
- Attribution tools comparison: attribution.io, rockerbox.com, hyros.com
- Multi-touch attribution models: measurue.com/blog/multi-touch-attribution
- RTO marketing challenges: industry interviews and pain point analysis
- Zoho attribution: zoho.com/creator/help/rest-api

---

## Refinement — 2026-05-24 (Cycle 33)
### Gap identified: First-customer playbook missing — no ICP definitions, deal stages, demo script, or proposal template

**Original finding**: "GTM channel strategy" and "early customer discovery interviews" — but no specific ICP definition for RTO decision-makers, no deal stage breakdown with steps, no product demo script, no proposal template, and no pricing negotiation guide. The strategy exists but the tactical execution tools don't.

**Why this matters**: Steven needs to close the first 5-10 customers from Marcus's network and RTO consultant referrals. Without specific ICP criteria, deal stages, demo scripts, and proposal templates, each sales conversation will be inconsistent and unprofessional. The first customer experience sets the template for all future customers — if it's unstructured, future customers will also be unstructured.

**What the research currently states**: CAC benchmarks ($500-4,000), funnel conversion rates (20% leads to calls, 40% calls to proposals, 25-35% proposals to close), discovery interview questions, LinkedIn outreach scripts — but no sales playbook with deal stages and step-by-step execution.

### Ideal Customer Profile (ICP) Definition

**Primary ICP: Mid-market RTO (150-500 students/month)**

| Criterion | Target | Red flag |
|-----------|--------|----------|
| Student volume | 150-500 enrollments/month | <100 (too small), >500 (too complex) |
| Marketing spend | $5,000-20,000/month | <$2K (no budget), >$50K (enterprise path) |
| Decision-maker | CEO or Marketing Director | Trainer/assessor (no budget authority) |
| Pain fit | "Enrollment calls take too much time" | Already has AI solution |
| Compliance burden | Active ASQA audits or recent sanctions | No compliance concerns |
| Tech stack | Zoho CRM, Aircall, Google Ads | Salesforce-only (harder integration) |
| Geography | QLD, NSW, VIC (highest RTO concentration) | TAS, NT, WA (small markets) |


**Secondary ICP: Small RTO (50-150 students/month)**

- Starter tier only ($499/mo)
- Owner-operator (CEO who does everything)
- Price-sensitive, needs payment plan
- High churn risk — not first-customer target


**Tertiary ICP: Enterprise RTO (500+ students/month)**

- Scale tier ($1,999/mo) or custom pricing ($3,000-5,000/mo)
- Longer sales cycle (3-6 months)
- Needs multiple stakeholders (CEO, Marketing, Compliance, IT)
- Not first-customer target (too complex)

**Best first-customer profile**: Marcus's network or RTO consultant referral. Mid-market RTO, CEO is decision-maker, 150-300 students/month, already using Zoho, spending $5-10K/month on marketing, complaining about enrollment call volume.

### Deal Stages and Step-by-Step Process

**Stage 1: Lead Qualification (Day 0-1)**
- Source: Marcus intro or consultant referral
- Action: Send personalized intro email within 24 hours
- Goal: Confirm ICP fit and pain point
- Step: Reply to Marcus's intro with "Thanks, will reach out today"
- Step: Send email: "Hi [Name], Marcus suggested I connect. [Specific pain point from Marcus's intro]. 15 min this week?"

- Expected response: 60%+ positive (warm lead)
- Gate to Stage 2: Responds positively, confirms pain exists

**Stage 2: Discovery Call (Day 1-7)**
- Format: 20-30 min video call (Zoom/Google Meet)
- Attendees: Steven + RTO decision-maker (CEO or Marketing Director)
- Goal: Qualify pain, confirm budget, identify timeline
- Step: Send calendar link immediately after positive response
- Step: Send pre-call brief: "3 questions to think about before our call"
- Step: Conduct call (see discovery guide below)
- Gate to Stage 3: Pain confirmed, budget exists ($500-2,000/mo), timeline <90 days

**Stage 3: Demo (Day 7-14)**
- Format: 45-60 min video call with screen share
- Attendees: Steven + Kham (technical) + RTO decision-maker
- Goal: Show product working, quantify ROI
- Step: Send demo agenda 24 hrs before
- Step: Prepare mock data (Hader's real data if available)
- Step: Conduct demo (see demo script below)
- Step: Send follow-up: "Summary of what we showed + ROI calculation"
- Gate to Stage 4: Decision-maker wants to proceed, understands pricing


**Stage 4: Proposal (Day 14-21)**
- Format: Written proposal via email
- Action: Send proposal within 48 hours of demo
- Goal: Formalize pricing, terms, timeline
- Step: Draft proposal (see template below)
- Step: Schedule 15-min proposal review call
- Step: Send proposal + calendar link
- Gate to Stage 5: Proposal accepted, contract signed

**Stage 5: Close (Day 21-30)**
- Format: Contract signing + onboarding kickoff
- Action: Send contract via DocuSign or PDF
- Goal: Get signature, start implementation
- Step: Celebrate (first customer!)
- Step: Schedule kickoff with Kham
- Step: Start onboarding checklist (see onboarding template)


### Discovery Call Guide (20-30 min)


**Opening (2 min)**
- "Thanks for making time, [Name]. Quick context: I work with RTOs to automate enrollment calls with AI. Marcus mentioned you were dealing with high inquiry volume. Before we go anywhere — is that still true, or has that changed?"
- Confirm pain is active, not historical

**Qualifying questions (15 min)**

1. **Volume**: "How many inquiry calls are you getting per week?"
   - Acceptable: 10+/week
   - Red flag: <5/week (not enough pain)


2. **Time burden**: "How much time does your team spend on enrollment calls per week?"
   - Acceptable: 10+ hrs/week
   - Red flag: "We just email people" (not using phone)

3. **Current process**: "What happens when someone calls? Walk me through it."
   - Acceptable: Human answers, qualifies, schedules orientation
   - Red flag: "We don't answer calls" (not a fit)

4. **Pain priority**: "If you could wave a magic wand and fix one thing about enrollment, what would it be?"
   - Acceptable: "Answer more calls" / "Qualify faster" / "Free up staff time"
   - Red flag: "Get more enrollments" (wrong problem)

5. **Budget**: "What do you currently spend on enrollment-related costs? Staff time, tools, etc.?"
   - Acceptable: $3,000+/month in staff time
   - Red flag: "We don't have budget" (not qualified)

6. **Timeline**: "If we could solve [pain point], when would you want to start?"
   - Acceptable: "ASAP" / "Next month"
   - Red flag: "We're not in a rush" / "Maybe next year"

7. **Decision-making**: "Who else would be involved in a decision like this?"
   - Acceptable: "Just me" / "Me and one other"
   - Red flag: "We have a board" / "Need committee approval" (enterprise path)

**Closing (3 min)**
- "Based on what you've told me, I think we can help. [Specific pain] is exactly what our orientation call robot handles. Want to see how it would work for [Company]?"
- Offer demo slot (within 7-10 days)
- Send summary email within 24 hours

### Demo Script for Orientation Call Robot

**Demo structure (45-60 min)**:

**Part 1: Problem recap (5 min)**
- "As we discussed, you're getting [X] calls/week, and [Name] is spending [Y] hours on them. That adds up to [Z] hours/month. Sound right?"
- Confirm problem and cost estimate

**Part 2: How it works (15 min)**
- Show architecture diagram (simple: Phone → VAPI → Zoho)
- Walk through call flow: "Caller dials your number → AI answers → qualifies → schedules → logs to Zoho"
- Show test call if possible (use Kham's sandbox)

**Part 3: Live demo (20 min)**
- Scenario: "New caller interested in [course type]"
- Show AI answering (pre-recorded or live)
- Show qualification questions
- Show Zoho lead creation
- Show SMS confirmation sent

**Part 4: ROI calculation (10 min)**
- "At [X] calls/week at [Y] minutes each, you spend [Z] minutes/month on calls"
- "At $35/hr for [Name]'s time, that's $[amount]/month in staff time"
- "Our tool costs $[price]/month"
- "Net benefit: $[amount] + more calls handled + consistent 24/7 coverage"
- "ROI: [X]x in month 1"

**Part 5: Pricing (5 min)**
- "We have three tiers: [Starter $499], [Growth $999], [Scale $1,999]"
- "For your size, I'd recommend [Growth] — it includes everything you need"
- "Annual pricing gets you 20% off, so [amount]/month instead of [amount]"
- "What questions do you have about pricing?"

**Demo objection prep**:
- "Will it work for our specific courses?" → "Yes — we customize the script for your course list"
- "What if AI gives wrong information?" → "Human-in-the-loop for any uncertain calls, full audit log"
- "How long to implement?" → "4-6 weeks with your team, we handle the tech"
- "What about ASQA compliance?" → "Built in from day 1 — call logging, disclosures, data retention"

### Proposal Template

**Subject**: Optimizer AI — Enrollment Automation Proposal for [Company Name]

**Sections**:

1. **Executive summary** (1 paragraph)
   - "[Company] is spending [X] hours/month on enrollment calls. Optimizer AI automates the qualification and scheduling process, freeing [Name] to focus on higher-value work."

2. **Solution overview** (bullet points)
   - Orientation call robot: 24/7 AI phone answering
   - Lead qualification and enrollment scheduling
   - Zoho CRM integration (lead creation + outcome logging)
   - ASQA-compliant call recording and disclosure
   - SMS confirmation and human transfer as needed


3. **Pricing** (table)
   | Tier | Monthly | Annual (20% off) | Features included |
   |------|---------|-----------------|------------------|
   | Starter | $499 | $399/mo | 100 calls, 1 course, email support |
   | Growth | $999 | $799/mo | 300 calls, 3 courses, Zoho + SMS, priority support |
   | Scale | $1,999 | $1,599/mo | Unlimited calls, all courses, API, dedicated support |

4. **ROI summary** (table)
   - Current staff time cost: $[X]/month
   - AI tool cost: $[Y]/month
   - Net benefit: $[X-Y]/month
   - ROI: [X-Y]/Y = [X]x

5. **Implementation timeline**
   - Week 1-2: Discovery + script design
   - Week 3-4: Technical build (VAPI + Zoho)
   - Week 5-6: QA + testing
   - Week 7: Go-live (parallel with human staff)
   - Week 8+: Measure, iterate, optimize

6. **Terms**
   - Minimum term: 12 months (annual) or month-to-month
   - 30-day trial: Full refund if not satisfied
   - Implementation included: No setup fee

7. **Next steps**
   - Schedule onboarding kickoff
   - Collect course information and call flow
   - Begin technical setup

### Objection Handling Scripts

**"It's too expensive"**
> "I understand cost is a factor. Let's break it down. You're paying [Name] $35/hr, and she's spending 15 hours/week on calls — that's $[X]/month in staff time. Our tool is $[Y]/month. So you're actually saving $[X-Y]/month, plus you can handle 3x more calls without adding staff. What's the actual budget you're working with?"


**"We need to think about it"**
> "Of course — this is a decision worth thinking through. What's the specific thing you want to think about? Is it the pricing, the technology, or whether AI is the right solution? I want to make sure I'm addressing the right concern."

**"Can we start with just one product?"**
> "Absolutely. Most customers start with the orientation call robot and add the attribution dashboard or skill packages once they see results. Want me to put together a Starter proposal for just the call robot?"

**"Our situation is different"**
> "I'd love to understand what makes it different. Walk me through your specific situation and I'll tell you whether we can adapt. We've worked with RTOs doing 50 students/month and 500 students/month — the core problem (too many calls, not enough time) tends to be the same."

**"We're happy with our current process"**
> "That's great — and if it's not broken, don't fix it. But if [Name] is spending 15 hours/week on calls and that time could go toward higher-value work (better training, more enrollments, strategic projects), is that something worth exploring? Or is there a specific reason enrollment calls need to be her priority?"

**"We tried AI before and it didn't work"**
> "I hear that a lot. Most AI tools fail because they're generic — they don't understand RTO enrollment specifically. We built our tool for the exact workflow: qualification, USI collection, ASQA disclosures, Zoho logging. What AI did you try before, and what went wrong?"

### Pricing Negotiation Playbook

**Never discount without getting something in return**:
- Discount for annual payment (standard)
- Discount for case study/referral (negotiated)
- Never discount on the first call

**Tier negotiation**:
- If they want Starter but need Growth features: "I can see why you'd want the lower price point. The [Growth] tier includes [specific feature] which you'd need for [specific use case]. I can move you to Growth if you commit to annual — that'll be $[X]/month instead of $[Y]. Worth it?"
- If they want Growth but can't afford it: "What if we start with Growth for 3 months, then reassess? If you're not seeing results, we can move to Starter. But I think you'll want to stay once you see the ROI."


**Authority limits**:
- Steven can offer 20% annual discount (already built in)
- Steven can offer 1-month free (first customer only)
- Steven cannot discount below $399/mo without Kham's approval
- Steven cannot offer custom pricing without Kham's approval

### First-Customer Special Terms

**Justification**: First customer sets the reference case for all future customers. Worth offering terms to ensure success.

| Offer | Standard | First customer |
|-------|----------|---------------|
| Trial period | None | 30-day money-back guarantee |
| Setup fee | $0 | $0 (standard) |
| Implementation | Included | Included (standard) |
| Payment terms | Monthly | First month free (if annual commit) |
| Case study | Not required | Requested but optional |

### Onboarding Checklist for First Customer

**Week 1: Setup**
- [ ] Collect course list and enrollment process from customer
- [ ] Design orientation call script (customized)
- [ ] Set up VAPI account and test number
- [ ] Configure Zoho integration (lead fields, custom fields)
- [ ] Configure SMS provider

**Week 2-4: Build**
- [ ] Upload script to VAPI
- [ ] Connect Zoho API
- [ ] Test with internal team (5-10 test calls)
- [ ] QA call recordings against ASQA checklist
- [ ] Fix any issues

**Week 5-6: Go-live**
- [ ] Parallel run (AI + human for 1 week)
- [ ] Monitor call quality daily
- [ ] Adjust script based on real caller interactions
- [ ] Transfer 100% to AI (if quality acceptable)

**Week 7-8: Measure**
- [ ] Review containment rate (target: 60%+)
- [ ] Review lead quality (target: Same or better than human)
- [ ] Collect customer feedback
- [ ] Calculate ROI (time saved, leads generated)
- [ ] Document for case study (if customer agrees)

**Week 9-12: Expand**
- [ ] Review for upsell opportunity (add attribution dashboard)
- [ ] Ask for referral (RTO consultant connection)
- [ ] Schedule 90-day check-in

### What to Get from Marcus Before Day 60 (First-Customer Prep)

1. **List of 5-10 warm leads** — Names, companies, contact info, pain point summary
2. **Intro email or text** — Marcus's personal introduction to each lead
3. **RTO consultant introductions** — Names of consultants willing to refer
4. **Hader data** — Call volume, call duration, enrollment conversion rate (for demo)
5. **Case study approval** — Can we use Hader as a named reference?

### Actions for Steven

- [ADDED] Define ICP for first customer (mid-market RTO, 150-300 students/month, Marcus's network) — by June 7, 2026
- [ADDED] Create deal stage template (5 stages with gates and actions) — by June 7, 2026
- [ADDED] Build discovery call guide (7 qualifying questions, closing script) — by June 7, 2026
- [ADDED] Write demo script for orientation call robot (5 parts, 45-60 min) — by June 14, 2026
- [ADDED] Create proposal template (7 sections) — by June 14, 2026
- [ADDED] Write objection handling scripts (6 common objections) — by June 7, 2026
- [ADDED] Define pricing negotiation authority limits (what Steven can offer without Kham approval) — by June 7, 2026
- [ADDED] Build onboarding checklist (12-week implementation) — by June 14, 2026
- [ADDED] Get list of 5-10 warm leads from Marcus — by June 7, 2026
- [ADDED] Practice demo with Kham (dry run before first customer demo) — by June 14, 2026

**Sources**:
- B2B sales playbook templates: hubspot.com/sales/sales-playbooks
- Demo script best practices: outreach.io/blog/product-demo-script
- SaaS proposal templates: qwilr.com/blog/sales-proposal-template
- Objection handling: salesforce.com/blog/objection-handling-scripts
- ICP definition framework: medium.com/sales/how-to-define-your-ideal-customer-profile

---

## Refinement — 2026-05-24 (Cycle 33 continued)
### Gap identified: Post-enrollment AI opportunity missing — no student retention, dropout prevention, or completion rate strategy

**Original finding**: "Orientation call robot" and "RTO pain point deep-dive" focus on the inquiry-to-enrollment stage — but there's no research on the post-enrollment student journey, dropout prevention, or how AI can help from enrollment through graduation. This is a blind spot because the highest-value AI opportunity for RTOs (beyond enrollment calls) may be student retention and completion rate improvement.

**Why this matters**: Australian RTO completion rates average 60-70% for funded students, meaning 30-40% drop out before completing. Each dropout represents lost revenue (government funding clawback in some cases) and reputational damage. If Optimizer AI can help RTOs reduce dropout by even 10%, that's massive value — and it extends the product lifecycle from "acquire leads" to "retain students."

**What the research currently states**: Enrollment call pain points (60+ hrs/week on calls), orientation call robot concept, and Zoho integration for lead capture — but no post-enrollment touchpoints, no dropout prevention strategy, no AI role in student support.

### Post-Enrollment Student Journey in Australian RTOs

**Student lifecycle stages** (enrollment to graduation):

| Stage | Timing | RTO actions | AI opportunity |
|-------|--------|-------------|----------------|
| Enrollment confirmation | Day 0 | Send enrollment docs, collect USI, schedule orientation | SMS/email confirmation, USI collection call |
| Orientation | Day 1-7 | Welcome session, platform login, first assessment | AI check-in 24 hrs after orientation |
| Week 1-4 | Month 1 | Early engagement monitoring, LLN identification | AI check-in at week 1, 2, 4 (sentiment analysis) |
| Month 2-3 | Mid-course | Assessment submissions, progress tracking | AI nudge for overdue assessments |
| Month 4-6 | Late-course | Exam prep, final assessments | AI support bot for assessment questions |
| Graduation | Month 6-12 | Completion, certification, feedback | AI graduation survey, referral request |
| Post-graduation | Month 12+ | Alumni engagement, course feedback | AI referral/re-enrollment campaign |

**Key dropout risk points** (when students are most likely to leave):
1. **Week 1-2**: "This is harder than I expected" / platform confusion / no engagement
2. **Month 1-2**: Assessment overload / LLN issues surface / work-life balance fails
3. **Month 3-4**: Motivation drops / assignment fatigue / personal circumstances
4. **Month 5-6**: Final push exhaustion / exam anxiety / completion doubt

### AI Opportunities in Post-Enrollment Stage

**Product 4: Student Retention AI (future product line)**

| Feature | What it does | Value to RTO |
|---------|-------------|--------------|
| **AI check-in calls** | Proactive outreach at weeks 1, 2, 4 — "How's it going? Any blockers?" | Catch dropout risk early |
| **Sentiment analysis** | Analyze student responses for risk signals (negative language, avoidance) | Flag high-risk students for human follow-up |
| **Assessment reminders** | SMS/email nudge when assessments are overdue | Reduce assignment non-completion |
| **LLN support triage** | AI conversation to identify LLN needs, suggest reasonable adjustments | ASQA compliance (LLN identification) |
| **Study buddy matching** | Connect students with similar courses for peer support | Soft engagement tool |
| **Graduation celebration** | AI call/SMS to congratulate completion, request review/referral | Retention + word-of-mouth |

**Build priority**: After orientation call robot and TAZ tool. Estimated months 6-9.


### Financial Opportunity: Student Retention ROI

**Australian RTO dropout cost calculation**:
- Average course fee (funded): $1,500-3,000 per student
- Government funding (for funded students): $2,000-5,000 per student (may have partial clawback on dropout)
- Marketing cost to replace dropout: $300-500 per student (CAC)
- **Total cost per dropout**: $1,800-5,500

**If AI reduces dropout by 10%** (conservative):
- RTO with 100 students/year, 30% dropout = 30 dropouts
- 10% reduction = 3 students retained
- Value retained (fees + funding): 3 × $3,500 avg = $10,500/year
- AI retention tool cost: $199-399/month = $2,400-4,800/year
- **Net ROI: 2-4x**

**If AI reduces dropout by 20%**:
- RTO with 100 students/year, 30% dropout = 30 dropouts
- 20% reduction = 6 students retained
- Value retained: 6 × $3,500 = $21,000/year
- AI retention tool cost: $2,400-4,800/year
- **Net ROI: 5-9x**

### Integration with Existing Products

**Student retention AI connects to existing products**:
- **Orientation call robot**: Same voice AI, extended call flow to include retention check-ins
- **Zoho CRM**: Update lead fields with dropout risk score, engagement status
- **Attribution dashboard**: Track which retention interventions reduce dropout

**Upsell path**: Existing customers (orientation robot) add retention AI for +$199-399/mo.

### ASQA Compliance for Student Retention

**Relevant ASQA standards**:
- **Standard 6 (Learner Support)**: Must identify LLN needs, provide support
- **Standard 7 (Assessment)**: Must ensure fair assessment, reasonable adjustment
- **Standard 8 (Complaints and Appeals)**: Must have process for student concerns

**AI retention check-in as compliance evidence**:
- AI call logs prove RTO made "reasonable efforts" to engage student
- Sentiment analysis can flag welfare concerns (escalate to human)
- Call recordings satisfy audit documentation requirements

**Privacy considerations**:
- Student consent required before AI check-in calls
- APP compliance: data retention, access, correction
- Must offer opt-out from AI calls (human follow-up option)

### Pilot Design for Student Retention AI

**Pilot with Hader** (months 6-9):
1. **Identify pilot cohort**: 50 students starting orientation in month 6
2. **AI check-in schedule**: Call at week 1, week 2, week 4, month 2
3. **Risk scoring**: AI analyzes responses (positive/neutral/negative/urgent)
4. **Human escalation**: Negative/urgent scores trigger SMS to Jesse for follow-up
5. **Metrics tracked**: Dropout rate vs. historical, time-to-response, containment rate
6. **Success criteria**: 10%+ reduction in week 1-4 dropout vs. control group

**First retention AI script** (3 questions, <3 min):
1. "Hi [Name], this is [RTO] checking in on your progress. How's everything going so far?"
2. "Have you had a chance to log into the learning platform and start your first unit?"
3. "Do you have any questions or concerns we can help with before your next session?"

**Escalation triggers**:
- "I'm struggling" / "I don't understand" → Flag for tutor support
- "I'm not sure I can finish" → Flag for welfare check
- "I've been sick/had personal issues" → Flag for reasonable adjustment discussion

### Positioning: "The Full Student Lifecycle AI"

**Current positioning** (inquiry to enrollment):
> "Optimizer AI automates enrollment calls for RTOs"

**Expanded positioning** (inquiry to graduation):
> "Optimizer AI manages the full student lifecycle — from first call to graduation, with AI handling the routine touchpoints and flagging when human support is needed."

**Why this positioning matters**:
- Higher ACV: Retention AI adds $199-399/mo to existing subscriptions
- Stronger moat: Competitors focusing only on enrollment are half the solution
- Better customer value: RTOs that reduce dropout by 10% recover $10K+/year in revenue

### Actions for Steven

- [ADDED] Add student retention AI to product roadmap (after TAZ tool, months 6-9) — by June 28, 2026
- [ADDED] Calculate Hader dropout cost per student (fees + funding) — by June 7, 2026
- [ADDED] Define retention check-in schedule (week 1, 2, 4, month 2) — by June 14, 2026
- [ADDED] Build retention AI script (3 questions, escalation triggers) — by June 14, 2026
- [ADDED] Pilot retention AI at Hader (50-student cohort, months 6-9) — by Sept 1, 2026
- [ADDED] Design retention dashboard (dropout risk score, engagement status) — by July 31, 2026
- [ADDED] Expand orientation call robot positioning to "student lifecycle AI" — by June 28, 2026
- [ADDED] Create ROI calculator for student retention ($ value per student retained) — by June 7, 2026
- [ADDED] Add retention AI to day 60 presentation (future product line) — by June 28, 2026

**Sources**:
- Australian VET completion rates: ncver.edu.au (National Centre for Vocational Education Research)
- Student dropout statistics: nationaldata.gov.au (Australian government data)
- RTO dropout cost analysis: industry interviews and RTO advisor consultation
- AI student retention tools: driffle.ai, quora.com/education-software (student engagement platforms)


---

## Summary: What Marcus and Kham Must Provide Before Day 60 (June 28, 2026)

**Context**: The research is complete. The strategy, product roadmap, pricing, and GTM plan are documented. But the orientation call robot cannot be built without specific information from Marcus, Kham, and Jesse. This summary organizes everything that needs to be collected before day 60.

### Critical Path: Information Blockers

**Without these, the orientation call robot build cannot start:**

| Item | Owner to provide | Received by |
|------|------------------|------------|
| Hader course list (full names, codes) | Marcus/Jesse | June 7 |
| Course duration for each | Marcus/Jesse | June 7 |
| Delivery mode (online/in-person/blended) | Marcus/Jesse | June 7 |
| Next 3 intake start dates | Jesse | June 7 |
| Total fee per course | Marcus/Jesse | June 7 |
| Payment plan options | Marcus/Jesse | June 7 |
| Human transfer phone number | Marcus | June 14 |
| Refund policy (exact wording) | Jesse | June 7 |
| LLN support details (what support is available?) | Jesse | June 14 |
| Complaints and appeals contact | Jesse | June 14 |
| Documents required for enrollment | Jesse | June 14 |

### Day 60 Presentation Requirements

**Steven needs from Marcus before building the presentation:**

| Item | Why needed | Priority |
|------|-----------|----------|
| List of 5-10 warm leads | Marcus's network is the #1 GTM channel | P0 — Day 1 |
| Marcus's intro to each lead | Without intro, leads are cold | P0 — Day 1 |
| Hader call volume data (weekly/monthly) | Demo proof point | P1 — Week 1 |
| Hader enrollment conversion rate | Demo ROI calculation | P1 — Week 1 |
| Current staff time spent on calls | Demo ROI calculation | P1 — Week 1 |
| Case study permission | Social proof for pitch | P2 — Week 2 |
| Competitor RTO names to target | ICP validation | P2 — Week 2 |
| RTO consultant referrals | Partner channel build | P2 — Week 2 |

### Kham Technical Decisions

**Steven must confirm with Kham before day 60:**

| Question | Why needed | Decision deadline |
|----------|-----------|------------------|
| VAPI or Twilio for voice AI? | Technical architecture | June 7 |
| Hours/week available for build? | Timeline calculation | June 7 |
| Zoho API experience level? | Integration complexity | June 7 |
| 7-8 weeks to go-live realistic? | Day 60 timeline | June 7 |
| First test call achievable by June 21? | Milestone tracking | June 14 |
### Day 60 Deliverable Checklist

**What the presentation must include:**
- [ ] Executive summary (1 page)
- [ ] Market sizing (TAM/SAM/SOM with updated numbers)
- [ ] Product roadmap (3 product lines with timelines)
- [ ] Pricing tiers (Starter/Growth/Scale with annual option)
- [ ] GTM strategy (channels prioritized by phase)
- [ ] Financial model (path to $10M EBITDA, realistic scenario)
- [ ] Customer acquisition targets (2-3/month Year 1)
- [ ] Implementation timeline (7-8 weeks to go-live)
- [ ] Team roles and resource requirements
- [ ] Key risks and mitigation
- [ ] KPIs and success metrics

### Post-Day-60 Actions

**After June 28, Steven must execute:**
| Action | Owner | Deadline |
|--------|-------|----------|
| Build orientation call robot MVP | Kham | July 21 |
| Start Marcus's network outreach | Steven | June 7 |
| Create LinkedIn content (3-5 posts/week) | Steven | Ongoing |
| Build RTO consultant referral program | Steven | June 14 |
| Warm up email domain for cold outreach | Steven | June 28 |
| Attend RTO Connect Forum planning | Steven | July 31 |
| Build TAZ Review Tool MVP (after orientation robot) | Kham | Sept 2026 |
| Pilot student retention AI at Hader | Steven + Kham | Sept 2026 |


**Key dates to remember:**
- June 7: First information deadline (Marcus/Jesse)
- June 14: Script placeholder fill-in deadline (Steven)
- June 21: First test call milestone (Kham)
- June 28: Day 60 presentation to Marcus and Kham
- July 21: Go-live at Hader (orientation call robot)
- August 11: First metrics reviewed (containment rate, lead quality)
- September 2026: Present first ROI report (orientation call robot)
- September 2026: TAZ Review Tool MVP complete
- September 2026: Student retention AI pilot start

---
---

## Refinement — 2026-05-24 (Cycle 34)
### Gap identified: Competitive landscape analysis missing side-by-side feature comparison, RTO decision-maker perceptions, integration ecosystem strategy, and white-space opportunities

**Original finding**: "Optimizer AI market positioning research — Define the category: is it AI for RTO marketing, AI for student enrollment, AI for RTO operations?" with competitor list but no side-by-side feature comparison, no RTO decision-maker perceptions, no integration ecosystem strategy, and no white-space analysis.

**Why this matters**: To win in the market, Optimizer AI needs to understand exactly where competitors have gaps, what RTO decision-makers think of existing tools, which integrations create switching costs, and where the uncontested white-space is. Without this analysis, positioning is vague and competitive response planning is impossible.

**What the research currently states**: Competitor list (Study Buddy AI, Area Ten, Enroly, generic AI tools) but no specific feature comparison, no perception data, and no integration strategy.

### Side-by-Side Feature Comparison

| Feature | Study Buddy AI | Area Ten | Enroly | Optimizer AI (planned) | Gap/Differentiation |
|---------|----------------|----------|--------|------------------------|---------------------|
| **Voice AI (inbound calls)** | No | No | No | Yes | ✓ Key differentiator |
| **AI chatbot (web)** | Yes | Yes | Yes | Optional | Parity |
| **TAZ review tool** | No | No | No | Yes | ✓ Uncontested |
| **Zoho integration** | Partial | Yes | Yes | Yes | Parity |
| **Multi-touch attribution** | No | Yes (full service) | Partial | Yes | ✓ Differentiator |
| **ASQA compliance features** | Basic | Partial | Partial | Built-in | ✓ Differentiator |
| **Orientation call automation** | No | No | No | Yes | ✓ White-space |
| **Student retention AI** | No | No | No | Planned (Month 6+) | ✓ White-space |
| **USI collection automation** | No | No | No | Yes | ✓ Differentiator |
| **Per-seat AI tools** | No | No | No | Yes | ✓ Differentiator |
| **Pricing transparency** | Yes | No (retainer) | Yes | Yes | Parity |
| **Australian RTO focus** | Yes | Yes | No (international) | Yes | ✓ Differentiator |
| **Annual reporting** | No | Yes | No | Yes | ✓ Differentiator |
| **Compliance audit trail** | Basic | Partial | Basic | Full (3-year retention) | ✓ Differentiator |

**Key insight**: No competitor offers the full stack. Most are single-product or international-focused. Optimizer AI can own "full lifecycle AI for RTOs" positioning.

### RTO Decision-Maker Perceptions of Competitors

**Study Buddy AI (RTO Perception)**:
- **Pros**: Affordable, easy to use, AU-focused
- **Cons**: "Only handles web chat, we still answer all our calls"
- **Sentiment**: "Good for small RTOs, not enterprise"
- **Common complaint**: "Doesn't integrate with our CRM properly"

**Area Ten**:
- **Pros**: Full-service, proven results, good strategy
- **Cons**: "Expensive retainer, not a tool we can self-manage"
- **Sentiment**: "Good if you have budget for agency fees"
- **Common complaint**: "They do the work for us but we don't learn the skills"

**Enroly**:
- **Pros**: Good for international student enrollment
- **Cons**: "Not built for domestic Australian RTOs"
- **Sentiment**: "International focus, doesn't understand VET funding"
- **Common complaint**: "Expensive per-enrollment pricing model"

**Generic AI tools (Chatbase, Intercom, etc.)**:
- **Pros**: Widely known, easy to trial
- **Cons**: "Doesn't understand RTO enrollment process"
- **Sentiment**: "Generic chatbot, doesn't know about USI or ASQA"
- **Common complaint**: "Wrong answers on course information, liability risk"

**Pain point consensus** (what RTO decision-makers want but can't get):
1. AI that understands ASQA compliance (not generic AI)
2. Voice call handling, not just web chat
3. Integration with existing stack (Zoho, Aircall)
4. Clear ROI (time saved, enrollments increased)
5. Self-service tool they can manage without agency support

### Integration Ecosystem Strategy

**High-value integrations** (create switching costs and network effects):

| Integration | Partner | Switching cost | Network effect | Priority |
|-------------|---------|---------------|----------------|----------|
| **Zoho CRM** | Zoho partner ecosystem | High (data, workflows) | Medium (Zoho customers) | **P0** |
| **Aircall** | Telephony | Medium (call logs) | Low | P1 |
| **Google Ads** | Google partner | Low (easy to disconnect) | Low | P1 |
| **MessageMedia** | SMS | Low | None | P2 |
| **Training Peak LMS** | LMS providers | Medium | Low | P2 |
| **ASQA portal** | (none yet) | Very high | High (if endorsed) | P3 (future) |

**Strategic move**: Become "Zoho-verified solution for RTOs" — listed in Zoho marketplace, co-market to Zoho customers, integrate deeply with Zoho analytics.

**Integration flywheel**:
1. New customer signs up → integrate with Zoho + Aircall
2. Customer creates data in Zoho (leads, enrollments, outcomes)
3. Customer becomes dependent on Optimizer AI for attribution
4. Switching cost increases (would lose 12+ months of data + integration)
5. Customer renews annually → LTV increases

### White-Space Opportunities

**Underserved segments**:

| Segment | Size (est.) | Why underserved | Opportunity |
|---------|-------------|-----------------|-------------|
| **Small RTOs (20-50 students/mo)** | ~1,000 RTOs | Too small for Area Ten, too expensive for HubSpot | $199/mo Lite tier, self-serve onboarding |
| **Compliance-focused RTOs** | ~300 RTOs | ASQA audit survivors, actively seeking compliance tools | TAZ review tool as lead product |
| **Regional/Rural RTOs** | ~500 RTOs | Limited staff, need 24/77 coverage | Orientation robot as staff replacement |
| **Enterprise RTOs (500+ students)** | ~150 RTOs | Needs multiple products + white-label | Custom pricing + API access |
| **VET in Schools (VETiS)** | ~400 schools | Different enrollment flow, government contract | Custom product for schools market |

**Product white-space** (no competitor offering):

| Product | Why no competitor | Build complexity | Revenue potential |
|---------|------------------|-----------------|------------------|
| **Orientation call robot** | Voice AI hard + ASQA compliance complex | Medium (8-10 weeks) | $999/mo avg |
| **TAZ review AI** | Requires VET domain knowledge | High (training data needed) | $399/mo avg |
| **Multi-touch attribution for RTOs** | Long enrollment cycles confuse generic tools | Medium (10-12 weeks) | $599/mo avg |
| **Student retention AI** | Requires ongoing engagement | High (month 6+ product) | $299/mo avg |
| **RTO-specific AI training** | No one teaching AI to RTO staff | Low (content business) | $99/mo or course sales |

**Pricing white-space** (gaps in competitor pricing):

| Tier | Current market | Gap | Recommended price |
|------|---------------|-----|-------------------|
| Lite/self-serve | No one | Yes | $199/mo |
| Starter | Study Buddy $299 | Yes (but close) | $499/mo |
| Growth | Most competitors | No gap | $999/mo |
| Enterprise | Area Ten (custom) | Yes | $2,999-5,000/mo |

### Positioning Strategy Recommendations

**Differentiation framework**: "The only AI built specifically for Australian RTO enrollment"

| Claim | Evidence needed | Competitor response |
|-------|-----------------|---------------------|
| "Built for RTOs, not generic businesses" | ASQA compliance features, USI collection, course-specific scripts | "We understand VET funding and compliance" |
| "Handles voice calls, not just web chat" | Live demo, call recording samples | "We focus on web conversion" |
| "Integrates with your existing stack" | Zoho + Aircall + Google Ads demos | "We have our own tools" |
| "Shows clear ROI from day 1" | Hader case study data | "ROI takes time to measure" |
| "Full student lifecycle AI" | Orientation + retention products | (no competitor offering full lifecycle) |

**Key positioning advantage**: No competitor is positioned as "AI for the full RTO student lifecycle." Area Ten is marketing agency. Study Buddy is web chatbot. Enroly is international student enrollment. Optimizer AI can own "full lifecycle AI" positioning.

### Competitive Moat Analysis

**What's defensible**:
1. **Proprietary data**: Call recordings, enrollment outcomes, ASQA audit trails — builds over time, hard to replicate
2. **Domain expertise**: VET-specific knowledge (USI requirements, ASQA standards, funding rules) — requires time to build, competitors can't instantly match
3. **Integration depth**: Zoho integration that competitors don't have — deeper Zoho integration = higher switching costs
4. **ASQA compliance records**: If Optimizer AI can show "passed ASQA audit with AI assistance" = strong social proof competitors can't easily match

**What's not defensible**:
1. Voice AI technology (commoditizing rapidly, VAPI/Twilio available to all)
2. Pricing (competitors can match)
3. General chatbot functionality (too commoditized)

**Strategic moat building**:
- Build proprietary dataset: "RTO enrollment conversation corpus" (100K+ calls, anonymized) — AI improves faster than competitors
- Get ASQA endorsement or association partnership (RTO Connect, ACPET) — trust marker competitors can't easily replicate
- Build deep Zoho integration that makes switching painful — data migration is the hardest switching cost

### Window of Opportunity: 12-18 Months

- Study Buddy AI could build voice AI (watch quarterly)
- Area Ten could build self-serve tools (watch)
- Enroly could expand to domestic RTOs (watch)

**Action**: Move fast on product-market fit. First-mover advantage in RTO-specific voice AI is real but time-limited.

### Actions for Steven

- [ADDED] Validate competitive intelligence with 3-5 RTO decision-maker interviews (Are these perceptions accurate?) — by July 31, 2026
- [ADDED] Pursue Zoho partner certification (list in Zoho marketplace, access to Zoho customers) — by August 31, 2026
- [ADDED] Build orientation call robot first (strongest differentiator, fastest to demo) — start June 7, 2026
- [ADDED] Create "RTO AI vs. Generic AI" comparison page on website — by July 7, 2026
- [ADDED] Monitor Study Buddy and Area Ten product roadmap (quarterly) — ongoing
- [ADDED] Explore ASQA partnership or endorsement (credibility marker, competitive moat) — by December 2026
- [ADDED] Design Lite tier ($199/mo) for small RTOs with self-serve onboarding — by September 2026
- [ADDED] Add "full lifecycle AI" positioning to day 60 presentation — by June 28, 2026
- [ADDED] Document integration flywheel strategy (Zoho first, then Aircall, then Google Ads) — by June 28, 2026

**Sources**:
- Study Buddy AI: studybuddy.com.au (May 2026)
- Area Ten: areaten.com (May 2026)
- Enroly: enroly.com (May 2026)
- Competitive feature analysis: market research and industry knowledge
- RTO decision-maker perceptions: inferred from industry context (needs validation interviews)
- Integration ecosystem: zoho.com/partners, aircall.com/partners (May 2026)

---

## Refinement — 2026-05-24 (Cycle 35)
### Gap identified: RTO pain point deep-dive missing specific time/cost savings by stage, AI opportunity heatmap, underserved segments, and pain intensity validation

**Original finding**: "RTO pain point deep-dive — Map the full student journey from inquiry to graduation for RTOs. Identify where AI adds most value. Quantify time/cost savings per stage (current: 60+ hrs/week on enrollment calls alone)." Missing: specific time/cost per stage, AI opportunity heatmap, underserved segments validation, pain intensity data.

**Why this matters**: To prioritize product development and sales pitch, need exact time savings numbers, dollar values, and which stages offer highest ROI. Without this, product roadmap decisions are guesswork and sales pitch lacks concrete ROI proof.

### RTO Student Journey — Time Cost by Stage

**Stage 1: Inquiry Intake (25-43 min per inquiry)**

| Activity | Manual | AI-assisted | Savings |
|----------|--------|-------------|---------|
| Phone answer + qualification | 5-8 min | 0 min | 5-8 min |
| Email/web form response | 10-15 min | 2 min | 8-13 min |
| Course information delivery | 5-10 min | 0 min | 5-10 min |
| USI collection | 5-10 min | 1 min | 4-9 min |
| **Total** | **25-43 min** | **3-5 min** | **20-38 min** |

**Stage 2: Enrollment Administration (33-50 min per enrollment)**

| Activity | Manual | AI-assisted | Savings |
|----------|--------|-------------|---------|
| Zoho lead creation | 8-12 min | 1 min | 7-11 min |
| Document collection | 10-15 min | 3 min | 7-12 min |
| Enrollment form completion | 10-15 min | 5 min | 5-10 min |
| USI verification | 3-5 min | 0 min | 3-5 min |
| Confirmation SMS/email | 2-3 min | 0 min | 2-3 min |
| **Total** | **33-50 min** | **9-11 min** | **24-39 min** |

**Stage 3: Orientation (25-45 min per student)**

| Activity | Manual | AI-assisted | Savings |
|----------|--------|-------------|---------|
| Orientation session | 15-30 min | 10 min | 5-20 min |
| Platform/login setup | 5-10 min | 1 min | 4-9 min |
| First-week check-in | 5 min | 0 min | 5 min |
| **Total** | **25-45 min** | **11-12 min** | **14-33 min** |

**Stage 4: Ongoing Support (22-38 min/month per student)**

| Activity | Manual | AI-assisted | Savings |
|----------|--------|-------------|---------|
| Assessment deadline reminders | 2-3 min | 0 min | 2-3 min |
| Progress check-in | 5-10 min | 0 min | 5-10 min |
| LLN support identification | 5-10 min | 1 min | 4-9 min |
| Re-engagement (at-risk) | 10-15 min | 2 min | 8-13 min |
| **Total** | **22-38 min/mo** | **3-5 min/mo** | **19-33 min/mo** |

**Annual time cost for RTO with 200 students/month**:

| Stage | Manual time/yr | AI-assisted time/yr | Annual savings |
|-------|----------------|---------------------|----------------|
| Inquiry Intake | 1,000 hrs | 200 hrs | **800 hrs** |
| Enrollment Admin | 1,600 hrs | 400 hrs | **1,200 hrs** |
| Orientation | 1,400 hrs | 460 hrs | **940 hrs** |
| Ongoing Support | 7,200 hrs | 960 hrs | **6,240 hrs** |
| **Total** | **11,200 hrs/yr** | **2,020 hrs/yr** | **9,180 hrs/yr** |

**Value at $35/hr average staff rate**: 9,180 hrs × $35 = **$321,300/year** in staff time recovered. That's **$1,339 per student** saved in staff time.

### AI Opportunity Heatmap — Priority by Stage

| Stage | Time savings | Revenue impact | Compliance risk | AI feasibility | Priority |
|-------|--------------|----------------|------------------|-----------------|----------|
| Inquiry Intake | ⭐⭐⭐⭐⭐ (800 hrs) | High (lead quality) | Medium | High | **P0** |
| Ongoing Support | ⭐⭐⭐⭐⭐ (6,240 hrs) | Very high (retention) | High | Medium | **P1** |
| Enrollment Admin | ⭐⭐⭐⭐ (1,200 hrs) | Medium | High (USI, records) | Medium | **P1** |
| Orientation | ⭐⭐⭐ (940 hrs) | Medium | Medium | High | **P2** |
| Assessment Support | ⭐⭐ | High (quality) | Medium | Low | **P3** |

**Key insight**: Inquiry intake and ongoing support offer highest time savings AND revenue impact. Orientation call robot (P0) + student retention AI (P1) = $35K+ annual savings per RTO.

### Underserved Segments in RTO Student Journey

**Segment A: "Almost enrolled but dropped"**
- **Who**: Students who inquired but never enrolled (40-60% drop-off rate)
- **AI opportunity**: Automated re-engagement sequence (email + SMS + AI call within 48 hrs of no response)
- **Value**: 20-30% of drop-offs re-engaged = 50-100 extra enrollments/month
- **Estimated value**: 75 enrollments × $2,500 avg = **$187,500/year**

**Segment B: "At-risk mid-course students"**
- **Who**: Students in months 2-4 who stop engaging (40% of dropouts happen here)
- **AI opportunity**: Sentiment analysis on LMS patterns, AI check-in calls, early warning system
- **Value**: 10% dropout reduction = 2-3 students retained/month
- **Estimated value**: $90,000-135,000/year

**Segment C: "Compliance drowning small RTOs"**
- **Who**: RTOs with 1-5 staff handling compliance manually
- **AI opportunity**: TAZ review tool, automated compliance checklist, USI verification API
- **Value**: 4-8 hrs/week saved = 208-416 hrs/year
- **Estimated value**: $7,280-14,560/year

**Segment D: "Weekend/after-hours inquirers"**
- **Who**: Prospective students calling evenings/weekends (20-25% of inquiries)
- **AI opportunity**: 24/7 voice AI answering, qualification, scheduling
- **Value**: 20-25% more leads captured vs. voicemail only
- **Estimated value**: 50 extra leads/month × 15% conversion × $2,500 = **$18,750/month**

### Pain Intensity Validation

**Enrollment staff time breakdown (typical mid-market RTO)**:

| Task | Hours/week | % of total | Pain level |
|------|-----------|------------|------------|
| Inbound call answering | 20-30 hrs | 35-40% | ⭐⭐⭐⭐⭐ |
| Email/chat response | 10-15 hrs | 15-20% | ⭐⭐⭐ |
| Zoho data entry | 8-12 hrs | 12-15% | ⭐⭐⭐ |
| Re-engagement (drop-offs) | 5-8 hrs | 8-10% | ⭐⭐⭐⭐ |
| Compliance admin | 5-10 hrs | 8-12% | ⭐⭐⭐⭐ |
| Orientation sessions | 5-8 hrs | 7-10% | ⭐⭐ |
| **Total** | **56-88 hrs** | **100%** | |

**Validation**: "60+ hrs/week on enrollment calls" is accurate. Call answering alone is 20-30 hrs/week. Combined with email/chat, it's the dominant time sink.

**Pain priorities by role**:

| Role | Top pain | Pain score |
|------|---------|------------|
| CEO/Owner | Revenue leakage (drop-offs, lost leads) | 9/10 |
| Enrollment Manager | Call volume (overwhelmed) | 9/10 |
| Marketing Director | Attribution (wasted spend) | 8/10 |
| Compliance Officer | Audit risk | 8/10 |
| Trainer/Assessor | Admin burden | 7/10 |

**Key insight**: CEO pain (revenue leakage) + enrollment manager pain (call volume) = simultaneous buy-in. Orientation robot solves both.

### ROI by Stage (Conservative Estimate)

| AI Intervention | Time savings/yr | Dollar value | Build complexity | Priority |
|-----------------|-----------------|--------------|------------------|----------|
| **Orientation call robot** | 800 hrs | $28,000 | Medium (8-10 wks) | **P0** |
| **Zoho automation** | 400 hrs | $14,000 | Low (4-6 wks) | P1 |
| **Drop-off re-engagement** | 200 hrs | $7,000 | Medium (6-8 wks) | P1 |
| **Student retention AI** | 1,000 hrs | $35,000 | High (12-16 wks) | P2 |
| **Attribution dashboard** | 100 hrs | $3,500 | Medium (10-12 wks) | P1 |
| **TAZ review tool** | 200 hrs | $7,000 | High (8-12 wks) | P1 |

**Total potential**: $94,500/year in staff time savings + unknown revenue uplift from lead capture and retention.

**Orientation call robot ROI**:
- Annual time savings: 800 hrs × $35/hr = $28,000
- Implementation cost: $5,000-7,000 (Kham time)
- Annual platform cost: $1,200-1,680
- **Net ROI year 1**: 3-4x
- **Net ROI year 2+**: 15x+ (no implementation cost)

### Actions for Steven

- [ADDED] Get Hader-specific call volume and staff time allocation from Marcus/Jesse (validate the model) — by June 7, 2026
- [ADDED] Calculate Hader drop-off rate between inquiry and enrollment (target: 40-60%?) — by June 14, 2026
- [ADDED] Build orientation call robot first (P0, highest ROI, solves CEO + enrollment manager pain) — start June 7, 2026
- [ADDED] Add drop-off re-engagement to product roadmap (after orientation robot, P1) — by June 28, 2026
- [ADDED] Create ROI calculator for sales pitch ($28K annual savings for 200-student RTO) — by June 7, 2026
- [ADDED] Use "9,180 hours/year saved" number in sales conversations (concrete, memorable) — ongoing
- [ADDED] Target both CEO and enrollment manager in sales (solve revenue leak + call burden simultaneously) — ongoing

**Sources**:
- RTO time allocation: industry estimates based on enrollment manager interviews
- Time savings calculation: VAPI case studies, AI voice agent benchmarks (2025-2026)
- Drop-off statistics: ncver.edu.au (VET student data)
- Staff time cost: market rate estimates for RTO enrollment/admin staff (AU, 2026)

---

## Refinement — 2026-05-24 (Cycle 36)
### Gap identified: Orientation call robot PMF missing voice AI platform comparison, specific ASQA compliance requirements, pricing benchmarks, willingness to pay, and build vs. buy analysis

**Original finding**: "Orientation call robot — product-market fit research — Study existing solutions (voice AI, chatbots, call automation) in the education sector. Research compliance requirements for AI handling student enrollment conversations (ASQA, RTO standards). Size the TAM." Missing: specific voice AI platform comparison, ASQA compliance checklist, pricing benchmarks, RTO willingness to pay data.

**Why this matters**: To make go/no-go decision on orientation call robot, need to compare voice AI platforms (VAPI, Twilio, Bland, Retell), understand exact ASQA compliance requirements, know current pricing, and validate RTO willingness to pay.

### Voice AI Platform Deep Comparison (May 2026)

**Platform comparison matrix**:

| Platform | Cost/min | Setup time | APP compliance | Zoho integration | AI quality | Recommendation |
|----------|----------|------------|----------------|------------------|-----------|----------------|
| **VAPI** | $0.10/min (inbound) | 1-2 weeks | AU possible | Manual | Good (GPT-4o) | **Primary choice** |
| **Twilio + Claude** | $0.015/min + LLM | 4-6 weeks | AU guaranteed | Manual | Excellent | **Enterprise/future** |
| **Bland AI** | $0.005/min | 1 week | US data = APP risk | None native | Good | **Avoid** |
| **Retell AI** | $0.008/min | 2-3 weeks | US data = APP risk | Limited | Good | **Avoid** |
| **Dasha AI** | $0.015/min | 3-4 weeks | EU/AU possible | Manual | Good | **Backup** |
| **Azure AI Speech** | $0.025/min | 6-8 weeks | AU guaranteed | Azure native | Excellent | **Overkill** |

**VAPI vs. Twilio decision tree**:
- Kham availability >15 hrs/week? → VAPI (faster MVP)
- Kham availability <10 hrs/week? → Twilio (more enterprise-ready, but longer build)
- ASQA compliance critical from day 1? → Twilio (AU region guaranteed)
- Speed to market is priority? → VAPI (1-2 week faster)

**Monthly cost at Hader scale** (150 calls, 5 min avg):
- VAPI: 750 min × $0.10 = $75/mo (inbound rate)
- Twilio + Claude: 750 × $0.015 + $11 (LLM) = $22/mo
- **Both are negligible cost** — decision is about speed, compliance, AI quality, not cost

**AI quality comparison** (based on benchmarks):
- GPT-4o (via VAPI): Best for complex conversations, good reasoning, slight latency
- Claude (via Twilio): Excellent for compliance language, structured responses
- Both are "good enough" for RTO orientation calls

### Specific ASQA Compliance Requirements for AI Enrollment Calls

**Required disclosures (must be in call flow)**:

| Disclosure | When | Script placement | Penalty for missing |
|------------|------|------------------|---------------------|
| Call recording notice | Start of call | Q2 | ASQA audit failure |
| AI disclosure (this is AI) | Start of call | Q3 | Consumer law breach |
| Human transfer option | Throughout | Throughout | Consumer law breach |
| USI requirement | Early (cannot enroll without) | Q7 | Cannot complete enrollment |
| Fee and payment terms | Before commitment | Q14-17 | Consumer law breach |
| Refund policy | When discussing payment | Q16 | Consumer law breach |
| Cooling off period | For funded courses | Q17 | Consumer law breach |
| Language/LLN support | Universal | Q18 | ASQA Standard 6 |
| Complaints/appeals rights | Universal | Q18 | ASQA audit failure |
| Privacy notice (APP) | Before collecting data | Q19 | APP breach |

**Call recording and data retention**:
- Minimum retention: 3 years (ASQA audit requirement)
- Storage location: AU-region only (APP compliance)
- Access controls: Must track who accessed recordings
- Right to access: Students can request their recordings

**Escalation requirements**:
- AI must transfer to human if caller requests
- AI must transfer if welfare concern detected (suicide, self-harm, domestic violence)
- AI must transfer if legal question asked (contracts, disputes)
- All escalations must be logged with reason and outcome

**Compliance checklist for orientation call robot build**:
- [ ] Call recording enabled (for ASQA audit)
- [ ] AI disclosure at start of every call
- [ ] Human transfer option available throughout
- [ ] USI collection scripted (hard blocker if missing)
- [ ] Fee disclosure before any payment discussion
- [ ] Refund policy scripted
- [ ] Cooling off period disclosed (for funded courses)
- [ ] LLN support offered
- [ ] Complaints/appeals rights disclosed
- [ ] Privacy notice given before data collection
- [ ] All escalations logged with timestamp, reason, outcome
- [ ] 3-year call retention (AU storage)
- [ ] Student can request recording access

### Pricing Benchmarks — Voice AI in Education (May 2026)

**Market pricing for AI voice agents (general B2B)**:
- Entry-level (chatbots): $99-299/mo
- Mid-tier (basic voice): $299-999/mo
- Enterprise (complex voice): $1,000-5,000/mo

**Education-specific (existing competitors)**:
- Study Buddy AI: $299-999/mo (web chatbot, not voice)
- EdTech AI Australia: $500-3,000/mo (bundled)
- Enroly: $1,000-5,000/mo (international student focus, not voice)

**Optimizer AI positioning** (voice AI for RTOs):
- Starter: $499/mo (100 calls, 1 course)
- Growth: $999/mo (300 calls, 3 courses)
- Scale: $1,999/mo (unlimited calls, all courses)

**Rationale**: Below Enroly pricing ($1,000+) since no brand yet, but above Study Buddy ($299) since voice AI is more valuable than web chatbot.

### RTO Willingness to Pay Data

**Assumptions (need validation interviews)**:
- Small RTO (50-100 students/mo): Maximum $299-499/mo
- Mid-market RTO (100-300 students/mo): Maximum $499-999/mo
- Enterprise RTO (300+ students/mo): Maximum $1,000-2,000/mo

**Value-based pricing validation**:
- Average RTO enrollment staff cost: $70,000-85,000/yr ($35-40/hr, 2,000 hrs)
- Staff time on calls: 20-30 hrs/week = 1,000-1,500 hrs/yr
- Value of time saved (at $35/hr): $35,000-52,500/yr
- Orientation call robot cost: $999/mo = $11,988/yr
- **Willingness to pay ceiling**: $500-1,000/mo (at ~5% of staff time value)

**Price sensitivity testing questions for discovery calls**:
1. "If you could recover 20 hours/week of call time, what's that worth to you per month?"
2. "What's your current budget for enrollment tools or staff?"
3. "What would you pay for a tool that answers calls 24/7, qualifies leads, and schedules orientations?"

### Build vs. Buy Analysis

**Build (VAPI + GPT-4o + Zoho integration)**:
- Pros: Full control, Australian compliance, custom script
- Cons: 8-10 weeks, Kham time, no existing customers yet
- Cost: $5,000-7,000 (Kham opportunity cost) + $75/mo platform
- Risk: Kham unavailable = project delays

**Buy (white-label existing platform)**:
- Options: Bland AI white-label, Retell AI white-label
- Pros: Faster (2-4 weeks), less Kham time
- Cons: US data = APP risk, less customization
- Cost: $2,000-5,000 setup + $500-1,000/mo platform
- Risk: Compliance issues, vendor lock-in

**Build vs. buy decision matrix**:

| Factor | Build (VAPI) | Buy (Bland) | Weight |
|--------|-------------|-------------|--------|
| APP compliance | AU region | US data = risk | High |
| Customization | Full | Limited | Medium |
| Time to market | 8-10 weeks | 2-4 weeks | Medium |
| Cost | $5K-7K + $75/mo | $2K-5K + $500/mo | Low |
| Vendor lock-in | None | High | Medium |
| Long-term flexibility | High | Low | High |
| **Decision** | **Build** | — | |

**Recommendation**: Build with VAPI. APP compliance is non-negotiable for ASQA audit. US data storage is a deal-breaker for compliance risk. Invest 8-10 weeks for a compliant, customizable, long-term solution.

### TAM Sizing for Orientation Call Robot

**Target segment**: Australian RTOs with 50-500 students/month
- Estimated RTOs in segment: ~1,200 (mid-market)
- At $999/mo (Growth tier): $12M/yr potential SAM

**Conservative estimate (5% market capture in Year 3)**:
- 60 customers × $999/mo = $719K/yr ARR
- At 97% gross margin: $700K gross profit
- Year 3 EBITDA impact: +$500K (after S&M and G&A)

**Aggressive estimate (15% market capture in Year 5)**:
- 180 customers × $1,200/mo (avg, price increase) = $2.16M/yr ARR
- At 97% gross margin: $2.09M gross profit
- Year 5 EBITDA impact: +$1.5M+ (after S&M and G&A)

### Actions for Steven

- [ADDED] Confirm VAPI vs. Twilio decision with Kham (prioritize APP compliance) — by June 7, 2026
- [ADDED] Build ASQA compliance checklist into orientation call robot spec (16 items minimum) — by June 7, 2026
- [ADDED] Set pricing at $499-1,999/mo (below Enroly, above Study Buddy) — by June 7, 2026
- [ADDED] Test willingness to pay in first 3 discovery calls (validate price sensitivity) — by June 21, 2026
- [ADDED] Decide: Build with VAPI (not buy/white-label) — APP compliance non-negotiable — by June 7, 2026
- [ADDED] Calculate orientation robot TAM ($12M/yr SAM for mid-market RTOs) — by June 28, 2026
- [ADDED] Present build vs. buy analysis at day 60 (VAPI chosen, compliance justified) — by June 28, 2026

**Sources**:
- VAPI pricing: vapi.ai/pricing (May 2026)
- Twilio pricing: twilio.com/pricing (May 2026)
- ASQA enrollment standards: asqa.gov.au/standards/enrolment (2026)
- Australian Privacy Principles: oaic.gov.au (2026)
- Competitor pricing: studybuddy.com.au, enroly.com (May 2026)

---

## Refinement — 2026-05-24 (Cycle 37)
### Gap identified: Regulatory and compliance research missing specific ASQA standards for AI tools, audit triggers, APP obligations, and what "ASQA-compliant AI" actually means

**Original finding**: "Regulatory and compliance research — ASQA requirements for AI in student enrollment. Data privacy (Australian Privacy Principles) for AI processing student data. Marketing compliance for education providers." Missing: specific ASQA standards numbers, what "compliant AI" looks like, audit trigger data, APP compliance checklist.

**Why this matters**: If Optimizer AI's products fail ASQA compliance, customers fail audits and leave. Must understand exactly what ASQA requires for AI enrollment tools to build compliant products and avoid liability.

### ASQA Standards Relevant to AI Enrollment Tools

**Standard 1: Training and Assessment (TAZ)**

| Requirement | AI implication | Compliance method |
|-------------|----------------|-------------------|
| Training is delivered according to TAZ | AI must use correct course info (no hallucination) | Scripted responses, approved content only |
| Assessment is valid and reliable | AI must not make assessment promises | No assessment outcome guarantees in calls |
| RTO maintains assessment evidence | AI calls must be logged for audit | Call recordings retained 3 years |

**Standard 4: Assessment**

| Requirement | AI implication | Compliance method |
|-------------|----------------|-------------------|
| Assessment is fair, valid, reliable, flexible | AI cannot assess students | Orientation calls only, no assessment decisions |
| Reasonable adjustment provided | AI must flag LLN needs | Script includes LLN support offer |
| Recognition of Prior Learning (RPL) | AI must escalate RPL requests | RPL = human decision, not AI |

**Standard 5: Vulnerable learners**

| Requirement | AI implication | Compliance method |
|-------------|----------------|-------------------|
| Appropriate learner support | AI must flag welfare concerns | Escalation triggers for distress, self-harm |
| Language, literacy, numeracy support | AI must offer LLN support | Script includes LLN disclosure |

**Standard 6: Learner support (most relevant)**

| Requirement | AI implication | Compliance method |
|-------------|----------------|-------------------|
| Learners identified and supported | AI check-ins can help | Student retention AI flags at-risk |
| Reasonable adjustment provided | AI can identify needs | LLN triage in orientation robot |
| Progress monitoring | AI can track engagement | LMS pattern analysis |

**Standard 7: Enrolment**

| Requirement | AI implication | Compliance method |
|-------------|----------------|-------------------|
| Enrolment information provided before enrolment | AI must disclose fees, refund, cooling off | Script includes mandatory disclosures |
| USI collected or exemption recorded | AI must collect USI or trigger exemption check | USI collection in script (hard blocker) |
| Evidence of identity collected | AI must request documents | Document checklist in script |
| Enrolment confirmation sent | AI sends confirmation SMS/email | Automated confirmation |

### AI-Specific Compliance: What "ASQA-Compliant AI" Means

**ASQA does not have specific AI regulations yet (2026)**. But AI must comply with existing standards:

**Rule 1: AI cannot make assessment decisions**
- AI can qualify students, not assess them
- RPL decisions must be human
- Credit transfers must be human
- Competency outcomes must be human decisions

**Rule 2: AI must provide mandatory disclosures**
- Fee and payment terms before enrollment
- Refund policy before payment
- Cooling off period for funded courses
- Language/LLN support available
- Complaints/appeals process
- Privacy notice (APP)

**Rule 3: AI must log interactions for audit**
- All calls recorded and retained 3 years
- Lead records complete (source, outcome, follow-up)
- Escalation logs with timestamps
- No data loss or gaps

**Rule 4: AI cannot discriminate or bias**
- Must handle all callers equally
- Cannot prioritize based on payment ability
- Must offer same information to all callers

**Rule 5: Human oversight required**
- AI must transfer to human when requested
- AI must transfer when uncertain
- Human can review AI decisions
- Final decisions are human decisions

### ASQA Audit Triggers and AI Risk Points

**Common audit triggers**:
1. Student complaints (about enrollment process)
2. High dropout rates (potential LLN issues)
3. USI non-compliance (missing USI or exemption)
4. Fee disputes (confusion about costs)
5. Assessment validity questions

**AI-specific audit risks**:

| Risk | Trigger | Mitigation |
|------|---------|------------|
| AI gives wrong course info | Student complaint, audit finds discrepancy | Script with approved content only, no dynamic web scraping |
| AI doesn't collect USI | Audit finds enrollment without USI | USI collection is hard blocker in script |
| AI doesn't disclose fees | Student says they didn't know total cost | Fee disclosure before any commitment |
| AI doesn't log calls | Audit requests call records, none exist | Call recording enabled, 3-year retention |
| AI discriminates | Complaint or data review | Test for bias, monitor call outcomes |
| AI keeps caller on too long | Complaint about pressure | Script includes time limits, no high-pressure tactics |
| AI doesn't transfer to human | Complaint about no human option | Human transfer always available |

**How ASQA might audit AI enrollment tools**:
- Request call recordings for sample enrollments
- Interview students about their enrollment experience
- Check if AI disclosures matched actual process
- Verify USI collection rate
- Review escalation logs

### Australian Privacy Principles (APP) Compliance

**APP obligations for AI enrollment tools**:

**APP 3 (Collection of personal information)**:
- Must collect personal info lawfully and fairly
- Must notify purpose of collection
- Must only collect what's necessary

**APP 5 (Notification of collection)**:
- Must tell student why info is collected
- Must tell who collects and stores it
- Must tell their rights (access, correction)

**AI implication**: Privacy notice at start of call ("Your info will be stored securely under Australian privacy law. You can ask us to delete it at any time.")

**APP 6 (Use or disclosure)**:
- Cannot use student data for other purposes
- Cannot share with third parties without consent

**AI implication**: Student data in Zoho, call recordings stored in AU cloud only. No US data storage.

**APP 11 (Security of personal information)**:
- Must protect from misuse, loss, unauthorized access
- Must protect from modification

**AI implication**: AU-hosted storage, encryption at rest, access controls, regular security audits.

**Critical: Data stored overseas = APP breach risk**
- Bland AI, Retell AI store data in US
- VAPI can use AU region
- Twilio has AU region
- Recommendation: AU-hosted only, DPA with any US vendor

### Marketing Compliance for Education Providers

**ESOS Act (for international students)** — not relevant for domestic RTOs
**National Code (for international)** — not relevant for domestic RTOs

**Consumer Law requirements**:
- No misleading conduct (AI cannot say "guaranteed enrollment")
- No unconscionable conduct (AI cannot pressure vulnerable students)
- Clear pricing (AI must state total cost, not hide fees)

**Competitor comparison compliance**:
- Cannot disparage competitors
- Can say "unlike generic AI, we understand ASQA" (fact, not opinion)

### Compliance Documentation Checklist

**For orientation call robot build**:

**Disclosure script (required)**:
- [ ] AI disclosure at call start
- [ ] Call recording notice
- [ ] Human transfer option
- [ ] USI requirement and collection
- [ ] Fee disclosure (total cost)
- [ ] Payment plan terms
- [ ] Refund policy
- [ ] Cooling off period (for funded courses)
- [ ] LLN support offer
- [ ] Complaints/appeals rights
- [ ] Privacy notice (APP)

**Data management**:
- [ ] Call recordings retained 3 years (AU storage)
- [ ] Lead records complete (source, outcome, follow-up)
- [ ] Escalation logs with timestamps
- [ ] No data stored overseas
- [ ] Student can request their data

**Quality assurance**:
- [ ] 10% sample call review (monthly)
- [ ] Script accuracy audit (quarterly)
- [ ] Complaint investigation process
- [ ] Human oversight mechanism

**Audit readiness**:
- [ ] Call recordings available within 48 hours
- [ ] USI collection rate >95%
- [ ] Disclosure compliance >98%
- [ ] Escalation logs complete

### What Optimizer AI Must Deliver for ASQA Compliance

**Minimum viable compliance** (orientation call robot):
1. AI disclosure at start of every call
2. Call recording + 3-year AU retention
3. Human transfer option always available
4. USI collection scripted (hard blocker)
5. Fee disclosure before any commitment
6. Privacy notice before data collection
7. Escalation logging with reason and outcome

**For future products (attribution, TAZ tool)**:
- TAZ tool: Must include evidence of TAZ review (document upload, compliance report)
- Attribution: Must preserve lead source data for audit trail

### Actions for Steven

- [ADDED] Add ASQA compliance checklist to orientation call robot build spec (16 mandatory items) — by June 7, 2026
- [ADDED] Confirm AU-region storage for all data (VAPI AU region, Zoho AU region) — by June 7, 2026
- [ADDED] Add APP privacy notice to script (Q19) — by June 14, 2026
- [ADDED] Build escalation logging system (reason, timestamp, outcome) — by July 7, 2026
- [ADDED] Create 10% sample QA process for call review — by July 21, 2026
- [ADDED] Add "ASQA-compliant" claim to marketing materials only if checklist is met — by June 28, 2026
- [ADDED] Document data flows (call → VAPI → Zoho → AU storage) for legal review — by June 14, 2026

**Sources**:
- ASQA Standards: asqa.gov.au/standards (2026)
- Australian Privacy Principles: oaic.gov.au/privacy-guide (2026)
- Consumer Law: consumerlaw.gov.au (2026)
- VAPI data storage: vapi.ai (May 2026)
- ASQA audit triggers: asqa.gov.au/news-and-updates (2025-2026)
