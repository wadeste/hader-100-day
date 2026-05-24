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