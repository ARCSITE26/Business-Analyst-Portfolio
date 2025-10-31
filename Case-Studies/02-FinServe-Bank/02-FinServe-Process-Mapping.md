# FinServe Bank — Loan Approval Automation
## Process Mapping: AS-IS vs TO-BE

---

## CURRENT PROCESS (AS-IS) — 25-30 Days, Sequential/Waterfall

```
DAY 0
│
├─ Customer Submits Application
│  └─ Online form + documents uploaded (PDF)
│
├─ 🔴 DAYS 1-3: Document Verification (MANUAL)
│  ├─ Verification team checks: PAN format, Aadhaar validity, salary slips, bank statements
│  ├─ Manual data entry from PDFs (high error risk)
│  ├─ Email-based workflow (no centralized system)
│  ├─ Errors found → Rework loop
│  └─ → Output: Verified documents + extracted data
│
├─ 🔴 DAYS 2-4: Credit Bureau Check (MANUAL)
│  ├─ Credit officer logs into CIBIL portal
│  ├─ Manually downloads CIBIL report (PDF)
│  ├─ Reviews credit history line-by-line
│  ├─ **BOTTLENECK:** Takes 2 days but should take 30 minutes
│  └─ → Output: Credit score, default history
│
├─ 🔴 DAYS 5-8: Income Verification (PHONE CALLS)
│  ├─ Officer calls customer (often unreachable → multiple attempts)
│  ├─ Officer calls employer HR (slow to respond)
│  ├─ Confirmation recorded manually
│  ├─ No standardized process
│  └─ → Output: Verified income details
│
├─ 🔴 DAYS 9-15: Underwriting & Risk Decision (MANUAL REVIEW)
│  ├─ Credit manager reviews ALL documents
│  ├─ Manager handles 50+ applications simultaneously (bottleneck)
│  ├─ Applies risk assessment rules (unclear prioritization)
│  ├─ Decision delayed by manager availability
│  └─ → Output: Approve/Reject/Request More Info
│
├─ ⚠️ DAYS 16-20: Compliance Review (SEQUENTIAL, LATE!)
│  ├─ Compliance officer checks AML/KYC
│  ├─ Reviews SEBI regulatory requirements
│  ├─ **CRITICAL FLAW:** Done AFTER all above steps
│  ├─ If issues found → ENTIRE PROCESS RESTARTS
│  ├─ High rework rate (causes delays)
│  └─ → Output: Compliance clearance (or rejection)
│
├─ 🔴 DAYS 21-25: Loan Disbursement Setup (MANUAL)
│  ├─ Operations team creates loan account (legacy system, slow)
│  ├─ Generates offer letter (Word template, manual editing)
│  ├─ Backend system integration issues
│  ├─ Manual verification of account details
│  └─ → Output: Loan account created
│
└─ 🔴 DAYS 26-30: Final Approval & Disbursement
   ├─ Senior manager reviews application (paper-based)
   ├─ Signs off on disbursement
   ├─ Manual fund transfer initiation
   ├─ Senior manager bottleneck (approves sequentially, not batched)
   └─ → Output: Funds transferred to customer account

TOTAL TIME: 25-30 DAYS (Waterfall = longest dependency path)
PROCESS TYPE: Sequential (each step waits for previous)
HANDOFFS: 8 different teams/people
ERROR RATE: High (manual data entry, rework loops)
AUTOMATION: <5% (mostly manual)
```

---

## PROPOSED PROCESS (TO-BE) — 7 Days, Parallel/Agile

```
DAY 0
│
└─ Customer Submits Application (Digital)
   ├─ Online form filled
   ├─ Documents uploaded
   ├─ AI-powered OCR extracts data (PAN, Aadhaar, salary slips)
   └─ System auto-validates formats + authenticity

DAY 1 → ✨ PARALLEL PROCESSING (3 Tracks Simultaneously)
│
├─ 🟢 TRACK A: Document Verification (Automated + Video)
│  ├─ AI OCR extracts 90% of data accurately
│  ├─ Video call scheduled automatically (customer + verification officer)
│  ├─ Officer joins video call, customer shows PAN/Aadhaar on camera
│  ├─ AI face-match verification (liveness check)
│  ├─ Manual confirmation of 10% flagged items
│  ├─ **TIME: 1 day (vs 3 days currently)**
│  └─ → Output: ✅ VERIFIED (moved from manual emails to structured call)
│
├─ 🟢 TRACK B: Credit Bureau Check (API Automation)
│  ├─ System auto-pulls CIBIL score via REST API
│  ├─ Credit history displayed in real-time dashboard
│  ├─ Red flags auto-highlighted (defaults, high utilization, liens)
│  ├─ **TIME: 10 minutes (vs 2-4 days currently!)**
│  └─ → Output: ✅ INSTANT credit report
│
└─ 🟢 TRACK C: Income Verification (Automated + Video)
   ├─ System pulls bank statements via Account Aggregator API
   ├─ Salary credits auto-detected (pattern recognition, AI)
   ├─ Video call: Customer confirms employment (pre-recorded verification available)
   ├─ **TIME: 1 day (vs 5-8 days currently)**
   └─ → Output: ✅ VERIFIED income

DAY 2 → Compliance Check (Automated + Smart Manual)
│
├─ AI scans for AML/KYC red flags
│  ├─ Sanctions list check (instant)
│  ├─ PEP (Politically Exposed Person) check
│  ├─ Income verification vs loan amount (ratio check)
│
├─ Compliance officer reviews ONLY flagged cases (not all applications)
│  ├─ 80% auto-pass (zero issues)
│  ├─ 20% flagged (need manual review)
│
└─ → Output: ✅ COMPLIANCE CLEARED (same day, no rework)

DAYS 3-5 → Underwriting & Decision (Hybrid: AI + Manual)
│
├─ AI Credit Scoring Model runs
│  ├─ Considers: CIBIL score, income, loan history, existing debt
│  ├─ Auto-approves low-risk applicants (CIBIL >750, DTI <40%)
│
├─ Credit Manager reviews ONLY borderline cases
│  ├─ High-risk: CIBIL 600-750, multiple credit lines
│  ├─ Complex scenarios: Self-employed, non-standard income
│  ├─ Manager can now focus on judgment calls (not data entry)
│
└─ → Output: Decision (Approve/Reject/Request Info)

DAY 6 → Disbursement Setup (Fully Automated)
│
├─ System auto-creates loan account (API integration with core banking)
│ ├─ Account number generated
│ ├─ Loan terms stored
│ └─ **TIME: 30 seconds (vs 5 days currently!)**
│
├─ Digital offer letter generated (auto-populated)
│ ├─ PDF created with loan terms
│ ├─ Sent via email + SMS link
│ └─ Customer accepts via e-signature (DocuSign/eSign Genie)
│
└─ → Output: Offer accepted, account ready

DAY 7 → Final Approval & Disbursement (Batch Processing)
│
├─ Senior Manager reviews dashboard summary
│  ├─ Sees batch of 50+ applications (not individual files)
│  ├─ All pre-checked for compliance + risk
│  ├─ One-click batch approval (not sequential)
│
├─ Funds auto-transferred via NEFT/RTGS
│  ├─ System initiates transfer automatically
│  └─ Money reaches customer account same day
│
└─ → Output: ✅ CUSTOMER RECEIVES FUNDS

TOTAL TIME: 7 DAYS (Parallel = fastest path, not sum of all)
PROCESS TYPE: Parallel (multiple tracks simultaneously) + Batch processing
HANDOFFS: Reduced from 8 to 4 (less friction)
ERROR RATE: Low (<2%, mostly AI-caught)
AUTOMATION: 85%+ (only human judgment on borderline cases)
COMPLIANCE: Earlier detection, zero rework
CUSTOMER EXPERIENCE: Predictable 7-day timeline
```

---

## KEY IMPROVEMENTS

### **Time Savings by Stage**

| **Stage** | **Current** | **Proposed** | **Saved** | **Why** |
|---|---|---|---|---|
| Document Verification | 3 days | 1 day | 2 days | OCR + Video call (parallel) |
| Credit Check | 2-4 days | 10 mins | 3.5 days | API integration (instant) |
| Income Verification | 5-8 days | 1 day | 6 days | Video call + Bank statement API |
| Underwriting | 9-15 days | 3 days | 10 days | AI + rule-based (manager only on borderline) |
| Compliance | 4 days (at end) | 1 day (Day 2) | 3 days | Earlier + automated screening |
| Disbursement | 5 days | 1 day | 4 days | API-based account creation |
| Final Approval | 4 days | 1 day | 3 days | Batch approval dashboard |
| **TOTAL** | **25-30 days** | **7 days** | **18-23 days** | **Parallel + Automation** |

### **Process Changes**

| **Aspect** | **Current** | **Proposed** | **Benefit** |
|---|---|---|---|
| **Workflow Type** | Sequential (waterfall) | Parallel (agile) | 70% faster |
| **Compliance Review** | Day 16-20 (late, causes rework) | Day 2 (early, prevents rework) | Zero rework, faster approvals |
| **Data Entry** | Manual from PDFs | OCR automation | 90% accuracy, instant |
| **Underwriting** | All 100% applications reviewed | AI auto-approves 80%, manager reviews 20% | Manager freed for judgment calls |
| **Approval** | Sequential sign-offs | Batch processing | Removes bottleneck |
| **Customer Touchpoints** | 3-4 calls over 30 days | 2-3 video calls over 7 days | Better experience |

---

## HANDOFF REDUCTION

**Current (8 Handoffs):**
1. Customer → Verification team
2. Verification team → Credit team
3. Credit team → Income verification officer
4. Officer → Underwriting team
5. Underwriting → Compliance team
6. Compliance → Operations team
7. Operations → Senior manager
8. Senior manager → Finance (disbursement)

**Proposed (4 Handoffs):**
1. Customer → Video verification officer (combines doc + income verification)
2. Officer → AI underwriting engine (automated 80%)
3. AI engine → Credit manager (human review 20%)
4. Manager → Batch approval system (auto-disburse)

**Benefit:** Less friction, fewer errors, faster processing

---

*Document Version: 1.0 | Last Updated: October 2025*
